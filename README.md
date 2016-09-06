# Drupal 8 starter project with Docker and composer

It's based on the [Composer template](https://github.com/drupal-composer/drupal-project).

## Usage

First you need to [install composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

> Note: The instructions below refer to the [global composer installation](https://getcomposer.org/doc/00-intro.md#globally).
You might need to replace `composer` with `php composer.phar` (or similar) for your setup.

After that you can create the project:

```
git clone git@github.com:OzConseil/drupal-project.git my-new-drupal
```

Install all dependencies with [composer create-project](https://getcomposer.org/doc/03-cli.md#create-project)

```
cd my-new-drupal
composer create-project --stability dev --no-interaction
```

Use [drush si](http://drushcommands.com/drush-7x/site-install/site-install) to install Drupal.
If you launch drush without the composer script you must specify the root directory: `./vendor/bin/drush --root=html site-install` 
Or lauch drush from html directory: `../vendor/bin/drush site-install`.

```
// with local sqlite db
composer drush -- site-install --db-url=sqlite://sites/default/files/.ht.db.sqlite
// with MySQL db
composer drush -- site-install --db-url=mysql://user:pass@server:port/dbname
```

With `composer require ...` you can download new dependencies to your installation.

```
cd some-dir
composer require drupal/media_entity:8.1.*
```

## What does the template do?

When installing the given `composer.json` some tasks are taken care of:

* Drupal will be installed in the `html`-directory.
* Autoloader is implemented to use the generated composer autoloader in `vendor/autoload.php`,
  instead of the one provided by Drupal (`web/vendor/autoload.php`).
* Modules (packages of type `drupal-module`) will be placed in `html/modules/contrib/`
* Theme (packages of type `drupal-module`) will be placed in `html/themes/contrib/`
* Profiles (packages of type `drupal-profile`) will be placed in `html/profiles/contrib/`
* Latest version of drush is installed locally for use at `vendor/bin/drush`.


## Generate composer.json from existing project

With using [the "Composer Generate" drush extension](https://www.drupal.org/project/composer_generate)
you can now generate a basic `composer.json` file from an existing project. Note
that the generated `composer.json` might differ from this project's file.


## FAQ

### Should I commit the contrib modules I download

Composer recommends **no**. They provide [argumentation against but also workrounds if a project decides to do it anyway](https://getcomposer.org/doc/faqs/should-i-commit-the-dependencies-in-my-vendor-directory.md).
