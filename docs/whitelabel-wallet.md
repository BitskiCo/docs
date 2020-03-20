*NOTE: To use whitelabel wallets you will need to request access. Please email sales@bitski.com if you are interested.*

## Using our API

You probably want to create a new ethereum address each time one of your users signs up. That way you can assign that address to the user and then can start transfering assets to their new account.

To do that your backend needs to take the following steps:

- Get an access token
- Make a POST request to `/v1/accounts` using that access token.

### Getting an Access Token

First, you'll use your credential id and secret to request an access token using OAuth. Most platforms have a library that can handle this step for you. Your token has a relatively short lifespan, so you should store the expiration date and request a new one when it expires. In order to sign transactions, you must request the scope `eth_sign`.

```text
POST /oauth2/token HTTP/2
Host: https://account.bitski.com

grant_type=client_credentials
&client_id=YOUR CREDENTIAL ID
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

### Getting a New Ethereum Address

Once you have an access token, you can go ahead and start creating accounts. Each time you create an account you will get an ethereum address to use. You can then use that address to sign transactions.

```text
POST /v1/accounts HTTP/2
Host: https://api.bitski.com
Content-Type: application/json
Authorization: Bearer YOUR ACCESS TOKEN
X-API-Key: YOUR CLIENT ID
```

```text
HTTP/2 200 OK
Content-Type: application/json

{
  "ethereumAddress": "0xb60e8dd61c5d32be8058bb8eb970870f07233155"
}
```

You are now ready to send [JSON RPC](programatic-wallets-json-rpc.md) requests.
