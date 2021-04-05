---
title: "Run tests with robot framework on Azure Devops from zero to 1"
date: 2021-02-14T21:31:49+08:00
draft: true
---

### Tools

* [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/)
  * [Installing Required Azure DevOps Extensions](https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform)
* [Terrform CLI](https://www.terraform.io/)
* [Docker](https://www.docker.com/)

### Environment

We are going build three components for End to End testing environment on Azure DevOps

1. Pipelines
   1. Build robot-framework docker image for executing tests
   2. Execute test case with robot framework
2. Infrastructure - All services in end-to-end testing environment, include pipeline, repo, variables, agnet pool
   * Test Runner - The machine installed robot framework to execute test cases as container
   * Azure Container Registry - All test runners are managed by Azure Container Registry which managed by Microsoft

#### Pipelines



#### Test Runner

* Multiple test runner run as container within Azure Container Instances Group
  * [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)
  * [Docker registry service connections](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints?view=azure-devops#sep-docreg)
  * Tasks used in your pipeline to [build images](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/containers/build-image?view=azure-devops), [push images](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/containers/push-image?view=azure-devops)  
  * The template used to create your test runner: [docker-robot-framework](https://github.com/ppodgorsek/docker-robot-framework)
  * The template used to provision your test runner in Azure container Group: [terraform-azurerm-aci-devops-agent](https://github.com/Azure/terraform-azurerm-aci-devops-agent/)
* Execute sample test cases in pipeline to choose one test runner from Azure agent pool

### Troubleshoot

1. Build your docker iamge on local machine

```bash
docker build -t="latest" .
```

2. Run 