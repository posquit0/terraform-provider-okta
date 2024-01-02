---
page_title: "Resource: okta_idp_saml"
description: |-
  Creates a SAML Identity Provider. This resource allows you to create and configure a SAML Identity Provider.
---

# Resource: okta_idp_saml

Creates a SAML Identity Provider. This resource allows you to create and configure a SAML Identity Provider.

## Example Usage

```terraform
resource "okta_idp_saml" "example" {
  name                     = "testAcc_replace_with_uuid"
  acs_type                 = "INSTANCE"
  sso_url                  = "https://idp.example.com"
  sso_destination          = "https://idp.example.com"
  sso_binding              = "HTTP-POST"
  username_template        = "idpuser.email"
  kid                      = okta_idp_saml_key.test.id
  issuer                   = "https://idp.example.com"
  request_signature_scope  = "REQUEST"
  response_signature_scope = "ANY"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `issuer` (String) URI that identifies the issuer.
- `kid` (String) The ID of the signing key.
- `name` (String) Name of the IdP
- `sso_url` (String) URL of binding-specific endpoint to send an AuthnRequest message to IdP.

### Optional

- `account_link_action` (String) Specifies the account linking action for an IdP user. Default: `AUTO`
- `account_link_group_include` (Set of String) Group memberships to determine link candidates.
- `acs_type` (String) The type of ACS. It can be `INSTANCE` or `ORG`. Default: `INSTANCE`
- `deprovisioned_action` (String) Action for a previously deprovisioned IdP user during authentication. Can be `NONE` or `REACTIVATE`. Default: `NONE`
- `groups_action` (String) Provisioning action for IdP user's group memberships. It can be `NONE`, `SYNC`, `APPEND`, or `ASSIGN`. Default: `NONE`
- `groups_assignment` (Set of String) List of Okta Group IDs to add an IdP user as a member with the `ASSIGN` `groups_action`.
- `groups_attribute` (String) IdP user profile attribute name (case-insensitive) for an array value that contains group memberships.
- `groups_filter` (Set of String) Whitelist of Okta Group identifiers that are allowed for the `APPEND` or `SYNC` `groups_action`.
- `issuer_mode` (String) Indicates whether Okta uses the original Okta org domain URL, or a custom domain URL
- `max_clock_skew` (Number) Maximum allowable clock-skew when processing messages from the IdP.
- `name_format` (String) The name identifier format to use. By default `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`.
- `profile_master` (Boolean) Determines if the IdP should act as a source of truth for user profile attributes.
- `provisioning_action` (String) Provisioning action for an IdP user during authentication. Default: `AUTO`
- `request_signature_algorithm` (String) The XML digital Signature Algorithm used when signing an `AuthnRequest` message. It can be `SHA-256` or `SHA-1`. Default: `SHA-256`
- `request_signature_scope` (String) Specifies whether to digitally sign an AuthnRequest messages to the IdP. It can be `REQUEST` or `NONE`. Default: `REQUEST`
- `response_signature_algorithm` (String) The minimum XML digital signature algorithm allowed when verifying a `SAMLResponse` message or Assertion element. It can be `SHA-256` or `SHA-1`. Default: `SHA-256`
- `response_signature_scope` (String) Specifies whether to verify a `SAMLResponse` message or Assertion element XML digital signature. It can be `RESPONSE`, `ASSERTION`, or `ANY`. Default: `ANY`
- `sso_binding` (String) The method of making an SSO request. It can be set to `HTTP-POST` or `HTTP-REDIRECT`. Default: `HTTP-POST`
- `sso_destination` (String) URI reference indicating the address to which the AuthnRequest message is sent.
- `status` (String) Default to `ACTIVE`
- `subject_filter` (String) Optional regular expression pattern used to filter untrusted IdP usernames.
- `subject_format` (Set of String) The name format.
- `subject_match_attribute` (String) Okta user profile attribute for matching transformed IdP username. Only for matchType `CUSTOM_ATTRIBUTE`.
- `subject_match_type` (String) Determines the Okta user profile attribute match conditions for account linking and authentication of the transformed IdP username. By default, it is set to `USERNAME`. It can be set to `USERNAME`, `EMAIL`, `USERNAME_OR_EMAIL` or `CUSTOM_ATTRIBUTE`.
- `suspended_action` (String) Action for a previously suspended IdP user during authentication. Can be `NONE` or `REACTIVATE`. Default: `NONE`
- `username_template` (String) Okta EL Expression to generate or transform a unique username for the IdP user. Default: `idpuser.email`

### Read-Only

- `acs_binding` (String)
- `audience` (String)
- `id` (String) The ID of this resource.
- `type` (String)
- `user_type_id` (String)

## Import

Import is supported using the following syntax:

```shell
terraform import okta_idp_saml.example &#60;idp id&#62;
```