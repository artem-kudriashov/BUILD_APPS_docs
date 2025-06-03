# Make your first API request

All requests to Ecwid REST API require an **access token**. Ecwid uses OAuth 2.0 to provide secure access to the store data for public apps. If you customize your own store, however, you can skip OAuth and easily get an access token for your store.

This guide provides a walkthrough of a basic Ecwid API interaction, specifically, retrieving store profile information. To gain a deeper understanding of Ecwid API objects and their connections, refer to the API reference.

### Before you begin

There is **no test mode** in Ecwid API, so we recommend setting up a separate test store. This way you can safely experiment and develop without impacting your live store and its data. By isolating your testing activities, you can maintain a smooth experience for both development and production environments.

### Step 1. Get your secret app token

API access to the store data is locked behind app authentication and request authorization based on the OAuth 2.0 standard. However, access to your store data is much simpler.

After signing up with Ecwid and getting a custom app, you already have two tokens:

* **Public token** allows only public data to be received and is safe to use in public code.
* **Secret token** grants full access to REST API (provided the app has all required permissions) and therefore must be kept safe.&#x20;

{% hint style="success" %}
Learn more about tokens, permissions, and other application settings in the [app-settings.md](../develop-apps/app-settings.md "mention") guide.
{% endhint %}

From the [app dashboard](https://my.ecwid.com/#develop-apps), open the **Details** page of the custom app, then copy one of the access tokens:

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdNwBhLxVmiemZCVBdOYd56HzCSkWeNb2sbmLGz06KIY_sZrBsQmh3Tn1X2TaZFqfiVw-K_jTcYggvqkwn7KKi0UyN9uoWiUi8HePkSGM6eiOm9s6CWJZsLt6l3BfTNS1WOeDeicA?key=18nFffab1qSi-Qn7GXfMEUb2" alt=""><figcaption></figcaption></figure>

If the custom app is uninstalled from the store, you can reinstall it from the **Details** page. Click the **Install** button, then copy access tokens.

### Step 2. Make your first REST API request

Now you have everything to start making REST API requests. Let's start with a simple GET request. Such requests require only two variables: **store ID** and **access token**.

You already have a custom app with access tokens. Get your store ID from any Ecwid admin page from URL or the footer.&#x20;

Now make a simple “Get products” request and execute it using, for example, the [Postman app](https://www.postman.com/).

Add **store ID** to the _request path_, your **secret access token** as a _Bearer Token on the Authorization tab_, and click _Send_:

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfH7BGOQ7TNpVkg9mBDW_aubmgMw8mxA011JpR6ZXXuuqxBtzF20-D6Dg7sg-1PuZwX3dmS2cqwgPUjhlyQF1eeO3u6ajw6-xoNnQA77GCNhrzWhX7Txms2OdC6IsoXyJWoPNba?key=18nFffab1qSi-Qn7GXfMEUb2" alt=""><figcaption></figcaption></figure>

That’s it. You should receive a JSON-formatted response with details about products in your store.

### **Next steps**

Congratulations on completing the quickstart guide!&#x20;

Now you can make REST API requests, so it’s time to move further:

* [Learn Ecwid API features](../ecwid-api-features.md)
* [Learn more about app settings: access tokens, scopes, etc.](../develop-apps/app-settings.md)
* [Add more features to your custom app](add-more-features-to-your-custom-app.md)
