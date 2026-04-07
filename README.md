## Step For Run Pipeline using Azure CLI

#### Step 1: Install Azure CLI
     az --version

#### Step 2: Install Azure DevOps Extension
     az extension add --name azure-devops

#### Step 3: Login
     az login

##### Step 4: Set Defaults (Important)
    az devops configure --defaults \
      organization=https://dev.azure.com/YOUR_ORG \
      project=YOUR_PROJECT


##### Step 5: Run Pipeline from CMD
     az pipelines run --name "My Python Pipeline"

##### OR using pipeline ID:
     az pipelines run --id 

#### Pass Variables (Optional)
    az pipelines run \
      --name "My Python Pipeline" \
      --variables appName=my-app env=prod


##### Check Pipeline Status
    az pipelines runs list
    az pipelines runs show --id <run-id>

### Method 2: Using Python Script (API Trigger)

~~~
If you want to run pipeline via Python:

import requests
from requests.auth import HTTPBasicAuth

organization = "your_org"
project = "your_project"
pipeline_id = 1
pat = "YOUR_PAT"

url = f"https://dev.azure.com/{organization}/{project}/_apis/pipelines/{pipeline_id}/runs?api-version=7.0"

response = requests.post(
    url,
    auth=HTTPBasicAuth('', pat)
)

print(response.json())

~~~

### Method 3: Using cURL (Pure CMD)
    curl -u :YOUR_PAT \
     -X POST \
     -H "Content-Type: application/json" \
    https://dev.azure.com/YOUR_ORG/YOUR_PROJECT/_apis/pipelines/1/runs?api-version=7.0
