# WordPress Edge Integrations: Interest

## Function reference

### `get_interest`

Return or alter interest data in the global header.

#### Parameters

__(array)__ Data to pass to the HeaderData class. If an empty arrat is passed, `get_interest` will return all Interest data.

#### Return

_(string)_ The interest data in a JSON encoded string.

#### Example

```php
use Pantheon\EI\WP\Interest;

// Returns interest data from HeaderData class.
$interest = Interest\get_interest();

// Manually pass data to interest header.
$data = ['HTTP_INTEREST' =>'Carl Sagan|Richard Feynman'];
$interest = Interest\get_interest( $data );
```

### `set_interest`

Set the interest header key and data.

#### Parameters

$key __(array)__ Key for the header, or array of keys.
$data __(array)__ Data to pass to the HeaderData class.

#### Example

```php
use Pantheon\EI\WP\Interest;

$key = [ 'Comes' ];

$data = [
    'HTTP_IGNORED' => 'HTTP Ignored Entry',
    'IGNORED_ENTRY' => 'Completely ignored entry',
    'HTTP_SHOULD_BE_FOUND' => 'Should be found',
    'HTTP_VARY' => 'Something, Wicked, This, Way',
];

Interest\set_interest( $key, $data )
```

## Filter reference

### `pantheon.ei.localized_terms`

Modify terms before they are localized.

#### Parameters

__(array)__ An array of terms to modify.

#### Example

Add term to array:
```php
add_filter( 'pantheon.ei.localized_terms', 'pantheon_ei_add_term' );
function pantheon_ei_add_term( array $terms ) : array {
	$terms[] = 'term-from-theme';

	return $terms;
}
```

Remove term(s) from array:
```php
add_filter( 'pantheon.ei.localized_terms', 'pantheon_ei_remove_term' );
function pantheon_ei_remove_term( array $terms ) : array {
	// This can be one or many terms.
	$terms_to_remove = [ 'category-1', 'category-2' ];

	foreach ( $terms_to_remove as $term ) {
		$key = array_search( $term, $terms );
		if ( $key !== false ) {
			unset( $terms[ $key ] );
		}
	}

	return array_values( $terms );
}
```

### `pantheon.ei.interest_threshold`

Modify the interest threshold. Default `3`.

#### Parameters

__(int)___ The interest threshold.

#### Example

```php
add_filter( 'pantheon.ei.interest_threshold', 'pantheon_ei_change_threshold' );
function pantheon_ei_change_threshold() : int {
	return 5;
}
```

## `pantheon.ei.taxonomy`

Modify the targeted taxonomy. Default `category`.

### Parameters

__(array)__  An array of taxonomies to target for personalization.

#### Example

Replace default taxonomy:
```php
add_filter( 'pantheon.ei.taxonomy', 'pantheon_ei_replace_taxonomy' );
function pantheon_ei_replace_taxonomy( array $taxonomy ) : array {
	$taxonomy = 'my-custom-taxonomy';

	return $taxonomy;
}
```

Add interest taxonomy:
```php
add_filter( 'pantheon.ei.taxonomy', 'pantheon_ei_add_taxonomy' );
function pantheon_ei_add_taxonomy( array $taxonomy ) : array {
	$taxonomy[] = 'my-custom-taxonomy';

	return $taxonomy;
}
```

### `pantheon.ei.post_types`

Modify post type support. Default `post`.

#### Parameters

__(array)__ An array of post types to target for personalization.

#### Example

```php
add_filter( 'pantheon.ei.post_types', 'pantheon_ei_add_post_type' );
function pantheon_ei_add_post_type( array $post_types ) : array {
	$post_types[] = 'my-custom-post-type';

	return $post_types;
}
```

### `pantheon.ei.parsed_interest_data`

Get the interest data from the HeaderData class and allow it to be modified.

#### Parameters

__(array)__ The full, parsed Interest data as an array.

#### Example

```php
add_filter( 'pantheon.ei.parsed_interest_data', 'pantheon_ei_parsed_interest_data' );
function pantheon_ei_parsed_interest_data( array $data ) : array {
	// Add term to array of interests.
	$data[] = 'some-interest';

	return $data;
}
```

### `pantheon.ei.set_interest_data`

Modify HeaderData being set as a vary header from set_interest.

#### Parameters

__(array)__ Interest data as an array.

#### Example

```php
add_filter( 'pantheon.ei.set_interest_data', 'pantheon_ei_set_interest_data' );
function pantheon_ei_set_interest_data( array $data ) : array {
	// Remove last element from $data.
	return array_pop( $data );
}
```
