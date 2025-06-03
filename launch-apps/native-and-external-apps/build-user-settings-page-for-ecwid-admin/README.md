# Build user settings page for Ecwid admin

When users open your Native app, Ecwid opens your **settings page** inside an iframe. The app must go through authentication and initialization to show your settings page.

### Initialize the app

The `EcwidApp.init()` method is **required**. Call it once when the **iframeUrl** is opened. If it's not called, then Ecwid won't show the app. Your **iframeUrl** will load on a separate page but won't work inside Ecwid admin.

```
EcwidApp.init({
  app_id: "client_id", // client_id of your application
  autoloadedflag: true,
  autoheight: true
});
```

Add your app _client\_id_ as _app\_id_ value. Leave _autoloadedflag_ and _autoheight_ fields with _true_. For most applications, it will be enough.

Read more about `init()` function and other functions available with [Native app JS SDK](use-native-app-js-sdk.md).

### Show page to users

Now the app can show its **settings page** to users. Add `EcwidApp.init()` and JS file from Native app SDK in the `<head>`. Add JS and CSS files for CSS Framework to `<head>` and `<body>`.

We have an HTML template with up-to-date versions of all required files. Use it to get started:

```html
<!doctype html>
<html>

<head>
  <!-- Include Ecwid JS SDK -->
  <script src="https://djqizrxa6f10j.cloudfront.net/ecwid-sdk/js/1.3.0/ecwid-app.js"></script>
	<!-- Add values from the decrypted payload and initialize the app -->
  <script>
    // Initialize the application
    EcwidApp.init({
      app_id: "client_id", // client_id of your application
      autoloadedflag: true, 
      autoheight: true
    });

    // Get store ID, language, and access token from decrypted payload JSON
    var payload = <?php echo $result; ?>;
    var storeId = payload.store_id;
    var secret_token = payload.access_token;
    var language = payload.lang;

    if (payload.public_token !== undefined){
      var publicToken = payload.public_token;
    }
    
    if (payload.app_state !== undefined){
      var appState = payload.app_state;
    }

    // load additional scripts, styles if necessary...
  </script>

  <!-- Include Ecwid CSS Framework -->
  <link rel="stylesheet" href="https://d35z3p2poghz10.cloudfront.net/ecwid-sdk/css/1.3.19/ecwid-app-ui.css"/>  
</head>

<body class='normalized'>
  <div>Show something</div>

<!-- JS for CSS Framework components -->
  <script src="https://d35z3p2poghz10.cloudfront.net/ecwid-sdk/css/1.3.19/ecwid-app-ui.min.js">
  </script>
</body>

</html>
```

### Use Ecwid CSS Framework

Native apps become a part of an Ecwid admin, so they must look accordingly. Our [CSS Framework](https://developers.ecwid.com/ecwid-css-framework/) has a large collection of ready-to-use UI elements and blocks. Use it to create an interface matching Ecwid admin faster and easier.

To access CSS Framework elements inside the Native app, add the required CSS and JS files to the page:

`<head>`:\
`https://d35z3p2poghz10.cloudfront.net/ecwid-sdk/css/1.3.19/ecwid-app-ui.css`

`<body>`:\
`https://d35z3p2poghz10.cloudfront.net/ecwid-sdk/css/1.3.19/ecwid-app-ui.min.js`

Code example:

```html
<head>
  <link rel="stylesheet" href="https://d35z3p2poghz10.cloudfront.net/ecwid-sdk/css/1.3.19/ecwid-app-ui.css"/>
</head>

<body>
  
  <div>Native app page</div>

  <script type="text/javascript" src="https://d35z3p2poghz10.cloudfront.net/ecwid-sdk/css/1.3.19/ecwid-app-ui.min.js"></script>
</body>
```
