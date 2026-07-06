# terraform-aws-mcaf-privatelink
Terraform module to create and manage a [Interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-service-overview.html) using Network Load Balancer in AWS PrivateLink.

- Exposes a service running in VPC A to VPC B using PrivateLink. Creates a private DNS name that can used do to access the
service. NOTE: To use a private hosted zone, you must set the following VPC attributes to true: `enableDnsHostnames` and `enableDnsSupport`.

```terraform
module "privatelink" {
  source                   = "github.com/schubergphilis/terraform-aws-mcaf-privatelink"
  name                     = "test"
  allowed_principals       = ["arn:aws:iam::xxyyzz:root"]
  domain_name              = "test.com"
  private_subnet_ids       = ["subnet-XXYYZZ"]
  target_ips                = ["192.168.0.1", "192.168.0.2"]
  target_port              = 80
  target_protocol          = "TCP"
  vpc_id                   = "vpc-xxyyzz"
  zone_id                  = "AAABBBCCC1234"

  tags = {
    environment = "test"
  }
}
```

<!--- BEGIN_TF_DOCS --->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.13 |
| aws | >= 3.23 |

## Providers

| Name | Version |
|------|---------|
| aws | >= 3.23 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| allowed\_principals | List of allowed AWS principals to access the endpoint service | `list(string)` | n/a | yes |
| name | Name to use for the PrivateLink resources | `string` | n/a | yes |
| private\_dns\_name | Private DNS hostname to connect to the endpoint service | `string` | n/a | yes |
| private\_subnet\_ids | List of subnet IDs assigned to the network load balancer | `list(string)` | n/a | yes |
| tags | A mapping of tags to assign to the resources | `map(string)` | n/a | yes |
| target\_port | The target port of the endpoint service | `number` | n/a | yes |
| vpc\_id | The ID of the VPC | `string` | n/a | yes |
| zone\_id | The ID of the DNS Zone | `string` | n/a | yes |
| target\_ips | A list of target IP addresses of the endpoint service | `list(string)` | `[]` | no |
| target\_protocol | The target protocol of the endpoint service | `string` | `"TCP"` | no |

## Outputs

| Name | Description |
|------|-------------|
| private\_dns\_name | Name of the private DNS to access the service |
| service\_name | Service name of the Endpoint Service |

<!--- END_TF_DOCS --->

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 3.23 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 3.23 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_lb.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb) | resource |
| [aws_lb_listener.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_listener) | resource |
| [aws_lb_target_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_target_group) | resource |
| [aws_lb_target_group_attachment.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_target_group_attachment) | resource |
| [aws_route53_record.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_vpc_endpoint_service.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc_endpoint_service) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_allowed_principals"></a> [allowed\_principals](#input\_allowed\_principals) | List of allowed AWS principals to access the endpoint service | `list(string)` | n/a | yes |
| <a name="input_name"></a> [name](#input\_name) | Name to use for the PrivateLink resources | `string` | n/a | yes |
| <a name="input_private_dns_name"></a> [private\_dns\_name](#input\_private\_dns\_name) | Private DNS hostname to connect to the endpoint service | `string` | n/a | yes |
| <a name="input_private_subnet_ids"></a> [private\_subnet\_ids](#input\_private\_subnet\_ids) | List of subnet IDs assigned to the network load balancer | `list(string)` | n/a | yes |
| <a name="input_tags"></a> [tags](#input\_tags) | A mapping of tags to assign to the resources | `map(string)` | n/a | yes |
| <a name="input_target_port"></a> [target\_port](#input\_target\_port) | The target port of the endpoint service | `number` | n/a | yes |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | The ID of the VPC | `string` | n/a | yes |
| <a name="input_zone_id"></a> [zone\_id](#input\_zone\_id) | The ID of the DNS Zone | `string` | n/a | yes |
| <a name="input_target_ips"></a> [target\_ips](#input\_target\_ips) | A list of target IP addresses of the endpoint service | `list(string)` | `[]` | no |
| <a name="input_target_protocol"></a> [target\_protocol](#input\_target\_protocol) | The target protocol of the endpoint service | `string` | `"TCP"` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_private_dns_name"></a> [private\_dns\_name](#output\_private\_dns\_name) | Name of the private DNS to access the service |
| <a name="output_service_name"></a> [service\_name](#output\_service\_name) | Service name of the Endpoint Service |
<!-- END_TF_DOCS -->