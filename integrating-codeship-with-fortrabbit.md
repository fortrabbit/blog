---

title:      Integrating codeship with fortrabbit
author:     uk
excerpt: "Learn how to do continuous integration with Codehip on fortrabbit."
created: 2013/08/28 15:57:00

---

# fortrabbit + Codeship

We have got a lot of requests concerning **continuous integration** lately. That's why we've published a new general [article](http://fortrabbit.com/docs/in-depth/integrating-external-ci) in our docs on how to integrate CI in your fortrabbit workflow.

Pieter from [wercker](http://wercker.com/) also just published this [great article](http://born2code.net/blog/2013/08/26/Deploying-from-wercker-to-fortrabbit/) on how to integrate fortrabbit with wercker. Here is another one from us on how you could something similar combining [Codeship](http://codeship.io) with fortrabbit. 

## Preparations

You should first create a fresh App on fortrabbit. You could also use an existing one, but it's simpler to start from the scratch. Now you have to setup a repository on [Github](https://github.com) or [Bitbucket](http://bitbucket.org/). Best name it the same as your App on fortrabbit… or however you can remember it best. I'd recommend to use a private repo, as long as you don't plan on going public with your source code. I'll go with Bitbucket in this example, 'cause they offer (a limited amount of) private repos for free. 

## Setup Codeship

Now you can sign in to codeship with your Bitbucket (or Github) account and create a new repo. ![Create project](/blog-assets/img/create-project.png) Following the create link you can choose your repository provider. I went with Bitbucket and chose my `my-app` repository. ![Choose repo](/blog-assets/img/select-repo.png) In the next screen of the setup process codeship tells you how to set up your hook. Follow the instructions and make a first commit and push to your (Bitbucket) repo. ![Setup hook](/blog-assets/img/setup-hook-1.png) Now you need to choose the _Technology_, i.e. your test environment. Choose _PHP_ in the top select bar. If you need (I didn't) modify the setup and test commands. ![Setup hook](/blog-assets/img/choose-technology.png)

## Setup your fortrabbit App

You need to install your codeship project's SSH key in your fortrabbit App so that codeship will be allowed to push to fortrabbit. You can find the key in the _General_ tab of your project's settings. ![Get SSH key](/blog-assets/img/get-ssh-key.png) Copy and paste the key as a new user in the _Git_ tab of your App on fortrabbit. ![](/blog-assets/img/save-ssh-key-with-fortrabbit.png)

## Setup deployment: codeship -> fortrabbit

This is final step. Go again to your project settings on codeship and open the _Deployment_ tab. Choose _$script_ from the buttons and enter the following in the deployment command (modify according to your App's Git URL and App name): 
    
    
    git remote | grep -q frbit-master || git remote add frbit-master git@git1.eu1.frbit.com:my-app.git
    git push frbit-master master
    

It should look alike to (the textarea breaks the lines, but it should be two, not three): ![Setup deployment](/blog-assets/img/setup-deployment.png)

## Commit, push, test and deploy

Well, you did it. Now just do you first code, test & deploy cycle. For this you need of course something testable. Here is a [demo app](/blog-assets/archives/testable.tar.gz) you can use if you haven't one at your fingertips. Add your code, commit everything and push (to Bitbucket): 
    
    
    $ git add -A
    $ git commit -am 'Test and deploy'
    $ git push
    

On codeship, you should see something like this: ![Test and deploy](/blog-assets/img/deployment-log.png) And on fortrabbit, your code has been deployed! 

## Going multi stage

No problem. With codeship, you can setup a different deployment script for each branch. So assuming you followed our [multi stage guide](http://fortrabbit.com/docs/in-depth/multi-stage-environment) and read the extension about [CI and multi-stage](http://fortrabbit.com/docs/in-depth/integrating-external-ci#how-to-use-it-with-multi-stage), just modify the deploy script on codeship for each branch like so (of course: replace the actual App Git URLs): **test branch**
    
    
    git remote | grep -q frbit-test || git remote add frbit-test git@git1.eu1.frbit.com:my-app-test.git
    git push frbit-master refs/heads/test:refs/heads/master
    

**stage branch**
    
    
    git remote | grep -q frbit-stage || git remote add frbit-stage git@git1.eu1.frbit.com:my-app-stage.git
    git push frbit-master refs/heads/stage:refs/heads/master
    

**prod branch**
    
    
    git remote | grep -q frbit-prod || git remote add frbit-prod git@git1.eu1.frbit.com:my-app-prod.git
    git push frbit-master refs/heads/prod:refs/heads/master
    

* * *

**Disclaimer**: Of course [wercker](http://wercker.com/) and [Codeship](https://www.codeship.io/) are not the only "Continuous Integration as a Service" providers. You might also have a look at [CircleCI](https://circleci.com/), [TravisCI](http://travis-ci.com/) or others. [fortrabbit](http://fortrabbit.com) is definitely also not the only place to host your PHP application, but maybe the coolest. Don't forget to check out our [big list of developer facing services](https://docs.google.com/spreadsheet/ccc?key=0An6rx68cKNFNdDNYdFdSSTNzZXl5eGRSY0ZxSW10aHc#gid=1).