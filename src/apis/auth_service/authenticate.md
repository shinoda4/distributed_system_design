# Authenticate APIs

<!-- toc -->

## Registration

After user created successfully, `joser` will send an email that includes activation url to user email.

### URL

`api/auth/users/`

### Request Method

`post`

### Request body

#### Required

_username_: `string`

_password_: `string`

_re_password_: `string`

_email_: `string`

_phone_number_: `string`

<!-- #### Optional -->

#### Json body

```json
{
  "username": "mike",
  "password": "passwd123",
  "re_password": "passwd123",
  "email": "hello@world.com",
  "phone_number": "1234567890"
}
```

### Response

**code**: `HTTP_201_CREATED`

**body**:

```json
{
  "email": "hello@world.com",
  "username": "mike",
  "id": 1
}
```

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
    "username": [
        "A user with that username already exists."
    ],
    // Required fields...
    "password": ...,
    "re_password": ...,
    ...
}
```

## Activatation

After created user, djoser will send an email which include `uid` and `token` to user email that provided in creation paramters. Like this `http://127.0.0.1:8000/activate/Mzk/cysm5f-ef12575f6699ca8694221dc97a3da11e`, so refer to this `activate/{uid}/{token}`, the `uid` is `Mzk`, and `token` is `cysm5f-ef12575f6699ca8694221dc97a3da11e`.

### URL

`auth/users/activation/`

### Method

`post`

### Request body

#### Required

_uid_: `string`

_token_: `string`

#### Json body

```json
{
  "uid": "Mzk",
  "token": "cysm5f-ef12575f6699ca8694221dc97a3da11e"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to activate.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "uid": ["Invalid user id or user doesn't exist."],
  "token": ["Invalid token for given user."]
}
```

**code**: `HTTP_403_FORBIDDEN`

Already activated.

**body**:

```json
{
  "detail": "Stale token for given user."
}
```

## User Resend Activation E-mail

Use this endpoint to re-send the activation e-mail. Note that no e-mail would be sent if the user is already active or if they don’t have a usable password. Also if the sending of activation e-mails is disabled in settings, this call will result in `HTTP_400_BAD_REQUEST`.

### URL

`api/auth/users/resend_activation/`

### Method

`post`

### Request body

#### Required

_email_: `string`

#### Json body

```json
{
  "email": "hello@world.com"
}
```

### Response

**code**:

`HTTP_204_NO_CONTENT`

