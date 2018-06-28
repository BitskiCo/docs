Here are some answers to the questions we get asked most often.

### What networks do you support?

Bitski currently supports only the Kovan and Rinkeby test networks. However, we will have support for the main Ethereum network soon.

---

### How much does Bitski charge?

Bitski is currently free of charge for users and developers.

---

### What are the benefits of Bitski managing key storage for new users?

Secure key storage is very challenging, and a siloed approach will be inconvenient for your users. Users will have to fund this wallet separately, and can only manage their assets through your interface.

---

### How should I integrate Bitski in my dapp?

A great place to start is to put our sign in button wherever you're currently asking people to install Metamask.

---

### I already have an app that uses Metamask, can I use Bitski?

The Bitski SDK is designed to be compatible with other wallets and dapp browsers, while providing a great experience for users who don't already have a wallet. Learn more about integrating our JS SDK [here](https://github.com/BitskiCo/bitski-js).

---

### How are you storing and managing private keys?

Our keys are both created and stored on our HSMs (Hardware Security Module). Approved transactions are passed to the HSM to sign. The keys never leave the hardware.

---

### Do you have an Android SDK?

Not at the moment, but that is on our roadmap.

---

### How will users fund their wallet?

Currently for ETH, users will need to use another service to purchase ETH with fiat currency, and transfer that to their Bitski wallet. We will eventually have a more integrated process.

However, if you're working with digital assets, we suggest using our app wallet API to send assets to users directly. This prevents the need for the user to purchase ETH, while allowing them to have decentralized ownership.
