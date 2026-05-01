## Resource Group & Lock Configuration

### Resource Groupt Overview:
1. Name: RG-Cyberportfolio-Prod
2. Region: South Africa North
3. Purpose: It will contain all resources for this lab. It also makes it easy to manage everything within the project as one can delete the whole folder later to wipe everything out at once.

### Steps to create Resource group:
1. Logged into an Azure account
2. Clicked on Azure CLI. Two options were provided: Bash and Powershell. Chose Bash as it was the kernel I am most familiar with.
3. The command used to create the resource group, name it, choose its region, was:
```bash
az group create --name RG-CyberPortfolio-Prod --location southafricanorth --tags Project=Portfolio
```

And the result was:

<img width="1159" height="286" alt="rg-creation" src="https://github.com/user-attachments/assets/9c5c0e02-e414-4562-a1e5-437787591628" />


Next, creating a lock.

### Lock Overview:
1. Name: Lock-PreventDelete
2. Asociated resource group: RG-Cyberportfolio-Prod
3. Lock type: Gives a brief description of what the lock does: CanNotDelete
4. Purpose: It is a "safety pin". This tells Azure that even if one accidentally clicks delete, it should not let it happen, thus wiping everything within the resource group. This is a key Governance skill for the AZ-900.

**Command used to create the lock:**
```bash
az lock create --name Lock-PreventDelete --resource-group RG-Cyberportfolio-Prod --lock-type CanNotDelete
```
The result:

<img width="1282" height="209" alt="lock" src="https://github.com/user-attachments/assets/52efd7bf-0725-4897-9477-d0d0843724e2" />









