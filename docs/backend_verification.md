# User Wallet Verification

## Obtaining an Access Token

Before you can verify a user's wallet you will need to obtain an access token, either via the Bitski JS SDK or via a custom redirect flow.

### Using the [Bitski JS SDK](https://bitskico.github.io/bitski-js/)

Once your user has signed in with Bitski, simply call `bitski.getCurrentAccessToken()` to get the access token of the current user. You can then send that access token to your backend.

### Using OAuth2/OpenID Connect

If your app is not using the [Bitski JS SDK](https://bitskico.github.io/bitski-js/) and you want to authenticate a user you will need to complete the following:

1. Configure your backend for [OAuth](oauth.md) integration.
2. Get an access token for the current user.
3. Use that access token to make API calls.

Configuring your backend will be different based on the web framework you use. Here is an example using Ruby on Rails:

```ruby
require 'oauth2'
client_id = 'YOUR_CLIENT_ID'
client_secret = 'YOUR_CLIENT_SECRET' #optional

client = OAuth2::Client.new(client_id, client_secret, :site => 'https://account.bitski.com')
auth_url = client.implicit.authorize_url(:redirect_uri => 'http://localhost:8080/oauth/callback')
# get the token params in the callback and
token = OAuth2::AccessToken.from_kvform(client, query_string)
```

Once you have your access token, you can make JSON RPC calls. For user wallets you will not be able to sign on behalf of the user, but you can request their accounts. All API calls need the `x-api-key` header, and any calls that require user authentication need an access token bassed as bearer authentication. For example:

## Verifying accounts

Once you have an access token you can get a Bitski verified list of accounts for any user:

```ruby
uri = URI('https://api.bitski.com/v1/web3/mainnet')
params = {id: 1,jsonrpc: '2.0', method: 'eth_accounts',params:[]}
headers = {
    'Authorization' => "Bearer #{token}",
    'X-API-Key' => "Bearer #{client_id}",
    'Content-Type' => 'application/json',
    'Accept' => 'application/json'
}

http = Net::HTTP.new(uri.host, uri.port)
response = http.post(uri.path, params.to_json, headers)
```

## Verifying User Information

You can retrieve details about the current logged in user using the standard OpenID Connect UserInfo endpoint. This might be part of your OAuth framework, but if it isn't you can make the request manually:

```ruby
uri = URI('https://account.bitski.com/userinfo')
headers = {
    'Authorization' => "Bearer #{token}",
    'Content-Type' => 'application/json',
    'Accept' => 'application/json'
}

http = Net::HTTP.new(uri.host, uri.port)
response = http.get(uri.path, headers)
```

This will return json with at the very least a unqique subject:

```json
{
    "sub": "b8fbfbfe-0692-4e96-85a7-8833634a4538"
}
```

It will also contain the user's email address if you requested it and the user accepted.

## Offline Access

You can also request offline access which will let you make calls on behalf of the user even if they close their browser tab. Consult the documentation on your oauth framework for instructions to obtain a refresh token and how to exchange it for an access token. If you are using the [Bitski JS SDK](https://bitskico.github.io/bitski-js/) you can get a refresh token with `bitski.getCurrentRefreshToken()` but you will still need to use your provider's method of exchanging it for an access token.
