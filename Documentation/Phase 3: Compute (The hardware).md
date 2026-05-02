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

To troubleshoot, since free slots in datacenters normally run out, I tried a different VM size while keeping the rest of the command intact.

**Command used:**
```bash
az vm create --resource-group RG-Cyberportfolio-Prod --name VM-Portfolio-Web --image Ubuntu2204 --size Standard_DS1_v2 --admin-username azureuser --vnet-name VNet-Portfolio --subnet Subnet-Web --nsg NSG-Web-Secure --generate-ssh-keys --public-ip-sku Standard
```

The result:

<img width="1600" height="290" alt="vm creation" src="https://github.com/user-attachments/assets/cfa29011-a7b1-4ed1-9c0a-262ddcb1e468" />

<br>

The VM was successfully created. It means that the Standard_B2s slot server was full in the datacenter, and Standard_DS1_v2 still had an empty slot to hold my VM.


After creating any asset/resource, it is always best to check if it works as intended to avoid Security incidents later. 

Now that I had a publicIpAddress to the newly created virtual machine, I went ahead and tried to ssh into it.

**Command used:**
```bash
ssh azureuser@40.123.244.120
```
The result:
<img width="1055" height="119" alt="1st vm ssh" src="https://github.com/user-attachments/assets/08c3f10a-4471-4c0e-9540-d8f86ce2e487" />

<br>

The connection timed out. This means that the connection I tried to make was ignored by the firewall (the NSG), dropped it silently. This means that there was an IP Address mismatch since the NSG in phase 2 of the project was only allowed to take requests from my physical laptop's IP address. 

To make sure that I was troubleshooting this matter correctly, I used a command within the Azure CLI terminal to check the machine's IP Address.
**Command used:**
```bash
curl ifconfig.me
```

The IP Address that was returned was entirely different from the one I used to configure the NSG rules in Phase 2. A mistake was made.
Since the project is built in the Azure CLI entirely, there was no need for me to use my physical laptop's IP Address, I had to use that of the server, Azure Cloud Shell hosting my terminal.

Therefore, I need to update the NSG rules by whitelisting my specific Cloud Shell IP.
**Command used:**
```bash
az network nsg rule update --resource-group RG-Cybersecurity-Prod --nsg-name NSG-Web-Secure --name AllowRestrictedSSH --source-address-prefixes 172.201.33.160/32
```

The result:

<img width="1600" height="461" alt="nsg-update1" src="https://github.com/user-attachments/assets/daf722c2-a68f-441a-b019-2a0462766810" />

<br> 

The NSG rule have theen updated and the only IP Address whitelisted to make requests is the one that hosts my terminal, the Azure Cloud Shell. Now to check if I can SSH into the VM after this update,
**Command used:**
```bash
ssh azureuser@40.123.244.120
```

The result:
<img width="1600" height="684" alt="Screenshot (1038)" src="https://github.com/user-attachments/assets/086879b1-fcd6-47a4-8514-206a8ea705f8" />

<br>

The SSH connection was successful!
