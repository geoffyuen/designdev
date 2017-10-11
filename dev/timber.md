# Timber, Twig, Wordpress Cheatsheet

- [URLs and Paths](#urls-and-paths)
- [Debugging](#debuging)
- [Menus](#menus)

## Comment Form with WPML

First, the form needs to submit to the correct url:

Change the action from this
```
<form id="form" class="comment-form" method="post" action="{{ site.url ~ '/wp-comments-post.php' }}">
```

to

```
<form id="form" class="comment-form" method="post" action="/wp-comments-post.php">
```

This assumes that Wordpress is installed at the root of the domain - otherwise use `get_option('siteurl')`. The reason for this change is that WPML adds the two letter language to the site.url (or maybe Timber does...). Eg. If you're in the French site, the url will be thesitedomain.com/fr. This will trip up the form submission unless you change it.

Addtionally, the form needs the 2 letter language code added inside the custom comment form to return to the correct page after submitting:

```
<input name="wpml_language_code" type="hidden" value="{{ site.language|split('-')[0] }}">
```

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
