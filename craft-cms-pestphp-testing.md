---
author: os
created: 2022-12-01
title: Testing Craft CMS sites with Pest
intro: Using Pest to test Craft CMS websites.
lead: Testing a Craft CMS website might be less difficult than you think. Level up and follow us along as we learn about frontend testing Craft CMS websites.
figure:
  src: craft-pestphp.jpg
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'craft, craftcms, craft-cms, hosting, testing, pest, pestphp'
---

## Testing is hard until you practice it

You may think writing automated tests is complex and not worth the effort. That's usually the main argument against it.

However, even if you've never written a test, you did testing in a way. You did it manually using browser over and over again. You set some expectation in your mind and iterated until you reach the defined goal or acceptance criteria. Your manual testing practice is the answer to the first question: What should I test?

The next question you'll come across is: Which tool should I use and how to set it up?
To be honest, getting started ain't easy. In Craft the barrier for getting into testing is quite high. So far there is no test tool that integrates with Craft properly and lets you get started in a few minutes.

There is some documentation for Codeception, the default test framework for Yii, but it feels like nobody is using it. The adoption of modern frontend testing tools like Cypress or Playwright is probably a bit higher, but those are very generic by nature and do not fully integrate with Craft. We compared both in the [previous blog post](/craft-cms-frontend-testing-with-codeception-and-cypress).

## Why Pest?

![](/images/craft-pest-poster.png)

Pest is not reinventing the wheel. It is a layer on top of PHPUnit, the de facto standard tool for testing in PHP. The syntax and the philosophy are inspired by Jest, a popular testing framework in the JavaScript world. [Nuno Maduro](https://github.com/nunomaduro) created it for PHP as he liked writing tests in Jest. Within the last months it became increasingly popular in the Laravel community, hopefully soon in the Craft space too.

Pest doesn't work out-of-the-box with Craft. [Mark Huot](https://github.com/markhuot) put a lot of effort into a plugin that takes care of bootstrapping Pest, so you don't have to. The plugin also adds additional functionality which is needed to fully test Craft sites properly.
Its main focus is on HTTP tests, which means stuff you previously did manually in the browser becomes an automated test, by using a syntax that is easy to write and read.

Although Craft Pest isn't released yet, there is a lot of documentation on [craft-pest.com](https://www.craft-pest.com) already. The docs are not complete, but you can find useful examples to get started quickly.

## How to set up Pest for Craft?

It's easy, they said - and it is:

```
# Require the plugin using composer
composer require markhuot/craft-pest --dev
```

```
# Enable the plugin
php craft plugin/install pest
```

The install command registers the plugin and creates three files:

- `phpunit.xml` The PHPUnit config you rarely need to touch
- `tests/Pest.php` Here you can define functions you may want to use in your tests
- `tests/ExampleTest.php` A very basic HTTP test on the `/` route (you can remove it later)

## Write your first test

In contrast to PHPUnit or Codeception, tests are not defined in PHP classes. All you need is a PHP file in the `/tests` folder. If it becomes crowded create your own structure using subfolders.

```php
<?php # tests/SomeBasicAssertionsTest.php

it ('loads the homepage', function() {
  $this->get('/')->assertOk();
});

it ('loads the contact form', function() {
  $this->get('/contact')->assertOk();
});
```

## Testing Forms

The following test is very straight forward, but it introduces some new things we need to break down.

```php
<?php # tests/SearchFormTest.php

it ('finds two articles with matching keyword', function () {
    // Show and submit the search form
    $response = $this->get('/search')
        ->form('#search-form')
        ->fill('q', 'Pine Mountain')
        ->submit()
        ->assertRedirect()
        ->followRedirect();

    // Result: count items
    $response
        ->querySelector('.article-card')
        ->assertCount(2);

    // Result: assert text
    $articleCards = $response->querySelector('.article-card');
    expect($articleCards->getText())
        ->each()
        ->toContain('Pine Mountain');
});
```

Explanation:

First we visit the `/search` route and assume there is a `<form id="search-form">` element. Inside this form there is an `<input name="q" type="text">` which we fill with a search string.
Then we submit the form, expect a redirect response and follow it. All of these steps must be successful to get the test passing.

The previous `followRedirect()` creates a new request and returns a new response we can work with. The `querySelector()` method allows us to narrow down the HTML of the response body. In this example we select DOM elements that match `.article-card` and assert two of them exist.

Using Pest's Expectation API you express your expectation in a more human-readable way. This is what we do in the last step, it reads like this:

```php
expect(something_given)->toBe/toContain(expectation);
```

## There is more

### Datasets

Datasets in Pest, also known as data providers in PHPUnit, allow you to run certain tests with different data. This is where automated testing really shines.

For example, instead of testing a search form with only one static search term `Pine Mountain`, you define an array of terms but keep your actual test simple.

More: <https://pestphp.com/docs/datasets>

### Factories

Testing against a consistent dataset is important, this you can achieve by importing a sql dump or by using fixtures. Often more a bit more flexibility is required, and here is where factories come into play.
If you have some experience with Laravel, you will notice what this implementation was inspired by.

With factories, you actually fill the database with entries and fields for a specific scenario you want to test, then Craft can query against it in the next request.
After the test all changes (`INSERT`s, `UPDATE`s, `DELETE`s) are rolled back, so you don't pollute your database with dummy data.

More: <https://craft-pest.com/factories>

### Act as a logged-in user

In order to test certain behaviour as a logged-in user, you don't need to fill and submit the login form. There is an `actingAs()` helper method as a shortcut.
It accepts the email of an existing user, or you can create one on-the-fly using a factory. This feature is not fully documented so far, but it's a good opportunity to see that tests are also a good way of documenting code. Have a look at [tests/ActingAsTest.php](https://github.com/markhuot/craft-pest/blob/master/tests/ActingAsTest.php) to understand how it works.

```php
<?php

it ('allows admin users accessing the plugin in the cp', function () {
    $this->actingAs('existing.admin@domain.com');
    $this->get('/admin/actions/plugin-handle/controller/show')->assertOk();
});
```

### More complex examples

Reading others' tests helps in writing your own. That's why we've created a test for the multi-step checkout process of the official Craft Commerce demo site:

<https://github.com/fortrabbit/spoke-and-chain-pestphp/blob/pest/tests/Feature/CheckoutTest.php>

## Closing thoughts

When you start with testing, you will notice there is a lot of jargon that scares people away. Things like "mocks", "fakes", and "stubs" are terms you don't need to understand in the beginning.

To learn testing you need to practice it. And at some point you will love it as it creates certainty when launching a site, and more importantly, when you introduce changes to an existing project. Once you are into it, when shipping something without test coverage you may get the feeling something is missing - at least this applies to me.
