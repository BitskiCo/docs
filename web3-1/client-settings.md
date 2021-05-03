# Client Settings

You can configure your app's settings from the [developer portal](https://developer.bitski.com). Here some of the things you can configure, and what they mean.

## App Info

This is metadata about your app that gives users more context. While only name is required, these details should ideally be provided for the best possible user experience.

**Name**

This is the name we'll use to reference your app in various parts of the Bitski interface. For example, in the list of connected apps under the user's account.

**App URL**

This is the URL we'll link to when referencing your app in Bitski.

**Contact Email**

This should be an email where we can contact you about any issues regarding your app. It is not currently exposed to users.

**Privacy Policy URL**

We will feature this link when asking users if they want to authorize your app.

**Terms URL**

We will feature this link when asking users if they want to authorize your app.

## Redirect URLs

These are approved URLs that clients using your _client id_ can ask to be redirected to. It's important to keep this list as small as possible so malicious apps cannot pose as you. If a client asks to be redirected to a URL that is not on this list, they will receive an error.

Note: These redirect urls must match what your client enters exactly. It is case sensitive and every character counts. Common mistakes are entering http instead of https, or entering just the domain and not the actual path \([http://localhost:3000](http://localhost:3000) instead of [http://localhost:3000/callback](http://localhost:3000/callback)\).

## Approved Scopes

These are the scopes that we have approved you to request access to in your app. For web apps, generally this is just openid. Native apps need openid and offline scopes. If you would like access to a scope and it isn't on this list, please [contact us](mailto:hello@bitski.com).

