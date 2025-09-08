# Native and external apps

While custom apps work only in one store, **public applications** can be used by thousands of clients. Therefore, they must be able to:

* Have some form of SQL database for managing users and REST API access to their data.
* Provide users with a personal settings page populated with the store data.
* Handle simultaneous access to REST API and settings pages.

When starting public app development, decide how to handle all these processes. Ecwid has two solutions named **Native apps** and **External apps**.

### Native vs External apps comparison table

<table><thead><tr><th width="204">Property</th><th>Native apps</th><th>External apps</th></tr></thead><tbody><tr><td>Integrated to Ecwid admin</td><td>✓</td><td>-</td></tr><tr><td>Access to store data</td><td>Ecwid sendsan encrypted <strong>payload</strong> as a query param <em>every time</em> users open a settings page.<br><br><strong>Payload</strong> contains details for store identification and REST API access.</td><td>Ecwid sends <strong>code</strong> query param <em>only once</em> when a user installs the app.<br><br>The <strong>code</strong> is exchanged for store identification and REST API access which must be safely stored on your side.</td></tr><tr><td>Tools for building a settings page</td><td><strong>CSS Framework</strong> - large collection of functional UI elements, blocks, and page templates following Ecwid admin style guide.<br><br><strong>Native app JS SDK</strong> - collection of JavaScript methods for Native Apps.</td><td>-</td></tr><tr><td>Required self-hosted endpoints</td><td><strong>iframeUrl</strong> - user settings page of your app built on  HTML.<br><br>The page loaded inside Ecwid admin when users open the app and provides you with Ecwid API access every time it''s opened.</td><td><strong>redirectUrl</strong> - handles the authentication process, when users install the app and your app gets access to the store data.<br><br><strong>openAppUrl</strong> - an external settings page/dashboard for your app. <br><br>It's a URL that allows users to click the "Open app" button in Ecwid admin. However, the URL doesn't carry any data for user identification or Ecwid API access.</td></tr><tr><td>Personal user settings storage</td><td><strong>App storage</strong> - secure storage for user data handled by Ecwid.<br><br>It has private (available only through REST API) and public parts (also available on the storefront) allowing you to use it, for example, for storefront customizations.</td><td>-</td></tr></tbody></table>

### Build Native application

Native is the recommended application type for the Ecwid App Market. Check out our guides for managing the store access, user settings page, and storage for user settings below.

* [Access store data](access-store-data-from-the-app.md)
* [Create user settings page](build-user-settings-page-for-ecwid-admin/)
* [Manage personal user settings storage](https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/add-app-storage-data)

### Build External application

If you already have a working UI on your website, Ecwid won't force you to develop an integrated user settings page. Instead, your app passes an authentication process to identify the store and receive REST API access to its data.

The app must authenticate users **only once** when they click the "Install" button. At the end of authentication, you receive a _store ID_ and _access token_ for REST API access.

To make an External app, provide us with two endpoints:

* **redirectUrl** is used in the authentication process when users click the "Install button".
* **openAppUrl** opens an external dashboard when users click the "Open app" button.

#### Receive temporary `code` and `store_id`

The installation process begins when the user clicks the "Install" button in Ecwid admin. Ecwid installs the app and runs the process of getting an **access token** for the app.

To do so, the user is automatically redirected to your **redirectUrl** after installing the app. When it happens, you also receive a call to **redirectUrl** with additional params.

Example of the call with params:

`https://www.example.com/myapp?code=abcd123456&store_id=1003`

where:

* `https://www.example.com/myapp` part is **redirectUrl**
* `abcd123456` is **code**
* `1003` is **store\_id**

Keep in mind that the **code** is short-lived. It must be exchanged for an _access token_ by your app in a few minutes. It can also be used only once in the exchange call.

#### Exchange `code` for an access token

This part of the authentication process must be invisible to users. While the **code** is exchanged in the background, users are still sitting on the **redirectUrl**.

