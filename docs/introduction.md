# Website Personalization Overview

Website Personalization is the process of creating customized experiences for visitors to a website. Rather than providing a single experience for all visitors, website personalization allows you to give visitors unique experiences tailored to their needs and desires. With this SDK, you will be able to personalize based on Geotargeting(geo) and Interest targeting.

## Geotargeting Functionality

Geotargeting is a method that delivers different content to visitors based on their geolocation. This includes country, region, city, and other criteria.

### Geotargeting Default Behavior and Available Customizations

Personalized data can be served to visitors based on an array of geo data types. With the `get_geo` function, you can get location-specific data from site visitors, which includes: `country`, `region`, `city`, `continent`, `conn-speed`  (connection speed, e.g. `broadband`) and `conn-type` (connection type, e.g. `wireless`). You can modify these data types using the `pantheon.ei.geo_allowed_values` filter. 

You can also access geo data via the `pantheon.ei.before_get_geo` action. This action fires after the geo data is retrieved, but before it is returned. It allows developers to hook into the geo data retrieval process and access the geo value, the type of data requested, and the full passed data, if it exists.

Additionally, you can retrieve and alter geo data with the `pantheon.ei.get_geo` filter. This filter fires after the data is parsed and before it is returned, making this the last stop before data is output. It also allows developers to modify the requested geo data.

### Test Geotargeting

Geotargeting can be tested or verified in two different ways.

- Use the `pantheon.ei.parsed_geo_data` filter to get the geo data from the [`HeaderData` class](https://github.com/pantheon-systems/pantheon-edge-integrations/) and allow it to be filtered. This filter allows you to spoof geo information by passing in `city`, `region`, `country`, etc.

- Use the `get_geo` function to return the visitor's location from the `HeaderData` class, which can be used in a variety of ways to display personalized content for a given visitor.

## Interest Targeting Functionality

The Interest targeting functionality gathers a visitor's behavioral data and interactions with a site that has the [Pantheon WordPress Edge Integrations plugin](https://github.com/pantheon-systems/pantheon-wordpress-edge-integrations/) installed and activated.

When a visitor navigates to 3 or more posts containing a given taxonomy term, that term (or terms) is considered an Interest. When an Interest is defined, a cookie containing the Interest data is created and pushed to the `HeaderData` class.

Interests can then be fetched from the `HeaderData` class and used to serve personalized content in a variety of ways, including cached pages or related content blocks.

### Interest Default Behavior and Available Customizations

By default, the WordPress plugin uses the default taxonomy, `category`, to determine Interests. This taxonomy can be changed, or added to, using the `pantheon.ei.taxonomy` filter.

The number of views it takes for a term to be considered an Interest is automatically set to 3. However, this number, or threshold, can be modified using the `pantheon.ei.interest_threshold` filter.

The post type that is used to determine Interests is `post` by default, but can be modified using `pantheon.ei.post_types` filter.

### Test Interest Targeting

Interests can be tested or verified in two different ways.

- Use the `pantheon.ei.parsed_interest_data` filter to get, and modify, Interest data from the `HeaderData` class. With this filter, you can confirm whether an Interest is set, and modify the Interest data before it is returned by the `get_interest` function.

- Use the `get_interest` function. You can return the Interest(s) from the `HeaderData` class, which can be used with the `WP_Query` class to fetch personalized content for a given visitor.

### Code Samples

- [Geolocation](https://github.com/pantheon-systems/edge-integrations-wordpress-sdk/blob/main/docs/geo.md)

- [Interest](https://github.com/pantheon-systems/edge-integrations-wordpress-sdk/blob/main/docs/interest.md)