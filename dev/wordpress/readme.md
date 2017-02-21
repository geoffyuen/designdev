# WordPress

## Things I have to lookup every time

### Register menus

    register_nav_menus( array(
    	'main_menu' => 'Navigation Bar',
    	'social_menu' => 'Your Social Account URLs'
    ) );

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

