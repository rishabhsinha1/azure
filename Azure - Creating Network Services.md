# Azure - Creating Network Services

## Creating Network Services

### Creating Vnet(Virtual Network)

Search for Virtual Network  Create Virtual Network

![image](https://github.com/user-attachments/assets/88a3805f-2466-4ff4-aedf-b8a54d801dd1)

Fill the required details in the Basics tab,

![image](https://github.com/user-attachments/assets/6a72ce22-2d77-46aa-9f55-591de9d1e15e)

After that select the required security options

![image](https://github.com/user-attachments/assets/265a1f2a-d15a-40c1-bfeb-758dc1d84b7b)

Go to next, give a IP address

![image](https://github.com/user-attachments/assets/1ca5b5f6-4ef9-476b-a046-3309046a0aa2)

Go to next , create any tags if required  Next  Review + Create Create. 

![image](https://github.com/user-attachments/assets/94b63515-1c76-49c9-af20-da4716a3c2cc)

Now we can see VNet is created ,

![image](https://github.com/user-attachments/assets/92214351-5c6d-459e-afe0-56f92d1dc3a2)

## Adding a subnet in the Vnet

For creating a subnet, go in the Vnet Created  Settings Subnets  Create Subnet.

![image](https://github.com/user-attachments/assets/855f8239-3d8a-4f02-a9db-bec38a2e1e3c)

Give the IP address details and click on Add

![image](https://github.com/user-attachments/assets/55e9df4f-1047-4374-a845-c904e33c0d17)

Now we can see the new subnet is added in the Vnet.

![image](https://github.com/user-attachments/assets/d9fb57b1-69e4-4a21-92a5-05899c426850)

## Creating a NSG(Network Security Group)

In the search box, type Network Security Groups and select it

![image](https://github.com/user-attachments/assets/5f14be57-908d-4445-a185-88fd40995676)

Click on + Create.

Fill in the required details  Create.

![image](https://github.com/user-attachments/assets/6ea3fb84-a52b-4476-a64d-d5b7a3aded85)

Now we can see the NSG is created.

![image](https://github.com/user-attachments/assets/5ebe040a-30f9-4330-b24d-321456c58d1c)

## Adding Inbound Security Rules

After the NSG is created, navigate to the NSG we just created.

Go to Setting  Inbound Security Rules  +Add  Fill the required details.

![image](https://github.com/user-attachments/assets/ef4019ee-21f6-48dd-9270-fe4fe91779a3)

## Adding Outbound Security Rules

After the NSG is created, navigate to the NSG we just created.

Go to Setting  Outbound Security Rules  +Add  Fill the required details.

![image](https://github.com/user-attachments/assets/45b7fe75-ec5b-4a04-8e7a-ce04e768a42d)

## Associating the NSG with a Subnet

Navigate to the virtual network that contains the subnet.

Vnet  Settings  Subnets  Select the subnet we want to associate with the NSG  Click on Network security group  select the NSG we created.

![image](https://github.com/user-attachments/assets/8f58c543-5f3f-4596-8a39-4fe6d4c679dc)

Now the NSG will be attached to the subnet.

![image](https://github.com/user-attachments/assets/b442009e-4eaf-4624-ac9e-53efcfdd8773)

























