# Use Native app JS SDK

Native app JS SDK offers useful JavaScript methods for interacting with Ecwid stores from within your app. Use our HTML template or manually add the required JS file into your **iframeUrl** to use the SDK: `https://djqizrxa6f10j.cloudfront.net/ecwid-sdk/js/1.3.0/ecwid-app.js`

```html
<head>
<!-- Include Ecwid JS SDK -->
<script src="https://djqizrxa6f10j.cloudfront.net/ecwid-sdk/js/1.3.0/ecwid-app.js"></script>
</head>
```

Find the list of available methods below:

### `EcwidApp.init()`

This method initializes your app inside Ecwid admin. Call it once at the beginning of executable code in your app. This method is **required** to make the app work inside the Control Panel.

Code example:

```javascript
// Initialize the application
EcwidApp.init({
  app_id: "my-super-app", // App's client_id
  autoloadedflag: true, 
  autoheight: true
});
```

Available fields:

| Name           | Type    | Description                                                                                                                                                                                                                                                                 |
| -------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **app\_id**    | string  | <p>Must be <code>client_id</code> of your application. If you don't know it, go to the application <em>Details</em> page from <a href="https://my.ecwid.com/#develop-apps">#develop-apps</a> and find it there.<br><br>Required</p>                                         |
| autoloadedflag | boolean | <p>Set <code>true</code> if you want Ecwid to detect when the app is loaded, stop the "Loading" animation, and display the settings page to users.</p><p></p><p>Set <code>false</code>if you want to control this moment with the <code>EcwidApp.ready()</code> method.</p> |
| autoheight     | boolean | <p>Set <code>true</code> if you want Ecwid to adjust the iframe height dynamically depending on the settings page content. </p><p></p><p>Set <code>false</code>if you want to control iframe size with the <code>EcwidApp.setSize()</code> method.</p>                      |

Only the `app_id` field is required, but we recommend leaving all three fields and [emailing us](mailto:ec.apps@lightspeedhq.com) if you notice any issues with your app loading or height.

### `EcwidApp.openPage(page)`

Use this method to redirect users to another Ecwid admin page. Specify the page with the hash (#) part in the URL. For example, `billing` will open the _Billing_ page, `products` will open the _Catalog - Products_ page:

Page URL: `https://my.ecwid.com/store/1003#products`\
Call: `EcwidApp.openPage('products');`

This method supports everything users can see after the hash (#), including order IDs, product IDs, etc:

Page URL: `https://my.ecwid.com/store/5035009#order:id=938&return=orders`\
Call: `EcwidApp.openPage('order:id=938&return=orders');`

### `EcwidApp.ready()`

Use this method to "manually" inform Ecwid when your application is ready to be shown to users.

For example, your app needs some API calls or additional heavy assets before it is ready for display. Pass `false` in the `autoloadedflag` parameter in the `EcwidApp.init()` method and call the `EcwidApp.ready()` function when you are ready.

Code example:

```json
// Initialize the application
EcwidApp.init({
  app_id: "my-super-app", // App's client_id
  autoloadedflag: false, // Disable automatic detection of ready state
  autoheight: true
});

// Show app UI
EcwidApp.ready();
```

### `EcwidApp.setSize(height)`

Use this method to set the application iframe height in pixels manually.

We recommend using the `autoheight: true` in the `EcwidApp.init()` method to let Ecwid dynamically adjust your app iframe size depending on your application content.&#x20;

However, if you want to control the iframe size on your side, omit the `autoheight` param or set it as `false`, then call the `EcwidApp.setSize()` method to specify the iframe height.

Code example:

```json
// Initialize the application
EcwidApp.init({
  app_id: "my-super-app", // App's client_id
  autoloadedflag: true,
});

// Set app height to 800 pixels. 
EcwidApp.setSize({height: 800});
```

### `EcwidApp.sendUserToUpgrade(features)`

Use this method to initiate the plan upgrade process for users right from your app interface. The `features` argument supports multiple values separated by a comma.

Code example:

```javascript
// Send user to upgrade to get Product Variations feature
EcwidApp.sendUserToUpgrade(["COMBINATIONS"]);

// Send user to upgrade to the minimal plan where Order Editor and Marketplaces features are available
EcwidApp.sendUserToUpgrade(["ORDER_EDITOR", "MARKETPLACES"]);
```

Ecwid determines the minimum required plan for the store owner to use the features you pass and then initiates the upgrade process.

Find a list of features in `availableFeatures` field in the [Get store profile](https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/store-profile/get-store-profile) endpoint.
