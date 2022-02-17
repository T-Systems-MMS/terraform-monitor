<!-- BEGIN_TF_DOCS -->
# monitor

This module manages Azure Monitor and Diagnostic.

<-- This file is autogenerated, please do not change. -->

## Requirements

| Name | Version |
|------|---------|
| terraform | >=1.0 |
| azurerm | >=2.79 |

## Providers

| Name | Version |
|------|---------|
| azurerm | >=2.79 |

## Resources

| Name | Type |
|------|------|
| azurerm_monitor_diagnostic_setting.monitor_diagnostic_setting | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| monitor_diagnostic_setting | resource definition, default settings are defined within locals and merged with var settings | `any` | `{}` | no |



## Examples

```hcl
module "monitor" {
  source = "registry.terraform.io/T-Systems-MMS/monitor/azurerm"
  monitor_diagnostic_setting = {
    virtual_network.name = {
      target_resource_id         = virtual_network.id
      log_analytics_workspace_id = data.azurerm_log_analytics_workspace.log_analytics_workspace.id
      metric = {
        category = ["AllMetrics"]
        enabled  = true
        retention_policy = {
          days    = 30
          enabled = true
        }
      }
    }
    frontdoor.name = {
      target_resource_id         = frontdoor.id
      log_analytics_workspace_id = data.azurerm_log_analytics_workspace.log_analytics_workspace.id
      log = {
        category = ["FrontdoorWebApplicationFirewallLog"]
        enabled  = true
        retention_policy = {
          days    = 30
          enabled = true
        }
      }
      metric = {
        category = ["AllMetrics"]
        enabled  = true
        retention_policy = {
          days    = 30
          enabled = true
        }
      }
    }
  }
}
```
<!-- END_TF_DOCS -->