---
layout: enterprise2
page_title: "Organizations - API Docs - Terraform Enterprise"
sidebar_current: "docs-enterprise2-api-organizations"
---

# Organizations API

-> **Note**: These API endpoints are in beta and are subject to change.

The Organizations API is used to list, show, create, update, and destroy organizations.

## List Organizations

`GET /organizations`

Status  | Response                                        | Reason
--------|-------------------------------------------------|----------
[200][] | [JSON API document][] (`type: "organizations"`) | The request was successful
[404][] | [JSON API error object][]                       | Organization not found or user unauthorized to perform action

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/organizations
```

### Sample Response

```json
{
  "data": [
    {
      "id": "hashicorp",
      "type": "organizations",
      "attributes": {
        "name": "hashicorp",
        "created-at": "2017-09-07T14:34:40.492Z",
        "email": "user@example.com",
        "session-timeout": null,
        "session-remember": null,
        "collaborator-auth-policy": "password",
        "enterprise-plan": "pro",
        "permissions": {
          "can-update": true,
          "can-destroy": true,
          "can-create-team": true,
          "can-create-workspace": true,
          "can-update-oauth": true,
          "can-update-api-token": true,
          "can-update-sentinel": true,
          "can-traverse": true,
          "can-create-workspace-migration": true
        }
      },
      "links": {
        "self": "/api/v2/organizations/hashicorp"
      }
    }
  ]
}
```

## Show an Organization

`GET /organizations/:organization_name`

Parameter            | Description
---------------------|------------
`:organization_name` | The name of the organization to show

Status  | Response                                        | Reason
--------|-------------------------------------------------|----------
[200][] | [JSON API document][] (`type: "organizations"`) | The request was successful
[404][] | [JSON API error object][]                       | Organization not found or user unauthorized to perform action

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/organizations/hashicorp
```

### Sample Response

```json
{
  "data": {
    "id": "hashicorp",
    "type": "organizations",
    "attributes": {
      "name": "hashicorp",
      "created-at": "2017-09-07T14:34:40.492Z",
      "email": "user@example.com",
      "session-timeout": null,
      "session-remember": null,
      "collaborator-auth-policy": "password",
      "enterprise-plan": "pro",
      "permissions": {
        "can-update": true,
        "can-destroy": true,
        "can-create-team": true,
        "can-create-workspace": true,
        "can-update-oauth": true,
        "can-update-api-token": true,
        "can-update-sentinel": true,
        "can-traverse": true,
        "can-create-workspace-migration": true
      }
    },
    "links": {
      "self": "/api/v2/organizations/hashicorp"
    }
  }
}
```

## Create an Organization

`POST /organizations`

Status  | Response                                        | Reason
--------|-------------------------------------------------|----------
[201][] | [JSON API document][] (`type: "organizations"`) | The organization was successfully created
[404][] | [JSON API error object][]                       | Organization not found or user unauthorized to perform action
[422][] | [JSON API error object][]                       | Malformed request body (missing attributes, wrong types, etc.)

[201]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/201
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[422]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Request Body

This POST endpoint requires a JSON object with the following properties as a request payload.

Properties without a default value are required.

Key path                    | Type   | Default | Description
----------------------------|--------|---------|------------
`data.type`                 | string |         | Must be `"organizations"`
`data.attributes.name`      | string |         | Name of the organization
`data.attributes.email`     | string |         | Admin email address

### Sample Payload

```json
{
  "data": {
    "type": "organizations",
    "attributes": {
      "name": "hashicorp",
      "email": "user@example.com"
    }
  }
}
```

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request POST \
  --data @payload.json \
  https://app.terraform.io/api/v2/organizations
```

### Sample Response

```json
{
  "data": {
    "id": "hashicorp",
    "type": "organizations",
    "attributes": {
      "name": "hashicorp",
      "created-at": "2017-09-07T14:34:40.492Z",
      "email": "user@example.com",
      "session-timeout": null,
      "session-remember": null,
      "collaborator-auth-policy": "password",
      "enterprise-plan": "pro",
      "permissions": {
        "can-update": true,
        "can-destroy": true,
        "can-create-team": true,
        "can-create-workspace": true,
        "can-update-oauth": true,
        "can-update-api-token": true,
        "can-update-sentinel": true,
        "can-traverse": true,
        "can-create-workspace-migration": true
      }
    },
    "links": {
      "self": "/api/v2/organizations/hashicorp"
    }
  }
}
```

## Update an Organization

`PATCH /organizations/:organization_name`

Parameter            | Description
---------------------|------------
`:organization_name` | The name of the organization to update

Status  | Response                                        | Reason
--------|-------------------------------------------------|----------
[200][] | [JSON API document][] (`type: "organizations"`) | The organization was successfully updated
[404][] | [JSON API error object][]                       | Organization not found or user unauthorized to perform action
[422][] | [JSON API error object][]                       | Malformed request body (missing attributes, wrong types, etc.)

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[422]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Request Body

This PATCH endpoint requires a JSON object with the following properties as a request payload.

Key path                                   | Type    | Default  | Description
-------------------------------------------|---------|----------|------------
`data.type`                                | string  |          | Must be `"organizations"`
`data.attributes.name`                     | string  |          | Name of the organization
`data.attributes.email`                    | string  |          | Admin email address
`data.attributes.session-timeout`          | integer |    20160 | Session timeout after inactivity (minutes)
`data.attributes.session-remember`         | integer |    20160 | Session expiration (minutes)
`data.attributes.collaborator-auth-policy` | string  | password | Authentication policy (`password` or `two_factor_mandatory`)

### Sample Payload

```json
{
  "data": {
    "type": "organizations",
    "attributes": {
      "email": "admin@example.com"
    }
  }
}
```

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request PATCH \
  --data @payload.json \
  https://app.terraform.io/api/v2/organizations/hashicorp
```

### Sample Response

```json
{
  "data": {
    "id": "hashicorp",
    "type": "organizations",
    "attributes": {
      "name": "hashicorp",
      "created-at": "2017-09-07T14:34:40.492Z",
      "email": "admin@example.com",
      "session-timeout": null,
      "session-remember": null,
      "collaborator-auth-policy": "password",
      "enterprise-plan": "pro",
      "permissions": {
        "can-update": true,
        "can-destroy": true,
        "can-create-team": true,
        "can-create-workspace": true,
        "can-update-oauth": true,
        "can-update-api-token": true,
        "can-update-sentinel": true,
        "can-traverse": true,
        "can-create-workspace-migration": true
      }
    },
    "links": {
      "self": "/api/v2/organizations/hashicorp"
    }
  }
}
```

## Destroy an Organization

`DELETE /organizations/:organization_name`

Parameter            | Description
---------------------|------------
`:organization_name` | The name of the organization to destroy

Status  | Response                                        | Reason
--------|-------------------------------------------------|----------
[204][] |                                                 | The organization was successfully destroyed
[404][] | [JSON API error object][]                       | Organization not found or user unauthorized to perform action

[204]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request DELETE \
  https://app.terraform.io/api/v2/organizations/hashicorp
```

### Sample Response

The response body will be empty if successful.
