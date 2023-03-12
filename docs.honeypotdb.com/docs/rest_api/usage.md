# REST API Usage

To ease the process of interfacing with HoneypotDB programmatically, all of our capabilities are accessible through our REST API at [api.honeypotdb.com](https://api.honeypotdb.com).

Our swagger documentation for all endpoints can be found at the [subdomain's root](https://api.honeypotdb.com), and we try our best to conform to the OpenAPI and REST APi standards as much as we can.

## Authentication

Our REST API will require authentication before you can use it, this is either in the form of a JWT or an API Key.

JWTs are used only by our authentication endpoints, and allow you to manage your account, organization and your API keys. Once you have created an API key, you can then use this API key as authentication for all other endpoints.

Each endpoint also operation requires a specific permission. For example, the ability to read and create monitoring rules are separate permissions.

Your user account will have a list of permissions assigned to it that you can use from creation.For a normal user, this will include every permission you need to use the platform. Users that require access to sections like billing will have additional permissions to allow this.

### API Keys

API Keys are our primary form of authentication when accessing the REST API and are managed via your account configuration (either via the web UI or Auth API). 

When creating your API keys you can give it a meaningful description, set an expiration date (defaults to 1 month) and assign a list of permissions to it. These assigned permissions dictate what that specific API key can do. Note that you need to have the permission assigned to your own user before tou can assign it to one of your API keys.

Once an API Key has been created you'll be shown the key **ONLY ONCE**, so make sure you store it in a safe place.

API keys consist of a 6-byte prefix and a 32-byte body. The key's prefix is shown on the API Keys management page and used as a handy reference so you know which key is which. The key's body is the secret bit and can't be recovered if you lose it.

A valid API Keys must be passed in a header named `X-API-Key` when accessing an endpoint, make sure you pass both the prefix and body separated by a period `.`.

Example API Key in `X-API-Key` header:

```text
> X-API-Key: TKblhGT.EuYwJ5-XE46tVMXReF6H_spY7wcYwKjgkRWvZ_aQFME
```


### JWTs

!!! note "These are not the tokens you're looking for"
    JWTs are only used by the UI and auth API to manage your account and create API keys, which should be done via the web UI anyway. You probably want to look at that API Keys section instead.

JWTs (JSON Web Tokens) are also used to authenticate a user accessing the platform. These are used under the hood when you use our web UI to navigate the platform.

You may also use JWTs on certain API endpoints by passing a valid JWT beraer token in the Authorization header (the usual way).

Example JWT in `Authorization` header:

```text
> Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

## Quotas and Rate Limiting

As much as we'd like to `tail -f /var/logs/nginx/access.log` and watch the requests fly in, servers are expensive.  To combat this, we impose a rate limits to keep our servers running smoothly and usage quotas to keep our commercial team happy.

### Rate Limiting

We impose a global rate limit of 100 requests per minute, per API key. If you exceed this limit you'll start to receive HTTP code `429` as your response.

If this poses an issue for you, we encourage you to take a look at implementing some form of short lived cache (Like REDIS) to reduce the amount of requests you're sending. Contact our support team if you need further assistance.


### Usage Quotas

Your usage quota will depend on the type of account you or your organization has, and can be viewed on your account management page.

## Responses

All responses from our REST API will contain a standardized response body in JSON format, coupled with an associated HTTP code.

### Body

The response object contains a `data` key which lists results returned by the API. This is the main key where results will be returned from the API.

A `status`, `error` and `message` key are provided to show the request's outcome along with a `meta` key to provide meta information about the request.

Example API response body:

```json
{
  "data": [
    {
      "added": "2022-11-11T12:36:07",
      "id": "598f5fcf-aea6-4593-99e7-c27945b1b6a6",
      "indicator": "175.21.34.56",
      "modified": "2022-11-11T12:36:07",
      "score": 4366,
      "type": "HOSTNAME"
    },
    {
      "added": "2022-11-11T12:47:05",
      "id": "e17216a3-d9dc-4500-9d28-5197fdc75906",
      "indicator": "175.21.34.76",
      "modified": "2022-11-11T12:47:05",
      "score": 10,
      "type": "IPV4_ADDRESS"
    }
  ],
  "error": 0,
  "message": "Success",
  "meta": {
    "items": 2,
    "page": 1,
    "pages": 1
  },
  "success": true
}

```

### HTTP Codes

The API will response with a specific HTTP code depending on the outcome of the request, these are:

| HTTP Code | Meaning      | Description                                       |
|-----------|--------------|---------------------------------------------------|
| 200       | Success      | The request was successful                        |
| 201       | Created      | The object was created successfully               |
| 400       | Bad Request  | Your request was malformed, make sure all your parameters are correct.
| 401       | Unauthorized | You don't have authorization to use this endpoint, check your API key is valid and its permissions  |
| 403       | Forbidden    | Your request was forbidden, it probably looks like it was doing something dodgy.
| 404       | Not found    | The requested resource was not found                   |
| 5xx       | Server error | Something went wrong on our end, if the issue keeps occurring please contact support |