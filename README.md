# Tokenize

[![Build Status](https://img.shields.io/travis/UseMuffin/Tokenize/master.svg?style=flat-square)](https://travis-ci.org/UseMuffin/Tokenize)
[![Coverage](https://img.shields.io/coveralls/UseMuffin/Tokenize/master.svg?style=flat-square)](https://coveralls.io/r/UseMuffin/Tokenize)
[![Total Downloads](https://img.shields.io/packagist/dt/muffin/tokenize.svg?style=flat-square)](https://packagist.org/packages/muffin/tokenize)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)

Security tokens for CakePHP 3.

## Why?

Ever wanted to force users to activate their account upon registration?

Or maybe just a confirmation link when updating their credentials?

Ok, ok - maybe before cancelling a subscription or better, before sending funds out.

Well, now you can. Attach listeners to your models for sending out emails (or any other 
notification method of your choice), and you're good to go!

## Install

Using [Composer][composer]:

```
composer require muffin/tokenize:1.0.x-dev
```

You then need to load the plugin. You can use the shell command:

```
bin/cake plugin load Muffin/Tokenize
```

or by manually adding statement shown below to `bootstrap.php`:

```php
Plugin::load('Muffin/Tokenize');
```

## How it works

When creating or updating a record, and if the data contains any *tokenized* field(s), a token
will automatically be created along with the value of the field(s) in question. 

When this happens the `Model.afterTokenize` event is fired and passed the operation's related 
entity and the associated token that was created for it. 

The initial (save or update) operation resumes but without the *tokenized* fields. 

The *tokenized* fields will only be updated upon submission of their associated token.

## Usage

To tokenize the `password` column on updates, add this to your `UsersTable`:

```php
$this->addBehavior('Muffin/Tokenize.Tokenize', [
    'fields' => ['password'],
]);
```

If instead you wanted to have it create a token both on account creation and credentials update:

```php
$this->addBehavior('Muffin/Tokenize.Tokenize', [
    'fields' => ['password'],
    'implementedEvents' => [
        'Model.beforeSave' => 'beforeSave',
        'Model.afterSave' => 'afterSave',
    ],
]);
```

## Patches & Features

* Fork
* Mod, fix
* Test - this is important, so it's not unintentionally broken
* Commit - do not mess with license, todo, version, etc. (if you do change any, bump them into commits of
their own that I can ignore when I pull)
* Pull request - bonus point for topic branches

To ensure your PRs are considered for upstream, you MUST follow the [CakePHP coding standards][standards].

## Bugs & Feedback

http://github.com/usemuffin/tokenize/issues

## License

Copyright (c) 2015, [Use Muffin][muffin] and licensed under [The MIT License][mit].

[cakephp]:http://cakephp.org
[composer]:http://getcomposer.org
[mit]:http://www.opensource.org/licenses/mit-license.php
[muffin]:http://usemuffin.com
[standards]:http://book.cakephp.org/3.0/en/contributing/cakephp-coding-conventions.html
