# WordPress

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
- [Woocommerce](#woocommerce)
- [Single Product Hooks Visual Guide](#single-product-hooks-visual-guide)
- [Reorder single product template](#reorder-single-product-template)
- [When to use hooks, templates](#when-to-use-hooks-templates)
- [Subscription - let user choose length via dropdown](#subscription---let-user-choose-length-via-dropdown)
- [Customize the checkout page](#customize-the-checkout-page)
- [Add fields to checkout](#add-fields-to-checkout)
- [Hide shipping form for local pickup on checkout](#hide-shipping-form-for-local-pickup-on-checkout)
- [Limit shipping to one state](#limit-shipping-to-one-state)
- [Choose pickup time for local pickup (only on sameday)](#choose-pickup-time-for-local-pickup-only-on-sameday)
- [Product with no price, just for viewing](#product-with-no-price-just-for-viewing)
- [Change Select Text for variations](#change-select-text-for-variations)

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
## Woocommerce

- https://code.tutsplus.com/categories/woocommerce
- http://chrislema.com/woocommerce-category-pages/

### Single Product Hooks Visual Guide

- https://businessbloomer.com/woocommerce-visual-hook-guide-single-product-page/

### Reorder single product template

- http://ohsoren.github.io/reorder-single-product-template/

### When to use hooks, templates

- https://www.speakinginbytes.com/2016/06/woocommerce-use-hooks-use-templates/
- http://wpcandy.com/teaches/how-to-use-wordpress-hooks/

### Subscription - let user choose length via dropdown

- https://docs.woocommerce.com/document/subscriptions/faq/#section-12

TLDR: Use *variable subscriptions*. Create attribute (eg. Months). Create variations from the attribute. 
Result will be a select on the frontend.

### Customize the checkout page

- https://www.uploadwp.com/customizing-the-woocommerce-checkout-page/

### Add fields to checkout

- https://docs.woocommerce.com/document/checkout-field-editor/
- http://www.increativeweb.com/create-conditional-checkout-fields-woocommerce

### Hide shipping form for local pickup on checkout

- https://businessbloomer.com/woocommerce-hide-shipping-local-pickup-selected/

### Limit shipping to one state

- https://businessbloomer.com/woocommerce-limit-shipping-one-state/

### Choose pickup time for local pickup (only on sameday)

- https://github.com/mattbanks/woocommerce-local-pickup-time

### Product with no price, just for viewing

- http://kb.oboxthemes.com/articles/woocommerce-how-to-setup-display-only-or-virtual-products/

### Change Select Text for variations

- https://gist.github.com/targetimc/b92dbf2ebde2bc5e54e8967f9bf7d149

### Change quantity input to select
-https://www.cloudways.com/blog/change-display-quantity-select-box-in-woocommerce/

To apply on only some products, check a taxomomy term and then apply. You will need to write a template for the dropdown 
and then regular input! In the cart page loop, the $product->get_id() will have a parent. Use that id with has_term to 
see if the term is applied on the product.

Other:

- https://www.vanpattenmedia.com/2014/code-snippet-woocommerce-quantity-select-field
- https://gerhardpotgieter.com/2013/09/09/woocommerce-product-quantity-dropdown/

### Misc

- Replace "Choose and option" for variable product: http://www.howtoonlinetips.com/how-to-replace-choose-an-option-with-attribute-name-in-variation-select-menu-in-woocommerce/
  - https://wordpress.stackexchange.com/questions/99814/woocommerce-changing-the-variations-select-default-value
- Show minimum price for variable product on shop: https://www.themelocation.com/how-to-display-minimum-price-from-multiple-variations-in-woocommerce/
- Search products in price range: https://wordpress.stackexchange.com/questions/177316/woocommerce-search-products-between-price-range-using-wp-query
- product search form: https://stackoverflow.com/questions/15369229/merging-a-general-wordpress-search-with-a-woocommerce-product-search
- adjust quantity input values: https://docs.woocommerce.com/document/adjust-the-quantity-input-values/
- product variation prices hook: https://stackoverflow.com/questions/45806249/change-product-variation-prices-via-a-hook-in-woocommerce-3
- get category for product page: https://stackoverflow.com/questions/15303031/woocommerce-get-category-for-product-page
- purchase limits: https://www.cloudways.com/blog/set-purchase-limits-on-woocommerce/
- product coming soon plugin (free): http://terrytsang.com/shop/shop/woocommerce-coming-soon-product/
- min/max quanities without plugin? https://www.tychesoftwares.com/how-to-set-minimum-and-maximum-allowable-product-quantities-to-be-added-in-woocommerce-cart/
  - This one works ok: https://wordpress.org/plugins/woocommerce-max-quantity/
- update your custom cart info area when WC uses ajax to update quantities: https://gist.github.com/geoffyuen/8646723e9279834ee3864963809b357d
