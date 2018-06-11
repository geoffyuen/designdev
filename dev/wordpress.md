# WordPress

## General

- This guys SO is a goldmine: https://wordpress.stackexchange.com/users/9364/stephen-harris

## Plugins

- Login Designer: https://wordpress.org/plugins/login-designer/

## Things I have to lookup every time

- [Register menus](#register-menus)
- [Enqueue Jquery that doesn't come installed in WP (still on v1 at the time of this writing)](#enqueue-jquery-that-doesnt-come-installed-in-wp-still-on-v1-at-the-time-of-this-writing)
- [Enqueue CSS, Googlefonts and JS](#enqueue-css-googlefonts-and-js)
- [Change styling of the wysiwyg](#change-styling-of-the-wysiwyg)
- [Add .classes to the wysiwg dropdown menu](#add-classes-to-the-wysiwg-dropdown-menu)
- [Get posts with a taxonomy](#get-posts-with-a-taxonomy)
- [Add honeypot to comment form](#add-honeypot-to-comment-form)
- [Redirect Child page to Parent](#redirect-child-page-to-parent)
- [WYSIWYG classes](#wysiwyg-classes)
- [Change user password via phpmyadmin](#change-user-password-via-phpmyadmin)
- [Gravity Forms](#gravity-forms)
- [Collection of functions.php snippets:](#collection-of-functionsphp-snippets)
- [Plugin maker CRUD thingy](#plugin-maker-crud-thingy)
- [MySQL posts showing return and newline characters \r\n](#mysql-posts-showing-return-and-newline-characters-rn)
- [Don't use Contact Form 7 CSS](#dont-use-contact-form-7-css)
- [Add custom class or id to Contact Form 7](#add-custom-class-or-id-to-contact-form-7)


### Register menus

    register_nav_menus( array(
    	'main_menu' => 'Navigation Bar',
    	'social_menu' => 'Your Social Account URLs'
    ) );

### Enqueue Jquery that doesn't come installed in WP (still on v1 at the time of this writing)

functions.php

    function jquery_enqueue() {
        wp_enqueue_script('jquery');
        wp_register_script('jquery', '//ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js', false, null);
    }
    if ( !is_admin() ) {
        add_action('wp_enqueue_scripts', 'jquery_enqueue', 11);
    };

### Enqueue CSS, Googlefonts and JS

    function theme_assets() {
        wp_enqueue_style( 'googlefonts', 'https://fonts.googleapis.com/css?family=Lato:300,300i,900,900i' );
        wp_enqueue_style( 'slickcss', 'https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.6.0/slick.min.css' );
        wp_enqueue_style( 'theme-style', get_stylesheet_uri() );
        wp_deregister_script('jquery');
        wp_enqueue_script( 'slickjs', 'https://cdnjs.cloudflare.com/ajax/libs/slick-carousel/1.6.0/slick.min.js', array( 'jquery' ), '', true );
        wp_enqueue_script( 'theme-scripts', get_stylesheet_directory_uri() . '/js/main.js', array( 'jquery', 'slickjs' ), '', true );
    }

    add_action( 'wp_enqueue_scripts', 'theme_assets' );

### Change styling of the wysiwyg

functions.php:

    add_editor_style('editor.css');

editor.css:

    .mceContentBody.wp-editor {
    	background-color: #ddd;
    	font-family: 'Lato', sans-serif;
    }

Why? If you have white text you can't see it. 

### Add .classes to the wysiwg dropdown menu

functions.php

    function wpb_mce_buttons_2($buttons) {
        array_unshift($buttons, 'styleselect');
        return $buttons;
    }
    add_filter('mce_buttons_2', 'wpb_mce_buttons_2');

    function my_mce_before_init_insert_formats( $init_array ) {
        $style_formats = array(
            array(
                'title' => 'UPPERCASE',
                'block' => 'span',
                'classes' => 'UC',
                'wrapper' => true,

            ),
            array(
                'title' => 'Button (dark)',
                'block' => 'span',
                'classes' => 'btn',
                'wrapper' => true,
            ),
            array(
                'title' => 'Button (light)',
                'block' => 'span',
                'classes' => 'btn btn--rev',
                'wrapper' => true,
            ),
        );
        $init_array['style_formats'] = json_encode( $style_formats );
        return $init_array;
    }
    // Attach callback to 'tiny_mce_before_init'
    add_filter( 'tiny_mce_before_init', 'my_mce_before_init_insert_formats' );

### Get posts with a taxonomy

    $args = array(
        'post_type' => 'post',
        'tax_query' => array(
            array(
                'taxonomy' => 'people',
                'field'    => 'slug',
                'terms'    => 'bob',
            ),
        ),
    );
    $query = new WP_Query( $args );
    
Ref: https://codex.wordpress.org/Class_Reference/WP_Query#Taxonomy_Parameters

## Add honeypot to comment form

```
function elio_add_honeypot() {
    echo '<p style="display:none!important"><input type="text" name="gc-email-verify" id="gc-email-verify"></p>';
}
function elio_check_honeypot( $approved ) {
    return empty( $_POST['gc-email-verify'] ) ? $approved : 'spam';
}

add_action( 'comment_form', 'elio_add_honeypot' );
add_filter( 'pre_comment_approved', 'elio_check_honeypot' );
```

If you're using Timber, you should manually add the field in the first function. At this time I'm not sure if the filter (2nd function) actually fires.

- https://elio.blog/2014/04/prevent-wordpress-comment-spam-with-a-honeypot/

## Redirect Child page to Parent

- http://askwpgirl.com/redirect-parent-page-first-child-page-wordpress/

## WYSIWYG classes

- https://digwp.com/2010/05/default-wordpress-css-styles-hooks/

## Change user password via phpmyadmin

- http://www.wpbeginner.com/beginners-guide/how-to-reset-a-wordpress-password-from-phpmyadmin/

## Gravity Forms

- https://gravitywiz.com/

## Collection of functions.php snippets:

- http://wordpress.stackexchange.com/questions/1567/best-collection-of-code-for-your-functions-php-file

## Plugin maker CRUD thingy

- http://projects.tareq.co/wp-generator/

## MySQL posts showing return and newline characters \r\n

```
UPDATE `wp_posts` SET `post_content` = REPLACE(`post_content`, '\\r\\n', '\r\n');
UPDATE `wp_posts` SET `post_content` = REPLACE(`post_content`, '\\n', '\n');
UPDATE `wp_posts` SET `post_content` = REPLACE(`post_content`, '\\r', '\r');
```

## Don't use Contact Form 7 CSS

```
add_action( 'wp_print_styles', 'wps_deregister_styles', 100 );
function wps_deregister_styles() {
    wp_deregister_style( 'contact-form-7' );
}
```

## Add custom class or id to Contact Form 7

Form specific:

```
[contact-form-7 id="1234" title="Contact form 1" html_id="contact-form-1234" html_class="form contact-form"]
```

Field specific:

```
[text* first-name class:full class:field placeholder "FIRST NAME"]
```
