### Making JSON-RPC requests

Now that you have an access token and an ethereum address you can start sending transactions. We support all the standard Web3 JSON-RPC methods, so you can also use any Web3 client to send these transactions.

```text
POST /web3/mainnet HTTP/2
Host: https://api.bitski.com
Content-Type: application/json
Authorization: Bearer YOUR ACCESS TOKEN
X-API-Key: YOUR CLIENT ID

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

Assuming your token is valid, this account is funded, and the transaction is valid, it will be signed.

Transactions submitted via this API must include all fields with the exception of _nonce_.

For a list of all the supported methods, see [Ethereum's JSON-RPC spec](https://github.com/ethereum/wiki/wiki/JSON-RPC).

## JSON-RPC Endpoints

Name | URL
-----|-----
ethereum | https://api.bitski.com/v1/web3/mainnet
kovan | https://api.bitski.com/v1/web3/kovan
rinkeby | https://api.bitski.com/v1/web3/rinkeby
