---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "confluent_private_link_attachment_connection Data Source - terraform-provider-confluent"
subcategory: ""
description: |-
   
---

# confluent_private_link_attachment_connection Data Source

[![Limited Availability](https://img.shields.io/badge/Lifecycle%20Stage-Limited%20Availability-%2345c6e8)](https://docs.confluent.io/cloud/current/api.html#section/Versioning/API-Lifecycle-Policy)
[![Request Access To Networking v1](https://img.shields.io/badge/-Request%20Access%20To%20Networking%20v1-%23bc8540)](mailto:ccloud-api-access+networking-v1-early-access@confluent.io?subject=Request%20to%20join%20networking/v1%20API%20Early%20Access&body=I%E2%80%99d%20like%20to%20join%20the%20Confluent%20Cloud%20API%20Early%20Access%20for%20networking/v1%20to%20provide%20early%20feedback%21%20My%20Cloud%20Organization%20ID%20is%20%3Cretrieve%20from%20https%3A//confluent.cloud/settings/billing/payment%3E.)

-> **Note:** `confluent_private_link_attachment_connection` data source is available in **Limited Availability** for early adopters. Preview features are introduced to gather customer feedback. This feature should be used only for evaluation and non-production testing purposes or to provide feedback to Confluent, particularly as it becomes more widely available in follow-on editions.  
**Limited Availability** features are intended for evaluation use in development and testing environments only, and not for production use. The warranty, SLA, and Support Services provisions of your agreement with Confluent do not apply to Preview features. Preview features are considered to be a Proof of Concept as defined in the Confluent Cloud Terms of Service. Confluent may discontinue providing preview releases of the Preview features at any time in Confluent’s sole discretion.

`confluent_private_link_attachment_connection` describes a Private Link Attachment Connection data source.

## Example Usage

```terraform
data "confluent_private_link_attachment_connection" "main" {
  id = "plattc-p5j3ov"
  environment {
    id = "env-8gv0v5"
  }
}

output "plattc" {
  value = data.confluent_private_link_attachment_connection.main
}
```

<!-- schema generated by tfplugindocs -->
## Argument Reference

The following arguments are supported:

- `id` - (Required String) The ID of the Private Link Attachment Connection, for example, `plattc-p5j3ov`.
- `environment` (Required Configuration Block) supports the following:
  - `id` - (Required String) The ID of the Environment that the Private Link Attachment Connection belongs to, for example `env-xyz456`.

## Attributes Reference

In addition to the preceding arguments, the following attributes are exported:

- `display_name` - (Optional String) The name of the Private Link Attachment Connection.
- `resource_name` - (Required String) The Confluent Resource Name of the Private Link Attachment Connection, for example `crn://confluent.cloud/organization=1111aaaa-11aa-11aa-11aa-111111aaaaaa/environment=env-75gxp2/private-link-attachment=platt-1q0ky0/private-link-attachment-connection=plattc-77zq2w`.
- `private_link_attachment` (Optional Configuration Block) supports the following:
  - `id` - (Required String) The unique identifier for the private link attachment.
- `aws` - (Optional Configuration Block) supports the following:
  - `vpc_endpoint_id` - (Required String) Id of a VPC Endpoint that is connected to the VPC Endpoint service.