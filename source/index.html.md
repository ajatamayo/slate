---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - countries

search: true
---

# Introduction

Welcome! This is a work in progress for what we could use for Omnisent's KYC process. This is based on AQWIRE's KYC process.

# Registration and Login

## Register

This endpoint registers a new user.

### HTTP Request

`POST /api/auth/register`

### Post data

Parameter | Required | Description
--------- | -------- | -----------
email | Yes | A valid email.
password | Yes | A password.
referrer | No | If the user is a referral of another user, specify the code here.

<aside class="notice">
A link to verify the email is sent to the user upon registration.
</aside>

> On success, this endpoint returns JSON structured like this:

```json
{
  "success": true,
  "message": "Please check your email for instructions."
}
```

## Login

This endpoint logs in a user. A JWT token is returned for further use in protected routes.

### HTTP Request

`POST /api/auth/login`

### Post data

Parameter | Required | Description
--------- | -------- | -----------
email | Yes | A valid email.
password | Yes | The password.
clientId | Yes | A unique string to identify the user's client. Sample: `5588f2a8babac226c6fff7fc0297ca298de00cb1`.

> On success, this endpoint returns JSON structured like this:

```json
{
  "success": true,
  "token_type": "Bearer",
  "clientId": "5588f2a8babac226c6fff7fc0297ca298de00cb1",
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7Il9pZCI6IjVkYWQ5NjcwMWFjOGUyNTE2NWEwMTAzNiIsInNjb3BlIjp7InVzZXJzIjpbInJlYWQiLCJ1cGRhdGUiXX19LCJpYXQiOjE1NzE2NzMxNTIsImV4cCI6MTU3MTY3Njc1Mn0.Tjk4He3WwVnwnK8cAXvgGXRu0Do57jxq88HwjofUw8s",
  "refreshToken": "3b48adeb5e2da344d45065f8da54d960b12a9ee04c436f41cf3436aef779e2b09698a3bef83c6e52"
}
```

## Refresh JWT Token

This endpoint refreshes a user's access token.

### HTTP Request

`POST /api/auth/token`

### Post data

Parameter | Required | Description
--------- | -------- | -----------
client_id | Yes | The client ID.
grant_type | Yes | Will only accept this value: `refresh_token`
refresh_token | Yes | The user's refresh token.

> On success, this endpoint returns JSON structured like this:

```json
{
  "success": true,
  "clientId": "5cc148dac7fc6ddbb311333f9ceca4c42e4cbe7a5588f2a8babac226c6fff7fc0297ca298de00cb1",
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7Il9pZCI6IjVkYWQ5NjcwMWFjOGUyNTE2NWEwMTAzNiIsInNjb3BlIjp7InVzZXJzIjpbInJlYWQiLCJ1cGRhdGUiXX19LCJpYXQiOjE1NzE2NzM3ODMsImV4cCI6MTU3MTY3NzM4M30.xpgc6alAjsIFXdZ6Jlb9_ML_T-mri1cEIIgQOOJms58"
}
```

# Authentication

<aside class="notice">
All endpoints, except <strong>Register</strong> and <strong>Login</strong>, require a token for authentication.
</aside>

JSON Web Tokens are used. To specify a token with a request, add the `Authorization` header with a string value of the format `Bearer xxxx.yyyy.zzzz`.

`xxxx.yyyy.zzzz` is the user's access token returned from the login endpoint.

# Profile

## Update profile

This endpoint updates a user's profile.

### HTTP Request

`PUT /api/users/profile`

### Request data

Parameter | Required | Description
--------- | -------- | -----------
firstName | Yes | The user's first name.
lastName | Yes | The user's last name.
citizenship | Yes | The user's country of citizenship. Check the end of this document for a list of valid countries.
residence | Yes | The user's country of residence. Check the end of this document for a list of valid countries.

> On success, this endpoint returns JSON structured like this:

```json
{
  "message": "User information updated.",
  "success": true,
  "user": {
    "__v": 0,
    "_id": "5dad96701ac8e25165a01036",
    "agreement": false,
    "authentication": null,
    "bountyUpdatedAt": "2019-10-21T15:52:33.268Z",
    "citizenship": "Philippines",
    "createdAt": "2019-10-21T11:28:48.348Z",
    "email": "aj@qwikwire.com",
    "emailVerified": true,
    "firstName": "Ariel",
    "forRecording": false,
    "id": "5dad96701ac8e25165a01036",
    "images": [],
    "isApproved": false,
    "isDenied": false,
    "isPending": false,
    "isRevised": false,
    "isSubmitted": false,
    "isUploaded": false,
    "lastName": "Tamayo",
    "residence": "Philippines",
    "updatedAt": "2019-10-21T16:08:51.480Z",
    "whitelistStatus": [
      "new"
    ]
  }
}
```

## Upload photo

<aside class="warning">
This section is still under construction.
</aside>

This endpoint allows for uploading of a photo.

### HTTP Request

`POST /api/users/upload-kyc`

### Request data

Parameter | Required | Description
--------- | -------- | -----------
files[] | Yes | A list of binary files.

> On success, this endpoint returns JSON structured like this:

