# Portal specification: `Search`

Specification document (this README), [design screenshots](./images), [API reference](#api-reference), [code samples](#code-samples), and the [master sketch file](./search.sketch) for the Paradigm/Kosu search portal.

## Contents

- [Background](#background)
    - [Prerequisites](#prerequisites)
- [Specification](#specification)
    - [Main page](#main-page)
    - [Filter form](#filter-form)
    - [Order table](#order-table)
- [API Reference](#api-reference)
    - [Orders for query](#orders-for-query)
    - [Order by ID](#order-by-id)
- [Code samples](#code-samples)
    - [Connect to Metamask](#connect-to-metamask)
    - [Load address](#load-address)
    - [Check order status](#check-order-status)
    - [Verify fill](#verify-fill)
    - [Execute fill](#execute-fill)
    - [Check allowances](#check-allowances)
    - [Check balances](#check-balances)
    - [Await transaction](#await-transaction)
    - [Validate Ethereum address](#validate-ethereum-address)

## Background
The search portal enables users to view and fill [0x](https://0x.org) orders that have been relayed through the [Kosu](https://docs.kosu.io) network. It provides a simple interface to query orders across token pairs for bids and asks, and to sort by price and size.

The portal relies on an external RPC API server to act as a bridge between the Kosu network and clients. This API server is not yet built, and the underlying Kosu network is not yet relaying orders. However, the REST API for the RPC server is defined here, and it will eventually be built to meet this spec. 

The [specification](#specification) section contains screenshots of relevant states, however the full [sketch file](./search.sketch) should still be reviewed in detail.

### Prerequisites
- Basic understanding of the 0x system ([link](https://github.com/0xProject/0x-protocol-specification/blob/master/v2/v2-specification.md))
- Basic understanding of `web3` and Ethereum ([link](https://web3js.readthedocs.io/en/1.0/))
- Usage of the `0x.js` library and other 0x tools ([link](https://0x.org/docs/0x.js))
- Understanding of quote vs. base currency ([link](https://en.wikipedia.org/wiki/Currency_pair))
- Understanding of bids vs. asks and relation to currency pair ([link](https://www.investopedia.com/terms/b/bid-and-ask.asp))
- Understanding of basic order book concepts ([link](https://en.wikipedia.org/wiki/Central_limit_order_book))

## Specification

### Main page

#### On load
![Main page: on-load](./images/main-no-metamask.png)

#### Metamask connection
![Main page: connected](./images/main-connected.png)

#### Showing balances
![Main page: balance bar](./images/main-balance-bar.png)

### Filter form

#### Standard tokens
![Filter form: standard tokens](./images/filter-main-state.png)

#### Bid and ask
![Filter form: bid and ask](./images/filter-bid-ask.png)

#### Token drop-down
![Filter form: token drop-down](./images/filter-drop-down.png)

#### Standard to custom
![Filter form: standard to custom](./images/filter-token-custom.png)

#### Custom to custom
![Filter form: custom to custom](./images/filter-custom-custom.png)

#### Coming soon
![Filter form: coming soon hover](./images/filter-coming-soon.png)

#### Search button

### Order table

#### Prompt to fill
![Order table: main state](./images/order-table-main.png)

#### Confirmation and signature
![Order table: confirm and sign](./images/order-table-confirm.png)

#### Pending state
![Order table: fill pending](./images/order-table-pending.png)

#### Successful fill
![Order table: fill success](./images/order-table-taken.png)

#### Failed fill
![Order table: fill failed](./images/order-table-failed.png)

## API Reference
API reference for a future middleware server that will respond to client requests from a database of Kosu orders.

### Orders for query
Load and paginate historical orders submitted by a given maker's trading `pair`, and order `side` (bid/ask).

### Order by ID
Load a full 0x order object from the Kosu network, provided an `orderId` string.

## Code samples
JavaScript code samples for working with the `0x.js` and `web3` libraries for checking balances and filling orders.

### Connect to Metamask
Use the following sample to connect to Metamask and load the user's `coinbase` address. This action should be triggered by a user clicking the "Connect to MetaMask" button. If the following throws, it can be assumed the user is in an incompatible browser (or doesn't have Metamask installed).

The `web3` instance and `coinbase` address should be saved and accessible throughout the application.

```javascript
import Web3 from "web3";

async function connectMetamask() {
    if (window.ethereum !== void 0) {
        try {
            // will prompt user with pop-up to allow site access
            await window.ethereum.enable();

            // load this web3 into state somewhere (needed later)
            web3 = new Web3(window.ethereum);

            // additionally, store the users address somewhere
            coinbase = await web3.eth.getCoinbase();
        } catch (error) {
            throw new Error("user denied site access");
        }
    } else if (window.web3 !== void 0) {
        // same as above, var (or let) scoped, or stored in redux state
        web3 = new Web3(web3.currentProvider);
        coinbase = await web3.eth.getCoinbase();

        // optional
        global.web3 = web3;
    } else {
        throw new Error("non-ethereum browser detected");
    }
  }
```

### Load address
The user's `coinbase` address may be loaded any time from an [initialized `web3`](#connect-to-metamask) instance. It should be stored in-state for easy access.

```javascript
async function loadCoinbase() {
    const coinbase = await web3.eth.getCoinbase();
    return coinbase;
}
```

### Check order status

### Verify fill

### Execute fill

### Check allowances

### Check balances

### Await transaction

### Validate Ethereum address
An Ethereum address is a 20-byte identifier used to receive assets on the Ethereum network, and is usually represented as a 42-character ("0x" prefixed) hexadecimal encoded string. They can be validated with a simple regular expression.

```javascript
function isValidAddress(maybeAddress) {
    if (typeof maybeAddress !== "string") {
        return false;
    }
    return /^0x[a-fA-F0-9]{40}$/.test(maybeAddress);
}
```