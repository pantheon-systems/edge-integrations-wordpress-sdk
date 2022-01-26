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

### Installing into a project without Integrated Composer but Composer is installed

If you aren't running a project with Integrated Composer but you _do_ use Composer otherwise, you can still get started with the Edge Integrations WordPress SDK without too much trouble.

#### Step 1: Clone this repository

The first step is cloning this repository:

```bash
git clone git@github.com:pantheon-systems/edge-integrations-wordpress-sdk.git
```

Where it's cloned isn't important, but we recommend cloning it into `mu-plugins`.

#### Step 2: `composer install`

After you've cloned the repository, you'll need to run `composer install` to pull down the dependent packages that make this SDK. `cd` into the directory you cloned into and run the `composer install` command. For example, if you cloned into `mu-plugins` your full command history will look like this:

```bash
cd mu-plugins
git clone git@github.com:pantheon-systems/edge-integrations-wordpress-sdk.git
cd edge-integrations-wordpress-sdk
composer install
```

Running the `install` command will pull down the [`pantheon-edge-integrations` library](https://github.com/pantheon-systems/pantheon-edge-integrations) and the [`pantheon-wordpress-edge-integrations` WordPress plugin](https://github.com/pantheon-systems/pantheon-edge-integrations).

#### Step 3: Add to `mu-plugins` loader file

To load the library and the plugin, we need to tell WordPress about them, especially since they are now in a non-standard location.