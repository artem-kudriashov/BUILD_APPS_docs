# Deep linking

Apps in Ecwid admin can receive specific store information before loading through **deep linking**. When an app is opened from a specific page, Ecwid sends a URI-encoded page slug as an `app_state` query parameter. Use its value to adjust app flow depending on the page users came from.

Default **iframeUrl** example: `https://my.ecwid.com/store/1234567#app:name=my-cool-app&parent-menu=sales`

Example of the **iframeUrl** with **deep linking**: `https://my.ecwid.com/store/1234567/#app:name=my-cool-app&app_state=orderId%3A%2012`

With the `app_state`, you can redirect users to the page they came from with the [EcwidApp.OpenPage()](ref:native-app-js-sdk#ecwidappopenpagepage) method.

### Receive app state when accessing store data

Apps loading in Ecwid admin can receive the `app_state` before the [authentication process](../access-store-data-from-the-app.md). When users open the app, you'll receive a request on your server:

`GET https://www.example.com/my-app-iframe-page?payload=353035362c226163636573735f746f6b656e223a22776d6&app_state=orderId%3A%2012&cache-killer=13532`

Check `app_state` in your authentication flow and save its value to a variable.

Code example:

```php
<?php

// URL Encoded App state passed to the app
  if (isset($_GET['app_state'])){
    $app_state = $_GET['app_state'];
  }
?>
```

Decoded payload example:

```json
{
  "store_id": 1003,
  "lang": "en",
  "access_token":"xxxxxxxxxxxxxxxx",
  "app_state":"orderId%3A%2012"
}
```
