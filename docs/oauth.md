Instead of using a browser extension to provide your app a wallet, Bitski uses OAuth2 to connect you to the user and their wallet. OAuth is a great standard for securely sharing data between services.

## How it works

The flow for using Bitski is a little different than with dapp browsers, and browser extensions.

First, you should check to see if the user is already logged in. Our SDKs provide an easy way to do this. If the user is already logged in, you're done!

If the user is not already logged in, you'll want to handle this in your app somehow. We provide a drop in button component on web that will make this easy for you. This can be displayed where you currently show a prompt to install Metamask or other dapp browsers.

Once the user clicks "Continue with Bitski", they will be taken through our auth flow, and eventually redirected back to your app.

For users who already have a Bitski account, it's just 1-2 clicks to get started. For people who are new to Bitski, the sign up is designed to be quick and easy. We only ask for the bare essentials during this process.

## OAuth

When you set up the SDK, you choose what permissions and data you want access to through *scopes*. By default our SDKs only request the `openid` scope.

Then, when a user visits your app for the first time and chooses to authenticate with their Bitski account, they will see the requested scopes. The user can then make a decision to approve all, some, or none of the scopes.

Once the user has made a decision to grant your app various permissions, they will be redirected back to your app at the *callback url* that you specified. Note that the callback url specified from your client must match your url settings in the developer portal.

Through being redirected, you'll receive an access token that can be used to interact with Bitski's apis on behalf of the user.

Our various SDKs automatically handle passing that access token to Web3, so most likely you won't need to do anything with the authentication token yourself.

During subsequent sessions, the user will only be asked for permission again if the scopes you requested are different.

## Available Scopes

Name | Description
---- | ------------
`openid` | Access to the user's unique identifier.
`email` | Gives you access to the user's email address. Contact us to add this to your app.
`offline` | Allows your token to be renewed with a refresh token. This is required to renew your access tokens automatically.
