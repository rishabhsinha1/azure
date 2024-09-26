# Find Free IP Addresses in a Subnet

## Overview

This document describes a Bash script that interacts with Azure to list virtual networks (VNets) within a specified resource group, allows the user to select a virtual network, lists the subnets within the selected virtual network, and then retrieves the details of free IP addresses in a selected subnet. The script uses the Azure CLI and includes input validation and constants for improved readability and maintainability.

## Prerequisites

Azure CLI: Ensure that the Azure CLI is installed and configured on your system.

Azure Login: You must be logged in to the Azure CLI with appropriate permissions to query virtual networks and subnets.

jq: Ensure that jq is installed on your system for JSON parsing.

## Steps Performed by the Script

### Constants:

The script defines constants for repeated strings or values such as prompts and error messages. This makes the script easier to update and maintain.

### Prompt for Resource Group Name:

The script prompts the user to input the name of the resource group.

Input validation ensures that the resource group name is not empty. If the input is empty, an error message is displayed, and the prompt is repeated.

### List Virtual Networks:

The script lists the virtual networks in the specified resource group using the az network vnet list command.

The virtual networks are displayed in a tabular format.

If no virtual networks are found, the script exits with an appropriate message.

### Prompt for Virtual Network Name:

The script prompts the user to input the name of the virtual network from the list displayed.

Input validation ensures that the virtual network name is not empty. If the input is empty, an error message is displayed, and the prompt is repeated.

### List Subnets:

The script lists the subnets in the specified virtual network within the specified resource group using the az network vnet subnet list command.

The subnets are displayed in a tabular format, including the addressPrefix or addressPrefixes property.

If no subnets are found, the script exits with an appropriate message.

### Prompt for Subnet Name:

The script prompts the user to input the name of the subnet from the list displayed.

Input validation ensures that the subnet name is not empty. If the input is empty, an error message is displayed, and the prompt is repeated.

### Find Free IP Addresses:

The script lists the available IP addresses in the specified virtual network using the az network vnet list-available-ips command.

The free IP addresses are displayed in a readable format.

### Main Function:

The script includes a main function to orchestrate the workflow by calling the defined functions in sequence.

### Run the Main Function:

The script ends by calling the main function to execute the workflow.

### Script


#!/bin/bash


# Constants

RESOURCE_GROUP_PROMPT="Enter the resource group name: "

VNET_PROMPT="Enter the virtual network name from the list above: "

SUBNET_PROMPT="Enter the subnet name from the list above: "

NO_VNETS_FOUND="No virtual networks found."

NO_SUBNETS_FOUND="No subnets found."

NO_IPS_FOUND="No free IP addresses found."


# Function to prompt for resource group name

prompt_resource_group() {

  while true; do
  
    read -p "$RESOURCE_GROUP_PROMPT" resource_group
    
    if [ -n "$resource_group" ]; then
    
      echo -e "\nResource group entered: $resource_group"
      
      break
    
    else
    
      echo "Resource group name cannot be empty. Please try again."
    
    fi
  
  done

}

# Function to list virtual networks in the resource group
list_virtual_networks() {
  echo -e "\nListing virtual networks in the resource group '$resource_group'..."
  vnets=$(az network vnet list --resource-group "$resource_group" --query '[].{Name:name, Location:location}' -o table)
  echo -e "\nVirtual Networks:"
  if [ -z "$vnets" ]; then
    echo "  $NO_VNETS_FOUND"
    exit 1
  else
    echo "$vnets"
  fi
}


# Function to prompt for virtual network name
prompt_vnet_name() {
  while true; do
    read -p "$VNET_PROMPT" vnet_name
    if [ -n "$vnet_name" ]; then
      echo -e "\nVirtual network entered: $vnet_name"
      break
    else
      echo "Virtual network name cannot be empty. Please try again."
    fi
  done
}


# Function to list subnets in the virtual network

list_subnets() {

  echo -e "\nListing subnets in the virtual network '$vnet_name' within resource group '$resource_group'..."
  
  subnets=$(az network vnet subnet list --resource-group "$resource_group" --vnet-name "$vnet_name" -o json)
  
  echo -e "\nSubnets:"
  
  if [ -z "$subnets" ]; then
  
    echo "  $NO_SUBNETS_FOUND"
    
    exit 1
  
  else
  
    echo "$subnets" | jq -r '.[] | "\(.name)\t\(.addressPrefix // .addressPrefixes[0])"' | column -t
  
  fi

}


# Function to prompt for subnet name

prompt_subnet_name() {

  while true; do
  
    read -p "$SUBNET_PROMPT" subnet_name
    
    if [ -n "$subnet_name" ]; then


     echo -e "\nSubnet entered: $subnet_name"
      break
    else
      echo "Subnet name cannot be empty. Please try again."
    fi
  done
}


# Function to find free IP addresses in the subnet

find_free_ips() {

  echo -e "\nFinding free IP addresses in the subnet '$subnet_name' within virtual network '$vnet_name' and resource group '$resource_group'..."
  
  used_ips=$(az network vnet list-available-ips --resource-group "$resource_group" --name "$vnet_name" --query "[]" -o tsv)
  
  
  echo -e "\nFree IP Addresses:"
  
  if [ -z "$used_ips" ]; then
  
    echo "  $NO_IPS_FOUND"
  
  else
  
    echo "$used_ips"
  
  fi

}


# Main function to orchestrate the script

main() {

  prompt_resource_group
  
  list_virtual_networks
  
  prompt_vnet_name
  
  list_subnets
  
  prompt_subnet_name
  
  find_free_ips

}


# Run the main function

main
















