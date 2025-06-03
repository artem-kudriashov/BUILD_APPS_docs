# Monetize public apps

When you build a public application for Ecwid App Market, you get access to thousands of our users who can become your clients. While choosing pricing options, check out Ecwid billing.

### Why sell the app with Ecwid billing

* Ecwid handles payments: Set a monthly price for your app, and that's it. Ecwid billing will take care of the rest.
* Set up different pricing options: make your application free or with a monthly price. Add Premium or pay-per-use features with custom charges. Combine any options to make unique and flexible billing.
* Choose between several currencies: we can accept payments in USD, EUR, GBP, AUD, MXN, and INR.
* Adjust app price: Set up trial periods from 1 day to half a year, change your application price, and process refunds with our support.
* Get paid quarterly: our team will report your app’s performance and make the payment.
* Track your app and payout stats: We provide automated monthly reports that include stats about app usage and generated revenue.

### Set up flexible billing with custom charges

While Ecwid billing allows you to set up a monthly price for the app, you can use **custom charges** to create a flexible billing flow based on the features your clients want to use. Additional charges could be a monthly price increase, one-time purchase, or pay-per-use.

* **Subscription levels**. Add new, cool features to a higher subscription level. If users upgrade their subscription level, call custom charge once a month. Use the base application's monthly price as a default or a starter plan.
* **Pay-per-use functionalities**. Call custom charges for additional bulk or advanced features in your application. For example, products synced from an XML file are $10 for 1000 products, paid image enhancer.
* **Free basic app. Paid Premium version**. Distribute your application for free with some basic functionality. Open access to additional cool features with a one-time paid Premium version.

Call custom charges through REST API requests. Ecwid processes them immediately, and you receive the transaction status in the response.

Custom charges have the following **withdrawal limits**:

* Daily withdrawal limit per store: $5000
* Withdrawal limit per transaction: $500

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Custom charges in REST API</strong></td><td><a href="https://app.gitbook.com/s/G9n5VxMY9T0Ob3D56PSD/rest-api/application/custom-charge-with-ecwid-billing">Custom charge with Ecwid billing</a></td></tr></tbody></table>

### How to show custom charges in the app

Ecwid doesn't ask for confirmations when custom charges are triggered. To make sure the store owner understands that he will be charged and accepts it, we recommend the following:

* Highlight triggers for custom charges with a text explaining that it is a paid feature.
* Show a warning message or a pop-up with a confirmation button before sending a charge request.

If customers accidentally click a charge button and you want to give them a refund, please [email us](mailto:ec.apps@lightspeedhq.com) with the details. We will help you.
