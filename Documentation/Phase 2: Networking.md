## VNet, Subnet, and NSG Configuration

First, I had to conform that the work from phase 1 was still there and not wiped when the previous session expired. This is to ensure environmental consistency, as everything in this project willbe built inside the resource group, and prevent resource sprawl

**Command used to check if the resource group was still in place:**
```bash
az group list --output table
```

The output was:

<img width="687" height="100" alt="rg-check" src="https://github.com/user-attachments/assets/ca7d9c02-931a-43bb-a31e-1987e3b5de19" />


**Command used to confirm that the lock was still in place and configured correctly:**

```bash
az lock list --resource-group RG-Cyberporfolio-Prod --output table
```

Result:

<img width="764" height="77" alt="lock-confirmation" src="https://github.com/user-attachments/assets/f9c844a0-b5af-4fe1-9998-ef04ff44b886" />


Now that I was sure that the resources I created were still in place, I could then go on to configure the VNet, Subnet and NSG resources.
Think of it like checking your mirrors before you start driving a car. You know that they were there yesterday, but checking again takes 2 seconds and prevents a massive accident. This is why it is always important to confirm that the resources/assets that were created are still there and configured properly.

### Vnet and Subnet Overview:




