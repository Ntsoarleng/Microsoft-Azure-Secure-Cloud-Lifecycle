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

The VNet and Subnet were configured correctly and still in place.
<br>
<br>

### Virtual Machine(VM) Overview:

Now to create a virtual machine in the subnet,

**Command used:**
```bash
az vm create --resource-group RG-Cyberportfolio-Prod --name VM-Portfolio-Web --image Ubuntu2204 --size Standard_B2s --admin-username azureuser --vnet-name VNet-Portfolio --subnet Subnet-Web --nsg NSG-Web-Secure --generate-ssh-keys --public-ip-sku Standard
```
What the command does:
1. It creates the virtual machine inside the Subnet, within the resource group, VNet and NSG.
2. Admin username: azureuser
3. Operating system of the virtual machine: Ubuntu v22.04
4. Size: Standard_B2s. This is the normal Free Tier slot VM size in a southafricanorth, Johannesburg datacenter.
5. --generate-ssh-keys tells Azure to handle the "Identity" of the server for me automatically. It creates a private and a public key. The public key is stored inside the VM in a file called authorized_keys, and the private key is saved on the local machine (usually in ~/.ssh/id_rsa). They are normally referred to as the 'Lock' and 'Physical key' respectively. Setting this up is better than having a password that can be brute-forced. It ensures that even if someone steals my username, they cannot get in without my physical private key file.
6. --public-ip-sku Standard ensures that the VM's Public IP does not change everytime one stops and starts the machine. It maintains the static IP address, providing consistent connectivity for the portfolio's web traffic.

The result:
<img width="1600" height="597" alt="vm initial error" src="https://github.com/user-attachments/assets/b2c96a36-88ca-4f2c-98ee-7f80250b8d2f" />
<br>

An ERROR!

To troubleshoot, since free slots in datacenters normally run out, I tried a different VM size, while keeping the rest of the command intact.

**Command used:**
```bash
az vm create --resource-group RG-Cyberportfolio-Prod --name VM-Portfolio-Web --image Ubuntu2204 --size Standard_DS1_v2 --admin-username azureuser --vnet-name VNet-Portfolio --subnet Subnet-Web --nsg NSG-Web-Secure --generate-ssh-keys --public-ip-sku Standard
```

The result:

<img width="1600" height="290" alt="vm creation" src="https://github.com/user-attachments/assets/cfa29011-a7b1-4ed1-9c0a-262ddcb1e468" />

The VM was successfully created. It means that the Standard_B2s slot server was full in the datacenter, and Standard_DS1_v2 still had an empty slot to hold my VM.

