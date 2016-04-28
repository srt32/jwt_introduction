# JWT Web Tokens Overview

## Introduction

### Use cases
* Authentication: This is the most common scenario for using JWT. Once the user
is logged in, each subsequent request will include the JWT, allowing the user
to access routes, services, and resources that are permitted with that token.
Single Sign On is a feature that widely uses JWT nowadays, because of its
small overhead and its ability to be easily used across different domains.

* Information Exchange: JSON Web Tokens are a good way of securely transmitting
information between parties, because as they can be signed, for example using
public/private key pairs, you can be sure that the senders are who they say
they are. Additionally, as the signature is calculated using the header and
the payload, you can also verify that the content has not been tampered with.

Source: https://jwt.io/introduction/


### Benefits

* Compact (compated to XML usage in SAML)
* easy to sign, easy to parse
* Self-contained
* Based on a standard (used by other APIs such as [Box](https://developers.box.com/) and [Auth0](https://auth0.com/docs)): https://tools.ietf.org/html/rfc7519


### Components
* Header: `typ` and `alg` (required)
* Payload: reserved claims (such as `iss`) and public claims (such as `user`)
* Signature: encoded header and payload signed with a secret (held by sender and receiver)
* Secret

Example header:

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Example payload:

```
{
  "sub": "1234567890",
  "user_id": "0a2054a3-55d1-48d6-b95b-be1042034146",
}
```

final encoded token looks like `[encoded header].[encoded payload].[signature]`

An example signed token:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6IjMyZmEzMWY1LTBkYTAtNDE0Yi04NGNmLTdiYWE0ZDc2YTdjMiIsImlhdCI6MTQ2MTI1NTE2MiwiZXhwIjoxNDYxMjczMTYyfQ.b3bQBhLqBnxTaO6EevMykOk-Xg9EmBV9m4C7RHQhFf8
```

### For usage in authentication
#### Example: log in with username and password
![JWT Authentication Steps](https://cdn.auth0.com/content/jwt/jwt-diagram.png)

### For usage in information exchange:
#### Example: passing around the permissions of a user

```
{
  "sub": "1234567890",
  "name": "John Doe Deer",
  "admin": true,
  "roles": ["buyer", "supplier"]
}
```

## Other Resources

* Great resource for interactively generating and validating tokens: https://jwt.io/
* Example libraries: https://www.npmjs.com/package/express-jwt, https://github.com/jpadilla/pyjwt
