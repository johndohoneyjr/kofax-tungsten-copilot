# Homework: Moving Local Docker Container to Azure Container Registry (ACR) with GitHub Copilot

#### Prerequisites:
- Docker Desktop installed and running on your PC.
- Azure CLI installed on your PC. To install Azure CLI, visit the official Microsoft documentation and follow the instructions for Windows.
- An Azure subscription. If you don't have one, you can create a free account.
- Visual Studio Code with GitHub Copilot extension installed.

#### Step 1: Introduction to Azure Container Registry (ACR)
- **Objective:** Explain what ACR is and its benefits.
- **GitHub Copilot Prompt:** "Explain Azure Container Registry and its use cases."

#### Step 2: Installing Azure CLI on Windows
- **Objective:** Guide on installing Azure CLI.
- **GitHub Copilot Prompt:** "How to install Azure CLI on Windows."
- **Action:** Follow the instructions provided by Copilot to install Azure CLI.

```powershell
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process .\AzureCLI.msi
```

#### Step 3: Logging into Azure via Azure CLI
- **Objective:** Authenticate to Azure to perform operations.
- **GitHub Copilot Prompt:** "Log into Azure using Azure CLI."
- **Action:** Execute the Azure CLI command to log in.

```bash
az login --use-device-code
```

#### Step 4: Creating Azure Container Registry using ARM Template
- **Objective:** Use ARM template to create an ACR instance.
- **GitHub Copilot Prompt:** "Create an ARM template for Azure Container Registry."
- **Action:** Generate the ARM template and explain the need to change values like `location`.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "resources": [
    {
      "type": "Microsoft.ContainerRegistry/registries",
      "apiVersion": "2019-05-01",
      "name": "YourACRName",
      "location": "{location}",
      "sku": {
        "name": "Standard"
      },
      "properties": {
        "adminUserEnabled": true
      }
    }
  ]
}
```

- **Note:** Replace `{location}` with your desired Azure region, e.g., `westus` or `eastus`, and `YourACRName` with your unique ACR name.  For the following step, be sure to name this ARM template file: template.json.

#### Step 5: Deploying ARM Template
- **Objective:** Deploy the ARM template to Azure.
- **GitHub Copilot Prompt:** "Deploy ARM template using Azure CLI."
- **Action:** Use the following command to deploy the ARM template.

```bash
# Create Resoruce Group
az group create --name YourResourceGroupName --location `{location}`

az deployment group create --resource-group YourResourceGroupName --template-file path/to/your/template.json
```

#### Step 6: Pushing Docker Image to ACR
- **Objective:** Tag and push the Docker image to the newly created ACR.
- **GitHub Copilot Prompt:** "Push a Docker image to Azure Container Registry using Azure CLI."
- **Action:** Follow the steps provided by Copilot to tag your Docker image and push it to ACR.

```bash
# Log in to ACR
az acr login --name YourACRName

# Tag your Docker image
docker tag your-image:tag YourACRName.azurecr.io/your-image:tag

# Push the image to ACR
docker push YourACRName.azurecr.io/your-image:tag
```

#### Step 7: Conclusion and Cleanup
- **Objective:** Summarize what was accomplished and guide on cleaning up resources to avoid unnecessary charges.
- **GitHub Copilot Prompt:** "How to delete an Azure Container Registry using Azure CLI."
- **Action:** Provide the command to delete the ACR and remind students to also consider deleting other resources if they're no longer needed.

```bash
az acr delete --name YourACRName --resource-group YourResourceGroupName

# Delete the resource group
az group delete --name YourResourceGroupName --yes --no-wait
```

#### Additional Notes:
- Be sure to use GitHub Copilot for generating code snippets and solving problems.
- It is a good idea to replace placeholder values in commands and templates with actual values relevant to their Azure subscription and resources.
