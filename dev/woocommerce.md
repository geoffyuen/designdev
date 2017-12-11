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