Success to resend activation email.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "email": ["Enter a valid email address."]
}
```

## User Login (JWT Create)

Authenticate user and return token.

### URL

`api/auth/jwt/create/`

### Method

`post`

### Request body

#### Required

_username_: `string`

_password_: `string`

#### Json body

```json
{
  "username": "mike",
  "password": "passwd123"
}
```

### Response

**code**: `HTTP_200_OK`

**body**:

```json
{
  "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTc2MjQzNDQ3NiwiaWF0IjoxNzYyMzQ4MDc2LCJqdGkiOiI2NjlkODdkNGFjZmQ0Zjg2ODc1MDM3NzFkMmE2ZjQ2ZCIsInVzZXJfaWQiOiI3Iiwicm9sZXMiOltdLCJwZXJtaXNzaW9ucyI6W10sInVzZXJuYW1lIjoibWlrZSJ9.M_M1-QReSTHux7T_iVvidCEMY8MyAbCZ_t-82W2uaUs",
  "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzYyMzUxMDc2LCJpYXQiOjE3NjIzNDgwNzYsImp0aSI6IjY0NTZhYjAyNmZlMzQ5MWZiNWFiOGFhNmNkOTYzMDVjIiwidXNlcl9pZCI6IjciLCJyb2xlcyI6W10sInBlcm1pc3Npb25zIjpbXSwidXNlcm5hbWUiOiJtaWtlIn0.wVwm5N7Apm33n2NxBruXzeTFqjCzuplLMKmRPSJTk0w"
}
```

**code**: `HTTP_401_UNAUTHORIZED`

non_field_errors

**body**:

```json
{
  "password": ["This field is required."]
}
```

## JWT Refresh

Refresh access token.

### URL

`api/auth/jwt/refresh/`

### Method

`post`

### Request body

#### Required

_refresh_: `string`

#### Json body

```json
{
  "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTc2MjQzNjUwOCwiaWF0IjoxNzYyMzUwMTA4LCJqdGkiOiJhNmE3MDVlY2ZjNWE0ZWJkOWM3ODFlZGFmMGFjNWM0MCIsInVzZXJfaWQiOiI3In0.WTQ9QI_EpleiiaNAoAdwXAp2RF0URKFa_ahDaYQYNy0"
}
```

### Response

**code**: `HTTP_200_OK`

**body**:

```json
{
  "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzYyMzUzMTMxLCJpYXQiOjE3NjIzNTAxMzEsImp0aSI6ImI3NmQ3MzY0MTQ3OTQ3Y2JiZTZlZjU5MTJmYjVmYzJjIiwidXNlcl9pZCI6IjcifQ.hgy3Zm7p3WETLdAoNX7smf7uAmZRMih_RFZNoe1j4Kg"
}
```

**code**: `HTTP_401_UNAUTHORIZED`

non_field_errors

**body**:

```json
{
  "refresh": ["This field is required."]
}
```

## JWT Verify

Verify access token.

### URL

`api/auth/jwt/verify/`

### Method

`post`

### Request body

#### Required

_token_: `string`

#### Json body

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTc2MjI1MzE0NSwiaWF0IjoxNzYyMTY2NzQ1LCJqdGkiOiI1MjM1NGU2ZDkyMWU0NjNjYjgyNDRiMTNmMGRjZjAzMiIsInVzZXJfaWQiOiIxIn0.Ija21SaYGw99NEHFKtZFy5mSh0uMpUbuXoSNchm1-7I"
}
```

### Response

**code**: `HTTP_200_OK`

**body**:

```json
{}
```

**code**: `HTTP_401_UNAUTHORIZED`

**body**:

Token is expired.

```json
{
  "detail": "Token is expired",
  "code": "token_not_valid"
}
```

**code**: `HTTP_400_BAD_REQUEST`

non_field_errors

```json
{
  "token": ["This field is required."]
}
```

## User

Get the currently logged in user information.

### URL

`api/auth/users/me/`

### Method

`get`

### Response

**code**: `HTTP_200_OK`

**body**:

```json
{
  "email": "hello@world.com",
  "username": "mike",
  "id": 1
}
```

### Method

`put` or `patch` to update user info.

Note that if user changed his email by `put` or `patch`, the user will be set to inactive and an activation email will be sent to the new email address. User should reactivate his account via the new email address.

### Response

**code**: `HTTP_200_OK`

**body**:

```json
{
  "id": 7,
  "roles": [],
  "last_login": null,
  "username": "mike",
  "first_name": "",
  "last_name": "",
  "is_active": true,
  "date_joined": "2025-11-05T12:45:00.628205Z",
  "phone_number": "1234567890",
  "email": "hello@world.com"
}
```

**code**: `HTTP_400_BAD_REQUEST`

non_field_errors

**body**:

```json
{
  "email": ["Enter a valid email address."]
}
```

## User Delete

Delete the currently logged in user.

### URL

`api/auth/users/me/`

### Method

`delete`

### Request body

#### Required

_current_password_: `string`

#### Json body

```json
{
  "current_password": "passwd123"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to delete user.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "current_password": ["This field is required."]
}
```

## Set Username

### URL

`{{baseURL}}/api/auth/users/set_username/`

### Method

`post`

### Request body

#### Required

_new_username_: `string`

_current_password_: `string`

#### Json body

