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

![rs (37)](https://github.com/user-attachments/assets/5c7c3830-daac-4e9a-ba99-0e1cfc16899d)

#### Now we have to check the configuration we imported, for that we have to run the command –

terraform state show azuread_user.testuser

![rs (38)](https://github.com/user-attachments/assets/9b747b99-5689-4d6b-88e0-31f55a168e15)

## Creating a new user using Imported Template

#### For creating a new user using that imported template, we have to create a provider file,

#### Enter these details in “provider.tf” file –

provider "azuread" {
  tenant_id = var.tenant_id
}

resource "azuread_user" "testuser" {
    account_enabled                = true
    business_phones                = []
    disable_password_expiration    = false
    disable_strong_password        = false
    display_name                   = "testuser_template"
    mail_nickname                  = "testuser"
    other_mails                    = []
    show_in_address_list           = false
    user_principal_name            = "testuser_template@******.onmicrosoft.com"
    password                       = "AzureVM@!2024"
}

#### Also we have to create a variable file which can be referred for the variables in provider file,

#### Enter these details in “vars.tf” file –

variable "tenant_id" {
  description = "The tenant ID for the Azure provider"
  type        = string
  default     = "d7721f7d-2452-41bf-8fae-e29441ea930c"
}

#### After that, now we have to run “terraform init” command to initialize the working directory and to download the necessary provider plugins.

![Our latest women's fashion collection is now available on our official store  (3)](https://github.com/user-attachments/assets/606cd393-a8e9-405d-87d0-7a3735d11c57)

#### After that, now we have to run “terraform plan” command to create an execution plan,

![azure](https://github.com/user-attachments/assets/12d21b84-a73c-4254-bcdb-523f5ea0481d)

![azure (1)](https://github.com/user-attachments/assets/a49b4326-1193-43aa-a0c3-ea9570e0eda3)

#### After that, now we have to run “terraform apply” command to apply the changes,

![image](https://github.com/user-attachments/assets/b372c75a-2f86-4e00-ad7e-45be21345320)

![image](https://github.com/user-attachments/assets/31a890a6-65c5-4f07-96dd-f71230c3f2e7)

#### After that now the user will be created, we can verify it by checking into the Azure Console, 

#### Here we can see the new user “testuser_template” is showing.

![image](https://github.com/user-attachments/assets/6f4f2e72-e56b-4c39-a8dd-0dbc898ad130)

#### Here “testuser” user is which we used to import the configurations and “testuser_template” user is the one we created using that template.


















































