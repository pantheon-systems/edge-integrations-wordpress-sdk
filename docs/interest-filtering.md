# Interests

Engineers are able to customize the data used for interest personalization. Such as:

- Terms: The post terms used to define a personalized experience for an end user. Additional terms can be added, or existing terms can be excluded.
- Threshold: The number of times a page with a particular taxonomy term should be viewed before that term is considered an interest.
- Taxonomies: Define which taxonomies can be interests. `category` is the interest taxonomy by default.

## Available filters

`pantheon.ei.localized_terms`: modify terms before they are localized.

```bash
add_filter( 'pantheon.ei.localized_terms', 'pantheon_add_ei_term' );
function pantheon_add_ei_term( $terms ) {
	$terms[] = 'term-from-theme';

	return $terms;
}
```

`pantheon.ei.interest_threshold`: modify the interest threshold. Default `3`.

```bash
add_filter( 'pantheon.ei.interest_threshold', 'pantheon_ei_threshold' );
function pantheon_ei_threshold() {
	return 5;
}
```

`pantheon.ei.taxonomy`: modify the targeted taxonomy. Default `category`.

Replace default taxonomy:
```bash
add_filter( 'pantheon.ei.taxonomy', 'pantheon_ei_taxonomy' );
function pantheon_ei_taxonomy( $taxonomy ) {
	$taxonomy = 'my-custom-taxonomy';

	return $taxonomy;
}
```

Add interest taxonomy:
```bash
add_filter( 'pantheon.ei.taxonomy', 'pantheon_ei_taxonomy' );
function pantheon_ei_taxonomy( $taxonomy ) {
	$taxonomy[] = 'my-custom-taxonomy';

	return $taxonomy;
}
```

`pantheon.ei.post_types`: modify post type support. Default `post`.

```bash
add_filter( 'pantheon.ei.post_types', 'pantheon_ei_post_type' );
function pantheon_ei_post_type( $post_types ) {
	$post_types[] = 'my-custom-post-type';

	return $post_types;
}
```
