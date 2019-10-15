# Introduction

Welcome to the Yamasee SkyPath API! You can use our API to access SkyPath Server API endpoints, which can get information on various aspects of the turbulence avoidance system. Using the API the application can also report new turbulence areas and aircraft geo position. 

We have language bindings in Shell Curl and nodejs! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```bash
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "x-access-token: --access token--"
```
> Make sure to replace `--access token--` with the JWT access token you recived as a response to the login request.

SkyPath uses JWT Tokens to allow access to the API. You can register a new user account to be able to exchange it for a JWT token at our [developer portal](https://yamasee.global).

SkyPath expects for the JWT access token to be included in all API requests to the server in a header that looks like the following:

`x-access-token: --access token--`

<aside class=notice>
You must replace <code>--access token--</code> with the token recived in the response to the login request.
</aside>

## Login

```bash
curl "https://server.yamasee-skypath.com/api/v2/auth/login"
```

> The above command returns JSON structured like this:

```json
{
   "token": "--JWT token format",
   "refresh_token" : "",
   "company_id":  ""
}
```

This endpoint authenticates a user and returns an access token, it's public and so do not need an access token

<aside class=warning>
You need to first call this method to be able to access any no public SkyPath functions.
</aside>

### HTTP Request 

`POST https://server.yamasee-skypath.com/api/v2/auth/login_key`

### Body Parameters

The call requires the following parameters in the POST body section

Parameter | Description
--------- | -----------
api_access_key | a unique API access key for the third party who's accesing the system 
user_id | a unique ID for the user doing the login
company_id | a unique ID for the airline company 

### Return JSON

The call returns the following JSON

Parameter | Description
--------- | -----------
token | a new JWT token valid for 3 hours usually 
refresh_token | a refresh token used to get additional valid access tokens
company_id | a unique ID for the airline company used by the user


## Validate Token

```bash
curl "https://server.yamasee-skypath.com/api/v2/auth/validate"
  -H "Authorization: --access-token--"
```
> The above command returns JSON structured like this:

```json
{
   "valid":      true / false,
   "expires":    "14543545435",
   "iat" : "145435455",
   "company_id": "id",
   "user_id":      "user_id"
}
```

This endpoint validates the current JWT token, can be used by a client to inspect 
the claims and expiry in a token

### HTTP Request (with ID)

`GET https://server.yamasee-skypath.com/api/v2/auth/valid`

### URL Parameters or Body parameters 

none



## Refresh Token

```

```bash
curl "https://server.yamasee-skypath.com/api/v2/auth/refresh"
  -H "Authorization: --refresh-token--"
```

> The above command returns JSON structured like this:

```json
{
   "token": "new JWT token",
   "refresh_token" : "empty or new refresh token",
}
```
This endpoint uses a refresh token to re-issue a new valid JWT token for the next 3 hours.

<aside class=warning>
Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.
</aside>

### HTTP Request (with ID)

`GET https://server.yamasee-skypath.com/api/v2/auth/refresh`

### URL Parameters or body parameters

none

# Globals

## Get All Aircraft types. 

Note that this API is public and you can call it without an auth token. 

```bash
curl "https://server.yamasee-skypath.com/api/v2/global/aircraft_types"
```

> The above command returns JSON structured like this:

```json
[
   {
      "id":          "737",
      "short_name":  "737",
      "long_name":   "Boeing 737",
   },
   {
      "id":         "A380",
      "short_name": "A380",
      "long_name":  "Airbus A380"
   }
]
```

This endpoint retrieves all aircraft types.

### HTTP Request

`GET https://server.yamasee-skypath.com/api/v2/global/aircraft_types`

### Query Parameters

none 

<aside class=success>
Remember — the system needs a valid aircraft type to be able to display correct turbulence severity levels.
</aside>

