# Getting Started

## Creating an app

All apps that use the Bitski need to be registered in our Developer Portal. We use this to keep track of permissions a user has granted you.

To register, visit our [developer portal](https://developer.bitski.com), and click **New App**.

Once registered, you can select your new app from the list, and you should now be able to see your client id.

## Configuring your client settings

Once you have created your app, you'll need to configure the OAuth settings for your app. You can do this from the OAuth tab under your app details page in the [developer portal](https://developer.bitski.com).

The most important setting here is the redirect url\(s\). We use this to ensure that only the domains you approve will be able to get access tokens for your client id.

For more information on all the settings, see [Client Settings](client-settings.md).

## Integrate with your app

Now that you have a configured your app on Bitski, you can start using our SDKs in your app.

A great place to start for new web-based apps is our [Quickstart Truffle Box](https://github.com/BitskiCo/quickstart).

You can find more details on integrating with your app by reviewing the instructions for the particular SDK you're using:

* [JavaScript](https://github.com/BitskiCo/bitski-js)
* [iOS](https://github.com/BitskiCo/bitski-ios)

For web based apps, you'll need to be able to respond to the callback from our servers.

It's also important to consider the user experience for various states your user will be in. Our SDKs can tell you whether or not the user is currently logged in, and you should update your UI based on that information.

