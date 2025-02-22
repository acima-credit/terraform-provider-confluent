---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "confluent_kafka_topic Data Source - terraform-provider-confluent"
subcategory: ""
description: |-
  
---

# confluent_kafka_topic Data Source

[![General Availability](https://img.shields.io/badge/Lifecycle%20Stage-General%20Availability-%2345c6e8)](https://docs.confluent.io/cloud/current/api.html#section/Versioning/API-Lifecycle-Policy)

`confluent_kafka_topic` describes a Kafka Topic data source.

## Example Usage

### Option #1: Manage multiple Kafka clusters in the same Terraform workspace

```terraform
provider "confluent" {
  cloud_api_key    = var.confluent_cloud_api_key    # optionally use CONFLUENT_CLOUD_API_KEY env var
  cloud_api_secret = var.confluent_cloud_api_secret # optionally use CONFLUENT_CLOUD_API_SECRET env var
}

data "confluent_kafka_topic" "orders" {
  kafka_cluster {
    id = confluent_kafka_cluster.basic-cluster.id
  }

  topic_name    = "orders"
  rest_endpoint = confluent_kafka_cluster.basic-cluster.rest_endpoint

  credentials {
    key    = "<Kafka API Key for confluent_kafka_cluster.basic-cluster>"
    secret = "<Kafka API Secret for confluent_kafka_cluster.basic-cluster>"
  }
}

output "config" {
  value = data.confluent_kafka_topic.orders.config
}
```

### Option #2: Manage a single Kafka cluster in the same Terraform workspace

```terraform
provider "confluent" {
  kafka_id            = var.kafka_id                   # optionally use KAFKA_ID env var
  kafka_rest_endpoint = var.kafka_rest_endpoint        # optionally use KAFKA_REST_ENDPOINT env var
  kafka_api_key       = var.kafka_api_key              # optionally use KAFKA_API_KEY env var
  kafka_api_secret    = var.kafka_api_secret           # optionally use KAFKA_API_SECRET env var
}

data "confluent_kafka_topic" "orders" {
  topic_name    = "orders"
}

output "config" {
  value = data.confluent_kafka_topic.orders.config
}
```

<!-- schema generated by tfplugindocs -->
## Argument Reference

The following arguments are supported:

- `kafka_cluster` - (Optional Configuration Block) supports the following:
  - `id` - (Required String) The ID of the Kafka cluster, for example, `lkc-abc123`.
- `topic_name` - (Required String) The name of the topic, for example, `orders-1`. The topic name can be up to 255 characters in length and can contain only alphanumeric characters, hyphens, and underscores.
- `rest_endpoint` - (Optional String) The REST endpoint of the Kafka cluster, for example, `https://pkc-00000.us-central1.gcp.confluent.cloud:443`).
- `credentials` (Optional Configuration Block) supports the following:
    - `key` - (Required String) The Kafka API Key.
    - `secret` - (Required String) The Kafka API Secret.

-> **Note:** A Kafka API key consists of a key and a secret. Kafka API keys are required to interact with Kafka clusters in Confluent Cloud. Each Kafka API key is valid for one specific Kafka cluster.

!> **Warning:** Terraform doesn't encrypt the sensitive `credentials` value of the `confluent_kafka_topic` data source, so you must keep your state file secure to avoid exposing it. Refer to the [Terraform documentation](https://www.terraform.io/docs/language/state/sensitive-data.html) to learn more about securing your state file.

## Attributes Reference

In addition to the preceding arguments, the following attributes are exported:

- `id` - (Required String) The ID of the Kafka topic, in the format `<Kafka cluster ID>/<Kafka Topic name>`, for example, `lkc-abc123/orders-1`.
- `partitions_count` - (Required Number) The number of partitions to create in the topic. Defaults to `6`.
- `config` - (Optional Map) The custom topic settings:
    - `name` - (Required String) The setting name, for example, `cleanup.policy`.
    - `value` - (Required String) The setting value, for example, `compact`.

-> **Note:** For more information on the topic settings, see [Custom topic settings for all cluster types supported by Kafka REST API and Terraform Provider](https://docs.confluent.io/cloud/current/clusters/broker-config.html#custom-topic-settings-for-all-cluster-types-supported-by-kafka-rest-api-and-terraform-provider) and [Schema Validation Configuration options on a topic](https://docs.confluent.io/cloud/current/sr/broker-side-schema-validation.html#sv-configuration-options-on-a-topic).
