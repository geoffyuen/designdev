- [URLs and Paths](#urls-and-paths)
- [Debugging](#debuging)
- [Menus](#menus)

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
