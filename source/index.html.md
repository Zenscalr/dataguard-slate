---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the DataGuard API
---

# Introduction

Welcome to the DataGuard API! You can use our API to access DataGuard API endpoints, which allows programmatic access to the DataGuard Secure LLM Systems.

We have language bindings in Shell, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: api_key"
```

```javascript
const dataguard = require("dataguard");

let api = dataguard.authorize("api_key");
```

> Make sure to replace `api_key` with your API key.

DataGuard uses API keys to allow access to the API. You can register a new DataGuard API key at our [developer portal](http://example.com/developers).

DataGuard expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: api_key`

<aside class="notice">
You must replace <code>api_key</code> with your personal API key.
</aside>

# Chat

## The Chat Session object

| Attribute      | Type           | Description                                                             | Readonly |
| -------------- | -------------- | ----------------------------------------------------------------------- | -------- |
| **id**         | UUID           | The unique identifier for the chat session                              | Yes      |
| **user_id**    | UUID           | The unique identifier for the user involved in the chat session         | Yes      |
| **messages**   | Array          | An array of message objects associated with the chat session            | No       |
| **method**     | `api` or `web` | The method through which the chat session was initiated                 | Yes      |
| **engine**     | String         | The LLM engine used in the chat session                                 | Yes      |
| **status**     | String         | The status of the chat session (active, closed, suspended, etc.)        | No       |
| **start_time** | String         | The start time of the chat session                                      | Yes      |
| **end_time**   | String         | The end time of the chat session (null if the session is still ongoing) | No       |
| **created_at** | String         | The date and time when the chat session was created                     | Yes      |
| **updated_at** | String         | The date and time when the chat session was last updated                | Yes      |

## Get all chat sessions

```shell
curl "http://example.com/api/chat" \
  -H "Authorization: api_key"
```

```javascript
const dataguard = require("dataguard");

let api = dataguard.authorize("api_key");
let chats = api.chats.get();
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

| Parameter    | Default | Description                                                                      |
| ------------ | ------- | -------------------------------------------------------------------------------- |
| include_cats | false   | If set to true, the result will also include cats.                               |
| available    | true    | If set to false, the result will include kittens that have already been adopted. |

## Get a Specific Chat Session

```shell
curl "http://example.com/api/chat/2" \
  -H "Authorization: api_key"
```

```javascript
const dataguard = require("dataguard");

let api = dataguard.authorize("api_key");
let chats = api.chats.get(2);
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

This endpoint retrieves a specific chat session.

### HTTP Request

`GET http://example.com/api/chat/<ID>`

### URL Parameters

| Parameter | Description                            |
| --------- | -------------------------------------- |
| ID        | The ID of the chat session to retrieve |

## Delete a Specific Chat Session

```shell
curl "http://example.com/api/chat/2" \
  -X DELETE \
  -H "Authorization: api_key"
```

```javascript
const dataguard = require("dataguard");

let api = dataguard.authorize("api_key");
let chats = api.chats.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted": ":("
}
```

This endpoint deletes a specific chat session.

### HTTP Request

`DELETE http://example.com/api/chat/<ID>`

### URL Parameters

| Parameter | Description                          |
| --------- | ------------------------------------ |
| ID        | The ID of the chat session to delete |
