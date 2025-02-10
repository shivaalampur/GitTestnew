# Azure dev environment details
This document describes the tooling and dev environment decisions for the project and This document describes Azure dev environment details for the project and getting an access to the environment.

Tenant ID: a11959d0-ca0a-422e-80d3-b05cf9cafb22
Primary domain: MngEnvMCAP786396.onmicrosoft.com
License: Microsoft Entra ID P2

# Getting access to the environment:
1) Have someone from the team to create a new user account in the Azure Entra tenant a11959d0-ca0a-422e-80d3-b05cf9cafb22. 
The temporaray 
2) Get newly created alias added to the SG TardigradeTeam@MngEnvMCAP786396.onmicrosoft.com.

## Linting

The following lists the linting coverage we intend to use for the repository. The linters that run in the CI flow should be able to be run locally so a developer can
resolve linter errors before submitting a PR.

- markdown linting
  - local dev: [VS Code extension](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
  - CI: [GitHub action]

* **Option C):** Using SDK

  Language        |  SDK Name   | Document Link
  ---------------- | -------------- | -----------------------------------------------
  .NET          | azure-mgmt-resourcegraph       | [Document Link][DotNet]
  Python          | azure-mgmt-resourcegraph     | [Document Link][Python]
  Java            | azure-mgmt-resourcegraph     | [Document Link]()

  [DotNet]: https://learn.microsoft.com/en-us/dotnet/api/overview/azure/ResourceManager.ResourceGraph-readme?view=azure-dotnet
  [Python]: https://learn.microsoft.com/en-us/python/api/overview/azure/resource-graph?view=azure-python


## 1) Azure Resources

Item                    | Comment
--------------------    | -----------------------------------------------
Description             | To get a complete list of the resources in a tenant
Data type format        | It’s real time stream data available in a table format. It accepts Kusto queries to customize
Data refresh            | It is real time data available as soon as any new resources got created in Azure and get deleted when resource gets deleted from Azure.
Access Permissions      | Any user in a tenant able to read the data.
Data Retention          | ?
Data dictionary         | Yet to publish

**This section covers various data extraction methods based on data types.**

* **Option A):** Using "Azure Resource Graph explorer" in the Azure portal. Below is a sample query.

    ```kusto
    resources
    | extend Team = ['tags'].Team,
             Environment = ['tags'].Environment,
             Application = ['tags'].Application
    | project id, name, type, tenantId, kind, location, resourceGroup,
              subscriptionId, managedBy,  sku,  plan, properties, tags, identity,
              zones,  extendedLocation, Environment, Team, Application
    | where type != "microsoft.sql/servers/databases" and name != "master"
    | where ['type'] != "microsoft.compute/virtualmachines/extensions"
    ```

* **Option B):** Using API

  Document                       |  End point                   | Request Type
  ----------------               | --------------               | -------------------------------
  [Document Link][DocumentLink]  | [API link][ApiLink]          | POST

    [DocumentLink]: https://learn.microsoft.com/en-us/azure/governance/resource-graph/first-query-rest-api?tabs=powershell

    [APIlink]: https://management.azure.com/providers/Microsoft.ResourceGraph/resources?api-version=2022-10-01

    Request Body: Sample request body to get 5 resouces from resources table. Leave everything null get complete resouces list from tenant. Because Azure Resource Graph returns a maximum of 1,000 entries in a single query response, you might need to paginate your queries to get the complete dataset you want by passing skipToken in the query.

    ```json
        {
        "options": {  "skipToken": "<$skipToken value>" },
        "subscriptions": [
            "{subscriptionID}"
        ],
        "query": "Resources | limit 5"
        }


* **Option C):** Using SDK

  Language        |  SDK Name   | Document Link
  ---------------- | -------------- | -----------------------------------------------
  .NET          | azure-mgmt-resourcegraph       | [Document Link][DotNet]
  Python          | azure-mgmt-resourcegraph     | [Document Link][Python]
  Java            | azure-mgmt-resourcegraph     | [Document Link][Java]

  [DotNet]: https://learn.microsoft.com/en-us/dotnet/api/overview/azure/ResourceManager.ResourceGraph-readme?view=azure-dotnet

  [Python]: https://learn.microsoft.com/en-us/python/api/overview/azure/resource-graph?view=azure-python

  [Java]: https://learn.microsoft.com/en-us/python/api/overview/azure/resource-graph?view=azure-python
