# Pantheon Edge Integrations WordPress SDK

[![Unsupported](https://img.shields.io/badge/pantheon-unsupported-yellow?logo=pantheon&color=FFDC28&style=for-the-badge)](https://github.com/topics/unsupported?q=org%3Apantheon-systems "Unsupported, e.g. a tool we are actively using internally and are making available, but do not promise to support")

Welcome to the Pantheon Edge Integrations WordPress SDK!

This repository serves as a one-stop shop for integrating your WordPress site on Pantheon with our Edge Integrations toolset.

## Setup

### Installing into a project with Integrated Composer.

Adding Edge Integrations support to your Integrated Composer project is simple and is the recommended means of adding the Edge Integrations WordPress SDK.

#### Step 1: Require the Composer package

To get started, all you need to do is to add this repository as a dependency:

```bash
composer require pantheon-systems/edge-integrations-wordpress-sdk
```

That command will add this repository to your `/vendor` directory, as well as all of the dependencies, which include a [global, CMS-agnostic PHP library](https://github.com/pantheon-systems/pantheon-edge-integrations) and a [WordPress plugin](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations) as well as all of the documentation for the SDK.

#### Step 2: Require the Composer autoloader

You'll need to make sure your WordPress project is loading the Composer autoloader (`vendor/composer/autoload.php`). One way to do this is in a `mu-plugins` loader file like [this one](https://github.com/pantheon-systems/wordpress-bedrock-recommended/blob/master/packages/pantheon-wp-loader/loader.php) <!-- TODO: Update this link when this is broken out into a new repository -->, but other methods exist, such as adding an `include_once __DIR__ . '/vendor/composer/autoload.php` line in your `wp-config.php` or other file that runs before WordPress is executed.

### Installing manually

If you aren't running a project with Integrated Composer but you _do_ use Composer otherwise, you can still get started with the Edge Integrations WordPress SDK without too much trouble. This still assumes you have Composer installed on at least one machine.

#### Step 1: Clone the WordPress Edge Integrations plugin

First, you'll need to get a copy of the [WordPress Edge Integrations plugin](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations). Clone or download the plugin into your `wp-content/plugins` directory.

```bash
git clone git@github.com:pantheon-systems/pantheon-wordpress-edge-integrations.git
```

Alternately, you can use Composer to download the package.

```bash
composer require pantheon-systems/pantheon-wordpress-edge-integrations
```

#### Step 2: Install Pantheon Edge Integrations library

Once you have the plugin downloaded, you'll need to run `composer install` to get the Pantheon Edge Integrations library. `cd` into the plugin's directory and run `composer install`. From the `wp-content/plugins` directory, run the following commands:

```bash
cd pantheon-wordpress-edge-integrations
composer install
```

This will install `pantheon-edge-integrations` into the plugin's `vendor` directory. You'll still need to call the file(s) manually. <!-- TODO: Is this 100% accurate? We can maybe run a <?php if ( ! class_exists( 'HeaderData' ) ) ?> check in the plugin to see if we have the package and either display a message, attempt to load it manually, or bail otherwise. -->

Using a `mu-plugins/loader.php` file like the one linked above, add the Composer `autoload.php` file from the plugin to the `$mu_plugins` list. <!-- TODO: Validate that this still works. -->

```php
// Add your mu-plugins here.
$mu_plugins = [
	'/../plugins/pantheon-wordpress-edge-integrations/vendor/composer/autoload.php',
];
```

Requiring the `autoload.php` file from inside the plugin will ensure that any files that are autoloaded using Composer will be loaded into WordPress. Alternately, you can `require` this file anywhere in your project that makes sense, for example, in a `wp-config.php` file or some file that's included from `wp-config`, as long as it is available before `plugins_loaded`.