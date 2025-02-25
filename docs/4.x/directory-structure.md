# Directory Structure

A fresh Craft 4 [installation](./installation.md) will have the following folders and files in it.

### `config/`

Holds all of your Craft and plugin [configuration files](config/README.md), as well as your `license.key` file.

::: tip
You can customize the name and location of this folder by setting the [CRAFT_CONFIG_PATH](config/README.md#craft-config-path) PHP constant in your [entry script](./config/README.md#entry-script).
:::

### `modules/`

Holds any [Yii modules](https://www.yiiframework.com/doc/guide/2.0/en/structure-modules) your site might be using.

### `storage/`

This is where Craft stores a bunch of files that get dynamically generated at runtime.

Some of the folders you might find in there include:

- `backups/` – Stores database backups that get created when you update Craft or run the DB Backup utility.
- `logs/` – Stores Craft’s logs and PHP error logs.
- `rebrand/` – Stores the custom Login Page Logo and Site Icon files, if you’ve uploaded them.
- `runtime/` – Pretty much everything in here is there for caching and logging purposes. Nothing that Craft couldn’t live without, if the folder happened to get deleted.

For the curious, here are the types of things you will find in `storage/runtime/` (though this is not a comprehensive list):

  - `assets/` – Stores image thumbnails, resized file icons, and copies of images stored on remote asset volumes, to save Craft an HTTP request when it needs the images to generate new thumbnails or transforms.
  - `cache/` – Stores data caches.
  - `compiled_classes/` – Stores some dynamically-defined PHP classes.
  - `compiled_templates/` – Stores compiled Twig templates.
  - `temp/` – Stores temp files.
  - `validation.key` – A randomly-generated, cryptographically secure key that is used for hashing and validating data between requests.

::: tip
You can customize the name and location of this folder by setting the [CRAFT_STORAGE_PATH](config/README.md#craft-storage-path) PHP constant in your [entry script](./config/README.md#entry-script).
:::

### `templates/`

Your front-end Twig templates go in here. Any local site assets, such as images, CSS, and JS that should be statically served, should live in the [web](directory-structure.md#web) folder.

::: tip
You can customize the name and location of this folder by setting the [CRAFT_TEMPLATES_PATH](config/README.md#craft-templates-path) PHP constant in your [entry script](./config/README.md#entry-script).
:::

### `vendor/`

This is where all of your Composer dependencies go—including Craft and any plugins you’ve installed. This directory should _not_ be tracked in version control. Instead, commit [`composer.lock`](#composerlock), and use [`composer install`](https://getcomposer.org/doc/03-cli.md#install-i) to rebuild it.

::: tip
You can customize the name and location of this folder by changing the [CRAFT_VENDOR_PATH](config/README.md#craft-vendor-path) PHP constant in your [entry script](./config/README.md#entry-script). If you choose to relocate it, make sure you update your `.gitignore` file to continue excluding it from version control.
:::

### `web/`

This directory represents your server’s web root. The public `index.php` file lives here and this is where any of the local site images, CSS, and JS that is statically served should live.

::: tip
You can customize the name and location of this folder. If you move it so it’s no longer living alongside the other Craft folders, make sure to update the [CRAFT_BASE_PATH](config/README.md#craft-vendor-path) PHP constant in your [entry script](./config/README.md#entry-script).
:::

### `.env`

This is your [PHP dotenv](https://github.com/vlucas/phpdotenv) `.env` configuration file. It defines sensitive or [environment-specific config](./config/README.md#env) values that don’t make sense to commit to version control.

### `.env.example`

This is your [PHP dotenv](https://github.com/vlucas/phpdotenv) `.env` file template. It should be used as a starting point for any actual `.env` files, stored alongside it but out of version control on each of the environments your Craft project is running in.

### `.gitignore`

Tells Git which files it should exclude when committing changes. At minimum, this should ignore `.env` and Composer’s `vendor/` directory.

### `bootstrap.php`

The [starter project](depo:craftcms/craft) consolidates important bootstrapping logic (like defining path [constants](./config/README.md#php-constants) and loading environment variables from the [`.env`](#env) file) into this file. Both the HTTP and console entry scripts (`web/index.php` and [`craft`](#craft), respectively) include this file—but each goes on to instantiate a different [type of application](guide:structure-entry-scripts) suited for that request context.

### `composer.json`

The starting point `composer.json` file that should be used for all Craft projects. See the [Composer documentation](https://getcomposer.org/doc/04-schema.md) for details on what can go in here.

### `composer.lock`

This is a Composer file that tells Composer exactly which dependencies and versions should be currently installed in `vendor/`.

### `craft`

This is a command line executable used to execute Craft’s [console commands](console-commands.md). Its structure is similar to `web/index.php`, insofar as it is responsible for bootstrapping the appropriate Craft application—but instead of a <craft4:craft\web\Application>, it creates a <craft4:craft\console\Application>.

### `.ddev/`

If you followed the [installation](./installation.md) guide, DDEV will have left a `.ddev/` directory in the root of your project. This is safe to keep in version control—DDEV may make changes to it from time to time, but a separate `.gitignore` file exists within it to ensure only necessary files are tracked.
