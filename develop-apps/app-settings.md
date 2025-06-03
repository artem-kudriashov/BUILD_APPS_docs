# App settings

Configuration for all Ecwid apps consists of the following settings:

* **Access scopes** - a list of permissions defining API access for the app.
* **Access tokens** - non-expiring authorization keys for REST API requests.
* **Endpoints** - static URLs on the developer's server interacting with specific Ecwid APIs.
* **App keys** - unique and constant values used in request decoding and public app authentication.

When created, custom applications automatically get default access scopes and both access tokens unlocking some REST API requests. Both app keys are also automatically generated, though they have no use for a custom app with a default configuration.

All app settings are always available on the [Ecwid admin > #develop-apps > Details](https://my.ecwid.com/#develop-apps) page (read-only).

### Access tokens

Access tokens allow you to authorize REST API requests for the specific app in the specific store. Even for the same app, an access token from one store won't work for another one.

Access tokens also **do not expire**, so once you get them for your custom app, save and use these tokens on your side for as long as you need.

{% hint style="info" %}
You can get access tokens for your store without going through oAuth flow
{% endhint %}

Depending on the store data and type of API request, you need to use one of the two access tokens:

* **Secret token**\
  A secret token (`secret_token`) is only limited by the app permissions, so it must not be used in the publically available code. Secret tokens exposed on the storefront put the store data at risk. \
  \
  Secret token example: `secret_EZWiLeBXWsGg82XH3SfSFfdw418QNBBM`.\

*   **Public token**\
    A public token (`public_token`) is safe to use on the storefront as it can only work with the publically available store data. It grants access **only** to:

    * Receiving details of enabled products and categories.
    * Receiving highly limited store profile data.
    * Placing orders without "Paid" status.

    \
    Public token example: `public_B6mT2teCE55zT2jAeffLjzNJ4se3gfPj`.

### List of access scopes

Access to Ecwid API features is limited by permissions called **access scopes**.

One application can have from one to all scopes at the same time. However, we recommend keeping the minimum amount of permissions required for the app to work.

Find the full list of access scopes available to apps below:

<table><thead><tr><th width="266.7265625">Access scope</th><th>Notes</th></tr></thead><tbody><tr><td>read_store_profile</td><td>Get general store settings like format units, shipping origin address, email notification settings, etc. Receive webhooks about changes in store settings or applications. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>read_catalog</td><td>Get data about categories, products, product options, variations, and attributes. Receive webhooks about product and category changes. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>update_catalog</td><td>Update product and category details, upload images and files to products, and delete products or categories. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>create_catalog</td><td>Add new products and categories to the store. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>read_orders</td><td>Get data about orders placed in the store and abandoned carts. Receive webhooks about changes in carts and orders. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>update_orders</td><td>Change order details, update order statuses, and delete orders. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>public_storefront</td><td>Get a public access token for the app. <br><br><strong>Default scope for custom apps</strong>.</td></tr><tr><td>read_store_profile_extended</td><td>Get additional store settings like billing and channel information. Extends the <code>read_store_profile</code> access scope.</td></tr><tr><td>read_store_limits</td><td>Get store limits and restrictions. Extends the <code>read_store_profile</code> access scope.</td></tr><tr><td>update_store_profile</td><td>Update store settings, manage logo images, and close storefront for maintenance with REST API.</td></tr><tr><td>read_store_stats</td><td>Get store reports details.</td></tr><tr><td>update_catalog_batch_delete</td><td>Delete all products from the store in one request.</td></tr><tr><td>create_orders</td><td>Manually add new orders to the store. Convert abandoned carts to orders.</td></tr><tr><td>add_custom_blocks</td><td>Create new sections – building blocks of website pages – for the Ecwid website builder called  <a href="https://api-docs.ecwid.com/docs/intro-to-instant-site">Instant Site</a>.</td></tr><tr><td>add_custom_templates</td><td>Create new templates – design and functionality overhauls – for your website or all users of the Ecwid website builder called  <a href="https://api-docs.ecwid.com/docs/intro-to-instant-site">Instant Site</a>.</td></tr><tr><td>read_customers</td><td>Get data about store customers and customer groups from your store. Receive webhooks about customer changes.</td></tr><tr><td>update_customers</td><td>Update customer or customer group details and delete them.</td></tr><tr><td>create_customers</td><td>Add new customers to the store.</td></tr><tr><td>read_customers_extrafields</td><td>Get data about customer extra fields in the store.</td></tr><tr><td>update_customers_extrafields</td><td>Update and create new customer extra fields.</td></tr><tr><td>delete_customers_extrafields</td><td>Delete customer extra fields from the store.</td></tr><tr><td>read_discount_coupons</td><td>Get data about discount coupons. Receive webhooks about discount coupon changes.</td></tr><tr><td>update_discount_coupons</td><td>Update discount coupon details and delete coupons.</td></tr><tr><td>create_discount_coupons</td><td>Add new discount coupons to the store.</td></tr><tr><td>read_promotion</td><td>Get data about promotions in the store. Receive webhooks about any changes in promotions.</td></tr><tr><td>update_promotion</td><td>Update promotion conditions and delete them.</td></tr><tr><td>create_promotion</td><td>Add new promotions to the store.</td></tr><tr><td>read_reviews</td><td>Get data about product reviews with REST API. Receive webhooks about product review changes.</td></tr><tr><td>update_reviews</td><td>Update product review status and delete reviews.</td></tr><tr><td>read_sizecharts</td><td>Get data about sizecharts available in the store.</td></tr><tr><td>update_sizecharts</td><td>Update store sizecharts and delete them.</td></tr><tr><td>create_sizecharts</td><td>Add new sizecharts to the store with REST API.</td></tr><tr><td>customize_storefront</td><td>Get access to Ecwid JS API for storefront customization. Modify the storefront with a custom JavaScript code running from a self-hosted endpoint. <br><br>Requires <code>customJsUrl</code> endpoint to function. Optional endpoint: <code>customCssUrl</code>.</td></tr><tr><td>add_to_cp</td><td>Add an integrated user settings page for your app to Ecwid admin. <br><br>Requires a self-hosted <code>iframeUrl</code> endpoint to function.</td></tr><tr><td>add_shipping_method</td><td>Add live shipping rates to the store with Shipping API. The new shipping method provides live rates to customers at the checkout. <br><br>Requires a self-hosted <code>shippingUrl</code> endpoint to function.</td></tr><tr><td>add_payment_method</td><td>Allow customers to pay for orders online at the checkout with Payment API. <br><br>Requires a self-hosted <code>paymentUrl</code> endpoint to function.</td></tr><tr><td>customize_cart_calculation</td><td>Create a custom logic for calculating discounts or surcharges at the checkout. <br><br>Requires a self-hosted <code>discountUrl</code> endpoint to function.</td></tr><tr><td>buy_domains</td><td>Purchase and manage store domains.</td></tr><tr><td>read_invoices</td><td>Get data about order tax invoices. Receive webhooks about changes in order tax invoices.</td></tr><tr><td>read_brands</td><td>Get data about product brands.</td></tr><tr><td>read_subscriptions</td><td>Get data about purchased subscription products.</td></tr><tr><td>update_subscriptions</td><td>Update subscription products' details.</td></tr><tr><td>charge</td><td>Use custom charges in your app to expand monetization options with Ecwid billing. Available only for public apps.</td></tr><tr><td>read_staff</td><td>Get data about additional (staff) accounts in the store.</td></tr><tr><td>invite_staff</td><td>Send and resend staff account invites.</td></tr><tr><td>create_staff</td><td>Add new staff accounts to the store.</td></tr><tr><td>update_staff</td><td>Update staff account details.</td></tr><tr><td>delete_staff</td><td>Cancel the invite for the staff and revoke their access to your store.</td></tr></tbody></table>

### Self-hosted endpoints

{% hint style="info" %}
Access to REST API or storefront/checkout customizations does not require setting up self-hosted endpoints.
{% endhint %}

Some features require you to set up a live server listening to incoming requests from Ecwid API.&#x20;

For example, you need an endpoint called `webhookUrl` to receive webhooks – automatic notifications about any events in the store.&#x20;

Any self-hosted endpoint must work:

* On a static HTTPS URL&#x20;
* On a server that can handle HTTP requests.

List of available endpoints and features requiring them:

* `webhookUrl`: **Webhooks** about events happening in the store.
* `paymentUrl`: Payment API for adding online payment methods for the store.
* `shippingUrl`: Shipping API for adding live shipping rates for the checkout.
* `cartPromotionsUrl`: **Live discounts** for adding custom live discounts to the checkout.
* `customJsUrl`: **Storefront customization** with JavaScript code.
* `customCssUrl`: **Storefront customization** with CSS code.
* `iframeUrl`: **Native app** for creating a user settings page.

### Application keys

{% hint style="info" %}
Access to REST API or storefront/checkout customizations does not require app keys.
{% endhint %}

**App keys** are used in Payment API and app authentication. Values for app keys are unchangeable and unique for each application. There are two app keys:

* `client_id` - Unique application ID.
* `client_secret` - Application secret used for decryption in Native app authentication and Payment API processing.
