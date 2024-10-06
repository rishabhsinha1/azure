# Importing Network Service Using Terraform

## Importing the configurations of a Virtual Network

#### For Importing a Virtual Network, first we have to create a provider file,

#### Enter these details in “provider.tf” file –

provider "azurerm" {

  features {}

  subscription_id = var.subscription_id

}


resource "azurerm_virtual_network" "vnet" {

  name                = var.vnet_name
  
  address_space       = var.address_space
  
  location            = var.location
  
  resource_group_name = var.resource_group_name

}


Also we have to create a variable file which can be referred for the variables in provider file,

Enter these details in “vars.tf” file –

variable "subscription_id" {

  description = "The subscription ID for the Azure RM provider"
  
  type        = string
  
  default     = "247c515c-64fc-41b1-b954-f63ae5e89e30"

}


variable "resource_group_name" {

  description = "The name of the resource group"
  
  type        = string
  
  default     = "testresourcegroup"

}


variable "location" {

  description = "The location/region where the resources will be created"
  
  type        = string
  
  default     = "East US"

}



variable "vnet_name" {
  
  description = "The name of the Virtual Network"
  
  type        = string
  
  default     = "testvnet"

}


variable "address_space" {
  
  description = "The address space for the Virtual Network"
  
  type        = list(string)
  
  default     = "192.168.0.0/16"

}

#### Also for importing the Virtual Network , we need the “subscription_id” and “resource_group_name”, For that we have to go into the Virtual Network,

![image](https://github.com/user-attachments/assets/66966534-993b-43b1-8349-51c61e578dd1)

#### Now we can run the import command, In this we have to paste the subscription ID and resource group name,

terraform import azurerm_virtual_network.vnet /subscriptions/247c515c-64fc-41b1-b954-f63ae5e89e30/resourceGroups/testresourcegroup/providers/Microsoft.Network/virtualNetworks/testvnet

![image](https://github.com/user-attachments/assets/120b97a0-ec57-44a4-bf1c-5fade668522a)

#### After the Import is successful, the state list will be created, we can verify it using –

terraform state list

![image](https://github.com/user-attachments/assets/efb49ef0-7421-413b-a9ee-f7b8c4268146)

#### Now we have to check the configuration we imported, for that we have to run the command –

terraform state show azurerm_virtual_network.vnet

![image](https://github.com/user-attachments/assets/1669d7a0-f4dd-40e6-9ff1-ddf61f4c48dd)

#### Creating a new Virtual Network using Imported Template

#### For creating a new Virtual Network using that imported template, we have to create a provider file,

#### Enter these details in “provider.tf” file –

provider "azurerm" {
 
  features {}
  
  subscription_id = var.subscription_id

}

resource "azurerm_virtual_network" "vnet_template" {

  name                    = var.vnet_name
  
  address_space           = var.address_space
  
  location                = var.location
  
  resource_group_name     = var.resource_group_name

}

resource "azurerm_subnet" "subnet_template" {
 
  name                      = "subnet1"
  
  resource_group_name       = var.resource_group_name
  
  virtual_network_name      = azurerm_virtual_network.vnet_template.name
  
  address_prefixes          = var.subnet_address_prefixes
  
  private_endpoint_network_policies             = "Disabled"
  
  private_link_service_network_policies_enabled = true

}

#### Also we have to create a variable file which can be referred for the variables in provider file,

#### Enter these details in “vars.tf” file –

variable "subscription_id" {
  
  description = "The subscription ID for the Azure RM provider"
  
  type        = string
  
  default     = "247c515c-64fc-41b1-b954-f63ae5e89e30"

}


variable "resource_group_name" {

  description = "The name of the resource group"
  
  type        = string
  
  default     = "testresourcegroup"

}


variable "location" {

  description = "The location/region where the resources will be created"
  
  type        = string
  
  default     = "eastus"

}


variable "vnet_name" {

  description = "The name of the Virtual Network"
  
  type        = string
  
  default     = "vnet_template"

}



variable "address_space" {

  description = "The address space for the Virtual Network"
  
  type        = list(string)
  
  default     = ["172.16.0.0/16"]

}


variable "subnet_address_prefixes" {

  description = "The address prefixes for the subnet"
  
  type        = list(string)
  
  default     = ["172.16.0.0/24"]

}

#### After that, now we have to run “terraform init” command to initialize the working directory and to download the necessary provider plugins.

#### After that, now we have to run “terraform plan” command to create an execution plan,

![image](https://github.com/user-attachments/assets/fbb1bcf3-36d2-4096-9c55-6bb02853d37e)

#### After that, now we have to run “terraform apply” command to apply the changes,

![image](https://github.com/user-attachments/assets/49338dd0-02a0-4fa7-bd15-81adc0c28977)

![image](https://github.com/user-attachments/assets/28976cc7-f7c3-4ba5-b77b-87758b5daefa)

#### After that now the user will be created, we can verify it by checking into the Azure Console, 

#### Here we can see the new user “vnet_template” is showing.

![image](https://github.com/user-attachments/assets/dae3936a-288a-401a-b260-f0f45c00d76b)

#### Here “testvnet” vnet is which we used to import the configurations and “testvnet_template” vnet is the one we created using that template.








































