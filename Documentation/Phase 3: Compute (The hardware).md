## Virtual Machine (VM) Configuration

As a best practice, before going on to create the virtual machine, I need to ensure that resources from Phase 2 are still existent and conigured properly. This is to ensure that the previous expired session did not wipe everything out that was created within that session, and again, to prevent resource sprawl.

**Commands used to confirm that the VNet and Sutnet were still in place:**
```bash
az network vnet list --resource-group RG-Cyberportfolio-Prod --output table
```
```bash
az network vnet subnet list --resource-group RG-Cyberportfolio-Prod --vnet-name VNet-Portfolio --output table
```
The results:

<img width="1160" height="109" alt="vnet-check" src="https://github.com/user-attachments/assets/8839ff9d-502b-49c1-b2d9-8540cae4ae33" />
<img width="1403" height="106" alt="subnet-check" src="https://github.com/user-attachments/assets/76c7017b-d841-4bc0-a67c-672c9bae6e5c" />

<br>

The VNet and Subnet were configured correctly and still in place
