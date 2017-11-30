# [Timber, Twig, Wordpress Cheatsheet](#timber-twig-wordpress-cheatsheet)

- [Documentation](#documentation)
- [Comment Form with WPML](#comment-form-with-wpml)
- [Theme translation hack for WPML String Translation](#theme-translation-hack-for-wpml-string-translation)
- [jQuery](#jquery)
- [Menus](#menus)
- [URLs and Paths](#urls-and-paths)
- [Debuging](#debuging)

## Documentation

- https://github.com/timber/timber/tree/master/docs

## Comment Form with WPML

First, the form needs to submit to the correct url:

Change the action from this
```
<form id="form" class="comment-form" method="post" action="{{ site.url ~ '/wp-comments-post.php' }}">
```

to

```
<form id="form" class="comment-form" method="post" action="{{ fn('get_option','siteurl') }}/wp-comments-post.php">
```

The reason for this change is that WPML adds the two letter language to the site.url / site.link (or maybe Timber does...). Eg. If you're in the French site, the url will be `thesitedomain.com/fr`. This will trip up the form submission unless you change it.

Addtionally, the form needs the 2 letter language code added inside the custom comment form to return to the correct page after submitting:

```
<input name="wpml_language_code" type="hidden" value="{{ site.language|split('-')[0] }}">
```

## Theme translation hack for WPML String Translation

When you do a string translation scan on your theme, WPML only crawls through `.php` files and not your `.twig` files. A way around this is to concatenate your `.twig` files into a `.php` file and then do a scan. In your templates folder do this:

```
echo "<?php">index.php ; cat *.twig >> index.php
```

It doesn't matter that the result isn't really php. All WPML is scanning for is `__("Your string to be translated", "Your theme text-domain")`.

## jQuery

```
jQuery(document).ready(function($) {
});
```

## Menus

I use this in twig:

`{{ fn("wp_nav_menu","&theme_location=main_menu&container=false") }}`

...defined in functions.php as:

```
register_nav_menus( array(
	'main_menu' => 'Main Menu',
	'footer_menu' => 'Footer Menu',
) );
```

If you want to use the Timber nav walker, add the menu to the timber context:
```
	function add_to_context( $context ) {
		$context['main_menu'] = new TimberMenu(3);
		$context['footer_menu'] = new TimberMenu(4);
		$context['site'] = $this;
		$context['sidebar1'] = Timber::get_widgets('sidebar-1');
		$context['sidebar2'] = Timber::get_widgets('sidebar-2');
		return $context;
	}
```

## URLs and Paths

Theme url (for accessing theme assets like images, etc);

`{{ theme.link }}`

## Debuging

To use  `{{ dump(something) }}` add this to \wp_config.php :

`define( 'WP_DEBUG', true );`

or if you get errors (in old PHP (5.3?)) in the Admin:
```
ini_set('display_errors','Off');
ini_set('error_reporting', E_ALL );
define('WP_DEBUG', true);
define('WP_DEBUG_DISPLAY', false);
```

## Integrating with Woocommerce 

- some great information starting here: https://github.com/timber/timber/issues/79#issuecomment-42515989
- should be aware that these methods may not be compatible with WC plugins/addons because of WC's heavy use of actions and hooks
