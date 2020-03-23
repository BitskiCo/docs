The Bitski SDK can also be used without a user wallet to read content from the blockchain. This can be useful to display data before the user logs in, or for basic applications that don't require a user wallet.

This feature is built in to all Bitski SDKs. Just initlize the SDK as normal. You will be able to make read-only calls without signing in.

## Other SDKs

The Bitski node infrastructure can also be used separately from our SDK. All you need is a client ID from the <a href="https://developer.bitski.com" target="_blank">developer portal</a>. Then, simply include your client ID as the `X-API-Key` header:


```javascript
var Web3HttpProvider = require('web3-providers-http');

var options = {
    headers: [{name: 'X-API-Key', value: '<YOUR CLIENT ID>'}]
};

var provider = new Web3HttpProvider('https://api.bitski.com/v1/web3/mainnet', options);
```

## JSON-RPC Endpoints

Name | URL
-----|-----
ethereum | https://api.bitski.com/v1/web3/mainnet
kovan | https://api.bitski.com/v1/web3/kovan
rinkeby | https://api.bitski.com/v1/web3/rinkeby
