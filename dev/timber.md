Theme url (for accessing theme assets like images, etc);

`{{ theme.link }}`

To use  `{{ dump(something) }}` add this to \wp_config.php :

`define( 'WP_DEBUG', true );`

or if you get errors in the Admin:
```
ini_set('display_errors','Off');
ini_set('error_reporting', E_ALL );
define('WP_DEBUG', true);
define('WP_DEBUG_DISPLAY', false);
```
