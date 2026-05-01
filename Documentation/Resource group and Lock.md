## Resource Group & Lock Configuration

### Resource Groupt Overview:
1. Name: RG-Cyberportfolio-Prod
2. Region: South Afica North
3. Purpose: It will contain all resources for this lab. It also makes it easy to manage the project as one can delete the whole folder later to wipe everything out at once.

### Steps to create Resource group:
1. Logged into an Azure account
2. Clicked on Azure CLI. Two options were provided: Bash and Powershell. Chose Bash as it was the kernel I am most familiar with.
3. The command used to create the resource group, name it, choose its region, and create, was:
```bash
az group create --name RG-CyberPortfolio-Prod --location southafricanorth --tags Project=Portfolio
```

And the result was:

<img width="1159" height="286" alt="rg-creation" src="https://github.com/user-attachments/assets/9c5c0e02-e414-4562-a1e5-437787591628" />