Exchange happens through a POST request  `https://my.ecwid.com/api/oauth/token` with a URL-encoded request body. All params in the request body are **required** and are encoded with the `Content-Type: application/x-www-form-urlencoded` header.

Example of the exchange request:

```http
POST /api/oauth/token HTTP/1.1
Host: my.ecwid.com
Content-Type: application/x-www-form-urlencoded

client_id={client_id}&client_secret={client_secret}&code={code}&store_id={store_id}&redirect_uri={redirect_uri}&grant_type=authorization_code
```

```curl
curl --location 'https://my.ecwid.com/api/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'client_id={client_id}' \
--data-urlencode 'client_secret={client_secret}' \
--data-urlencode 'code={code}' \
--data-urlencode 'store_id={store_id}' \
--data-urlencode 'redirect_uri={redirect_uri}' \
--data-urlencode 'grant_type=authorization_code'
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://my.ecwid.com/api/oauth/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => '{client_id}&client_secret={client_secret}&code={code}&store_id={store_id}&redirect_uri={redirect_uri}&grant_type=authorization_code',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

Request body params:

<table><thead><tr><th width="149.9140625">Parameter</th><th width="149.54296875">Required</th><th>Description</th></tr></thead><tbody><tr><td>client_id</td><td>required</td><td><code>client_id</code> of your application. Find it at the bottom of the application <em>Details</em> page on <a href="https://my.ecwid.com/#develop-apps">#develop-apps</a>.</td></tr><tr><td>client_secret</td><td>required</td><td><code>client_secret</code> of your application. Find it at the bottom of the application <em>Details</em> page on <a href="https://my.ecwid.com/#develop-apps">#develop-apps</a>.</td></tr><tr><td>code</td><td>required</td><td>The temporary <code>code</code> received on the previous step.</td></tr><tr><td>store_id</td><td>required</td><td>The <code>store_id</code> received on the previous step.</td></tr><tr><td>redirect_uri</td><td>required</td><td><strong>redirectUrl</strong> of your application.</td></tr><tr><td>grant_type</td><td>required</td><td>Always <code>authorization_code</code>.</td></tr></tbody></table>

#### Receive store ID and access token

Ecwid responds to an exchange request with JSON containing _store ID_ and _access token_ details.

Response example:

```json
{
 "access_token":"secret_ab***cd",
 "token_type":"bearer",
 "scope":"read_store_profile update_catalog",
 "store_id":1003,
 "public_token":"public_qKDUqKkNXzcj9DejkMUqEkYLq2E6BXM9"
}
```

Ecwid responds with JSON-formatted data containing the access token and additional information. Response fields are listed below:

| Field         | Description                                                                                                           |
| ------------- | --------------------------------------------------------------------------------------------------------------------- |
| access\_token | Secret _access token_ for your app. Use it to authorize REST API requests.                                            |
| token\_type   | Always `bearer`                                                                                                       |
| scope         | List of permissions (Access scopes) given to the app. Find all available scopes in [Access scopes](ref:access-scopes) |
| store\_id     | Ecwid store ID.                                                                                                       |
| public\_token | Public _access token_ for your app. Ecwid gives it only if an app has `public_storefront` scope.                      |

#### Show dashboard page to users

Now you have Ecwid store ID and access to its data, so it's time to redirect them to your dashboard from the `redirectUrl`. Show them the UI and populate it with the data from their Ecwid store received through REST API.

We recommend processing as many REST API requests as possible in the background and automating UX. For example, if your service requires syncing store products to get started, do not make clients select "Ecwid" platform and click several buttons to start the sync. You know it's an Ecwid user, and you have REST API access to products after the authentication. Automate this process: select "Ecwid" platform for a user, and start products sync immediately.

#### How to keep users logged in

The `openAppUrl` doesn't support authentication, so it is impossible to identify a specific Ecwid user when the store owner clicks the "Open app" button and goes to `openAppUrl`.

If you want to rely on Ecwid for logging in users, we have a workaround solution for it. [Email us](mailto:ec.apps@lightspeedhq.com) to discuss how it will work for your application.
