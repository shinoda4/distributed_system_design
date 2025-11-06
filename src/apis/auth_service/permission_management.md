# Permission Management

<!-- toc -->

## Index

List permissions.

### URL

`api/permissions/`

### Method

`get`

### Request body

#### Optional

_limit_: `number`

_offset_: `number`

_search_: `string`

_[field]\_\_[lookup]_: `string`

### Fields

_id_: `number`

_permission_code_: `string`

_permission_name_: `string`

_description_: `string`

### Lookup

_exact_: `string`

_iexact_: `string`

_contains_: `string`

_icontains_: `string`

_startswith_: `string`

_istartswith_: `string`

_endswith_: `string`

_iendswith_: `string`

_in_: `string`

_gt_: `number`

_gte_: `number`

_lt_: `number`

_lte_: `number`

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
      "id": 1,
      "permission_code": "users.read",
      "permission_name": "Read users",
      "description": "Can read user list"
    }
  ]
}
```

## Create

### URL

`api/permissions/`

### Method

`post`

### Request body

#### Required

_permission_code_: `string`

_permission_name_: `string`

#### Optional

_description_: `string`

#### Json body

```json
{
  "permission_code": "roles.assign",
  "permission_name": "Assign roles",
  "description": "Can assign roles to users"
}
```

### Response

**code**:

`HTTP_201_CREATED`

**body**:

```json
{
  "id": 5,
  "permission_code": "roles.assign",
  "permission_name": "Assign roles",
  "description": "Can assign roles to users"
}
```

**code**:

`HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "permission_code": ["This field is required."]
}
```

## Retrieve

### URL

`api/permissions/{id}/`

### Method

`get`

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
  "id": 1,
  "permission_code": "users.read",
  "permission_name": "Read users",
  "description": "Can read user list"
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

`{{baseURL}}/api/permissions/{id}/`

### Method

`put`

### Request body

#### Required

_permission_code_: `string`

_permission_name_: `string`

_description_: `string`

#### Json body

```json
{
  "permission_code": "users.read",
  "permission_name": "Read users",
  "description": "Updated description"
}
```

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
  "id": 1,
  "permission_code": "users.read",
  "permission_name": "Read users",
  "description": "Updated description"
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

`HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "permission_code": ["This field is required."]
}
```

### Method

`patch`

### Request body

#### Optional

_permission_code_: `string`

_permission_name_: `string`

_description_: `string`

#### Request body example

```json
{
  "description": "Partially updated description"
}
```

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
  "id": 1,
  "permission_code": "users.read",
  "permission_name": "Read users",
  "description": "Partially updated description"
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

`api/permissions/{id}/`

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
