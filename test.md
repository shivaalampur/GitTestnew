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
