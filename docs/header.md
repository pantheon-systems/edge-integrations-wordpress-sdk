# WordPress Edge Integrations: Vary Header

## Filter reference

### `pantheon.ei.supported_vary_headers`

Modify the vary headers supported by the plugin.

#### Parameters

_(array)_ An array of vary headers supported by the plugin.

#### Example

```php
add_filter( 'pantheon.ei.supported_vary_headers', 'supported_vary_headers' );

function supported_vary_headers( array $data ) : array {
	// Disable Interest header.
	$data['Interest'] = false;
	return $data;
}
```