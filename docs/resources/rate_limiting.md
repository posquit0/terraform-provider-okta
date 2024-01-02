---
page_title: "Resource: okta_rate_limiting"
description: |-
  Manages rate limiting.
  This resource allows you to configure the client-based rate limit and rate limiting communications settings.
  ~> WARNING: This resource is available only when using a SSWS API token in the provider config, it is incompatible with OAuth 2.0 authentication.
  ~> WARNING: This resource makes use of an internal/private Okta API endpoint that could change without notice rendering this resource inoperable.
---

# Resource: okta_rate_limiting

Manages rate limiting.
This resource allows you to configure the client-based rate limit and rate limiting communications settings.

~> **WARNING:** This resource is available only when using a SSWS API token in the provider config, it is incompatible with OAuth 2.0 authentication.

~> **WARNING:** This resource makes use of an internal/private Okta API endpoint that could change without notice rendering this resource inoperable.

## Example Usage

```terraform
resource "okta_rate_limiting" "example" {
  login                  = "ENFORCE"
  authorize              = "ENFORCE"
  communications_enabled = true
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `authorize` (String) Called during authentication. Valid values: `ENFORCE` _(Enforce limit and log per client (recommended))_, `DISABLE` _(Do nothing (not recommended))_, `PREVIEW` _(Log per client)_.
- `login` (String) Called when accessing the Okta hosted login page. Valid values: `ENFORCE` _(Enforce limit and log per client (recommended))_, `DISABLE` _(Do nothing (not recommended))_, `PREVIEW` _(Log per client)_.

### Optional

- `communications_enabled` (Boolean) Enable or disable rate limiting communications. By default, it is `true`.

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
terraform import okta_rate_limiting.example .
```