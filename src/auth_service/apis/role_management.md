# Role Management

<!-- toc -->

## Index

List roles.

### URL

`api/roles/`

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

_role_name_: `string`

_description_: `string`

_permissions_: `array` of permission objects

Permission object fields:

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
      "id": 3,
      "role_name": "admin",
      "description": "Administrator role",
      "permissions": [
        {
          "id": 1,
          "permission_code": "users.read",
          "permission_name": "Read users",
          "description": "Can read user list"
        }
      ]
    }
  ]
}
```

## Create

### URL

`api/roles/`

### Method

`post`

### Request body

#### Required

_role_name_: `string`

#### Optional

_description_: `string`

> Note: in the current serializer `permissions` is read-only (nested). Assigning permissions should be done via a dedicated assign endpoint or by updating the role via the admin/other API that accepts permission ids if implemented.

#### Json body

```json
{
  "role_name": "editor",
  "description": "Can edit content"
}
```

### Response

**code**:

`HTTP_201_CREATED`

**body**:

```json
{
  "id": 4,
  "role_name": "editor",
  "description": "Can edit content",
  "permissions": []
}
```

**code**:

`HTTP_400_BAD_REQUEST`

**body**:

```json
{
  "role_name": ["This field is required."]
}
```

## Retrieve

### URL

`api/roles/{id}/`

### Method

`get`

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
  "id": 3,
  "role_name": "admin",
  "description": "Administrator role",
  "permissions": [
    {
      "id": 1,
      "permission_code": "users.read",
      "permission_name": "Read users",
      "description": "Can read user list"
    }
  ]
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

`{{baseURL}}/api/roles/{id}/`

### Method

`put`

### Request body

#### Required

_role_name_: `string`

_description_: `string`

#### Json body

```json
{
  "role_name": "new_name",
  "description": "Updated description"
}
```

### Response

**code**:

`HTTP_200_OK`

**body**:

```json
{
  "id": 4,
  "role_name": "new_name",
  "description": "Updated description",
  "permissions": []
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
  "role_name": ["This field is required."]
}
```

### Method

`patch`

### Request body

#### Optional

_role_name_: `string`

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
  "id": 4,
  "role_name": "new_name",
  "description": "Partially updated description",
  "permissions": []
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

`api/roles/{id}/`

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
