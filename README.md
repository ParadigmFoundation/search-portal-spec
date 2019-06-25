# Portal specification: `Search`

Specification document (this README), [design screenshots](./images), [API reference](#api-reference), [code samples](#code-samples), and the [master sketch file](./search.sketch) for the Paradigm/Kosu search portal.

## Contents

- [Background](#background)
- [Specification](#specification)
    - [Main page](#main-page)
    - [Filter form](#filter-form)
    - [Order table](#order-table)
- [API Reference](#api-reference)
    - [Orders for query](#orders-for-query)
    - [Order by ID](#order-by-id)
- [Code samples](#code-samples)
    - [Load address](#load-address)
    - [Execute fill](#execute-fill)
    - [Check fill status](#check-fill-status)
    - [Verify fill status](#verify-fill-status)
    - [Check allowances](#check-allowances)
    - [Check balances](#check-balances)
    - [Await transaction](#await-transaction)

## Background
The search portal enables users to view 

## Specification

### Main page

#### On load

#### Metamask connection

#### Showing balances

### Filter form

#### Standard tokens

#### Bid and ask

#### Standard to custom

#### Custom to custom

#### Search button

#### Coming soon

### Order table

#### Prompt to fill

#### Confirmation and signature

#### Pending state

#### Successful fill

#### Failed fill

## API Reference
API reference for a future middleware server that will respond to client requests from a database of Kosu orders.

### Orders for query
Load and paginate historical orders submitted by a given maker's trading `pair`, and order `side` (bid/ask).

### Order by ID
Load a full 0x order object from the Kosu network, provided an `orderId` string.

## Code samples
JavaScript code samples for working with the `0x.js` and `web3` libraries for checking balances and filling orders.

### Load address

### Execute fill

### Check fill status

### Verify fill success

### Check allowances

### Check balances

### Await transaction