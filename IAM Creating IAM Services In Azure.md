# Creating IAM Services

Creating User

We have to login into Azure Console 🡪 search for User 🡪 User

![image](https://github.com/user-attachments/assets/a0b224bb-5c63-453a-8f72-95c9601696be)

Here we have to click on New user

![image](https://github.com/user-attachments/assets/b743e5e0-e06d-484a-a108-236745faa8dd)

Fill all the details of user and click on create

![image](https://github.com/user-attachments/assets/49f9add4-49ef-4f50-a3fd-6bd91ef5acc3)

We can see user is created.
 
 ![image](https://github.com/user-attachments/assets/653c6a3e-88c6-419f-8b3a-ff1e1e6b7307)

# Checking User from CLI

We have to run this command to list the Users in our Azure AD tenancy.

az ad user list --output table

![image](https://github.com/user-attachments/assets/8fef7c7f-3651-4043-a24c-3876115bfcbc)

 
# Creating Group

Now we have to create a group, search for Group  Groups  New Group

![image](https://github.com/user-attachments/assets/13daeacb-ea3a-49ca-b3e4-72d15f9bf9a7)
 
Enter the details and click on create

![image](https://github.com/user-attachments/assets/27a78134-d685-4585-8668-1c97a58cfc61)
 
Group created

 ![image](https://github.com/user-attachments/assets/3935582c-5cd2-40a7-b75c-5fa15f92eb13)

# Checking Group from CLI

We have to run this command to list the Groups in our Azure AD tenancy.

az ad group list --output table

![image](https://github.com/user-attachments/assets/6fce0b0c-10eb-43ba-954e-0c75ebab0131)
 
# Adding the user to group

For adding the user to a group, we have to go inside the group created  Manage  Members  Add members.

![image](https://github.com/user-attachments/assets/4787ba5c-e356-4335-84e6-563c045953c5)
 
We have to select the users tab and select the user to add in the group.	.
 
![image](https://github.com/user-attachments/assets/52aecadd-9fde-43f3-9d38-ac3a6c17fa41)

Now we can see the user added to the group.

 ![image](https://github.com/user-attachments/assets/f12e2704-55b3-45b4-9d8f-0a658eaa68f4)

# Creating Resource Group

Search for resource group
 
 ![image](https://github.com/user-attachments/assets/407f6353-ecf3-4fda-9618-669b1408d535)

Click on create and fill the details and click on create.
 
 ![image](https://github.com/user-attachments/assets/08316a76-512b-4ca8-9aa3-d17dae73f560)

Resource group created.

 ![image](https://github.com/user-attachments/assets/d6323fa6-96a2-488f-87f7-46f4aaf50279)

# Checking Resource Group from CLI

We have to run this command to list the Resource Groups in our Azure AD tenancy.

az group list --output table

![image](https://github.com/user-attachments/assets/58f7e47c-cf2e-465a-8aad-80047c5608dc)
 
# Role Assignment

Here we have to assign a role to the resource group, for that we have to go inside the resource groups  Access Control(IAM)  Add role assignment.

 ![image](https://github.com/user-attachments/assets/0df92f4d-a366-4f7d-aa76-f5b218256176)

Select the required role and in the members  Add members  Select the group  Assign Access.
 
![image](https://github.com/user-attachments/assets/de5eea8a-c742-4eb4-a64d-30cf78ce4c13)













