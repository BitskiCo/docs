# Transaction Operator

The transaction operator allows transactions to be submitted over REST without specifying a nonce. The system will ensure that the next nonce is correctly specified, and that transactions are re-submitted in case of timeouts or other node errors. Submission is **idempotent** as long as the same transaction id is used.

## Usage:

This API can be used with any app wallet credentials that request the `eth_sign` scope. \(Chain id `1` is mainnet, `4` is rinkeby, etc\).

Curl example:

```text
$ curl -X POST -H "Authorization: Bearer <ACCESS_TOKEN>" -H "Content-Type: application/json" -d '{
  "transaction": {
    "id": "932018a0-3091-4323-ba80-e2145badc174",
    "params": {
      "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
      "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
      "gas": "0x76c0",
      "gasPrice": "0x9184e72a000",
      "value": "0x9184e72a",
      "data": "0x0"
    }
  }
}' https://api.bitski.com/v1/eth/chains/1/transactions

=> 
{
  "transaction": {
    "id": "932018a0-3091-4323-ba80-e2145badc174",
    "params": {
      "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
      "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
      "gas": "0x76c0",
      "gasPrice": "0x9184e72a000",
      "value": "0x9184e72a",
      "data": "0x0",
      "nonce": "0x01",
    },
    "status": "PENDING",
    "hash": "0x68fcfcf5aef8e7a79b8d6b7e498415896e4dd62861cd5b38fa11ad035f44582c",
    "signedData": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
    "lastError": null
  }
}
```

### Polling for updates:

Transactions are queued and submitted out of band \(status will be `PENDING`, `SUBMITTED`, or `ERROR`\). In order to see the status of a submitted transaction, all transactions can be queried, or a single transaction can be specified by id:

```text
$ curl -H "Authorization: Bearer <ACCESS_TOKEN>" https://api.bitski.com/v1/eth/chains/1/transactions

=> 
{
  "transactions": [{
    "id": "932018a0-3091-4323-ba80-e2145badc174",
    "params": {
      "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
      "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
      "gas": "0x76c0",
      "gasPrice": "0x9184e72a000",
      "value": "0x9184e72a",
      "data": "0x0",
      "nonce": "0x01",
    },
    "status": "PENDING",
    "hash": "0x68fcfcf5aef8e7a79b8d6b7e498415896e4dd62861cd5b38fa11ad035f44582c",
    "signedData": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
    "lastError": null
  }]
}

# Or by id
$ curl -H "Authorization: Bearer <ACCESS_TOKEN>" https://api.bitski.com/v1/eth/chains/1/transactions/932018a0-3091-4323-ba80-e2145badc174

=> 
{
  "transaction": {
    "id": "932018a0-3091-4323-ba80-e2145badc174",
    "params": {
      "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
      "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
      "gas": "0x76c0",
      "gasPrice": "0x9184e72a000",
      "value": "0x9184e72a",
      "data": "0x0",
      "nonce": "0x01",
    },
    "status": "PENDING",
    "hash": "0x68fcfcf5aef8e7a79b8d6b7e498415896e4dd62861cd5b38fa11ad035f44582c",
    "signedData": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
    "lastError": null
  }
}
```

## Current Limitations:

* Transactions that do not have a high enough gas price will not automatically have the gas price adjusted, so if gas prices spike, the transaction will remain in the queue until prices return to a low enough level. Alternatively a new transaction can be submitted with that same nonce via the standard JSON RPC api to increase the gas price and flush the transaction through.
* Transactions that cannot be submitted to the mempool could consume a nonce but be stuck getting retried forever. There are many checks to prevent this, but no guarantees.
* `gas` and `gasPrice` are not currently overridden, and must be provided by the caller.

