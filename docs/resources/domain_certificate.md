---
page_title: "Resource: okta_domain_certificate"
description: |-
  Manages certificate for the domain.
  This resource's 'certificate', 'privatekey', and 'certificatechain' attributes
  hold actual PEM values and can be referred to by other configs requiring
  certificate and private key inputs. This is inline with TF's best
  practices https://developer.hashicorp.com/terraform/plugin/sdkv2/best-practices/sensitive-state#don-t-encrypt-state
  of not encrypting state.
  See Let's Encrypt Certbot notes at the end of this
  documentation for notes on how to generate a domain certificate with Let's Encrypt Certbot
---

# Resource: okta_domain_certificate

Manages certificate for the domain.

This resource's 'certificate', 'private_key', and 'certificate_chain' attributes
hold actual PEM values and can be referred to by other configs requiring
certificate and private key inputs. This is inline with TF's [best
practices](https://developer.hashicorp.com/terraform/plugin/sdkv2/best-practices/sensitive-state#don-t-encrypt-state)
of not encrypting state.

See [Let's Encrypt Certbot notes](#lets-encrypt-certbot) at the end of this
documentation for notes on how to generate a domain certificate with Let's Encrypt Certbot

## Example Usage

```terraform
resource "okta_domain" "example" {
  name = "www.example.com"
}

resource "okta_domain_certificate" "test" {
  domain_id = okta_domain.test.id
  type      = "PEM"


  #certificate = file("www.example.com/cert.pem")
  certificate = <<CERT
-----BEGIN CERTIFICATE-----
MIIFNzCCBB+gAwIBAgISBAXomJWRama3ypu8TIxdA9wzMA0GCSqGSIb3DQEBCwUA
...
NSgRtSXq11j8O4JONi8EXe7cEtvzUiLR5PL3itsK2svtrZ9jIwQ95wOPaA==
-----END CERTIFICATE-----
CERT

  #certificate_chain = file("www.example.com/chain.pem")
  certificate_chain = <<CHAIN
-----BEGIN CERTIFICATE-----
MIIFFjCCAv6gAwIBAgIRAJErCErPDBinU/bWLiWnX1owDQYJKoZIhvcNAQELBQAw
...
Dfvp7OOGAN6dEOM4+qR9sdjoSYKEBpsr6GtPAQw4dy753ec5
-----END CERTIFICATE-----
CHAIN

  #private_key = file("www.example.com/privkey.pem")
  private_key = <<PK
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQC5cyk6x63iBJSW
...
nUFLNE8pXSnsqb0eOL74f3uQ
-----END PRIVATE KEY-----
PK
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `certificate` (String) Certificate content
- `certificate_chain` (String) Certificate chain
- `domain_id` (String) Domain's ID
- `private_key` (String) Certificate private key

### Optional

- `type` (String) Certificate type. Valid value is `PEM`

### Read-Only

- `id` (String) The ID of this resource.



## Let's Encrypt Certbot

This example demonstrates generatoring a domain certificate with letsencrypt
certbot https://letsencrypt.org/getting-started/

```
$ certbot certonly --manual --preferred-challenges dns --key-type rsa -d [DOMAIN]
```

Use letsencrypt's certbot to generate domain certificates in RSA output mode.
The generator's output corresponds to `okta_domain_certificate` fields in the
following manner.

Okta Field          | Certbot file
--------------------|--------------
`certificate`       | `cert.pem`
`certificate_chain` | `chain.pem`
`private_key`       | `privkey.pem`