---
layout: enterprise2
page_title: "Private Terraform Settings - API Docs - Terraform Enterprise"
sidebar_current: "docs-enterprise2-api-private-terraform-settings"
---

# Private Terraform Settings API

-> **Note**: These API endpoints are in beta and are subject to change. Additionally, these endpoints are only available in Private Terraform instances and only accessible by site administrators.

## List General Settings
`GET /api/v2/admin/settings/general`

-> **Note:** This endpoint cannot be accessed with [organization tokens](../users-teams-organizations/service-accounts.html#organization-service-accounts). You must access it with a [user token](../users-teams-organizations/users.html#api-tokens) which has the `site-admins` permission.

Status  | Response                                         | Reason
--------|--------------------------------------------------|-------
[200][] | Array of [JSON API document][]s (`type: "settings"`) | Successfully listed General settings
[404][] | [JSON API error object][]                    | User unauthorized to perform action

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/admin/settings/general
```

### Sample Response

```json
{
  "data": {
    "id": "general-settings",
    "type": "settings",
    "attributes": {
      "support_email_address": "support@example.com",
      "security_email_address": "security@example.com",
      "limit_user_org_creation": true
    }
  }
}
```

## Update General Settings
`PATCH /api/v2/admin/settings/general`

-> **Note:** This endpoint cannot be accessed with [organization tokens](../users-teams-organizations/service-accounts.html#organization-service-accounts). You must access it with a [user token](../users-teams-organizations/users.html#api-tokens) which has the `site-admins` permission.

Status  | Response                                     | Reason
--------|----------------------------------------------|----------
[200][] | [JSON API document][] (`type: "settings"`) | Successfully updated the General settings
[404][] | [JSON API error object][]                    | User unauthorized to perform action
[422][] | [JSON API error object][]                    | Malformed request body (missing attributes, wrong types, etc.)

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[422]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Request Body

This PATCH endpoint requires a JSON object with the following properties as a request payload.

Key path                    | Type   | Default | Description
----------------------------|--------|---------|------------
`data.attributes.support_email_address`  | string   | `"support@hashicorp.com"` | The support address for outgoing emails.
`data.attributes.security_email_address` | string   | `"security@hashicorp.com"` | The security address for outgoing emails.
`data.attributes.limit_user_org_creation`| bool     | `true` | Determines whether users who are not `site-admins` will be able to create new organizations.

### Sample Payload

```json
{
  "data": {
    "attributes": {
      "support_email_address": "support@example.com",
      "security_email_address": "security@example.com",
      "limit_user_org_creation": true
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
  https://app.terraform.io/api/v2/admin/settings/general
```

### Sample Response

```json
{
  "data": {
    "id":"general-settings",
    "type":"settings",
    "attributes": {
      "support_email_address": "support@example.com",
      "security_email_address": "security@example.com",
      "limit_user_org_creation": true
    }
  }
}
```

## List SAML Settings
`GET /api/v2/admin/settings/saml`

-> **Note:** This endpoint cannot be accessed with [organization tokens](../users-teams-organizations/service-accounts.html#organization-service-accounts). You must access it with a [user token](../users-teams-organizations/users.html#api-tokens) which has the `site-admins` permission.

Status  | Response                                         | Reason
--------|--------------------------------------------------|-------
[200][] | Array of [JSON API document][]s (`type: "settings"`) | Successfully listed SAML settings
[404][] | [JSON API error object][]                    | User unauthorized to perform action

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/admin/settings/saml
```

### Sample Response

```json
{
  "data": {
    "id": "saml-settings",
    "type": "settings",
    "attributes": {
      "enabled": true,
      "idp_cert": "SAMPLE-CERTIFICATE",
      "slo_target": "https://example.com/slo",
      "sso_target": "https://example.com/sso",
      "attr_groups": "MemberOf",
      "attr_site_admin": "SiteAdmin",
      "site_admin_role": "site-admins",
      "sso_api_token_session_timeout": 1209600
    }
  }
}
```

## Update SAML Settings
`PATCH /api/v2/admin/settings/saml`

-> **Note:** This endpoint cannot be accessed with [organization tokens](../users-teams-organizations/service-accounts.html#organization-service-accounts). You must access it with a [user token](../users-teams-organizations/users.html#api-tokens) which has the `site-admins` permission.

Status  | Response                                         | Reason
--------|--------------------------------------------------|-------
[200][] | Array of [JSON API document][]s (`type: "settings"`) | Successfully updated SAML settings
[404][] | [JSON API error object][]                    | User unauthorized to perform action
[422][] | [JSON API error object][]                    | Malformed request body (missing attributes, wrong types, etc.)

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[422]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Request Body

This PATCH endpoint requires a JSON object with the following properties as a request payload.

Properties without a default value are required if `data.attributes.enabled` is set to `true`.

Key path                    | Type   | Default | Description
----------------------------|--------|---------|------------
`data.attributes.enabled`    | bool   | `false` | Allows SAML to be used. If true, all remaining attributes are required.
`data.attributes.idp_cert`   | string |         | Identity Provider Certificate specifies the PEM encoded X.509 Certificate as provided by the IdP configuration.
`data.attributes.slo_target` | string |         | Single Log Out URL specifies the HTTP(s) endpoint on your IdP for single logout requests. This value is provided by your IdP configuration.
`data.attributes.sso_target` | string |         | Single Sign On URL specifies the HTTP(S) endpoint on your IdP for single sign-on requests. This value is provided by your IdP configuration.
`data.attributes.attr_groups`| string | `"MemberOf"` | Team Attribute Name specifies the name of the SAML attribute that determines team membership. The value of this attribute in the SAML assertion must be a string containing a comma-separated list of team names.
`data.attributes.attr_site_admin`| string |`"SiteAdmin"`| Specifies the role for site admin access, overridding the "Site Admin Role" method.
`data.attributes.site_admin_role`| string |`"site-admins"`| Specifies the role for site admin access, provided in the list of roles sent in the Team Attribute Name attribute.
`data.attributes.sso_api_token_session_timeout`| integer | 1209600 | Specifies the Single Sign On session timeout, defaulting to 14 days.

```json
{
  "data": {
    "attributes": {
      "enabled": true,
      "idp_cert": "SAMPLE-CERTIFICATE",
      "slo_target": "https://example.com/slo",
      "sso_target": "https://example.com/sso",
      "attr_groups": "MemberOf",
      "attr_site_admin": "SiteAdmin",
      "site_admin_role": "site-admins",
      "sso_api_token_session_timeout": 1209600
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
  https://app.terraform.io/api/v2/admin/settings/saml
```

### Sample Response

```json
{
  "data": {
    "id":"saml-settings",
    "type":"settings",
    "attributes": {
      "enabled": true,
      "idp_cert": "SAMPLE-CERTIFICATE",
      "slo_target": "https://example.com/slo",
      "sso_target": "https://example.com/sso",
      "attr_groups": "MemberOf",
      "attr_site_admin": "SiteAdmin",
      "site_admin_role": "site-admins",
      "sso_api_token_session_timeout": 1209600
    }
  }
}
```

## List SMTP Settings
`GET /api/v2/admin/settings/smtp`

-> **Note:** This endpoint cannot be accessed with [organization tokens](../users-teams-organizations/service-accounts.html#organization-service-accounts). You must access it with a [user token](../users-teams-organizations/users.html#api-tokens) which has the `site-admins` permission.

Status  | Response                                         | Reason
--------|--------------------------------------------------|-------
[200][] | Array of [JSON API document][]s (`type: "settings"`) | Successfully listed SMTP settings
[404][] | [JSON API error object][]                    | User unauthorized to perform action

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Sample Request

```shell
curl \
  --header "Authorization: Bearer $ATLAS_TOKEN" \
  --header "Content-Type: application/vnd.api+json" \
  --request GET \
  https://app.terraform.io/api/v2/admin/settings/smtp
```

### Sample Response

```json
{
  "data": {
    "id": "smtp-settings",
    "type": "settings",
    "attributes": {
      "enabled": true,
      "host": "example.com",
      "port": 25,
      "sender": "sample_user@example.com",
      "auth": "login",
      "username": "sample_user"
    }
  }
}
```

## Update SMTP Settings
`PATCH /api/v2/admin/settings/smtp`

-> **Note:** This endpoint cannot be accessed with [organization tokens](../users-teams-organizations/service-accounts.html#organization-service-accounts). You must access it with a [user token](../users-teams-organizations/users.html#api-tokens) which has the `site-admins` permission.

Status  | Response                                     | Reason
--------|----------------------------------------------|----------
[200][] | [JSON API document][] (`type: "settings"`) | Successfully updated the SMTP settings
[401][] | [JSON API error object][]                    | Failure during test message delivery, SMTP user credentials are invalid
[404][] | [JSON API error object][]                    | User unauthorized to perform action
[422][] | [JSON API error object][]                    | Malformed request body (missing attributes, wrong types, etc.)
[500][] | [JSON API error object][]                    | Failure during test message delivery, SMTP server server error
[504][] | [JSON API error object][]                    | Failure during test message delivery, SMTP server timeout

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[401]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/401
[404]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404
[422]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422
[500]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/504
[504]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/504
[JSON API document]: https://www.terraform.io/docs/enterprise/api/index.html#json-api-documents
[JSON API error object]: http://jsonapi.org/format/#error-objects

### Request Body

This PATCH endpoint requires a JSON object with the following properties as a request payload.

Properties without a default value are required if `data.attributes.enabled` is set to `true`.

Key path                    | Type   | Default | Description
----------------------------|--------|---------|------------
`data.attributes.enabled`   | bool   | `false` | Allows SMTP to be used. If true, all remaining attributes are required.
`data.attributes.host`      | string |         | The host address of the SMTP server.
`data.attributes.port`      | integer|         | The port of the SMTP server.
`data.attributes.sender`    | string |         | The desired sender address.
`data.attributes.auth`      | string | `"none"`| The authentication type. Valid values are `"none"`, `"plain"`, and `"login"`.
`data.attributes.username`  | string |         | The username used to authenticate to the SMTP server. Only required if `data.attributes.auth` is set to `"login"` or `"plain"`.
`data.attributes.password`  | string |         | The username used to authenticate to the SMTP server. Only required if `data.attributes.auth` is set to `"login"` or `"plain"`.

### Sample Payload

```json
{
  "data": {
    "attributes": {
      "enabled": true,
      "host": "example.com",
      "port": 25,
      "sender": "sample_user@example.com",
      "auth": "login",
      "username": "sample_user",
      "password": "sample_password"
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
  https://app.terraform.io/api/v2/admin/settings/smtp
```

### Sample Response

```json
{
  "data": {
    "id":"smtp-settings",
    "type":"settings",
    "attributes": {
      "enabled": true,
      "host": "example.com",
      "port": 25,
      "sender": "sample_user@example.com",
      "auth": "login",
      "username": "sample_user"
    }
  }
}
```
