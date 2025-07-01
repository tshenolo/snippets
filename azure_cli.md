# Azure CLI Cheatsheet

The Azure Command-Line Interface (CLI) is a set of commands used to create and manage Azure resources.

## Installation and Setup

*   **Install Azure CLI**: Follow official Microsoft documentation for your OS: [https://docs.microsoft.com/cli/azure/install-azure-cli](https://docs.microsoft.com/cli/azure/install-azure-cli)
*   **Login**:
    *   Interactive login (opens a browser):
        ```bash
        az login
        ```
    *   Login with a service principal (for automation):
        ```bash
        az login --service-principal -u <APP_ID_OR_NAME> -p <PASSWORD_OR_CERT> --tenant <TENANT_ID_OR_NAME>
        # Example:
        # az login --service-principal -u "http://my-app-sp" -p "mySecurePassword" --tenant "mytenant.onmicrosoft.com"
        ```
    *   Login with a managed identity (when running on an Azure resource like a VM):
        ```bash
        az login --identity
        ```
*   **List accounts and set active subscription**:
    *   List all subscriptions you have access to:
        ```bash
        az account list --output table # or --output json
        ```
    *   Show current active subscription:
        ```bash
        az account show --output table
        ```
    *   Set a specific subscription to be active:
        ```bash
        az account set --subscription "<SUBSCRIPTION_NAME_OR_ID>"
        # Example:
        # az account set --subscription "My Dev Subscription"
        ```
*   **Get help**:
    ```bash
    az --help
    az <group> --help # e.g., az vm --help
    az <group> <command> --help # e.g., az vm create --help
    ```
*   **Configure defaults** (e.g., default resource group, location):
    ```bash
    az configure --defaults group=<DEFAULT_RESOURCE_GROUP_NAME> location=<DEFAULT_LOCATION>
    # Example:
    # az configure --defaults group=MyWebAppResources location=eastus
    ```
    View current configuration:
    ```bash
    az configure --list-defaults
    ```

## Resource Groups

Resource groups are containers that hold related resources for an Azure solution.

*   **Create a resource group**:
    ```bash
    az group create --name <RESOURCE_GROUP_NAME> --location <LOCATION>
    # Example:
    # az group create --name MyWebAppRG --location eastus
    ```
*   **List resource groups**:
    ```bash
    az group list --output table
    ```
*   **Show details of a resource group**:
    ```bash
    az group show --name <RESOURCE_GROUP_NAME>
    ```
*   **Delete a resource group** (deletes all resources within it - use with caution!):
    ```bash
    az group delete --name <RESOURCE_GROUP_NAME> --yes --no-wait
    # --yes: Do not prompt for confirmation.
    # --no-wait: Do not wait for the long-running operation to finish.
    ```
*   **Check if a resource group exists**:
    ```bash
    az group exists --name <RESOURCE_GROUP_NAME> # Returns true or false
    ```

## Virtual Machines (VMs)

*   **List available VM images**:
    ```bash
    az vm image list --output table
    az vm image list --publisher Canonical --offer UbuntuServer --sku 18.04-LTS --all --output table
    ```
*   **List available VM sizes for a location**:
    ```bash
    az vm list-sizes --location <LOCATION> --output table
    # Example:
    # az vm list-sizes --location eastus --output table
    ```
*   **Create a Linux VM**:
    ```bash
    az vm create \
        --resource-group <RESOURCE_GROUP_NAME> \
        --name <VM_NAME> \
        --image UbuntuLTS \
        --admin-username <ADMIN_USERNAME> \
        --generate-ssh-keys # Or use --ssh-key-values /path/to/public_key.pub
    # Example:
    # az vm create --resource-group MyVMsRG --name MyLinuxVM1 --image UbuntuLTS --admin-username azureuser --generate-ssh-keys --size Standard_DS1_v2
    ```
*   **Create a Windows VM**:
    ```bash
    az vm create \
        --resource-group <RESOURCE_GROUP_NAME> \
        --name <VM_NAME> \
        --image Win2019Datacenter \
        --admin-username <ADMIN_USERNAME> \
        --admin-password "<ADMIN_PASSWORD>" # Ensure strong password
    # Example:
    # az vm create --resource-group MyVMsRG --name MyWinVM1 --image Win2019Datacenter --admin-username azureadmin --admin-password "P@$$wOrd123!"
    ```
*   **List VMs in a resource group**:
    ```bash
    az vm list --resource-group <RESOURCE_GROUP_NAME> --output table
    ```
*   **Show details of a VM**:
    ```bash
    az vm show --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME> --show-details
    ```
*   **Start a VM**:
    ```bash
    az vm start --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME>
    ```
*   **Stop a VM** (keeps resources provisioned, continues to incur compute costs for some resources):
    ```bash
    az vm stop --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME>
    ```
*   **Deallocate a VM** (stops the VM and releases compute resources, stopping compute charges):
    ```bash
    az vm deallocate --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME>
    ```
*   **Restart a VM**:
    ```bash
    az vm restart --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME>
    ```
*   **Delete a VM** (deletes the VM but associated resources like disks, NICs might remain unless specified):
    ```bash
    az vm delete --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME> --yes
    # To delete associated OS disk, NIC, and Public IP:
    # az vm delete --resource-group MyRG --name MyVM --delete-os-disk --delete-nics --delete-public-ips --yes
    ```
*   **Open a port on a VM** (modifies Network Security Group - NSG):
    ```bash
    az vm open-port --port <PORT_NUMBER> --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME> --priority <PRIORITY_NUMBER>
    # Example:
    # az vm open-port --port 80 --resource-group MyVMsRG --name MyLinuxVM1 --priority 100
    ```
*   **Connect to a VM via SSH** (gets public IP and initiates SSH):
    ```bash
    az ssh vm --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME> --local-user <ADMIN_USERNAME>
    # Example:
    # az ssh vm -g MyVMsRG -n MyLinuxVM1 --local-user azureuser
    ```
*   **Run a command on a VM** (uses Run Command feature):
    ```bash
    az vm run-command invoke --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME> --command-id RunShellScript --scripts "ls -l /tmp"
    # For Windows: --command-id RunPowerShellScript --scripts "Get-Process"
    ```
*   **Resize a VM**:
    ```bash
    az vm resize --resource-group <RESOURCE_GROUP_NAME> --name <VM_NAME> --size <NEW_VM_SIZE>
    # Example:
    # az vm resize --resource-group MyVMsRG --name MyLinuxVM1 --size Standard_D2s_v3
    ```

## Storage Accounts

*   **List storage account SKUs**:
    ```bash
    az storage account list-skus --location <LOCATION> --output table
    ```
*   **Create a storage account**:
    ```bash
    az storage account create \
        --name <STORAGE_ACCOUNT_NAME> \
        --resource-group <RESOURCE_GROUP_NAME> \
        --location <LOCATION> \
        --sku Standard_LRS \
        --kind StorageV2 # General-purpose v2 account
    # Example:
    # az storage account create --name mystorageapp123 --resource-group MyStorageRG --location eastus --sku Standard_LRS --kind StorageV2
    ```
*   **List storage accounts**:
    ```bash
    az storage account list --resource-group <RESOURCE_GROUP_NAME> --output table
    ```
*   **Show storage account connection string**:
    ```bash
    az storage account show-connection-string --name <STORAGE_ACCOUNT_NAME> --resource-group <RESOURCE_GROUP_NAME> --output tsv
    ```
*   **Manage storage account keys**:
    ```bash
    az storage account keys list --account-name <STORAGE_ACCOUNT_NAME> --resource-group <RESOURCE_GROUP_NAME> --output table
    az storage account keys renew --account-name <STORAGE_ACCOUNT_NAME> --resource-group <RESOURCE_GROUP_NAME> --key primary --output table
    ```

### Storage Blobs (requires connection string or account key/name)

Set environment variables for convenience:
`export AZURE_STORAGE_ACCOUNT="<your_storage_account_name>"`
`export AZURE_STORAGE_KEY="<your_storage_account_key>"`
OR
`export AZURE_STORAGE_CONNECTION_STRING="<your_connection_string>"`

*   **Create a blob container**:
    ```bash
    az storage container create --name <CONTAINER_NAME>
    # Example:
    # az storage container create --name myblobcontainer --account-name mystorageapp123
    ```
*   **List blob containers**:
    ```bash
    az storage container list --output table
    ```
*   **Upload a blob**:
    ```bash
    az storage blob upload --container-name <CONTAINER_NAME> --file </path/to/local/file> --name <BLOB_NAME>
    # Example:
    # az storage blob upload --container-name myblobcontainer --file ./image.jpg --name images/image.jpg
    ```
*   **List blobs in a container**:
    ```bash
    az storage blob list --container-name <CONTAINER_NAME> --output table
    ```
*   **Download a blob**:
    ```bash
    az storage blob download --container-name <CONTAINER_NAME> --name <BLOB_NAME> --file </path/to/local/destination>
    # Example:
    # az storage blob download --container-name myblobcontainer --name images/image.jpg --file ./downloaded_image.jpg
    ```
*   **Delete a blob**:
    ```bash
    az storage blob delete --container-name <CONTAINER_NAME> --name <BLOB_NAME>
    ```
*   **Generate SAS token for a blob**:
    ```bash
    az storage blob generate-sas --container-name <CONTAINER_NAME> --name <BLOB_NAME> --permissions r --expiry <YYYY-MM-DDTHH:MM:SSZ> --output tsv
    # Permissions: r (read), w (write), d (delete), l (list), a (add), c (create), u (update)
    ```

## App Service (Web Apps, Function Apps, Logic Apps)

*   **Create an App Service Plan** (defines region, size, features for web apps):
    ```bash
    az appservice plan create \
        --name <APP_SERVICE_PLAN_NAME> \
        --resource-group <RESOURCE_GROUP_NAME> \
        --sku <SKU_NAME> # e.g., B1 (Basic), S1 (Standard), P1V2 (Premium V2), F1 (Free)
    # Example:
    # az appservice plan create --name MyWebAppPlan --resource-group MyWebAppRG --sku B1 --is-linux # For Linux apps
    ```
*   **List App Service Plans**:
    ```bash
    az appservice plan list --output table
    ```
*   **Create a Web App**:
    ```bash
    az webapp create \
        --name <UNIQUE_WEBAPP_NAME> \
        --resource-group <RESOURCE_GROUP_NAME> \
        --plan <APP_SERVICE_PLAN_NAME> \
        --runtime "<RUNTIME_STACK>" # e.g., "NODE|16-LTS", "PYTHON|3.9", "DOTNETCORE|6.0", "PHP|8.0"
    # Example for a Node.js app on Linux:
    # az webapp create --name myuniqueappname123 --resource-group MyWebAppRG --plan MyWebAppPlan --runtime "NODE|16-LTS"
    ```
*   **List Web Apps**:
    ```bash
    az webapp list --resource-group <RESOURCE_GROUP_NAME> --output table
    ```
*   **Deploy to Web App using Zip Deploy**:
    ```bash
    # First, package your application code into a zip file (e.g., myapp.zip)
    az webapp deployment source config-zip \
        --name <WEBAPP_NAME> \
        --resource-group <RESOURCE_GROUP_NAME> \
        --src </path/to/your/app.zip>
    ```
*   **Configure Web App settings (e.g., environment variables)**:
    ```bash
    az webapp config appsettings set --name <WEBAPP_NAME> --resource-group <RESOURCE_GROUP_NAME> --settings Name1=Value1 Name2=Value2
    # Example:
    # az webapp config appsettings set -n myuniqueappname123 -g MyWebAppRG --settings API_ENDPOINT="https://api.example.com" DB_USER="appuser"
    ```
*   **Browse to a Web App**:
    ```bash
    az webapp browse --name <WEBAPP_NAME> --resource-group <RESOURCE_GROUP_NAME>
    ```
*   **View Web App logs (streaming)**:
    ```bash
    az webapp log tail --name <WEBAPP_NAME> --resource-group <RESOURCE_GROUP_NAME>
    ```
*   **Restart a Web App**:
    ```bash
    az webapp restart --name <WEBAPP_NAME> --resource-group <RESOURCE_GROUP_NAME>
    ```

## Azure Kubernetes Service (AKS)

*   **Create an AKS cluster**:
    ```bash
    az aks create \
        --resource-group <RESOURCE_GROUP_NAME> \
        --name <AKS_CLUSTER_NAME> \
        --node-count <NUMBER_OF_NODES> \
        --enable-addons monitoring \
        --generate-ssh-keys
    # Example:
    # az aks create --resource-group MyAKS_RG --name MyManagedCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys --location eastus
    ```
*   **Get credentials for an AKS cluster** (configures `kubectl`):
    ```bash
    az aks get-credentials --resource-group <RESOURCE_GROUP_NAME> --name <AKS_CLUSTER_NAME> [--admin]
    # --admin for cluster admin credentials (use with care)
    ```
*   **List AKS clusters**:
    ```bash
    az aks list --resource-group <RESOURCE_GROUP_NAME> --output table
    ```
*   **Scale an AKS cluster (node count)**:
    ```bash
    az aks scale --resource-group <RESOURCE_GROUP_NAME> --name <AKS_CLUSTER_NAME> --node-count <NEW_NODE_COUNT>
    ```
*   **Upgrade an AKS cluster's Kubernetes version**:
    ```bash
    # First, get available upgrade versions:
    # az aks get-upgrades --resource-group <RG_NAME> --name <AKS_NAME> --output table
    az aks upgrade --resource-group <RESOURCE_GROUP_NAME> --name <AKS_CLUSTER_NAME> --kubernetes-version <NEW_K8S_VERSION>
    ```
*   **Delete an AKS cluster**:
    ```bash
    az aks delete --resource-group <RESOURCE_GROUP_NAME> --name <AKS_CLUSTER_NAME> --yes --no-wait
    ```

## Azure SQL Database

*   **Create an Azure SQL Server** (logical server):
    ```bash
    az sql server create \
        --name <SQL_SERVER_NAME> \
        --resource-group <RESOURCE_GROUP_NAME> \
        --location <LOCATION> \
        --admin-user <ADMIN_USERNAME> \
        --admin-password "<ADMIN_PASSWORD>"
    ```
*   **Create a SQL Database**:
    ```bash
    az sql db create \
        --resource-group <RESOURCE_GROUP_NAME> \
        --server <SQL_SERVER_NAME> \
        --name <DATABASE_NAME> \
        --service-objective S0 # Example service tier (e.g., S0, P1, GP_Gen5_2)
    ```
*   **Configure firewall rule for SQL Server** (e.g., to allow your client IP):
    ```bash
    # To allow access from Azure services:
    # az sql server firewall-rule create --resource-group <RG_NAME> --server <SERVER_NAME> --name AllowAllWindowsAzureIps --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
    # To allow a specific client IP:
    az sql server firewall-rule create \
        --resource-group <RESOURCE_GROUP_NAME> \
        --server <SQL_SERVER_NAME> \
        --name <RULE_NAME> \
        --start-ip-address <YOUR_CLIENT_IP> \
        --end-ip-address <YOUR_CLIENT_IP>
    ```

## Output Formats and Querying

*   **Output Formats (`--output` or `-o`)**:
    *   `json` (default, good for scripting)
    *   `jsonc` (colorized JSON)
    *   `table` (human-readable ASCII table)
    *   `tsv` (tab-separated values, no headers)
    *   `yaml`
    *   `none` (no output)
*   **Querying output with JMESPath (`--query`)**:
    ```bash
    az vm list --query "[].{Name:name, OS:storageProfile.osDisk.osType, Location:location}" --output table
    az storage account list --query "[?location=='eastus'].name" --output tsv
    ```

This provides a solid, actionable cheatsheet for the Azure CLI. Next, I'll work on `gcloud_cli.md`.The `azure_cli.md` cheatsheet has been successfully updated with detailed command examples for various Azure services like Resource Groups, VMs, Storage, App Service, AKS, and SQL Database, along with notes on output formatting and querying.

Next, I will enhance `gcloud_cli.md` in a similar fashion, focusing on `gcloud` commands for managing Google Cloud Platform resources.