```json
{
  "new_username": "mikeshinoda",
  "current_password": "passwd123"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to set new username.

**code**: `HTTP_400_BAD_REQUEST`

non_field_errors

```json
{
  "current_password": ["This field is required."],
  "new_username": ["This field is required."]
}
```

## Reset Username

### URL

`api/auth/users/reset_username/`

### Method

`post`

### Request body

#### Required

_email_: `string`

#### Json body

```json
{
  "email": "hello@world.com"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to send reset username email.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "email": ["Enter a valid email address."]
}
```

## Reset Username Confirmation

Assuming that user has received the reset username email, he can use the `uid` and `token` in the email to reset his username.

`<a href="http://127.0.0.1:8000/auth/username-reset/OA/cystj8-e5be9cfa6c63528e37adf22ebf9f2f9a">http://127.0.0.1:8000/auth/username-reset/OA/cystj8-e5be9cfa6c63528e37adf22ebf9f2f9a</a>`

So refer to this `username-reset/{uid}/{token}`, the `uid` is `OA`, and `token` is `cystj8-e5be9cfa6c63528e37adf22ebf9f2f9a`.

### URL

`api/auth/users/reset_username_confirm/`

### Method

`post`

### Request body

#### Required

_uid_: `string`

_token_: `string`

_new_username_: `string`

_re_new_username_: `string`

#### Json body

```json
{
  "uid": "OA",
  "token": "cystj8-e5be9cfa6c63528e37adf22ebf9f2f9a",
  "new_username": "mikeshinoda",
  "re_new_username": "mikeshinoda"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to reset username.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "uid": ["Invalid user id or user doesn't exist."],
  "token": ["Invalid token for given user."],
  "new_username": ["This field is required."],
  // "new_username": [
  // "A user with that username already exists."
  // ],
  "re_new_username": ["This field is required."]
}
```

## Set Password

### URL

`{{baseURL}}/api/auth/users/set_password/`

### Method

`post`

### Request body

#### Required

_new_password_: `string`

_re_new_password_: `string`

_current_password_: `string`

#### Json body

```json
{
  "new_password": "newpasswd123",
  "re_new_password": "newpasswd123",
  "current_password": "passwd123"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to set new password.

**code**: `HTTP_400_BAD_REQUEST`

non_field_errors

```json
{
  "new_password": ["This field is required."],
  "re_new_password": ["This field is required."],
  "current_password": ["This field is required."]
}
```

## Reset Password

Use this endpoint to send email to user with password reset link. You have to setup `PASSWORD_RESET_CONFIRM_URL`.

### URL

`api/auth/users/reset_password/`

### Method

`post`

### Request body

#### Required

_email_: `string`

#### Json body

```json
{
  "email": "hello@world.com"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to send reset password email.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "email": ["Enter a valid email address."]
}
```

## Reset Password Confirmation

Assuming that user has received the reset password email, he can use the `uid` and `token` in the email to reset his password.

`<a href="http://127.0.0.1:8000/auth/password-reset/OA/cyu52z-f838db4a34f5a9a5fd5008191381405c">`

So refer to this `password-reset/{uid}/{token}`, the `uid` is `OA`, and `token` is `cyu52z-f838db4a34f5a9a5fd5008191381405c`.

### URL

`api/auth/users/reset_password_confirm/`

### Method

`post`

### Request body

#### Required

_uid_: `string`

_token_: `string`

_new_password_: `string`

_re_new_password_: `string`

#### Json body

```json
{
  "uid": "OA",
  "token": "cyu52z-f838db4a34f5a9a5fd5008191381405c",
  "new_password": "newpasswd123",
  "re_new_password": "newpasswd123"
}
```

### Response

**code**: `HTTP_204_NO_CONTENT`

Success to reset password.

**code**: `HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "uid": ["Invalid user id or user doesn't exist."],
  "token": ["Invalid token for given user."],
  "new_password": ["This field is required."],
  "re_new_password": ["This field is required."]
}
```
