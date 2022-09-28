# How it's Built? 8base Architecture

Created: December 23, 2019 10:43 AM

### 8base Layers

8base has a fairly simple structure. It is comprised of three primary layers. Every other service and features is an integration, some of which are more natively supported than others (Authentication, Roles and Permissions).

1. **API Gateway (+ websockets)**
    
    In tandem with setting up the unique API endpoint on which the GraphQL Engine gets mounted, we also configure [Lambda Websockets](https://aws.amazon.com/blogs/compute/announcing-websocket-apis-in-amazon-api-gateway/) by default and handle the provisioning of webhook routes that get mapped to deployed [custom webhook functions](https://docs.8base.com/docs/8base-console/custom-functions/webhooks/) (Lambdas). 
    
2. **Lambda (+ Mongo, Redis)**
    
    Workspace Schema's get stored in Mongo. These workspace specific data schemas get fetched and used to interpret the GraphQL queries. We use a managed MongoDB service ([cloud.mongodb.com](https://cloud.mongodb.com)).
    
    We use managed Redis service ([redislabs.com](https://redislabs.com)) for internal use; tasks like caching permissions, models, parts of schema, etc.
    
    **We do not do any caching of data. Data is never persisted anywhere other than the original data source (8base Database, Salesforce, external DB, etc.)**
    
    For relations between tables and ones in different systems (i.e. a table in 8base with a relationship to a table in an external database), we only store record IDs on join tables.
    
    The GraphQL schema gets cached in an LRU cache, which drives the GraphQL engine in every Lambda call.
    
3. **Aurora MySQL 5.7.+**
    
    [Disaster recovery policy](https://aws.amazon.com/blogs/database/implementing-a-disaster-recovery-strategy-with-amazon-rds/) - 8base adopts full AWS backup policy for Aurora.
    
    Database cluster with 2 instances (read and write)
    
    A separate database is generated for every single workspace. Additionally, 8base generates unique connection credentials that get encrypted and stored in encrypt. This in-forces an un-breach-able scope to user's specific database.
    

### Disaster Recovery

Full automated deployment - 8base's full cloud infrastructure is automatically deployed to AWS using Terraform. If at any point, the worst case scenario took place, our full operating infrastructure could be re-provisions in approximately 1-hour.

All databases are backed up twice a day and complete transaction logs are kept to ensure that any database could be restored to a specific point in time, if needed. By default, these backups (database's and logs) are stored by 8base for 7-days rolling.

### CI/CD

8base uses GitLab CI with branch specific testing and deployment scripts. Only one employee at the company, our VP of Technology, has the credentials required to deploy changes to our production AWS environment(s).

**Branch CI/CD Flows**

1. Master (ci/cd, serverless → aws staging)
2. Prestaging (ci/cd, serverless → aws prestaging)
3. tag (ci/cd, serverless → aws production) - for production deployment

### Extra Information (AWS Provisioning)

Our infrastructure is fully provisioned using Terraform (multiple environments): (

- Testing
- Production
- Staging
- QA
- Production

)

Using Serverless framework 8base provisions the managed Lambdas that enable the GraphQL API: (

- Sets up our special Lamba functions (Gql)

)

A custom specification (similar to Serverless framework) was developed for deploying custom function: (

- Subset of Serverless that deals directly with the AWS API

)

```
// Evgeny's notes
Main AWS account (Billing set-up, initial config)
Terraform: 
(Testing
Prestaging,
Staging
QA
Production)
master (ci/cd, serverless -> aws staging)
prestaging (ci/cd, serverless -> aws prestaging)
tag (ci/cd, serverless -> aws production)
User's deploy:
Salesforce table with 8base
salesforceRecordId - 8baseRecordId
Api gateway ( + ws )
   |
lambda (Mongo, Redis) - out VPC -> to VPC in next couple of month
   |
Aurora MySql 5.7.+ 
DB cluster with 2 instances (read and write)
Separate DB for every single workspace, +  we generate unique connection credentations (encrypt) scoped to a user's database
```