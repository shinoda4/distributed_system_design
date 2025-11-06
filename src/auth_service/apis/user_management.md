# User Management

<!-- toc -->

## Index

index users.

### URL

`api/users/`

### Method

`get`

### Request body

#### Optional

*limit*: `number`

*offset*: `number`

*search*: `string`

*[field]__[lookup]*: `string`

### Fields

*username*: `string`

*email*: `string`

*phone_number*: `string`

### Lookup

*exact*: `string`

*iexact*: `string`

*contains*: `string`

*icontains*: `string`

*startswith*: `string`

*istartswith*: `string`

*endswith*: `string`

*iendswith*: `string`

*in*: `string`

*gt*: `number`

*gte*: `number`

*lt*: `number`

*lte*: `number`

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 8,
            "roles": [],
            "last_login": "2025-11-06T07:37:34.364302Z",
            "username": "mike",
            "first_name": "",
            "last_name": "",
            "is_active": true,
            "date_joined": "2025-11-05T14:21:05.963153Z",
            "phone_number": "1234567890",
            "email": "hello@world.com"
        }
    ]
}
```

## Create

### URL

`api/users/`

### Method

`post`

### Request body

#### Required

*username*: `string`

*email*: `string`

#### Json body

```json
{
    "username": "jane_doe",
    "email": "hello@world.com"
}
```

#### Optional

### Response

**code**:

`HTTP_201_CREATED`

**body**:

```json
{
    "id": 9,
    "roles": [],
    "last_login": null,
    "username": "jane_doe",
    "first_name": "",
    "last_name": "",
    "is_active": true,
    "date_joined": "2025-11-06T08:00:00.000000Z",
    "phone_number": null,
    "email": "jane_doe@example.com"
}
```

**code**:

`HTTP_400_BAD_REQUEST`

**body**:

```json
{
    "username": [
        "A user with that username already exists."
    ],
    "email": [
        "user with this email already exists."
    ]
}
```

## Retrieve

### URL

`api/users/{id}/`

### Method

`get`

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
    "id": 8,
    "roles": [],
    "last_login": "2025-11-06T07:37:34.364302Z",
    "username": "mike",
    "first_name": "",
    "last_name": "",
    "is_active": true,
    "date_joined": "2025-11-05T14:21:05.963153Z",
    "phone_number": "1234567890",
    "email": "hello@world.com"
}
```

**code**:

`HTTP_404_NOT_FOUND`

**body**:

```json
{
    "detail": "Not found."
}
```

## Update

### URL

`{{baseURL}}/api/users/{id}/`

### Method

`put`

### Request body

#### Required

*username*: `string`

*email*: `string`

####  Json body

```json
{
    "username": "new",
    "email": "new@new.com"
}
```

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
    "id": 9,
    "roles": [],
    "last_login": null,
    "username": "new",
    "first_name": "",
    "last_name": "",
    "is_active": true,
    "date_joined": "2025-11-06T09:52:19.997422Z",
    "phone_number": null,
    "email": "new@new.com"
}
```

**code**:

`HTTP_404_NOT_FOUND`

**body**:

```json
{
    "detail": "Not found."
}
```

**code**:

``HTTP_400_BAD_REQUEST`

**body**:

```json
{
    "username": [
        "This field is required."
    ],
    "email": [
        "This field is required."
    ]
}
```

### Method

`patch`

### Request body

#### Optional

*username*: `string`

*email*: `string`

*phone_number*: `string`

*first_name*: `string`

*last_name*: `string`

### Request body

```json
{
    "first_name": "shinoda"
}
```

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
    "id": 9,
    "roles": [],
    "last_login": null,
    "username": "new",
    "first_name": "",
    "last_name": "",
    "is_active": true,
    "date_joined": "2025-11-06T09:52:19.997422Z",
    "phone_number": null,
    "email": "new@new.com"
}
```

**code**: `HTTP_404_NOT_FOUND`

**body**:

```json
{
    "detail": "Not found."
}
```

## Destroy

### URL

`api/users/{id}/`

### Method

`delete`

### Response

**code**:

`HTTP_204_NO_CONTENT`

**body**:

(no content)

**code**:

`HTTP_404_NOT_FOUND`

**body**:

```json
{
    "detail": "Not found."
}
```
