# WordPress

## Things I have to lookup every time

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

## Redirect Child page to Parent

- http://askwpgirl.com/redirect-parent-page-first-child-page-wordpress/

## Gravity Forms

- https://gravitywiz.com/

## Collection of functions.php snippets:

- http://wordpress.stackexchange.com/questions/1567/best-collection-of-code-for-your-functions-php-file

## Plugin maker CRUD thingy

- http://projects.tareq.co/wp-generator/
