# Add more features to your custom app

By default, custom apps have limited access to the store data and features. For example, such apps cannot add new customers through REST API or automate store processes with webhooks. To unlock additional features, you need to update the **app configuration**.

[Learn how to get your first custom app](set-up-your-dev-environment-in-ecwid.md)

### Check out all features available for your app

Check [List of app permissions](../develop-apps/app-settings.md) and [Ecwid API features](../ecwid-api-features.md) articles to find what access scopes are enabled for your app by default and what additional permissions you may need for the app.

One application can have any amount of access scopes allowing it, for example, to add widgets on the storefront and manage backend integrations at the same time. \
\
We recommend choosing the minimum amount of scopes for your app.

{% hint style="info" %}
Some features like **webhook automations** require [self-hosted endpoints](../develop-apps/app-settings.md#self-hosted-endpoints) working on your servers.\
\
Prepare URLs before requesting application update.
{% endhint %}

If you are not yet sure about your app functionality or required access scopes, contact [API Support team](../contact-ecwid-api-support-team.md) to get help.

### Request application update

Once you prepared a list of required changes (access scopes, endpoint URLs, etc), [request application update](../contact-ecwid-api-support-team.md#get-assistance-with-your-app) through the Ecwid admin.&#x20;

This way, you'll get access to new features for your app **in 24 hours or less** on business days.
