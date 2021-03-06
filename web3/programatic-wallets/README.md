# Programatic Wallets

In addition to managing wallets for users of your app, Bitski can also manage wallets for your backend apps and services. This is a very powerful tool, as it allows you to perform programmatic transactions on the server instead of the client, and in some cases remove the need for your users to pay gas.

Bitski offers two kinds of programatic wallets:

## [Enterprise Wallets](enterprise-wallet.md)

_Note: enterprise wallets were formerly known as app wallets_

Enterprise wallets are a great place to execute transations on behalf of your organization. For instance, you could:

* Mint tokens and send them to people.
* Execute meta transactions on behalf of your users.
* Update variables in your contract.

Additionally, you can use Enterprise Wallets in Truffle for deploying your smart contracts.

## [Whitelabel Wallets](whitelabel-wallet.md)

Whitelabel wallets are a great solution when you want complete control over a users blockchain experience and your users don't need to interact with any other applications. For instance, you could:

* Create a savings account for users where they can deposit DAI and earn interest.
* Create a unique address for each user in your game where their assets can be saved.

Authentication for whitelabel wallets is handled by your backend and users will not see any Bitski UI.

_Note: each whitelabel wallet is own ethereum account so it will need gas to execute transactions. Because of this we suggest combining whitelabel wallets with meta transactions so that you can pay fees from your enterprise wallet. This would also make it easy to transfer assets out if a user wants to sign up for their own wallet._

