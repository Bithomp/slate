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

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd"
```

```javascript
// With javascript, you can just pass the correct header with each request
$.ajax({
   url: "api_endpoint_here",
   type: "GET",
   contentType: "application/json"
   headers: {
      "x-bithomp-token": "abcd-abcd-0000-abcd-0123abcdabcd"
   },
   success: function (result) {
       // callback(result);
   },
   error: function (error) {

   }
});
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

Bithomp uses API keys to allow access to the API. You can register a new Bithomp API key at our [developer portal](https://bithomp.com/dev/register).

Bithomp expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-bithomp-token: abcd-abcd-0000-abcd-0123abcdabcd`

<aside class="notice">
You must replace <code>abcd-abcd-0000-abcd-0123abcdabcd</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
