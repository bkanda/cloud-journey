# Azure-ServiceBus

This template helps us creating the following Azure Service Bus resources in a single deployment

* Namespace
* Array of Queues
* Array of Topics
* Array of Subscription
* Authrule for client connectivity

### We could also automate this deployment with the given DevOps pipeline

### Azure Devops pipeline yaml:

<details><summary>pipeline.yaml</summary>
<p>

#### Azure Devops Pipeline Yaml

```
trigger:
- none

parameters:
- name: RGName
  displayName: Resource Group Name
  type: string
- name: location
  displayName: Resource location
  type: string
  default: northeurope 

stages:
- stage: deployment
  displayName: deploy ARM template for Service Bus
  jobs:
  - deployment: deployment
    displayName: deploy ARM template for Service Bus
    pool:
      vmImage: ubuntu-latest
    environment: deployment
    strategy:
      runOnce:
        deploy:
          steps:
          - checkout: self
          - task: AzureCLI@2
            inputs:
              azureSubscription: 'sb-sandbox'
              scriptType: 'bash'
              scriptLocation: 'scriptPath'
              scriptPath: 'servicebus/arm-templates/deploy.sh'
              arguments: '-g ${{ parameters.RGName }} -n Service-Bus -l ${{ parameters.location }}'

```
</p>
</details>

## Create a Service Bus Namespace, Queues and Topics with Subscriptions

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDigitalInnovation%2Fcloudintegration-templates%2Fazure-pipelines%2Fservicebus%2Farm-templates%2Fsb.deploy.json%3Ftoken%3DAHLGVIQFTZKWSQZTQLTUBSLAF25RQ)


For information about using this template, see [Create a Service Bus namespace using an ARM template](http://azure.microsoft.com/documentation/articles/service-bus-resource-manager-namespace/).
