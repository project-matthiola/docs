# API

The REST API for traders and brokers.

## Authentication

Matthiola uses [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token), or JSON Web Token for authentication. Traders should send a request to sign a contract with the broker, then the broker will return the access token.

| Code | Name | Description | Value |
| ---- | ---- | ----------- | ----- |
| sub | Subject | Identifies the subject of the JWT. | Firm ID |
| aud | Audience | Identifies the recipients that the JWT is intended for. | Firm Name |
| exp | Expiration time | Identifies the expiration time on or after which the JWT must not be accepted for processing. The value should be in NumericDate format. | Defined according to the request |
| iat | Issued at | Identifies the time at which the JWT was issued. | The current time |
| jti | JWT ID | Case sensitive unique identifier of the token even among different issuers. | UUID |

### Sign a Contract

> Request

```json
{
  "firm_name": "Matthiola",
  "expires_at": "2018-08-22T16:52:23Z"
}
```

> Response

```json
{
  "data": {
    "firm_id": 1,
    "firm_name": "Matthiola",
    "credit": 100,
    "token": "QWxhZGRpbjpvcGVuIHNlc2FtZQ=="
  }
}
```

#### HTTP REQUEST

`POST /server/api/v1/auth`
