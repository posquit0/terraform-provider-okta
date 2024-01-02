---
page_title: "Resource: okta_app_group_assignments"
description: |-
  Assigns groups to an application. This resource allows you to create multiple App Group assignments.
---

# Resource: okta_app_group_assignments

Assigns groups to an application. This resource allows you to create multiple App Group assignments.

## Example Usage

```terraform
resource "okta_app_group_assignments" "example" {
  app_id = "<app id>"
  group {
    id       = "<group id>"
    priority = 1
  }
  group {
    id       = "<another group id>"
    priority = 2
    profile  = jsonencode({ "application profile field" : "application profile value" })
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `app_id` (String) The ID of the application to assign a group to.
- `group` (Block List, Min: 1) A group to assign to this application (see [below for nested schema](#nestedblock--group))

### Read-Only

- `id` (String) The ID of this resource.

<a id="nestedblock--group"></a>
### Nested Schema for `group`

Required:

- `id` (String) A group to associate with the application

Optional:

- `priority` (Number) Priority of group assignment
- `profile` (String) JSON document containing [application profile](https://developer.okta.com/docs/reference/api/apps/#profile-object)

## Import

Import is supported using the following syntax:

```shell
terraform import okta_app_group_assignments.example &#60;app_id&#62
```