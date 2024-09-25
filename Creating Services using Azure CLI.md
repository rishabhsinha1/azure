# Creating Services using Azure CLI

## User

### Creating a User using Azure CLI

For creating a user using Azure CLI , we can run the below command, make sure to update the “user principal name” in the below command

az ad user create --display-name "testCLIuser" --user-principal-name testCLIuser@**************.onmicrosoft.com --password "testCLI123!"

![image](https://github.com/user-attachments/assets/709a6df7-2360-4359-9cd5-d2614bcea0b1)
 
We can check from the Azure console , the new user is created

![image](https://github.com/user-attachments/assets/a6954258-0025-46d0-93ad-f6adfca7a5fe)

## Checking status of a User using Azure CLI

For Checking status of a user using Azure CLI , we can run the below command, make sure to update the “user principal name” in the below command

az ad user show --id testCLIuser@***************.onmicrosoft.com

![azure (2)](https://github.com/user-attachments/assets/acf497d4-c4ca-4253-9a0a-130bb42767cd)

## Deleting a User using Azure CLI

For deleting a user using Azure CLI, we have to run the below command, make sure to update the “user principal name” in the below command,

az ad user delete --id testCLIuser@*****************.onmicrosoft.com

We can check from the Azure console, the new user will be deleted.

## Group

### Creating a Group using Azure CLI

For creating a group using Azure CLI, we have to run the below command,

az ad group create --display-name "testCLIgroup" --mail-nickname "testCLIgroup"

![azure (3)](https://github.com/user-attachments/assets/d6aeab5a-fa01-4929-bda0-f4b8ca226074)

We can check from the Azure console, the new group will be created

![image](https://github.com/user-attachments/assets/e97c2194-b94d-41e2-aa5f-9cfb3346979e)

## Checking status of a group using Azure CLI

For Checking status of a group using Azure CLI , we can run the below command,

az ad group show --group "testCLIgroup"

## Deleting a group using Azure CLI

For deleting a group using Azure CLI, we have to run the below command,

az ad group delete --group "testCLIgroup"

We can check from the Azure console, the new group will be deleted.

## Adding a User to a Group using Azure CLI

For creating a User to a Group using Azure CLI, 

First we have to get the “Object ID” of that user, for that we have to run the below command, make sure to update the “user principal name” in the below command.

az ad user show --id testCLIuser@**************.onmicrosoft.com

From the above command , we will get the “Id” of the user , we have to copy it.

After that we have to run the below command to add the User in a Group, make sure to update the “Id” in the below command,

az ad group member add --group "testCLIgroup" --member-id *************

Now we can check from the Azure console, the User will be added in the Group.

![image](https://github.com/user-attachments/assets/dab3913b-3425-43f7-a52a-151fbcd4ba40)






















