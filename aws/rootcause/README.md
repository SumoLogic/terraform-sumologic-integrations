# SumoLogic-AWS-RootCause

This module is used to create the SumoLogic AWS RootCause sources. Features include
- Create AWS IAM role or use an existing IAM role.
- Create Sumo Logic hosted collector or use an existing Sumo Logic hosted collector.
- Create Sumo Logic AWS Inventory and XRAY source.

## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.13.0 |
| aws | >= 3.42.0 |
| random | >= 3.1.0 |
| sumologic | >= 2.9.0 |
| time | >= 0.7.1 |

## Providers

| Name | Version |
|------|---------|
| aws | >= 3.42.0 |
| random | >= 3.1.0 |
| sumologic | >= 2.9.0 |
| time | >= 0.7.1 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| collector\_details | Provide details for the Sumo Logic collector. If not provided, then defaults will be used. | <pre>object({<br>    collector_name = string<br>    description    = string<br>    fields         = map(string)<br>  })</pre> | <pre>{<br>  "collector_name": "SumoLogic RootCause Collector <Random ID>",<br>  "description": "This collector is created using Sumo Logic terraform AWS Root Cause module.",<br>  "fields": {}<br>}</pre> | no |
| create\_collector | Provide "true" if you would like to create the Sumo Logic Collector. | `bool` | n/a | yes |
| create\_inventory\_source | Provide "true" if you would like to create the Sumo Logic AWS Inventory source. | `bool` | n/a | yes |
| create\_xray\_source | Provide "true" if you would like to create the Sumo Logic AWS Xray source. | `bool` | n/a | yes |
| iam\_details | Provide an existing AWS IAM role ARN value to attach to Sumo Logic sources. If this is kept empty, a new IAM role will be created. | <pre>object({<br>    create_iam_role = bool<br>    iam_role_arn    = string<br>  })</pre> | <pre>{<br>  "create_iam_role": true,<br>  "iam_role_arn": null<br>}</pre> | no |
| inventory\_source\_details | Provide details for the Sumo Logic AWS Inventory source. If not provided, then defaults will be used. | <pre>object({<br>    source_name         = string<br>    source_category     = string<br>    collector_id        = string<br>    description         = string<br>    limit_to_regions    = list(string)<br>    limit_to_namespaces = list(string)<br>    paused              = bool<br>    scan_interval       = number<br>    sumo_account_id     = number<br>    fields              = map(string)<br>  })</pre> | <pre>{<br>  "collector_id": "",<br>  "description": "This source is created using Sumo Logic terraform AWS RootCause module to collect AWS inventory metadata.",<br>  "fields": {},<br>  "limit_to_namespaces": [],<br>  "limit_to_regions": [],<br>  "paused": false,<br>  "scan_interval": 300000,<br>  "source_category": "Labs/inventory",<br>  "source_name": "Inventory Source",<br>  "sumo_account_id": 926226587429<br>}</pre> | no |
| sumologic\_organization\_id | Appears on the Account Overview page that displays information about your Sumo Logic organization. Used for IAM Role in Sumo Logic AWS Sources. | `string` | n/a | yes |
| wait\_for\_seconds | wait\_for\_seconds is used to delay sumo logic source creation. This helps persisting IAM role in AWS system.<br>        Default value is 180 seconds.<br>        If the AWS IAM role is created outside the module, the value can be decreased to 1 second. | `number` | `180` | no |
| xray\_source\_details | Provide details for the Sumo Logic AWS XRAY source. If not provided, then defaults will be used. | <pre>object({<br>    source_name      = string<br>    source_category  = string<br>    collector_id     = string<br>    description      = string<br>    limit_to_regions = list(string)<br>    paused           = bool<br>    scan_interval    = number<br>    sumo_account_id  = number<br>    fields           = map(string)<br>  })</pre> | <pre>{<br>  "collector_id": "",<br>  "description": "This source is created using Sumo Logic terraform AWS RootCause module to collect AWS Xray metrics.",<br>  "fields": {},<br>  "limit_to_regions": [],<br>  "paused": false,<br>  "scan_interval": 300000,<br>  "source_category": "Labs/xray",<br>  "source_name": "Xray Source",<br>  "sumo_account_id": 926226587429<br>}</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| aws\_iam\_role | AWS IAM role with permission to allow Sumo Logic to read logs from S3 Bucket. |
| inventory\_sumologic\_source | Sumo Logic AWS Inventory source. |
| random\_string | Random String value created. |
| sumologic\_collector | Sumo Logic hosted collector. |
| xray\_sumologic\_source | Sumo Logic AWS XRAY source. |
