# Interests

Engineers are able to customize the data used for interest personalization. Such as:

- Terms: The post terms used to define a personalized experience for an end user. Additional terms can be added, or existing terms can be excluded.
- Threshold: The number of times a page with a particular taxonomy term should be viewed before that term is considered an interest.
- Taxonomies: Define which taxonomies can be interests. `category` is the interest taxonomy by default.

## Available filters

### `pantheon.ei.localized_terms`

Modify terms before they are localized.

#### Parameters

$terms __(array)__ An array of terms to add.

```bash
add_filter( 'pantheon.ei.localized_terms', 'pantheon_ei_add_term' );
function pantheon_ei_add_term( $terms ) {
	$terms[] = 'term-from-theme';

	return $terms;
}
```

### `pantheon.ei.interest_threshold`

Modify the interest threshold. Default `3`.

#### Parameters

$threshold __(int)___ The interest threshold.

```bash
add_filter( 'pantheon.ei.interest_threshold', 'pantheon_ei_change_threshold' );
function pantheon_ei_change_threshold() {
	return 5;
}
```

### `pantheon.ei.taxonomy`

Modify the targeted taxonomy. Default `category`.

#### Parameters

$taxonomy __(array)__  An array of taxonomies to target for personalization.

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

### `pantheon.ei.post_types`

Modify post type support. Default `post`.

#### Parameters

$post_type __(array)__ An array of post types to target for personalization.

```bash
add_filter( 'pantheon.ei.post_types', 'pantheon_ei_add_post_type' );
function pantheon_ei_add_post_type( $post_types ) {
	$post_types[] = 'my-custom-post-type';

	return $post_types;
}
```
