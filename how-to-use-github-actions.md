---
title: Deploy to fortrabbit with GitHub Actions
intro: Why not automate this? Let's use the new cool kid in town.
created: 2019-11-19
author: yr
lead: GitHub Actions became public last week. This new CI system is free for all public repos. Private repos get 2000 minutes to build per month for free. This is a rough guide to use GitHub Actions as a deployment pipeline to fortrabbit.
figure:
  src: github-actions-poster.gif
tag:
  - webdev
---

## Why bother?

fortrabbit already has Git and even Composer build in without the need of any extra service. But fortrabbit currently does not offer a Node.js runtime during deployment, so common build tasks (Webpack) can not run here. So, one good use case to implement GitHub Actions is to automatically build static assets, like and JS, CSS. Or you can test and do other advanced stuff before deploying to fortrabbit.

## The goal

For now, let's build a prototype to deploy code to GitHub to trigger a simple Javascript build process and automatic deployment to fortrabbit afterwards.

## Get ready

You will need to generate an SSH key to allow GitHub to access your fortrabbit App. Start in the Terminal of your local computer (not the fortrabbit App):

1. Create a key pair: `$ ssh-keygen -t rsa -b 4096 -m pem -f /tmp/key-github`. This will generate two files: `/tmp/key-github.pub` and `/tmp/key-github`. The first one is the public key, the second one is the private one.
2. With the [fortrabbit Dashboard](https://dashboard.fortrabbit.com/), go to your App and add an **App-only SSH key**. Paste the content of the public key. This will allow anyone or any app having the corresponding private key to access this app.
3. On your GitHub repository, go to the Settings, and then go to Secrets. There, add a new secret, call it `SSH_PRIVATE_KEY` (if you want to follow our example, but you can obviously call it as you want), and paste the content of the private key.
4. Now you don't need the keys in your local `/tmp` folder anymore and you're all set up.

## Two methods

We will show two ways to integrate GitHub actions, both can have the same result, but the approach is different:

### 1. Git transport layer method

Available for Universal and Professional Apps.

Here, you commit all files, including the uglified JS, inside the CI's temporary Git repository, then force push to deploy. You can use this example workflow YAML as a starting point:

```
name: Deploy through git
on: [push]
jobs:
  build-and-deploy:
    env:
      GIT_EMAIL: <your-email-address>
      GIT_USERNAME: <your-name>
      REPO_URL: <your-fortrabbit-git-repository-address>
      REPO_BRANCH: <the branch you want to deploy (must be main, master or App name)>

    runs-on: ubuntu-latest

    steps:
    # This will pull the github repository to the current pipeline
    - uses: actions/checkout@v1

    # This will automatically set up ssh with our private key
    - uses: webfactory/ssh-agent@v0.5.4
      with:
        ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}

    # Use the version of Node.js you need
    - name: Use Node.js 10.x
      uses: actions/setup-node@v1
      with:
        node-version: 10.x

    # If you need node dependencies and to build some js/css
    - name: npm install and build
      run: |
        npm ci
        npm run <your-build-script>

    # If so, you can then remove the source assets folder
    - name: Remove the source assets files
      run: 'rm -Rf <your-assets-source-folder>'

    - name: Configure Git
      # The local git needs a user to be configured to commit & push
      run: |
        git config user.email $GIT_EMAIL
        git config user.name $GIT_USERNAME

    - name: Commit everything (with new built assets)
      # You can also specifically "git add public/your/path"
      run: |
        git checkout $REPO_BRANCH
        git add -A
        git commit -m "Build $($CURRENT_DATE_TIME)"
      env:
        CURRENT_DATE_TIME: "date +%Y-%m-%d:%H-%M"

    - name: deploy
      run: |
        git push --force $REPO_URL
      env:
        # This avoids a failure when the client does not know the SSH Host already
        GIT_SSH_COMMAND: "ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no"
```

As you may have noticed, we don't install PHP dependencies here, because when a Git deployment happens with fortrabbit, a Composer install is automatically triggered.

### 2. rsync transport layer method

Only available for Universal Apps.

Here we will use `rsync` to deploy to fortrabbit at the end. Instead of dealing with a temporary Git repository in the CI that you alter, you can directly send all the files through rsync.

```
name: Deploy through rsync
on: [push]
jobs:
  build-and-deploy:
    env:
      DESTINATION: "<your-fortrabbit-ssh-address>"

    runs-on: ubuntu-latest

    steps:
    # This will pull the github repository to the current pipeline
    - uses: actions/checkout@v1

    # This will automatically set up ssh with our private key
    - uses: webfactory/ssh-agent@v0.5.4
      with:
        ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}

    # We decide to use Node.js 10 here (could use 8, 10, or 12)
    - name: Use Node.js 10.x
      uses: actions/setup-node@v1
      with:
        node-version: 10.x

    - name: Validate composer.json and composer.lock
      run: composer validate

    - name: Install dependencies
      run: composer install --prefer-dist --no-dev --no-progress --no-suggest --optimize-autoloader --ignore-platform-reqs

    # If you need node dependencies and to build some js/css
    - name: npm install and build
      run: |
        npm ci
        npm run <your-build-script>

    # If so, you can then remove the source assets folder
    - name: Remove the source assets files
      run: 'rm -Rf <your-assets-source-folder>'

    - name: deploy
      # The StrictHostKeyChecking option avoids a failure when the client does not know the SSH Host already
      run: |
        rsync -azh -e 'ssh -o StrictHostKeyChecking=no' ./ --rsync-path='rsync' $DESTINATION:~/
```

A Composer install in GitHub's CI is triggered. Since the fortrabbit Git repo stays untouched, hence no Composer process will be launched on the deploy service. Everything will be transferred to fortrabbit already packed.

## Feedback please

Please let us know what you think! We are actively considering different implementation ideas.

What would you prefer: Having Node.js directly integrated with our service without the need to use an external service for this, or better integration with GitHub (and/or maybe BitBucket and others)? What do you think about the two approaches outlined above? Do you fully understand the differences? What would be your setup? Maybe, what's your use case?

## Thanks to our smart clients

We have mentioned this many times before, but we really do enjoy having such smart clients, constantly requesting features and producing edge cases. It helps to shape and build our services. This blog post and the actual prototype was heavily inspired by [diesdas.digital](https://diesdas.digital/)!
