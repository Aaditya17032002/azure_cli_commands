# Azure CLI Commands for Virtual Machines and Storage Accounts

## Prerequisite: Login to Azure
az login

# -----------------------------------
# Virtual Machine (VM) Commands
# -----------------------------------

## Create a Resource Group
az group create --name MyResourceGroup --location eastus

## Create a Virtual Machine
az vm create \
  --resource-group MyResourceGroup \
  --name MyVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys

## List all VMs in a Resource Group
az vm list --resource-group MyResourceGroup --output table

## Start a VM
az vm start --resource-group MyResourceGroup --name MyVM

## Stop a VM
az vm stop --resource-group MyResourceGroup --name MyVM

## Open Port (e.g., 80 for HTTP)
az vm open-port --port 80 --resource-group MyResourceGroup --name MyVM

## Delete a VM
az vm delete --resource-group MyResourceGroup --name MyVM --yes

## View VM Public IP
az vm list-ip-addresses --resource-group MyResourceGroup --name MyVM --output table

## Restart a VM
az vm restart --resource-group MyResourceGroup --name MyVM

## Resize a VM
az vm resize --resource-group MyResourceGroup --name MyVM --size Standard_DS2_v2

## Show VM Information
az vm show --resource-group MyResourceGroup --name MyVM --show-details --output json

## Deallocate a VM (stop but keep resources)
az vm deallocate --resource-group MyResourceGroup --name MyVM

## List Available VM Sizes in a Region
az vm list-sizes --location eastus --output table

## Attach a Data Disk to a VM
az vm disk attach \
  --resource-group MyResourceGroup \
  --vm-name MyVM \
  --name myDataDisk \
  --size-gb 10

## Detach a Data Disk from a VM
az vm disk detach --resource-group MyResourceGroup --vm-name MyVM --name myDataDisk

# -----------------------------------
# Azure Storage Account Commands
# -----------------------------------

## Create a Storage Account
az storage account create \
  --name mystorageaccount \
  --resource-group MyResourceGroup \
  --location eastus \
  --sku Standard_LRS

## List Storage Accounts
az storage account list --resource-group MyResourceGroup --output table

## Show Storage Account Details
az storage account show --name mystorageaccount --resource-group MyResourceGroup --output json

## Delete a Storage Account
az storage account delete --name mystorageaccount --resource-group MyResourceGroup --yes

# -----------------------------------
# Blob Storage Commands
# -----------------------------------

## Create a Blob Container
az storage container create \
  --name mycontainer \
  --account-name mystorageaccount

## Upload a File to Blob Storage
az storage blob upload \
  --container-name mycontainer \
  --name myfile.txt \
  --file /path/to/local/file.txt \
  --account-name mystorageaccount

## List Blobs in a Container
az storage blob list \
  --container-name mycontainer \
  --account-name mystorageaccount --output table

## Download a Blob
az storage blob download \
  --container-name mycontainer \
  --name myfile.txt \
  --file /path/to/download/file.txt \
  --account-name mystorageaccount

## Delete a Blob
az storage blob delete \
  --container-name mycontainer \
  --name myfile.txt \
  --account-name mystorageaccount

# -----------------------------------
# Queue Storage Commands
# -----------------------------------

## Create a Queue
az storage queue create --name myqueue --account-name mystorageaccount

## Add a Message to the Queue
az storage message put --queue-name myqueue --content "Hello World" --account-name mystorageaccount

## Peek at Queue Messages
az storage message peek --queue-name myqueue --account-name mystorageaccount

## Get Queue Messages
az storage message get --queue-name myqueue --account-name mystorageaccount

## Delete a Queue
az storage queue delete --name myqueue --account-name mystorageaccount

# -----------------------------------
# File Storage Commands
# -----------------------------------

## Create a File Share
az storage share create --name myshare --account-name mystorageaccount

## Upload a File to File Share
az storage file upload \
  --share-name myshare \
  --source /path/to/local/file.txt \
  --account-name mystorageaccount

## List Files in File Share
az storage file list \
  --share-name myshare \
  --account-name mystorageaccount --output table

## Download a File from File Share
az storage file download \
  --share-name myshare \
  --path file.txt \
  --dest /path/to/download/file.txt \
  --account-name mystorageaccount

## Delete a File from File Share
az storage file delete \
  --share-name myshare \
  --path file.txt \
  --account-name mystorageaccount

# -----------------------------------
# Table Storage Commands
# -----------------------------------

## Create a Table
az storage table create --name mytable --account-name mystorageaccount

## Insert an Entity into a Table
az storage entity insert \
  --table-name mytable \
  --entity PartitionKey=001 RowKey=001 Name=SampleData \
  --account-name mystorageaccount

## Query Entities from a Table
az storage entity query --table-name mytable --account-name mystorageaccount

## Delete a Table
az storage table delete --name mytable --account-name mystorageaccount

# -----------------------------------
# Data Lake Storage Commands
# -----------------------------------

## Enable Hierarchical Namespace (Data Lake Gen2) in Storage Account
az storage account update \
  --name mystorageaccount \
  --resource-group MyResourceGroup \
  --enable-hierarchical-namespace true

## Create a File System in Data Lake
az storage fs create --name myfilesystem --account-name mystorageaccount

## Upload a File to Data Lake
az storage fs file upload \
  --file-system myfilesystem \
  --path myfile.txt \
  --source /path/to/local/file.txt \
  --account-name mystorageaccount

## List Files in Data Lake File System
az storage fs file list --file-system myfilesystem --account-name mystorageaccount --output table

## Delete a File from Data Lake File System
az storage fs file delete --file-system myfilesystem --path myfile.txt --account-name mystorageaccount

# -----------------------------------
# Clean Up Resources
# -----------------------------------

## Delete Resource Group (and all resources within it)
az group delete --name MyResourceGroup --yes --no-wait
