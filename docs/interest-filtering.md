# Interest filters

## `pantheon.ei.localized_terms`

Modify terms before they are localized.

### Parameters

$terms __(array)__ An array of terms to modify.

### Example

Add term to array:
```bash
add_filter( 'pantheon.ei.localized_terms', 'pantheon_ei_add_term' );
function pantheon_ei_add_term( $terms ) {
	$terms[] = 'term-from-theme';

	return $terms;
}
```

Remove term(s) from array:
```bash
add_filter( 'pantheon.ei.localized_terms', 'pantheon_ei_remove_term' );
function pantheon_ei_remove_term( $terms ) {
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

## `pantheon.ei.interest_threshold`

Modify the interest threshold. Default `3`.

### Parameters

$threshold __(int)___ The interest threshold.

### Example

```bash
add_filter( 'pantheon.ei.interest_threshold', 'pantheon_ei_change_threshold' );
function pantheon_ei_change_threshold() {
	return 5;
}
```

## `pantheon.ei.taxonomy`

Modify the targeted taxonomy. Default `category`.

### Parameters

$taxonomy __(array)__  An array of taxonomies to target for personalization.

### Example

Replace default taxonomy:
```bash
add_filter( 'pantheon.ei.taxonomy', 'pantheon_ei_replace_taxonomy' );
function pantheon_ei_replace_taxonomy( $taxonomy ) {
	$taxonomy = 'my-custom-taxonomy';

	return $taxonomy;
}
```

Add interest taxonomy:
```bash
add_filter( 'pantheon.ei.taxonomy', 'pantheon_ei_add_taxonomy' );
function pantheon_ei_add_taxonomy( $taxonomy ) {
	$taxonomy[] = 'my-custom-taxonomy';

	return $taxonomy;
}
```

## `pantheon.ei.post_types`

Modify post type support. Default `post`.

### Parameters

$post_type __(array)__ An array of post types to target for personalization.

### Example

```bash
add_filter( 'pantheon.ei.post_types', 'pantheon_ei_add_post_type' );
function pantheon_ei_add_post_type( $post_types ) {
	$post_types[] = 'my-custom-post-type';

	return $post_types;
}
```
