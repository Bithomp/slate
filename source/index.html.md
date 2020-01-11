---
title: Bithomp API reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: JavaScript
  - php: PHP

toc_footers:
  - <a href='https://bithomp.com/dev/register'>Sign Up for a Developer Key</a>
  - <a href='https://coil.com/p/ihomp/XRP-Ledger-domain-verification/uJKPWh_4C'>XRPL domain verification</a>
  - <a href='https://github.com/bithomp/slate'>Edit this project on GitHub</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Bithomp API! You can use our API to access Bithomp API endpoints, which can get information on XRPL addresses, transaction hashes, validators, usernames and paymentIDs and more.

We have language bindings in Shell, JavaScript and PHP. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Changelog

## 11th January 2020

Added a new API endpoint:

* <a href="#genesis">**Historical data: Genesis**</a>

## 27th December 2019

* <a href="#address">**Get information for ONE: Address**</a>

Three new query parameters added: verifiedDomain, blacklisted, hashicon.

## 17th December 2019

Added two API endpoints:

* <a href="#address">**Get information for ONE: Address**</a>
* <a href="#validator">**Get information for ONE: Validator**</a>

# Direct URL examples

## XRPL Explorer

* <a href="https://bithomp.com/explorer/F10AB598E3197342C8FE173FB3AB5408E30B00F7B4838FDA645BB01AADBD9112">https://bithomp.com/explorer/{txid}</a>
* <a href="https://bithomp.com/explorer/rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B">https://bithomp.com/explorer/{address}</a>
* <a href="https://bithomp.com/explorer/bitstamp">https://bithomp.com/explorer/{username}</a>
* <a href="https://bithomp.com/explorer/F10AB598E3197342C8FE173FB3AB5408E30B00F7B4838FDA645BB01AADBD9112#comment">https://bithomp.com/explorer/{txid}#comment</a>
* <a href="https://bithomp.com/explorer/rsuUjfWxrACCAwGQDsNeZUhpzXf1n1NK5Z#comment">
https://bithomp.com/explorer/{address}#comment</a>
* <a href="https://bithomp.com/explorer/Bithomp#comment">
https://bithomp.com/explorer/{username}#comment</a>

## Validator pages

* <a href="https://bithomp.com/validators/nHB8QMKGt9VB4Vg71VszjBVQnDW3v3QudM4DwFaJfy96bj4Pv9fA">https://bithomp.com/validators/{validor pub key}</a>

## Username registration
* <a href="https://bithomp.com/username/Bithomp">https://bithomp.com/username/{username}</a>
* <a href="https://bithomp.com/username/rsuUjfWxrACCAwGQDsNeZUhpzXf1n1NK5Z">https://bithomp.com/username/{address}</a>

## XRPL account activation
* <a href="https://bithomp.com/activation/rsuUjfWxrACCAwGQDsNeZUhpzXf1n1NK5Z">https://bithomp.com/activation/{address}</a>

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd"
```

```javascript
// With javascript, you can just pass the correct header with each request
// Include jquery in order to use $.ajax or rewrite to vanila.js

function bithompRequest(url, callback) {
  $.ajax({
     url: url,
     type: "GET",
     contentType: "application/json",
     headers: {
        "x-bithomp-token": "abcd-abcd-0000-abcd-0123abcdabcd"
     },
     success: function(result) {
        callback(result);
     },
     error: function(error) {
        console.log(error);
        callback({"error": "error occurred"});
     }
  });
}

bithompRequest("api_endpoint_here", callback);
//replace callback with your function to process a received json

```

```php
function curl_bithomp($url) {
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_HTTPHEADER,
        array('x-bithomp-token:abcd-abcd-0000-abcd-0123abcdabcd')
    );
    $output = curl_exec($ch);
    curl_close($ch);
    return $output;
}

print curl_bithomp("api_endpoint_here")
```

> Make sure to replace `abcd-abcd-0000-abcd-0123abcdabcd` with your API key.

In order to use our APIs you need to request an API key via [the following form](https://bithomp.com/dev/register).

Bithomp expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd`

<aside class="notice">
You must replace <code>abcd-abcd-0000-abcd-0123abcdabcd</code> with your personal API key.
</aside>

# Get information for ONE

## Address

```shell
curl "https://bithomp.com/api/v2/address/rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY?service=true&username=true&paymentid=true&parent=true&verifiedDomain=true&blacklisted=true"
  -H "x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd"
```

```javascript
function getAddressInfo(json) {
  console.log(json)
}
bithompRequest("https://bithomp.com/api/v2/address/rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY?service=true&username=true&paymentid=true&parent=true&verifiedDomain=true&blacklisted=true", getAddressInfo);
```

```php
$addressInfo = curl_bithomp("https://bithomp.com/api/v2/address/rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY?service=true&username=true&paymentid=true&parent=true&verifiedDomain=true&blacklisted=true");
print $addressInfo;
```

> The above command returns JSON structured like this:

