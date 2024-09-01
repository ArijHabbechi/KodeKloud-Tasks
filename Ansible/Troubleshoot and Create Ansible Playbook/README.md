# Task: Create an Empty File on App Server 3
## Overview

This task involves creating an empty file `/tmp/file.txt` on App Server 3 in Stratos DC using an Ansible playbook.

  

## Inventory Setup

The `inventory` file has been configured to connect to App Server 3:

  

`stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_ssh_common_args='-o StrictHostKeyChecking=no' `

  
  
  

## SSH Key Setup

  

Before running the playbook, you need to ensure that your SSH key is set up to allow passwordless login to the App Server.

  

**1. Generate an SSH Key:** 
`ssh-keygen -t rsa -b 4096`

  

**2. Copy the SSH Key to App Server 3:**

  

`ssh-copy-id -i ~/.ssh/id_rsa.pub banner@172.16.238.12`

You will be prompted to enter the password for the banner user on the App Server.

  

## Running the Playbook

Once the SSH key setup is complete, you can run the playbook using:

  
  

`ansible-playbook -i inventory playbook.yml`

  

# Summary

This playbook ensures that an empty file is created at `/tmp/file.txt` on App Server 3. Ensure the SSH setup is complete before executing the playbook to avoid any connection issues.