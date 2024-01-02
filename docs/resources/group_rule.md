---
page_title: "Resource: okta_group_rule"
description: |-
  Creates an Okta Group Rule.
  This resource allows you to create and configure an Okta Group Rule.
  -> If the Okta API marks the 'status' of the rule as 'INVALID' the Okta
  Terraform Provider will act in a force/replace manner and call the API to delete
  the underlying rule resource and create a new rule resource.
---

# Resource: okta_group_rule

Creates an Okta Group Rule.

This resource allows you to create and configure an Okta Group Rule.

-> If the Okta API marks the 'status' of the rule as 'INVALID' the Okta
Terraform Provider will act in a force/replace manner and call the API to delete
the underlying rule resource and create a new rule resource.

## Example Usage

```terraform
resource "okta_group_rule" "example" {
  name   = "example"
  status = "ACTIVE"
  group_assignments = [
  "<group id>"]
  expression_type  = "urn:okta:expression:1.0"
  expression_value = "String.startsWith(user.firstName,\"andy\")"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `expression_value` (String) The expression value.
- `group_assignments` (Set of String) The list of group ids to assign the users to.
- `name` (String) The name of the Group Rule (min character 1; max characters 50).

### Optional

- `expression_type` (String) The expression type to use to invoke the rule. The default is `urn:okta:expression:1.0`.
- `remove_assigned_users` (Boolean) Remove users added by this rule from the assigned group after deleting this resource. Default is `false`
- `status` (String) Default to `ACTIVE`
- `users_excluded` (Set of String) The list of user IDs that would be excluded when rules are processed

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
terraform import okta_group_rule.example &#60;group rule id&#62;
```