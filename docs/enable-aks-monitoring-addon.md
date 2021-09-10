# Enable AKS Monitoring Addon using Azure Policy

In most enterprises collecting logs centrally allows a single pane for performing complaince checks on Cloud infrastructure and applications hosted on these infrastructure. AKS Monitoring Addon can integrate AKS cluster with an existing Log Analytics workspace centrally managed in a different subscription. But, this requires the deployer to have required role permissions on the Log Analytics workspace resource. 

This guide covers the approach to enable AKS Monitoring Addon using Azure Custom Policy. AKS Monitoring Addon require following roles on the managed identity used by Azure Policy:

- [azure-kubernetes-service-contributor-role](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-contributor-role)
- [log-analytics-contributor](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor)

