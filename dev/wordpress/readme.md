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
