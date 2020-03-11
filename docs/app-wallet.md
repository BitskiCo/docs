In addition to managing wallets for users of your app, Bitski can also manage wallets for your backend apps and services. This is a very powerful tool, as it allows you to perform programmatic transactions on the server instead of the client, and in some cases remove the need for your users to pay gas. Additionally, you can use App Wallet in Truffle for deploying your smart contracts.

## Creating an App Wallet

To create an app wallet, first you will need an app. Start by visiting our [Developer Portal](https://developer.bitski.com), then click *New App* and enter your details.

After you create your app, you can create your *App Wallet*. Navigate to your app details in the developer portal. Then, select the **Accounts** tab. Click *New Account* to generate an ethereum account. You will then see your account's address and current balance across our supported networks.

## Creating your credentials

In order to actually use your App Wallet in your code, you will need to create credentials. These credentials are exchanged with our OAuth server for an access token, which is then used to access your accounts.

To create a credential, first visit your app details page in the dev portal. Then, select the **Backend Credentials** tab, and click *New Credential*.

Your *credential id* and *client secret* will be displayed in a modal. Make sure to download the credentials or copy these down somewhere, as the secret cannot be retrieved later. If you lose the secret, you can regenerate it on this screen as well.

Currently, each credential can access all of the accounts under your app. We recommend creating one credential per app or service that uses it. That way you can remove access as needed with as little interruption as possible.

Important: Since these credentials allow you to send transactions from your app wallet without any prompt, you should treat them as a username and password, and be careful not to share them with any untrusted parties.

## Funding your App Wallet

For now, this is a manual process. We recommend buying ETH from a third-party such as <a href="https://coinbase.com" target="_blank">Coinbase</a> and sending it to your app wallet's address.

## Signing Rules

For additional security, we allow you to create rules around what transactions should be signed. These rules are specific to each individual address for additional flexibility. You can find these settings by visiting the **Accounts** tab under your app, then clicking *Edit* on the account you want to set rules for.

### Restrict To Addresses

This rule allows you to lock your App Wallet to only sign transactions where the recipient matches the list. When enabled, transactions will be checked for their "to" field and only transactions that match will be approved. This is a good feature to enable for use cases where your account is only being used to execute calls on a particular contract.

## Backend SDKs

We currently have SDKs for both Node.js and Python applications. These SDKs take your credentials and give you a web3 provider that is ready to use. If you would like to use App Wallet on another platform, please <a href="mailto:hello@bitski.com">contact us</a> and we will consider creating an SDK for it.

- [Node SDK](https://github.com/BitskiCo/bitski-node)
- [Python SDK](https://github.com/BitskiCo/bitski-py)

## Deploying Contracts with Truffle

We also have a simple Truffle plugin that makes deploying contracts from your App Wallet easy. Read more about it [here](https://github.com/BitskiCo/bitski-truffle-provider).

## Using our API

You can use our apis directly from your backend to perform anything you want using your wallet. Here's how it works:

### Getting an Access Token

First, you'll use your credential id and secret to request an access token using OAuth. Most platforms have a library that can handle this step for you. Your token has a relatively short lifespan, so you should store the expiration date and request a new one when it expires. In order to sign transactions, you must request the scope `eth_sign`.

```text
POST /oauth2/token HTTP/2
Host: https://account.bitski.com

grant_type=client_credentials
&client_id=YOUR CLIENT ID
&client_secret=YOUR CLIENT SECRET
&scope=eth_sign
```

```text
HTTP/2 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache

{
  "access_token": "YOUR ACCESS TOKEN",
  "token_type": "bearer",
  "expires_in": 3600,
  "scope": "eth_sign"
}
```

### Making JSON-RPC requests

Once you have an access token, you must add that to the Authorization header for all your Web3 API requests. We support all the standard Web3 JSON-RPC methods, so you can also use any Web3 client to send these transactions.

```text
POST /web3/mainnet HTTP/2
Host: https://api.bitski.com
Content-Type: application/json
Authorization: Bearer YOUR ACCESS TOKEN

{
  "id": 1
  "jsonrpc": "2.0",
  "method": "eth_sendTransaction",
  "params": [{
    "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
    "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
    "gas": "0x76c0",
    "gasPrice": "0x9184e72a000",
    "value": "0x9184e72a",
    "data": "0x0"
  }]
}
```

```text
HTTP/2 200 OK
Content-Type: application/json

{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

Assuming your token is valid, your account is funded, the transaction satisfies the signing rules, and the transaction is valid, it will be signed.

Transactions submitted via this API must include all fields with the exception of _nonce_.

For a list of all the supported methods, see [Ethereum's JSON-RPC spec](https://github.com/ethereum/wiki/wiki/JSON-RPC).

## JSON-RPC Endpoints

Name | URL
-----|-----
ethereum | https://api.bitski.com/v1/web3/mainnet
kovan | https://api.bitski.com/v1/web3/kovan
rinkeby | https://api.bitski.com/v1/web3/rinkeby
