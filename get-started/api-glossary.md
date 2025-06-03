# API glossary

#### Ecwid admin&#x20;

A one-for-all tool, where users can manage all aspects of their store: products, orders, customers, website, integrations, etc.

#### Ecwid app

Extension users can install to their Ecwid stores that adds some new functionality, integration, or a way to customize store content or design.

#### Ecwid user

Anyone who creates an Ecwid store is considered a user: site owners, merchants, and developers helping other users with managing their sites and business.

#### Instant Site

Website builder created by Ecwid that allows creating for both ecommerce and non-ecommerce sites.

#### Instant Site Editor

Native UI for building Ecwid websites available to all Ecwid users right from the Ecwid admin.

#### Ecwid App Market

Marketplace with applications that extend store functionality, add new ways of customization, or integrate a store with another service, for example, payment provider, CRM system, shipping rates calculator, etc.

[Go to App Market](https://www.ecwid.com/apps)

#### Custom app

Private application for accessing Ecwid API in a specific store. Ecwid creates one custom app for any user who visits the app dashboard in Ecwid admin for the first time.

#### Public app

An app available in the [Ecwid App Market](https://www.ecwid.com/apps). Learn more about publishing your app: [Broken link](broken-reference "mention")

#### App dashboard

Hidden page in Ecwid admin where developers can create new applications, check app settings, get access tokens, and request application updates.&#x20;

Go to the [app dashboard](https://my.ecwid.com/#develop-apps)

#### Access scope

Permission for the app to do a specific action or access some data in the store. For example, the `read_orders` scope allows the app to get information about orders placed in the store and the `add_payment_method` scope allows the app to add a new online payment method to the checkout.

[Learn more about access scopes](../develop-apps/app-settings.md)

#### API keys

Unchangeable and unique credentials for app authentication and decoding some API requests.&#x20;

Every application has two API keys: `client_id` (app ID) and `client_secret` (app secret).

#### App ID

An app key used to identify the particular application. For public apps, the app ID often matches with the app name. In API, we refer to this ID as the app’s `client_id`.

#### App secret

Unique authentication key of an app that must be kept hidden and secure as it grants access to app authentication. In documentation, reffered as `client_secret`.

#### Access tokens

Secure app credentials for authorizing REST API requests. If an app is installed in several Ecwid stores, it has unique access tokens for every store. \
\
There are two tokens:  `secret_token` and `public_token`. Learn more about app access tokens: [app-settings.md](../develop-apps/app-settings.md "mention")

#### App endpoint

Link to a self-hosted server URL connected to the app that enables a specific feature. For example, the `paymentUrl` endpoint allows you to receive online payment requests from your store through the app.

\
