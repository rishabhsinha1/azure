# Importing IAM Service Using Terraform

#### We can import using Cloud Shell and Visual Code also, here we are using Cloud Shell.

## Importing the configurations of a User

#### For Importing a user, first we have to create a provider file,

#### Enter these details in “provider.tf” file –

provider "azuread" {
  tenant_id = var.tenant_id
}	

resource "azuread_user" "testuser" {
  user_principal_name = "testuser@yourdomain.com"
  display_name        = "Test User"
}

#### Also we have to create a variable file which can be referred for the variables in provider file,

#### Enter these details in “vars.tf” file –

variable "tenant_id" {
  description = "The tenant ID for the Azure provider"
  type        = string
  default     = "d7721f7d-2452-41bf-8fae-e29441ea930c"
}

#### Also for importing the user , we need the “user_object_id”, For that we have to go into , 

#### Users  Select the user  Object ID

![rs (36)](https://github.com/user-attachments/assets/93975055-026b-404f-b490-cf7e0cddb0ea)

#### Now we can run the import command,

terraform import azuread_user.testuser <Object ID>

![Our latest women's fashion collection is now available on our official store  (1)](https://github.com/user-attachments/assets/50cc848f-2d0b-484d-a522-16e683218cdf)

#### After the Import is successful, the state list will be created, we can verify it using –

terraform state list

















