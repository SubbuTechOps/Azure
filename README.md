### Key Steps for Azure CLI Introduction and Usage

#### 1. **Install Azure CLI**
   - Download and install Azure CLI from the official Microsoft page: [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).
   - Verify the installation:
     ```bash
     az --version
     ```

#### 2. **Log in to Azure**
   - To log in to your Azure account:
     ```bash
     az login
     ```
   - For headless environments or servers without a browser, use:
     ```bash
     az login --use-device-code
     ```
   - To log in to a specific tenant:
     ```bash
     az login --tenant <TENANT_ID>
     ```

#### 3. **List and Set Subscriptions**
   - View all subscriptions:
     ```bash
     az account list --output table
     ```
   - Set a specific subscription:
     ```bash
     az account set --subscription <SUBSCRIPTION_ID>
     ```

#### 4. **Create a Service Principal**
   - Create a Service Principal for automation purposes:
     ```bash
     az ad sp create-for-rbac --name "my-service-principal" --role Contributor --scopes /subscriptions/<SUBSCRIPTION_ID>
     ```
   - Save the generated `appId`, `password`, and `tenant` securely.

#### 5. **List Azure Resources**
   - View all resources in the active subscription:
     ```bash
     az resource list --output table
     ```

#### 6. **Manage Azure Virtual Machines**
   - Create a new Virtual Machine:
     ```bash
     az vm create \
       --resource-group <RESOURCE_GROUP> \
       --name <VM_NAME> \
       --image UbuntuLTS \
       --admin-username azureuser \
       --generate-ssh-keys
     ```
   - List all Virtual Machines:
     ```bash
     az vm list --output table
     ```
   - Start a Virtual Machine:
     ```bash
     az vm start --name <VM_NAME> --resource-group <RESOURCE_GROUP>
     ```
   - Stop a Virtual Machine:
     ```bash
     az vm stop --name <VM_NAME> --resource-group <RESOURCE_GROUP>
     ```

#### 7. **Create Azure Resources Using Terraform**
   - Use Terraform with Azure by configuring the provider:
     ```hcl
     provider "azurerm" {
       tenant_id       = "<TENANT_ID>"
       subscription_id = "<SUBSCRIPTION_ID>"
       client_id       = "<APP_ID>"
       client_secret   = "<PASSWORD>"
       features        {}
     }
     ```
   - Initialize Terraform:
     ```bash
     terraform init
     ```
   - Apply configurations:
     ```bash
     terraform apply
     ```

#### 8. **Reset or Retrieve Admin Credentials**
   - Reset admin username or password for a Virtual Machine:
     ```bash
     az vm user update \
       --resource-group <RESOURCE_GROUP> \
       --name <VM_NAME> \
       --username azureuser \
       --password <NEW_PASSWORD>
     ```

#### 9. **Enable Dynamic Extension Installation**
   - Automatically install missing extensions when using certain commands:
     ```bash
     az config set extension.use_dynamic_install=yes_without_prompt
     ```

#### 10. **Best Practices for Security**
   - Use Azure Key Vault to store sensitive credentials securely.
   - Avoid hardcoding secrets in scripts or Terraform files.
   - Use environment variables for credentials:
     ```bash
     export TF_VAR_admin_username="azureuser"
     export TF_VAR_admin_password="SecurePassword123!"
     ```

---

These steps provide a comprehensive guide for working with Azure CLI, creating and managing resources, and ensuring secure practices. Let me know if you need further details on any specific step!

