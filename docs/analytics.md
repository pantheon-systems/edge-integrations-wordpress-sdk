# WordPress Edge Integrations: Analytics

## Function reference

### `get_gtm_code()`

Returns the Google Tag Manager (GTM) code for the current site, if one is set.

#### Return

__(bool|string)__ The GTM code for the current site, if one is set. Otherwise, returns `false` (the default). Can also be `true` if the filter is being used to override the GTM support built into the plugin. See [`pantheon.ei.gtm_code`](#pantheoneigtm_code).

#### Example

```php
$gtm_code = get_gtm_code();

// Bail early if we don't have a GTM code or if the GTM code is being overridden externally.
if ( is_bool( $gtm_code ) ) {
	return;
}
?>
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=<?php echo esc_attr( $gtm_code ); ?>"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
<?php
```

## Filter reference

### `pantheon.ei.gtm_code`

Allows the GTM code to be overridden. 

There are three possible values for the filter: `false`, `true` or a string. 

* `false` is the default, and assumes that no GTM code is set. 
* `true` is used to override the option in the WordPress admin General Settings page. If `true` is passed, no GTM codes will be output. This is useful for sites that do not want to use GTM or are using an external plugin to add the GTM codes.
* A string can be passed to the filter to define the GTM code. If a string is passed, the option will not appear in the WordPress admin General Settings page.

#### Parameters

__(bool|string)__ The GTM code for the current site.

#### Examples
Adding a GTM code via the filter:
```php
add_filter( 'pantheon.ei.gtm_code', 'override_gtm_code' );

function override_gtm_code( $gtm_code ) {
	return 'GTM-XXXXXXXX';
}
```

Disabling the GTM code via the filter:
```php
add_filter( 'pantheon.ei.gtm_code', '__return_true' );
```
