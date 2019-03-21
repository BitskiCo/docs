One of the main differences with using Bitski's wallet in your app over Metamask or other wallet providers is in the send transaction flow.

## How it works

When you submit a transaction via `sendTransaction(...)`, our SDK will pick up the transaction and show an approval dialog to the user. For security this approval dialog is hosted on Bitski's website. The user can then review the details of the transaction, and either approve it or reject it.

On the web, we show the dialog as a modal over your web app. On iOS, this happens in a Safari modal that displays over the native app.

If the user approves the transaction, Bitski will sign the transaction, submit it to the network, and return the transaction hash just like any other wallet. If the user declines the transaction, we will return an error.

## Optional fields

Bitski does not require all fields of a transaction to be submitted in order to process a transaction. The following fields are optional:

Name | Default behavior
---- | ----------------
nonce | Bitski will calculate the next nonce for you.
gasPrice | Bitski will calculate a gas price for you based on the current averages.

## Gas

We believe that most people don't want to have to think about gas and gas prices. They are confusing terms and concepts. In our transaction approval screen we display gas as a transaction fee, and don't currently offer the ability to customize it. This creates an experience that is more familiar to most people.
