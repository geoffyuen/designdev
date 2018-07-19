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
- Some dudes blog: https://wpsites.net/tag/woocommerce/
  - https://wpsites.net/best-plugins/woocommerce-conditional-tag-checks-all-pages/

## Integrating with Timber/Twig 

- Skeleton templates: https://github.com/timber/timber/blob/master/docs/guides/woocommerce.md
- some great information starting here (apply to the above): https://github.com/timber/timber/issues/79#issuecomment-42515989
- should be aware that these methods may not be compatible with WC plugins/addons because of WC's heavy use of actions and hooks
- the basic gist is: WC groups a bunch of elements in actions; remove things from the actions (desc, price, etc) and reinsert them using twig. You should keep the do_actions in there so that plugins will still work. I suspect it'll take a lot of trial and error to get things to appear like you want them to.
- product class: http://docs.woothemes.com/wc-apidocs/class-WC_Product.html
- WooCommerce object: http://docs.woothemes.com/document/class-reference/
- snippet to put cart link in your header: https://gist.github.com/geoffyuen/505240d02b992157ccc0a771575b3f6f
- someone's theme https://github.com/niklasravnsborg/blender-shop/blob/master/src/woocommerce.php
- another theme https://github.com/hrsetyono/generator-edje/tree/master/templates/wc-theme/views/woo

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
see if the term is applied on the product.*

* I'm not sure how safe it is to do this as you're rewritting WC's quanity input routines. Maybe if they made this framework easier to use there wouldn't be these kinds of work arounds.

Other:

- https://www.vanpattenmedia.com/2014/code-snippet-woocommerce-quantity-select-field
- https://gerhardpotgieter.com/2013/09/09/woocommerce-product-quantity-dropdown/

#### Update Shipping

- https://gist.github.com/neamtua/bfdc4521f5a1582f5ad169646f42fcdf
- https://stackoverflow.com/questions/31315357/updating-woocommerce-shipping-method-via-ajax
- https://stackoverflow.com/questions/47129882/woocommerce-checkout-update-shipping-value-more-than-once

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
- Skip Cart and go direct to checkout: https://gist.github.com/micc83/a129fe061e37932c44ea
- Customize checkout fields: https://docs.woocommerce.com/document/tutorial-customising-checkout-fields-using-actions-and-filters/#section-5
- Custom validation of checkout fields: https://stackoverflow.com/questions/28603144/custom-validation-of-woocommerce-checkout-fields/42848932

