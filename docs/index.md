Bitski lets you build *user-friendly* and *cross-platform* Ethereum apps. Using Bitski, you can build a decentralized app or game that feels just as easy to use as a standard app.

We provide you with access to the Ethereum network through our hosted nodes, and provide access to the user's wallet using OAuth. [Learn More](overview.md).

## Simple integration

You can sign up for a free developer account to get started in the <a href="https://developer.bitski.com" target="_blank">Developer Portal</a> to get your client id. Then install [bitski](https://www.npmjs.com/package/bitski)
and [web3](https://www.npmjs.com/package/web3) via npm.

```javascript
import { Bitski } from 'bitski';
import Web3 from 'web3';

// Configure Bitski and get a web3 provider
const bitski = new Bitski('CLIENT-ID', 'https://myapp.com/oauth-callback.html');
const provider = bitski.getProvider();
const web3 = new Web3(provider);

// Prompt user to sign in via a secure OAuth flow
await bitski.signIn();

// All set! you can now make web3 calls to get accounts
let accounts = await web3.eth.getAccounts();

// Or prompt the user to send a transaction
web3.eth.sendTransaction({
  from: [accounts[0]],
  to: '0x0000000000000000000000000000000000000000',
  value: web3.utils.toWei(1, 'ether')
});
```


## Shortcuts

- Need a developer account? <a href="https://developer.bitski.com" target="_blank">Sign up here</a>.
- Learn more how it works in our [overview](overview.md).
- Ready to start building? Check out [getting started](getting-started.md) and our [quickstart repo](https://github.com/BitskiCo/quickstart).
- Got questions? Chat with us in our <a href="https://discord.gg/5f6pAFN" target="_blank">Discord</a>.

## Platforms

We have SDKs for easy integration with various platforms. You can find more information on each SDK below.

- [JavaScript](https://github.com/BitskiCo/bitski-js/) – Add our user-friendly Ethereum wallet to your web app
- [Node.js](https://github.com/BitskiCo/bitski-node/) – Execute transactions from your backend, or deploy contracts with Truffle
- [iOS](https://github.com/BitskiCo/bitski-ios/) – Integrate Bitski with your iOS app

## FAQ

We've compiled a list of common questions [here](faq.md).

## Report Vulnerabilities
Bitski provides a “bug bounty” to engage with the security researchers in the community. If you have found a vulnerability in our product or service, please [submit a vulnerability report](https://www.bitski.com/bounty) to the Bitski security team.
