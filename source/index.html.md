---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: JavaScript
  - php: PHP

toc_footers:
  - <a href='https://bithomp.com/dev/register'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/bithomp/slate'>This project on GitHub</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Bithomp API! You can use our API to access Bithomp API endpoints, which can get information on XRPL addresses, transaction hashes, validators, usernames and paymentIDs and more.

We have language bindings in Shell, JavaScript and PHP! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Changelog

## 17th December 2019

Added two API endpoints:

* Address: Get XRPL address info
* Validator: Get Validator's XRP address

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

# Address

## Get XRPL address info

```shell
curl "https://bithomp.com/api/v2/address/rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY?service=true&username=true&paymentid=true&parent=true"
  -H "x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd"
```

```javascript
function getAddressInfo(json) {
  console.log(json)
}
bithompRequest("https://bithomp.com/api/v2/address/rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY?service=true&username=true&paymentid=true&parent=true", getAddressInfo);
```

```php
$addressInfo = curl_bithomp("https://bithomp.com/api/v2/address/rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY?service=true&username=true&paymentid=true&parent=true");
print $addressInfo;
```

> The above command returns JSON structured like this:

```json
{
  "address":"rPEPPER7kfTD9w2To4CQk6UCfuHM9c6GDY",
  "xAddress":"XV5sbjUmgPpvXv4ixFWZ5ptAYZ6PD2gYsjNFQLKYW33DzBm",
  "inception":1513126312,
  "username":"xrptipbot",
  "paymentId":"xrptipbot$bithomp.com",
  "service":{
    "name":"XRP Tip Bot",
    "domain":"xrptipbot.com",
    "accounts":{
      "twitter":"xrptipbot"
    }
  },
  "parent":{
    "address":"rDsbeomae4FXwgQTJp9Rs64Qg9vDiTCdBv",
    "xAddress":"XV3oNHx95sqdCkTDCBCVsVeuBmvh2du1vBfJR24EqdgwHDW",
    "inception":1481884572,
    "service":{
      "name":"Bitstamp",
      "domain":"bitstamp.net",
      "accounts":{
        "gravatar":"5b33b93c7ffe384d53450fc666bb11fb",
        "twitter":"Bitstamp",
        "facebook":"Bitstamp"
      }
    }
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
parent | false | If set to true, the result will include the same info for a parent account.

<aside class="notice">
Exclude unnecessary parameters to make your request faster.
</aside>

# Validator

## Get Validator's XRP address

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
