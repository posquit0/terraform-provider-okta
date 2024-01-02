---
page_title: "Resource: okta_policy_mfa_default"
description: |-
  Configures default MFA Policy.
  This resource allows you to configure default MFA Policy.
  ~> Requires Org Feature Flag 'OKTAMFAPOLICY'. Contact support mailto:dev-inquiries@okta.com to have this feature flag enabled.
  ~> Unless Org Feature Flag 'ENGENABLEOPTIONALPASSWORDENROLLMENT' is disabled 'oktapassword' or 'oktaemail' must be present and its 'enroll' value set to 'REQUIRED'. Contact support mailto:dev-inquiries@okta.com to have this feature flag disabled.
---

# Resource: okta_policy_mfa_default

Configures default MFA Policy.

This resource allows you to configure default MFA Policy.

~> Requires Org Feature Flag 'OKTA_MFA_POLICY'. [Contact support](mailto:dev-inquiries@okta.com) to have this feature flag ***enabled***.

~> Unless Org Feature Flag 'ENG_ENABLE_OPTIONAL_PASSWORD_ENROLLMENT' is ***disabled*** 'okta_password' or 'okta_email' must be present and its 'enroll' value set to 'REQUIRED'. [Contact support](mailto:dev-inquiries@okta.com) to have this feature flag ***disabled***.

## Example Usage

```terraform
resource "okta_policy_mfa_default" "classic_example" {
  is_oie = false

  okta_password = {
    enroll = "REQUIRED"
  }

  okta_otp = {
    enroll = "REQUIRED"
  }
}

resource "okta_policy_mfa_default" "oie_example" {
  is_oie = true

  okta_password = {
    enroll = "REQUIRED"
  }

  # The following authenticator can only be used when `is_oie` is set to true
  okta_verify = {
    enroll = "REQUIRED"
  }
}

### -> If the `okta_policy_mfa_default` is used in conjunction with `okta_policy_mfa` resources, ensure to use a `depends_on` attribute for the default policy to ensure that all other policies are created/updated first such that the `priority` field can be appropriately computed on the first plan/apply.
```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `duo` (Map of String)
- `external_idp` (Map of String)
- `fido_u2f` (Map of String)
- `fido_webauthn` (Map of String)
- `google_otp` (Map of String)
- `hotp` (Map of String)
- `is_oie` (Boolean) Is the policy using Okta Identity Engine (OIE) with authenticators instead of factors?
- `okta_call` (Map of String)
- `okta_email` (Map of String)
- `okta_otp` (Map of String)
- `okta_password` (Map of String)
- `okta_push` (Map of String)
- `okta_question` (Map of String)
- `okta_sms` (Map of String)
- `okta_verify` (Map of String)
- `onprem_mfa` (Map of String)
- `phone_number` (Map of String)
- `rsa_token` (Map of String)
- `security_question` (Map of String)
- `symantec_vip` (Map of String)
- `webauthn` (Map of String)
- `yubikey_token` (Map of String)

### Read-Only

- `default_included_group_id` (String) Default group ID (always included)
- `description` (String) Default policy description
- `id` (String) The ID of this resource.
- `name` (String) Default policy name
- `priority` (Number) Default policy priority
- `status` (String) Default policy status

## Import

Import is supported using the following syntax:

```shell
terraform import okta_policy_mfa_default.example .
```