# Set up your dev environment in Ecwid

Gaining API access requires you to have a store and a platform where you can configure permissions and generate access tokens. In Ecwid, we refer to this platform as an **application**. A private application that gives you access to store data through API is called a **custom application**.&#x20;

In the following guide, you’ll find instructions on getting yourself a test store with a custom app. Together, they'll allow you to make API requests and manage your store data through the code.

### **Step 1. Sign up with Ecwid**

The first step is to get yourself a store. Only stores on paid plans can access API. If you don’t yet have a store, [sign up with Ecwid](https://my.ecwid.com/cp/#register).

Ecwid provides a **free upgrade to a paid plan** if you:

* Work on a store customization project for your paid store or one of our clients.
* Want to build an integration for your working store in a safe environment, without risks of damaging the data.
* Develop a public application for our App Market.
* Build professional templates for the Ecwid website builder called Instant Site.

[Email us](../contact-ecwid-api-support-team.md#email-support) to get a free plan upgrade for your test store.

### **Step 2. Get your first application**

You can manage API access to your store data right in the Ecwid admin, through the [app dashboard](https://my.ecwid.com/#develop-apps). Here you can create and manage apps that grant API access only to your store.

When you open the app dashboard for the first time, Ecwid automatically generates the first **custom app** for you.

A custom app is your private way of accessing Ecwid API. It can only work with the store where it's created, but it allows you to completely skip the need for authentication. Just get the app and start making API requests with its **access tokens**. \
\
Custom apps come with some default permissions allowing you to:

* Receive, change, and delete details about products and categories in your store.
* Create new products and categories.
* Receive store profile details.
* Receive and change details of all placed and unfinished orders in your store.

Learn more about app settings:

[App settings](../develop-apps/app-settings.md)

[Add more features to your custom app](add-more-features-to-your-custom-app.md)