```json
{
  "message": "Documents uploaded.",
  "success": true,
  "user": {
    "__v": 0,
    "_id": "5dad96701ac8e25165a01036",
    "agreement": false,
    "authentication": null,
    "bountyUpdatedAt": "2019-10-21T15:52:33.268Z",
    "citizenship": "Philippines",
    "createdAt": "2019-10-21T11:28:48.348Z",
    "email": "aj@qwikwire.com",
    "emailVerified": true,
    "firstName": "Ariel",
    "forRecording": false,
    "id": "5dad96701ac8e25165a01036",
    "images": [
      {
        "_id": "5dade3e81ac8e25165a01047",
        "bucket": "aqwirepublic-test",
        "key": "crowdsale/5dad96701ac8e25165a01036/1571677158652-id-license.png",
        "tag": "id"
      },
      {
        "_id": "5dade3e81ac8e25165a01046",
        "bucket": "aqwirepublic-test",
        "key": "crowdsale/5dad96701ac8e25165a01036/1571677158661-selfie-photo.jpg",
        "tag": "selfie"
      }
    ],
    "isApproved": false,
    "isDenied": false,
    "isPending": false,
    "isRevised": false,
    "isSubmitted": false,
    "isUploaded": true,
    "lastName": "Tamayo",
    "residence": "Philippines",
    "updatedAt": "2019-10-21T16:59:20.964Z",
    "whitelistStatus": [
      "new",
      "uploaded"
    ]
  }
}
```

## Get profile

This endpoint retrieve's the current logged in user's profile

### HTTP Request

`GET /api/users/profile`

> On success, this endpoint returns JSON structured like this:

```json
{
  "success": true,
  "user": {
    "scopes": {
      "users": [
        "read",
        "update"
      ]
    },
    "agreement": true,
    "whitelistStatus": [
      "new",
      "uploaded",
      "submitted",
      "pending"
    ],
    "emailVerified": true,
    "forRecording": false,
    "_id": "5dad96701ac8e25165a01036",
    "email": "aj+21@qwikwire.com",
    "images": [
      {
        "_id": "5dade3e81ac8e25165a01047",
        "tag": "id",
        "bucket": "aqwirepublic-test",
        "key": "crowdsale/5dad96701ac8e25165a01036/1571677158652-id-betty.png"
      },
      {
        "_id": "5dade3e81ac8e25165a01046",
        "tag": "selfie",
        "bucket": "aqwirepublic-test",
        "key": "crowdsale/5dad96701ac8e25165a01036/1571677158661-selfie-tyler.jpg"
      }
    ],
    "createdAt": "2019-10-21T11:28:48.348Z",
    "updatedAt": "2019-10-21T17:07:24.031Z",
    "__v": 0,
    "bountyUpdatedAt": "2019-10-21T15:52:33.268Z",
    "citizenship": "Philippines",
    "firstName": "Ariel",
    "lastName": "Tamayo",
    "residence": "Philippines",
    "estEthAmount": "5",
    "ethAddress": "0x1234567124123986129036109823610298361029",
    "authentication": null,
    "isSubmitted": true,
    "isUploaded": true,
    "isPending": true,
    "isApproved": false,
    "isDenied": false,
    "isRevised": false,
    "id": "5dad96701ac8e25165a01036"
  }
}
```

## Finalize profile for verification

This endpoint finalizes a user's profile and submits it for verification.

### HTTP Request

`POST /api/users/finalize-kyc`

### Post data

No post data required.

<aside class="notice">
Two emails are sent upon success: first, to the user informing them of this action and what to expect, second, to the administrator to notify them that there's a new user who submitted their profile for verification.
</aside>

> On success, this endpoint returns JSON structured like this:

```json
{
  "message": "User information updated.",
  "status": "pending",
  "success": true,
  "user": {
    "__v": 0,
    "_id": "5dad96701ac8e25165a01036",
    "agreement": true,
    "authentication": null,
    "bountyUpdatedAt": "2019-10-21T15:52:33.268Z",
    "citizenship": "Philippines",
    "createdAt": "2019-10-21T11:28:48.348Z",
    "email": "aj+21@qwikwire.com",
    "emailVerified": true,
    "estEthAmount": "5",
    "ethAddress": "0x1234567124123986129036109823610298361029",
    "firstName": "Ariel",
    "forRecording": false,
    "id": "5dad96701ac8e25165a01036",
    "images": [
      {
        "_id": "5dade3e81ac8e25165a01047",
        "bucket": "aqwirepublic-test",
        "key": "crowdsale/5dad96701ac8e25165a01036/1571677158652-id-license.png",
        "tag": "id"
      },
      {
        "_id": "5dade3e81ac8e25165a01046",
        "bucket": "aqwirepublic-test",
        "key": "crowdsale/5dad96701ac8e25165a01036/1571677158661-selfie-photo.jpg",
        "tag": "selfie"
      }
    ],
    "isApproved": false,
    "isDenied": false,
    "isPending": true,
    "isRevised": false,
    "isSubmitted": true,
    "isUploaded": true,
    "lastName": "Tamayo",
    "residence": "Philippines",
    "updatedAt": "2019-10-21T17:07:24.031Z",
    "whitelistStatus": [
      "new",
      "uploaded",
      "submitted",
      "pending"
    ]
  }
}
```