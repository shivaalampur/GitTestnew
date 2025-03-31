# Data Security

Purpose of this document is to record all initial assumptions and constraints of the data security which will be helpful in capturing current decisions and make changes as we progress.

## Access

### Authentication and Authorization

Access to the application endpoints as like data store, UI, API and Analytics resources are protected with two factor authentication. Since this is a test environment all users in the team have persistent privileged access. This can be changed to least privileged role something like reader and just in time for privileged roles(owner, contributor, user access administrator) as needed. Access to the environment is managed through centralized security group.

  End point                                                             | Type                 | Authentication    | Authorization | Public access | Application Access
  ----------------------------------------------------------------------|----------------------|-------------------|---------------|---------------|--------------------
  [i43-cosmos-account-dev][i43-cosmos-account-dev-link]                      | Cosmos               | Two factor        | Owner         | Enabled       | NA
  [i43-ui-bgezdqgmb6c4bcc3][i43-ui-bgezdqgmb6c4bcc3-link]                    | Web APP              | Two factor        | Owner         | Disabled      | Two factor
  [i43-backend-api-efcfeaekbkacecgz][i43-backend-api-efcfeaekbkacecgz-link]  | Web APP              | Two factor        | Owner         | Disabled      | NA
  [i43-function-test][i43-function-test-link]                                | Function APP         | Two factor        | Owner         | Enabled       | NA
  [i43-synapse-workspace-dev][i43-synapse-workspace-dev-test]                | Synapse Analytics    | Two factor        | Owner         | Enabled       | NA

  [i43-cosmos-account-dev-link]: (https://i43-cosmos-account-dev.documents.azure.com:443/)  
  [i43-ui-bgezdqgmb6c4bcc3-link]: (https://i43-ui-bgezdqgmb6c4bcc3.westus2-01.azurewebsites.net)
  [i43-backend-api-efcfeaekbkacecgz-link]: (https://i43-backend-api-efcfeaekbkacecgz.westus2-01.azurewebsites.net)
  [i43-function-test-link]: (http://i43-function-test.azurewebsites.net)
  [i43-synapse-workspace-dev-test]: (https://web.azuresynapse.net?workspace=%2fsubscriptions%2fdf4684a9-d351-48e7-962b-597374e2ba67%2fresourceGroups%2frg-i43-infra-dev%2fproviders%2fMicrosoft.Synapse%2fworkspaces%2fi43-synapse-workspace-dev)
  
### System access

Secrets are considered to be most vulnerable for attacks. The preferred option is to use managed identity wherever possible to avoid secrets. If there are any limitations to making use of MI, other alternative solutions will be considered. When secrets are being used, they need be consumed through Key vault or GitHub secrets. Hard coding secrets in configuration or code is not a best practice.

1. Managed identity(user or system)
2. Federated credentials
3. App registrations

### Public access

Access to the end points can be restricted to the certain IP ranges or open to public or completely closed. Right now public access is enabled on some of the resources which can be changed once we decide on the network architecture approach of C42.

## Compliance

### Backup

No backups are enabled on the databases. This needs to be discussed and enable backup to meet C42 compliance requirements.

### Business continuity and disaster recovery

BCDR(Business continuity and disaster recovery) talks about how sooner the application needs to be back to normal working condition to avoid monitory/legal/brand impact. There are to key decisions to make to design the application to meet the compliance requirement. C42 to make this decisions as we progress.

1. Recovery Time Objective: what is the maximum amount of time I can afford to have application unavailable.
2. Recovery Point Objective: how much data can I lose before it negatively affect my organization.

### Data retention

This is not in place at this time. We have to come up with a logic to implement retention based on the input from C42

### Privacy

Some of our data sets contain PII data something like user full names, IP addresses, email, etc. Since these solutions are being consumed by CISO and InfoSec teams, needs an advice from C42 team on what level data can be extracted and stored. Based on the decision we can look for options of data redaction or masking.

### Secret management

Secret being used in the application needs to be rotated periodically. This needs to be assigned with C42 secret management policies.

### Access review

Periodic access review to the application and resources should be established

## Encryption

### Encrypt data at rest

Cosmos, storage, synapse provide default encryption at rest. If there are any additional compliance requirements from C42 this can be explored.

### Encrypt data in transit

All data sources, UI, API and Analytics supports encryption in transit with the TLS version (1.2 commonly) and Azure default certificate. If there are any requirement to encrypt data with C42 certificate that can be explored.
