# Module Azure Log Analytics

Module for creating and managing a Log Analytics Workspace.

## Usage

```
module "resource_group" {
  source = "git::https://github.com/danielscholl-terraform/module-resource-group?ref=v1.0.0"

  name     = "iac-terraform"
  location = "eastus2"

  resource_tags = {
    iac = "terraform"
  }
}

module "log_analytics" {
  source = "git::https://github.com/danielscholl-terraform/module-log-analytics?ref=v1.0.0"

  name                = "iac-terraform-logs-${module.resource_group.random}"
  resource_group_name = module.resource_group.name

  solutions = [
    {
        solution_name = "ContainerInsights",
        publisher = "Microsoft",
        product = "OMSGallery/ContainerInsights",
    }
  ]

  # Tags
  resource_tags = {
    iac = "terraform"
  }
}
```


<!--- BEGIN_TF_DOCS --->
## Providers

| Name | Version |
|------|---------|
| azurerm | >= 2.90.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| name | The name of the Virtual Network. (Optional) - names override | `any` | n/a | yes |
| names | Names to be applied to resources (inclusive) | <pre>object({<br>    environment = string<br>    location    = string<br>    product     = string<br>  })</pre> | <pre>{<br>  "environment": "tf",<br>  "location": "eastus2",<br>  "product": "iac"<br>}</pre> | no |
| naming\_rules | naming conventions yaml file | `string` | `""` | no |
| resource\_group\_name | The name of an existing resource group. | `string` | n/a | yes |
| resource\_tags | Map of tags to apply to taggable resources in this module. By default the taggable resources are tagged with the name defined above and this map is merged in | `map(string)` | `{}` | no |
| retention\_in\_days | The workspace data retention in days. Between 30 and 730. | `number` | `30` | no |
| security\_center\_subscription | List of subscriptions this log analytics should collect data for. | `list(string)` | `[]` | no |
| sku | Sku of the Log Analytics Workspace. | `string` | `"PerGB2018"` | no |
| solutions | A list of solutions to add to the workspace. | `list(object({ solution_name = string, publisher = string, product = string }))` | `[]` | no |

## Outputs

| Name | Description |
|------|-------------|
| id | The Log Analytics Workspace Id |
| workspace\_id | n/a |
| workspace\_key | n/a |
<!--- END_TF_DOCS --->