```json
{
  "address": "rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY",
  "xAddress": "XV5sbjUmgPpvXv4ixFWZ5ptAYZ6PD2gYsjNFQLKYW33DzBm",
  "inception": 1513126312,
  "username": "xrptipbot",
  "paymentId": "xrptipbot$bithomp.com",
  "service": {
    "name": "XRP Tip Bot",
    "domain": "xrptipbot.com",
    "accounts": {
      "twitter": "xrptipbot"
    }
  },
  "blacklisted": false,
  "verifiedDomain": "xrptipbot.com",
  "parent": {
    "address": "rDsbeomae4FXwgQTJp9Rs64Qg9vDiTCdBv",
    "xAddress": "XV3oNHx95sqdCkTDCBCVsVeuBmvh2du1vBfJR24EqdgwHDW",
    "inception": 1481884572,
    "service": {
      "name": "Bitstamp",
      "domain": "bitstamp.net",
      "accounts": {
        "gravatar": "5b33b93c7ffe384d53450fc666bb11fb",
        "twitter": "Bitstamp",
        "facebook": "Bitstamp"
      }
    },
    "blacklisted": false
  }
}
```

This endpoint retrieves information for a requested account.

### HTTP Request

`GET https://bithomp.com/api/v2/address/<address>`

### URL Parameters

Parameter | Description
--------- | -----------
address | The XRPL address, can be old r-address or a new X-address

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
service | false | If set to true, the result will also include Service details.
username | false | If set to true, the result will also include a username (rippletrade or bithomp).
paymentid | false | If set to true, the result will also include a paymentID.
verifiedDomain | false | If set true, the result will include a <a href="https://coil.com/p/ihomp/XRP-Ledger-domain-verification/uJKPWh_4C">verifiedDomain</a> if such exists.
blacklisted | false | If set true, the result will include a blacklisted status (status 3 in <a href="https://xrpforensics.org/list/">the xrpforensics list</a>)
hashicon | false | If set true, the result will include hashicon which can be used in img's src="" or in css, as background's url. (The icon is the same for x-address and r-address, such hashicons used in ToastWallet and Bithomp.)
parent | false | If set to true, the result will include the same info for a parent account.

<aside class="notice">
Exclude unnecessary parameters to make your request faster.
</aside>

## Validator

```shell
curl "https://bithomp.com/api/v2/validator/nHB8QMKGt9VB4Vg71VszjBVQnDW3v3QudM4DwFaJfy96bj4Pv9fA"
  -H "x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd"
```

```javascript
function getValidatorAddress(json) {
  console.log(json.publicKey + " validator's XRPL address: ", json.address);
}
bithompRequest("https://bithomp.com/api/v2/validator/nHB8QMKGt9VB4Vg71VszjBVQnDW3v3QudM4DwFaJfy96bj4Pv9fA", getValidatorAddress);
```

```php
$validatorAddress = curl_bithomp("https://bithomp.com/api/v2/validator/nHB8QMKGt9VB4Vg71VszjBVQnDW3v3QudM4DwFaJfy96bj4Pv9fA");
print $validatorAddress;
```

> The above command returns JSON structured like this:

```json
{
  "publicKey": "nHB8QMKGt9VB4Vg71VszjBVQnDW3v3QudM4DwFaJfy96bj4Pv9fA",
  "address": "rKontEGtDju5MCEJCwtrvTWQQqVAw5juXe"
}
```

This endpoint retrieves a XRPL address of a specific validator
<a href="https://github.com/codetsunami/xrpl-tools/blob/master/validator-address-tool/vatool.js">computed from the validator public key</a>

### HTTP Request

`GET https://bithomp.com/api/v2/validator/<validatorPublicKey>`

### URL Parameters

Parameter | Description
--------- | -----------
validatorPublicKey | The public key of the validator to retrieve

# Historical data

## Genesis

```shell
curl "https://bithomp.com/api/v2/genesis"
  -H "x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd"
```

```javascript
function printData(json) {
  console.log(JSON.stringify(json, undefined, 2));
}
bithompRequest("https://bithomp.com/api/v2/genesis", printData);
```

```php
$data = curl_bithomp("https://bithomp.com/api/v2/genesis");
print $data;
```

> The above command returns JSON structured like this:

```json
{
  "count": 136,
  "inception": 1357010470,
  "ledger_index": 32570,
  "genesis_balance_all": 99999999999.99632,
  "balance_all": 483189349.682485,
  "balance_update": 1578499794,
  "genesis": [
    {
      "address": "rBKPS4oLSaV2KVVuHH8EpQqMGgGefGFQs7",
      "genesis_balance": 370,
      "genesis_index": 1,
      "balance": 20.009958
    },
    {
      "address": "rLs1MzkFWCxTbuAHgjeTZK4fcCDDnf2KRv",
      "genesis_balance": 10000,
      "genesis_index": 2,
      "rippletrade": "leotreasure",
      "balance": 4507.158497
    },
    {

    }
  ]
}
```

This endpoint retrieves a list of addresses from the first available ledger in XRPL history.

### HTTP Request

`GET https://bithomp.com/api/v2/genesis`

### Response Format

Field | Value | Description
----- | ----- | -----------
count	| Integer	| The amount of returned addresses.
inception	| Integer	| Inception UNIX timestamp.
ledger_index | Integer | Ledger index (the first available in history).
genesis_balance_all | Float | Sum of all balances in the ledger_index.
balance_all | Float | Sum of balances of those addresses on the balance_update time.
balance_update | Integer | UNIX timestamp of the last update of balances.
genesis | Array | Array of addresses in ledger_index.
genesis[].address | String | Address
genesis[].genesis_balance | Float | XRP balance on that genesis[].address on the time of inception.
genesis[].genesis_index | Integer | Index of the address in the ledger_index.
genesis[].rippletrade | String | Username that genesis[].address used on rippletrade.com.
genesis[].nickname | String | Username that genesis[].address used on bitcointalk.org or assign by Ripple (X.).
genesis[].balance | Float | XRP balance on that genesis[].address on the time of balance_update.
