# WordPress Edge Integrations: API

## Constant reference

### `PANTHEON_EDGE_INTEGRATIONS_DIR`

The path to the Pantheon Edge Integrations plugin.

### `PANTHEON_EDGE_INTEGRATIONS_FILE`

The path to the Pantheon Edge Integrations main plugin file.

### `PANTHEON_EDGE_INTEGRATIONS_VERSION`

The current version of the Pantheon Edge Integrations plugin.

## Function reference

### `get_supported_vary_headers`

Gets an array of the vary headers supported by the plugin. Before returning the array of vary headers, the [`pantheon.ei.supported_vary_headers`](#pantheoneisupportedvaryheaders) filter is applied. Only the headers (the _keys_ of `pantheon.ei.supported_vary_headers`) are returned.

#### Return

__(array)__ An array of the vary headers supported by the plugin.

## Action reference

### `pantheon.ei.after_enqueue_script`

Fires immediately after the `pantheon-ei` script is enqueued.

#### Parameters

`$args` _(array)_ An arguments array containing `plugin_version` (the `PANTHEON_EDGE_INTEGRATIONS_VERSION` value) and `plugin_file` (the `PANTHEON_EDGE_INTEGRATIONS_FILE` value).

#### Example

```php
add_action( 'pantheon.ei.after_enqueue_script', 'after_enqueue_script' );
function after_enqueue_script( array $args ) {
	$plugin_version = $args['plugin_version'];
	$plugin_file    = $args['plugin_file'];

	wp_localize_script( 'pantheon-ei', 'myLocalizedObj', [
		'plugin_version' => $plugin_version,
		'plugin_file'    => $plugin_file,
	] );
}
```

## Filter reference

### `pantheon.ei.supported_vary_headers`

Allows developers to modify the list of vary headers that are supported by the plugin.

Array keys are the vary headers, and the values are whether or not they are supported.

#### Parameters

__(array)__ An array of vary headers and whether or not they are supported. The default values are below:

```php
$vary_headers = [
	'Audience-Set' => true,
	'Audience' => false,
	'Interest' => true,
];
```

#### Example
To set rich Geolocation data as the only supported personalization type:

```php
add_filter( 'pantheon.ei.supported_vary_headers', 'filter_vary_headers' );
function filter_vary_headers( array $vary_headers ) {
	$vary_headers['Audience'] = false;
	$vary_headers['Interest'] = false;

	return $vary_headers;
}
```

To use the country-based Geolocation data as the only supported personalization type:

```php
add_filter( 'pantheon.ei.supported_vary_headers', 'filter_vary_headers' );
function filter_vary_headers( array $vary_headers ) {
	$vary_headers['Audience-Set'] = false;
	$vary_headers['Interest'] = false;
	$vary_headers['Audience'] = true;

	return $vary_headers;
}
```

To set the vary headers to not be sent until consent has been granted (see also [Pantheon Edge Integrations Consent Management](https://github.com/pantheon-systems/pantheon-edge-integrations-consent-management)):

```php
function check_consent() {
	if ( ! function_exists( 'wp_has_consent' ) ) {
		return;
	}

	if ( ! wp_has_consent() ) {
		add_filter( 'pantheon.ei.supported_vary_headers', 'do_not_send_vary_headers' );
	}
}

function do_not_send_vary_headers() : array {
	return [
		'Audience-Set' => false,
		'Audience' => false,
		'Interest' => false,
	];
}
```