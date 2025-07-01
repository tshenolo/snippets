# Azure CLI Cheatsheet

*   **Purpose**: Command-line interface for managing Azure resources.
*   **Installation**: Available for Windows, macOS, Linux.
*   **Login**: `az login` (interactive) or `az login --service-principal -u APP_ID -p PASSWORD --tenant TENANT_ID`.
*   **Core Syntax**: `az <group> <subgroup> <command> --parameters`.
*   **Common Groups and Commands**:
    *   Account Management: `az account set --subscription <id>`, `az account list`.
    *   Resource Groups: `az group create --name MyResourceGroup --location eastus`, `az group list`, `az group delete`.
    *   Virtual Machines (VMs):
        *   `az vm create --resource-group MyRG --name MyVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys`
        *   `az vm list`, `az vm show`, `az vm start`, `az vm stop`, `az vm deallocate`, `az vm delete`.
    *   Storage:
        *   `az storage account create --name mystorageaccount --resource-group MyRG --location eastus --sku Standard_LRS`
        *   `az storage blob upload --account-name mystorageaccount --container-name mycontainer --name myfile.txt --file myfile.txt`
    *   App Service (Web Apps):
        *   `az appservice plan create --name MyPlan --resource-group MyRG --sku B1`
        *   `az webapp create --resource-group MyRG --plan MyPlan --name MyUniqueWebAppName --runtime "NODE|16-LTS"`
    *   Azure Kubernetes Service (AKS):
        *   `az aks create --resource-group MyRG --name MyAKSCluster --node-count 1 --generate-ssh-keys`
        *   `az aks get-credentials --resource-group MyRG --name MyAKSCluster`
    *   Azure SQL Database: `az sql server create`, `az sql db create`.
    *   Networking (VNet, Subnet, NSG): `az network vnet create`, `az network nsg create`.
*   **Parameters**: `--name`, `--resource-group`, `--location`, `--sku`, specific options for each command.
*   **Output Formats**: `--output json` (default), `table`, `tsv`, `yaml`.
*   **Querying Output**: `--query` (uses JMESPath query language, e.g., `az vm list --query "[?location=='eastus'].name"`).
*   **Scripting**: Use in Bash, PowerShell, or other scripting languages.
*   **Authentication**: Interactive, service principal, managed identity.
