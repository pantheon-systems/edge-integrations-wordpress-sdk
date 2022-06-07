# WordPress Edge Integrations: Geo

## Namespace: `Pantheon\EI\WP\Geo`

The namespace for the analytics functionality is `Pantheon\EI\WP\Geo`. When using functions that are part of this namespace, it is recommended that you `use` the namespace at the top of your file.

```php
use Pantheon\EI\WP\Geo;
```

Doing this allows you to use the functions without the full namespace prefix. 

**More information**
* [Namespaces](https://www.php.net/manual/en/language.namespaces.php) (php.net)
* [Namespace and Function Imports](https://engineering.hmn.md/standards/style/php/#namespace-and-function-imports) (engineering.hmn.md/standards)

## Function reference

### `Geo\get_geo()`

Returns geolocation data for the current user.

#### Parameters

`$data_type` _(string)_ The type of geolocation data to return. `get_geo` accepts the following values: `country-code`, `country-name`, `region`, `city`, `continent-code`, `conn-speed`, `conn-type` or an empty string.The default data type is `''`. If an empty string is passed, `get_geo` will return all Audience data encoded in JSON format.

`$data` _(mixed)_ Data to pass directly into the `EI\HeaderData` class. By default, `EI\HeaderData` will use the `$_SERVER` superglobal to get the data.

#### Return

_(string)_ The specific requested geolocation data or all geolocation data in a JSON encoded string.

#### Example

```php
use Pantheon\EI\WP\Geo;
...
$geo = Geo\get_geo( 'country' ); // Returns the country ISO code for the current user, e.g. 'US'.

switch ( $geo ) {
	case 'US':
		esc_html_e( 'Howdy, American!', 'example' );
		break;
	case 'AU':
		esc_html_e( 'G\'day, Australian!', 'example' );
		break;
	case 'FR':
		esc_html_e( 'Bonjour, Français!', 'example' );
		break;
	default:
		esc_html_e( 'Hello, World!', 'example' );
		break;
}
```

### `Geo\get_geo_allowed_values()`

Returns the array of allowed geolocation data types.

__See [`pantheon.ei.geo_allowed_values`](#pantheon.ei.geo_allowed_values).__

#### Example

```php
use Pantheon\EI\WP\Geo;
...
// If the passed data type is not allowed, return an empty string.
if ( ! in_array( $data_type, Geo\get_geo_allowed_values(), true ) ) {
	return '';
}
```

## Filter reference

### `pantheon.ei.parsed_geo_data`

Takes the geolocation data from `EI\HeaderData` and allows it to be filtered.

For filtering purposes, the data passed is an array of key/value pairs of geolocation data. Because this filter fires after the data types are checked, it is _possible_ (but not recommended) to provide data that might otherwise be filtered out.

#### Parameters

_(array)_ The full, parsed Audience geolocation data as an array.

#### Example

```php
add_filter( 'pantheon.ei.parsed_geo_data', 'filter_parsed_geo_data' );

function filter_parsed_geo_data( array $data ) : array {
	$data['city'] = 'Salt Lake City';
	$data['region'] = 'Utah';
	$data['country'] = 'US';
	return $data;
}
```

### `pantheon.ei.get_geo`

Allows the geolocation data to be filtered. This filter fires after the data is parsed and immediately before it is returned. This is the last stop before the data is output.

#### Parameters

_(string)_ The requested geolocation data.

```php
add_filter( 'pantheon.ei.get_geo', 'override_get_geo' );

function override_get_geo( string $value ) : string {
	// European Union countries.
	$eu = [ 'AT', 'BE', 'BG', 'CY', 'CZ', 'DE', 'DK', 'EE', 'ES', 'FI', 'FR', 'GB', 'GR', 'HR', 'HU', 'IE', 'IT', 'LV', 'LT', 'LU', 'MT', 'NL', 'PL', 'PT', 'RO', 'SK', 'SI', 'SE' ];

	// Default to US if not in the EU.
	if ( ! in_array( $value, $eu ) ) {
		return 'US';
	}

	return $value;
}
```

### `pantheon.ei.geo_allowed_values`

Allow the list of geolocation data types to be filtered.

Note: This does not affect the actual data types that are returned in the header data. However, if the data type _is_ available, the `get_geo_allowed_values` return values can be filtered.

#### Parameters

_(array)_ The list of geolocation data types.

#### Example

```php
add_filter( 'pantheon.ei.geo_allowed_values', 'filter_geo_allowed_values' );

function filter_geo_allowed_values( array $values ) : array {
	$values[] = 'county';
	return $values;
}

get_geo( 'county' ); // Returns the county name for the current user, if available.
```

If fewer data types are expressly required, the filter allows the default data types to be removed.

```php
add_filter( 'pantheon.ei.geo_allowed_values', 'filter_geo_allowed_values' );

function filter_geo_allowed_values( array $values ) : array {
	// Remove unsupported data types.
	unset( $values['region'] );
	unset( $values['city'] );
	unset( $values['continent'] );
	unset( $values['lat'] );
	unset( $values['lon'] );
	unset( $values['latlon'] );
	unset( $values['conn-speed'] );
	unset( $values['conn-type'] );
	return $values;
}
```

## Action reference

### `pantheon.ei.before_get_geo`

Fires after the geolocation data is retrieved but before it is returned.

Allows developers to hook into the geolocation data retrieval process and access the geolocation value, the type of data being requested and the full, passed data, if it exists.

#### Parameters

`$value` _(string)_ The geolocation value.

`$data_type` _(string)_ The requested geolocation data type.

`$data` _(mixed)_ Data passed to the `EI\HeaderData` class. By default, this is pulled from the `$_SERVER` superglobal.

#### Example
```php
add_action( 'pantheon.ei.before_get_geo', 'before_get_geo' );

function before_get_geo( string $value, string $data_type, $data ) {
	if ( 'country' === $data_type && 'US' === $value ) {
		// Do something specific to US.
	}
}
```
