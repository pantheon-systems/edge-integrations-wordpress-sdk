# WordPress Edge Integrations: API

## Namespace: `Pantheon\EI\WP\API`

The namespace for the API functionality is `Pantheon\EI\WP\API`. When using functions that are part of this namespace, it is recommended that you `use` the namespace at the top of your file.

```php
use Pantheon\EI\WP\API;
```

Doing this allows you to use the functions without the full namespace prefix. 

**More information**

* [Namespaces](https://www.php.net/manual/en/language.namespaces.php) (php.net)
* [Namespace and Function Imports](https://engineering.hmn.md/standards/style/php/#namespace-and-function-imports) (engineering.hmn.md/standards)

## API Documentation and Testing

Full documentation on the API endpoints and access to test responses is available on [Stoplight](https://pantheon.stoplight.io/docs/edge-integrations/fed9ddb2a5046-ei).

## Endpoint reference

### `pantheon/v1/ei`

The main Pantheon Edge Integrations API endpoint.

**Return Type:** _object_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/0cda792ad26fe-ei)

### `pantheon/v1/ei/config`

Current Edge Integrations configuration.

**Return Type:** _object_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/edaa3dbe9bca3-ei-config)

### `pantheon/v1/ei/config/geo/allowed`

Edge Integrations Geolocation configuration settings.

**Return Type:** _array_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/96585a3c74391-ei-config-geo-allowed)

### `pantheon/v1/ei/config/interest/cookie-expiration`

The interest cookie expiration in days.

**Return Type:** _int_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/15b15bd2b7eff-ei-config-interest-cookie-expiration)

### `pantheon/v1/ei/config/interest/post-types`

The currently enabled post types for interest tracking.

**Return Type:** _array_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/c5db87f36cc21-ei-config-interest-post-types)

### `pantheon/v1/ei/config/interest/taxonomies`

The current list of enabled taxonomies for Edge Integrations interest tracking.

**Return Type:** _array_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/fb47b8ec8fa31-ei-config-interest-taxonomies)

### `pantheon/v1/ei/config/interest/threshold`

The Edge Integrations interest tracking threshold.

**Return Type:** _int_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/970ac042750be-ei-config-interest-threshold)

### `pantheon/v1/ei/segments`

Returns a list of enabled segments for personalization.

**Return Type:** _object_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/48045c3028625-ei-segments)

### `pantheon/v1/ei/segments/geo`

The list of available geolocation segments.

**Return Type:** _array_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/68d178a2e5511-ei-segments-geo)

### `pantheon/v1/ei/segments/interests`

The list of available interest terms based on the enabled interest taxonomies.

**Return Type:** _array_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/79cac6693543c-ei-segments-interests)

### `pantheon/v1/ei/user`

Current Edge Integrations client data.

#### Query parameters

All the Edge Integrations user endpoints can have any of the following query parameters added to the URL to return the specified data.

##### `city`

The city of the user.

##### `conn-speed`

The connection speed of the user.

##### `conn-type`

The connection type of the user.

##### `continent-code`

The continent code of the user.

##### `country-code`

The country code of the user.

##### `country-name`

The country name of the user.

##### `region`

The region of the user.

##### `interest`

The user's interest.

**Return Type:** _object_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/9adbc8702b480-ei-user)

### `pantheon/v1/ei/user/conn-speed`

Current user connection speed.

**Return Type:** _string_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/df582b33b8768-ei-user-conn-speed)

### `pantheon/v1/ei/user/conn-type`

The current user connection type.

**Return Type:** _string_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/eb8e9ddfc5c03-ei-user-conn-type)

### `pantheon/v1/ei/user/geo/city`

The current user city.

**Return Type:** _string_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/dfa8f040f1594-ei-user-geo-city)

### `pantheon/v1/ei/user/geo/country-code`

The current user country code.

**Return Type:** _string_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/d869daad71b8d-ei-user-geo-country)

### `pantheon/v1/ei/user/geo/country-name`

The current user country name.

**Return Type:** _string_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/d869daad71b8d-ei-user-geo-country)

### `pantheon/v1/ei/user/geo/region`

The current user's region, state, or province.

**Return Type:** __

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/d869daad71b8d-ei-user-geo-region)

### `pantheon/v1/ei/user/interest`

The current user interest.

**Return Type:** _string_

[Reference](https://pantheon.stoplight.io/docs/edge-integrations/d50bfdfaea613-ei-user-interest)
