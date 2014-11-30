---
title: Tuxedio API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='http://www.tuxedio.com/sign_up'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Come one, come all! Welcome to the Tuxedio API. This documentation will help
you learn to use our API to facilitate user-driven experiences.

Our primary goal is to make this documentation *as helpful as possible*, so if
there are any hiccups in your experience please get in touch so we can fix the
problems while you get back to making innovative apps.

# Signing up `POST /v1/users(.:format)`

When you sign up, you create a user account with a handle (username), email,
and password. This will be used as your means for authentication for creating,
updating, and deleting resources.

> Submit your login:

```shell
curl "http://api.tuxedo.com/v1/login.json" \
  -H "Content-Type: application/json" \
  -d '{"user":{"email":"me@example.com","password":"foobar123"}}'
```


# Logging in `POST /v1/login(.:format)`

When you log in, you obtain a [JWT token](http://jwt.io/) by posting your email
and password. This token is used to authethenticate you for requests. By default,
it expires after 24 hours.

> To log in, use this code:

```shell
curl "http://api.tuxedo.com/v1/login.json" \
  -H "Content-Type: application/json" \
  -d '{"user":{"email":"me@example.com","password":"foobar123"}}'
```

<aside class="success">
Upon successful login, you will receive a token in the response which you can
use in subsequent requests.
</aside>

# Authentication

> To authorize, just pass in the JWT Token in the header of your request.

```shell
curl "http://api.tuxedo.com/v1/experiences" \
  -H "Authentication: Bearer MY_JWT_TOKEN"
```

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).


`Authentication: Bearer MY_JWT_TOKEN`

<aside class="notice">
You must replace `MY_JWT_TOKEN` with the personal JWT token that you recieved.
</aside>

# Experiences `GET /v1/experiences(.:format)`

```shell
curl "http://api.tuxedo.com/v1/experiences" \
  -H "Authentication: Bearer MY_JWT_TOKEN"
```

Parameter | Default | Description
--------- | ------- | -----------
upcoming  | true    | If set to true, only upcoming experiences show up


## Get All Kittens

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
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
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

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

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

