# Pantheon Edge Integrations WordPress SDK

[![Unsupported](https://img.shields.io/badge/pantheon-unsupported-yellow?logo=pantheon&color=FFDC28)](https://github.com/topics/unsupported?q=org%3Apantheon-systems "Unsupported, e.g. a tool we are actively using internally and are making available, but do not promise to support")

Welcome to the Pantheon Edge Integrations WordPress SDK!

This repository serves as a one-stop shop for integrating your WordPress site on Pantheon with our Edge Integrations toolset.

## Setup

### Installing into a project with Integrated Composer.

Adding Edge Integrations support to your Integrated Composer project is simple and is the recommended means of adding the Edge Integrations WordPress SDK.

#### Requiring the Composer package

To get started, all you need to do is to add this repository as a dependency:

```bash
composer require pantheon-systems/edge-integrations-wordpress-sdk
```

That command will add this repository to your `/vendor` directory, as well as all of the dependencies, which include a [global, CMS-agnostic PHP library](https://github.com/pantheon-systems/pantheon-edge-integrations) and a [WordPress plugin](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations) as well as all of the documentation for the SDK.

Alternately, you can add `pantheon-systems/edge-integrations-wordpress-sdk` as a dependency to your project's `composer.json` file and run `composer install`.

### Installing manually

If you aren't running a project with Integrated Composer but you _do_ use Composer otherwise, you can still get started with the Edge Integrations WordPress SDK without too much trouble. This still assumes you have Composer installed on at least one machine.

#### Step 1: Clone or `composer require` the WordPress Edge Integrations plugin

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

This will install `pantheon-edge-integrations` into the plugin's `vendor` directory. The plugin itself will handle loading the library if it's installed.