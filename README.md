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

<!--- END_TF_DOCS --->
