# Manage personal user settings storage

When users fill out settings in an app, the app needs to:

* Store user settings somewhere safe.
* Have access to user settings later.
* Support simultaneous access to user settings in different stores.

For Native apps, Ecwid provides an out-of-the-box storage for the safe storing and managing of personal user data named **Application storage**.

### About App storage

**App storage** allows storing data on Ecwid servers and accessing it using REST API instead of developing SQL databases on your server. Application storage is secure and fast. It also allows you to split private and public user data with only public settings being available on the storefront.

Application storage is a JSON array of objects, where each data entry is a **key-value** object. Every store that installs the app gets its own storage. App storage data entries example:

```yaml
[
  {
    "key": "show_reviews_in_app",
    "value": "true"
  },
  {
    "key": "user_email",
    "value": "ec.apps@lightspeedhq.com"
  },
  {
    "key": "public",
    "value": "{'button_color': 'red', 'button_text': 'Email us', 'corner': 'TOP_RIGHT', 'show': 'true'}"
  }
]
```

### Data types in App storage

App storage has both private and public data entries. Data type is defined by the key used to store it. The "public" key name is reserved for the public data. We recommend using it as the application config. Manage it from the settings page and get it on the storefront with a JavaScript call.

Public key example:

```yaml
  {
    "key": "public",
    "value": "Store public app config for storefront here"
  }
```

Read more about access to the "public" key on the storefront: [Get public app details](https://app.gitbook.com/s/aRJpOy0U8IpbjUfcox4D/get-storefront-details/get-public-app-details "mention")

All other keys are considered private, and therefore their data is unavailable to other applications or users, or through the `Ecwid.getAppPublicConfig()` method on the storefront.

### Limits

Keys you save in the application storage are only available to your app. Other applications cannot read these keys or even know if you have any keys saved.

Accessing keys works through REST API requests. The only exception is the "public" key which is also available on the storefront.

The size limit for private keys is **1MB**, and for public keys - **256KB**.

### Manage user settings with REST API

App storage works through REST API requests with default HTTP request types: GET, PUT, POST, and DELETE.

Find request descriptions for managing App storage below:

<table data-view="cards"><thead><tr><th data-type="content-ref"></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/get-all-app-storage-data">Get all app storage data</a></td><td></td></tr><tr><td><a href="https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/get-specific-app-storage-data">Get specific app storage data</a></td><td></td></tr><tr><td><a href="https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/add-app-storage-data">Add app storage data</a></td><td></td></tr><tr><td><a href="https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/update-specific-app-storage-data">Update specific app storage data</a></td><td></td></tr><tr><td><a href="https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/delete-specific-app-storage-data">Delete specific app storage data</a></td><td></td></tr></tbody></table>
