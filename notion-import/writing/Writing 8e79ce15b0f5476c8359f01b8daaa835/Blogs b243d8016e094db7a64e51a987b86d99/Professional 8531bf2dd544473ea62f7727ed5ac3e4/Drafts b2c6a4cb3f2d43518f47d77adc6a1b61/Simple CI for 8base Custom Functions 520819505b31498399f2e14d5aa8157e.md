# Simple CI for 8base Custom Functions

One of 8base's most powerful features is the use of *Custom Functions.* They allow developers total flexibility for writing server(less) side code, whether it's for a simple GraphQL resolver or a data heavy scheduled reporting job. Put simply, custom functions extend the full power of Node.js  to your 8base workspace.

That said, deploying custom functions can get tricky when multiple developers are collaborating on a workspace. If all team members have *deploy* privileges, it's easy for one developer to accidentally overwrite another's work.

Because of this, we recommend that you set up a CI/CD script that handles the deployment of custom functions to a workspace. By doing so, you remove the risk of engineers overwriting each others work, as well as create a single source of truth for your most up-to-date code; the repository!

### Tutorial

In this tutorial, we're going to go over setting up a simple CI/CD script on GitHub using Actions. Additionally, we will configure the roles and permissions needed to allow automatic deployment, as well as protect developers from overwriting deployed code.

### Step 1. Setting up the Roles

The first role we're going to [create is the *Developer* role](https://docs.8base.com/docs/8base-console/roles-and-permissions#create-new-role). This is the role that you'll assign any existing and new developers when they are invited to your project workspace. 

While the permissions that you choose grant these developers may vary from workspace to workspace, ensure that the *Deploy* permission - found in the *Roles > Developer > APPS* tab - is unchecked. This will make sure that developers are unable to deploy custom functions directly to a workspace using the 8base CLI.

![Simple%20CI%20for%208base%20Custom%20Functions%20520819505b31498399f2e14d5aa8157e/Deploy-role-off.png](Deploy-role-off.png)

The second role we're going to create is the *GitHub_Deploy* role. This is the role that we'll assign to an API Token that gets stored securely in GitHub. 

For this role, ensure that the *Deploy* permission - found in the *Roles > GitHub_Deploy > APPS* tab - is checked. All other permissions can be turned off. This permission allows the CI/CD script to deploy custom functions.

![Simple%20CI%20for%208base%20Custom%20Functions%20520819505b31498399f2e14d5aa8157e/ci-role.png](ci-role.png)

### Step 2. Creating an API Token

Navigate over to *Settings > API Tokens* and [create a new API Token](https://docs.8base.com/docs/8base-console/roles-and-permissions/#api-tokens) called *GITHUB_DEPLOY_TOKEN*. While creating it, make sure to associate the *GitHub_Deploy* role that you just created.

The token generated can only be seen once. Make sure to copy and save it somewhere safe for the time being, or be ready to repeat this step later. Either way, this token is what we'll use to authenticate against the 8base API in our GitHub Action script.

![Simple%20CI%20for%208base%20Custom%20Functions%20520819505b31498399f2e14d5aa8157e/api-token.png](api-token.png)

### Step 3. GitHub Actions

GitHub Actions makes it easy to automate all your software workflows by leveraging CI/CD. With the following script, we're going to make sure that whenever a merge is made into the *master* branch of our repo, our updated project code gets deployed to 8base.

```yaml
name: 8base Deploy Custom Functions

on:
  push:
    branches:
      - master

env:
  EIGHT_BASE_API_TOKEN: ${{ secrets.EIGHT_BASE_API_TOKEN }}
  EIGHT_BASE_WORKSPACE_ID: ${{ secrets.EIGHT_BASE_WORKSPACE_ID }}
  CI: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Install 8base-cli
        run: sudo npm i -g 8base-cli

      - name: Deploy to 8base
        working-directory: ./server
        run: |
          8base login --token ${{ env.EIGHT_BASE_API_TOKEN }}
          8base configure --workspaceId ${{ env.EIGHT_BASE_WORKSPACE_ID }}
          8base deploy
```

The YAML code should be added to a file located at the path *.github/workflows/deploy.yml -* in relation to the root directory of your project. The *working-directory* key indicates that the 8base project code exists in a directory located at *./server -* which may change based on your own directory structuring. If you're *8base.yaml* is located at the\ root of your repo, remove the *working-directory option.*

### Step 4. Setting Secrets in GitHub

In order for the Action script to access required deploy credentials, we must set them in GitHub.

![Simple%20CI%20for%208base%20Custom%20Functions%20520819505b31498399f2e14d5aa8157e/Screen_Shot_2020-04-13_at_4.16.54_PM.png](Screen_Shot_2020-04-13_at_4.16.54_PM.png)

While in your project's repo on GitHub, navigate to *Settings > Secrets* and add a new secret. There are two different secrets we need to set.

1. EIGHT_BASE_WORKSPACE_ID - The ID of the 8base workspace to which you want your code to be deployed.
2. EIGHT_BASE_API_TOKEN - The API Token that was generate in step two.

Once these values are all set, go ahead and commit and push to GitHub all the changes that have been made to your custom functions!

### Wrap Up

On you're next merge or push into the remote master branch, GitHub will detect the newly added Action script. Should all steps have been successfully completed, you'll quickly see the script having successfully run and your code deployed.

![Simple%20CI%20for%208base%20Custom%20Functions%20520819505b31498399f2e14d5aa8157e/Screen_Shot_2020-04-13_at_4.22.11_PM.png](Screen_Shot_2020-04-13_at_4.22.11_PM.png)