---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Integrating with Rill

Welcome to the Rill API! You can use our API to access Rill API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# BigQuery

> This page will help you get started with Rill Data. You'll be up and running in a jiffy!

```javascript
// Example code snippit
const kittn = require('kittn');

let api = kittn.authorize('rill-service-key');
let kittens = api.kittens.get();
```

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('rill-service-key')
```

```python
import kittn

api = kittn.authorize('rill-service-key')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: rill-service-key"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('rill-service-key');
```

> Make sure to replace `rill-service-key` with your API key.

Maybe have a link to Rill API support [developer portal](http://example.com/developers).

`Authorization: rill-service-key`

<aside class="notice">
You must replace <code>rill-service-key</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('rill-service-key')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('rill-service-key')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: rill-service-key"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('rill-service-key');
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

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('rill-service-key')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('rill-service-key')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: rill-service-key"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('rill-service-key');
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

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('rill-service-key')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('rill-service-key')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: rill-service-key"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('rill-service-key');
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

