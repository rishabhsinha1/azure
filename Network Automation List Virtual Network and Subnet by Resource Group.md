# Script to List Virtual Network and Subnet by Resource Group

## Overview

This document describes a Bash script that interacts with Azure to list virtual networks (VNets) within a specified resource group and subsequently lists the subnets within a selected virtual network. The script uses the Azure CLI and includes input validation and constants for improved readability and maintainability.
Prerequisites

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

The script uses jq to parse the JSON output and handle both addressPrefix and addressPrefixes properties.

### Main Function:

The script includes a main function to orchestrate the workflow by calling the defined functions in sequence.

### Run the Main Function:

The script ends by calling the main function to execute the workflow.

## Script


#!/bin/bash


# Constants

RESOURCE_GROUP_PROMPT="Enter the resource group name: "

VNET_PROMPT="Enter the virtual network name from the list above: "

NO_VNETS_FOUND="No virtual networks found."

NO_SUBNETS_FOUND="No subnets found."


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
  
  else
  
    echo "$subnets" | jq -r '.[] | "\(.name)\t\(.addressPrefix // .addressPrefixes[0])"' | column -t
  
  fi

}


# Main function to orchestrate the script

main() {

  prompt_resource_group
  
  list_virtual_networks
  
  prompt_vnet_name
  
  list_subnets

}


# Run the main function

main























