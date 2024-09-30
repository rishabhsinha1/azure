# Managing Azure AD Groups and Members Using Azure CLI

## Overview

This document describes a Bash script that interacts with Azure Active Directory (Azure AD) using the Azure CLI. The script lists all Azure AD groups and their 

Object IDs, prompts the user to select a group by its display name, and then lists the users in the selected group.

## Prerequisites

Azure CLI: Ensure that the Azure CLI is installed and configured on your system.

Azure Login: You must be logged in to the Azure CLI with appropriate permissions to list groups and group members.

## Steps Performed by the Script

### List All Groups:

●	The script starts by listing all Azure AD groups and their Object IDs.

●	It uses the az ad group list command with a query to format the output as tab-separated values (TSV).

### Check for Groups:

●	The script checks if any groups were found.

●	If no groups are found, it prints a message and exits.

### Display Groups:

●	The script displays the available groups to the user.

●	It extracts and prints the display names of the groups.

### Prompt for Group Selection:

●	The script prompts the user to input the display name of the group they want to check.

### Find Group Object ID:

●	The script finds the Object ID of the selected group based on the display name provided by the user.

●	It uses awk to match the display name and extract the corresponding Object ID.

### Check for Group Existence:

●	The script checks if the group was found.

●	If the group is not found, it prints a message and exits.

### List Group Members:

●	The script lists the users in the selected group.

●	It uses the az ad group member list command with a query to format the output as a table, showing the user principal names and display names of the group members.

### Script

#!/bin/bash

# List all groups and their Object IDs
echo "Listing all groups and their Object IDs..."
groups=$(az ad group list --query '[].{DisplayName:displayName, ObjectId:id}' --output tsv)

# Check if any groups were found
if [ -z "$groups" ]; then
  echo "No groups found."
  exit 1
fi

# Display the groups to the user
echo "Available Groups:"
echo "$groups" | awk -F'\t' '{print $1}'

# Prompt the user to input the display name of the group they want to check
read -p "Enter the display name of the group you want to check: " group_name

# Find the Object ID of the selected group



object_id=$(echo "$groups" | awk -F'\t' -v name="$group_name" '$1 == name {print $2}')

# Check if the group was found
if [ -z "$object_id" ]; then
  echo "Group not found."
  exit 1
fi

# List the users in the selected group
echo "Listing users in the group '$group_name' (Object ID: $object_id)..."
az ad group member list --group "$object_id" --query '[].{UserPrincipalName:userPrincipalName, DisplayName:displayName}' --output table






















