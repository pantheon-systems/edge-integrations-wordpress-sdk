# Pantheon Edge Integrations WordPress SDK

## Archived project
This project is **archived** as of August 2024 as it no longer receives active development.
The architecture provided by the tools in this SDK and the related projects are still valid and will continue to work on Pantheon AGCDN. However, we will not be responding to issues or pull requests or building these tools out more than they are already.

[![Unsupported](https://img.shields.io/badge/pantheon-deprecated-yellow?logo=pantheon&color=FFDC28)](https://docs.pantheon.io/oss-support-levels#deprecated) ![Packagist Version](https://img.shields.io/packagist/v/pantheon-systems/edge-integrations-wordpress-sdk) ![Commits since latest release](https://img.shields.io/github/commits-since/pantheon-systems/edge-integrations-wordpress-sdk/latest) ![MIT License](https://img.shields.io/github/license/pantheon-systems/edge-integrations-wordpress-sdk)

Welcome to the Pantheon Edge Integrations WordPress SDK!

This repository serves as a one-stop shop for integrating your WordPress site on Pantheon with our Edge Integrations toolset.

## Architecture

The diagram below illustrates the general overview of what this SDK provides and how the pieces fit together.

```mermaid
flowchart TB
agcdn[/Pantheon Advanced Global CDN\]-->ei[Pantheon Edge Integrations global library]
ei-->eiplugin(Pantheon WordPress Edge Integrations plugin)
eiplugin-. Optional -.->geoipplugin(Pantheon Geolocation Shortcodes plugin)
eiplugin-. Optional -.->consent(Pantheon Edge Integrations Consent Management plugin)
```

### Description

The Edge Integrations WordPress SDK is made up of several components that, in addition to the documentation stored in this repository, are all installed automatically when you `composer require` the project in your WordPress project root.

#### Pantheon Advanced Global CDN
Edge Integrations start with the "edge" itself, the CDN layer that is the last stop before a page is rendered in your browser. Pantheon's [Advanced Global CDN](https://pantheon.io/docs/guides/professional-services/advanced-global-cdn) has enabled Varnish configuration rules on our AGCDN platform to allow for geolocation information and interest tracking data to be sent back and forth with the CDN, enabling CDN caching for content personalized by those parameters. AGCDN is the first step for Pantheon Edge Integrations and allows us to render cached versions of personalized pages.

#### Pantheon Edge Integrations global library
The [Pantheon Edge Integrations](https://github.com/pantheon-systems/pantheon-edge-integrations) global library allows developers to interact with the header data sent to and from the CDN. This is a low level interface that simplifies the process of communicating with and interpretting headers sent from the CDN. It's important to note that the Edge Integrations library is built as a generic, CMS-agnostic PHP package, and is used as the base of both the WordPress and the Drupal implementations.

#### Pantheon WordPress Edge Integrations plugin
The [WordPress Edge Integrations](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations) plugin adds namespaced functions (e.g. `Pantheon\EI\WP\get_geo()` and `Pantheon\EI\WP\get_interest()`), hooks and filters that can empower WordPress developers to use our edge integrations for personalization without directly interfacing with the global library. It includes opinionated helper functions that guide the parameters and return values of our functions as well as implements interest tracking based on post categories (by default).

#### Pantheon Geolocation Shortcodes plugin
The [Pantheon Geolocation Shortcodes](https://github.com/pantheon-systems/pantheon-geolocation-shortcodes) plugin is an optional addition that can be included if all you want to do is display specific content in posts and pages to some geographic regions, but not other geographic regions. Parameters exist to display content by continent, country, region and city as well as allowing for conditions like `not_continent` and `not_city`.

#### Pantheon Edge Integrations Consent Management plugin
The [Pantheon Edge Integrations Consent Management](https://github.com/pantheon-systems/pantheon-edge-integrations-consent-management) plugin is another optional addition that can be included to enable a cookie consent banner that integrates natively with Pantheon Edge Integrations. It can be used as a consent management solution as-is, as a framework for developing your own bespoke consent management solution with Edge Integrations, or as a reference when integrating with a third-party consent management plugin. 

## Setup

### Install with Composer

Adding Edge Integrations support to your Composer-based project is simple and is the recommended means of adding the Edge Integrations WordPress SDK.

#### Requiring the Composer package

To get started, all you need to do is to add this repository as a dependency:

```bash
composer require pantheon-systems/edge-integrations-wordpress-sdk
```

That command will add this repository to your `/vendor` directory, as well as all of the dependencies, which include a [global, CMS-agnostic PHP library](https://github.com/pantheon-systems/pantheon-edge-integrations) and a [WordPress plugin](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations) as well as all of the documentation for the SDK.

Alternately, you can add `pantheon-systems/edge-integrations-wordpress-sdk` as a dependency to your project's `composer.json` file and run `composer install`.

### Install manually

If you do not use Composer on your project at all, you can still get started with the WordPress Edge Integrations plugin without any hassle. In this case, you won't be installing the SDK package, instead, go to the [Pantheon WordPress Edge Integrations Releases page](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations/releases).

* Download the Source Code (zip) file associated with the most recent version.
* Extract the plugin in your `wp-content/plugins` directory. You will get all of the compiled assets and included dependencies, including the CMS-agnostic, [global PHP library](https://github.com/pantheon-systems/pantheon-edge-integrations) in the package.

### Activate the plugin

In either case, the last step is activating the plugin from your WordPress dashboard Plugins page. There is no other admin interface for the WordPress plugin -- all the features and components are handled in the code itself, with hooks that developers can use to interact with the geolocation and interest tracking features.
