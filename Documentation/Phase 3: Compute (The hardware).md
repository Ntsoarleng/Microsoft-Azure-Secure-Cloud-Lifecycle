## Virtual Machine (VM) Configuration

As a best practice, before going on to create the virtual machine, I need to ensure that resources from Phase 2 are still existent and configured properly. This is to ensure that the previous expired session did not wipe everything out that was created within that session, and again, to prevent resource sprawl.

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

To create THE virtual machine in the Subnet,

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

To troubleshoot: since free slots in datacenters normally run out, I tried a different VM size while keeping the rest of the command intact.

**Command used:**
```bash
az vm create --resource-group RG-Cyberportfolio-Prod --name VM-Portfolio-Web --image Ubuntu2204 --size Standard_DS1_v2 --admin-username azureuser --vnet-name VNet-Portfolio --subnet Subnet-Web --nsg NSG-Web-Secure --generate-ssh-keys --public-ip-sku Standard
```

The result:

<img width="1600" height="290" alt="vm creation" src="https://github.com/user-attachments/assets/cfa29011-a7b1-4ed1-9c0a-262ddcb1e468" />

<br>

The VM was successfully created. It means that the Standard_B2s slot server was full in the datacenter, and Standard_DS1_v2 still had an empty slot to "house" the VM.


After creating any asset/resource, it is always best to check if it works as intended to avoid Security incidents later. 

Now that I had a publicIpAddress to the newly created virtual machine, I went ahead and tried to ssh into it.

**Command used:**
```bash
ssh azureuser@40.123.244.120
```
The result:
<img width="1055" height="119" alt="1st vm ssh" src="https://github.com/user-attachments/assets/08c3f10a-4471-4c0e-9540-d8f86ce2e487" />

<br>

The connection timed out. This means that the connection I tried to make was ignored by the firewall (the NSG), dropped it silently. This means that there was an IP Address mismatch since the NSG rule in Phase 2 of the project was only allowed to take requests from my physical laptop's IP address. 

To make sure that I was troubleshooting this matter correctly, I used a command within the Azure CLI terminal to check the machine's IP Address.
**Command used:**
```bash
curl ifconfig.me
```

The IP Address that was returned was entirely different from the one I used to configure the NSG rules in Phase 2. A mistake was made.
Since the project is built in the Azure CLI entirely, there was no need for me to use my physical laptop's IP Address, I had to use that of the server, Azure Cloud Shell, hosting my terminal.

Therefore, I needed to update the NSG rules by whitelisting my specific Cloud Shell IP.
<br>
**Command used:**
```bash
az network nsg rule update --resource-group RG-Cybersecurity-Prod --nsg-name NSG-Web-Secure --name AllowRestrictedSSH --source-address-prefixes 172.201.33.160/32
```

The result:

<img width="1600" height="461" alt="nsg-update1" src="https://github.com/user-attachments/assets/daf722c2-a68f-441a-b019-2a0462766810" />

<br> 

The NSG rule was updated and the only IP Address that was "Allowed" to make requests was the one hosting my terminal, the Azure Cloud Shell. To check if I could SSH into the VM after this update,
<br>
**Command used:**
```bash
ssh azureuser@40.123.244.120
```

The result:
<img width="1600" height="684" alt="Screenshot (1038)" src="https://github.com/user-attachments/assets/086879b1-fcd6-47a4-8514-206a8ea705f8" />

<br>

The SSH connection succeded!

One important factor to note is that Cloud Shell IPs are dynamic, meaning they can change, and are not always volatile, meaning that they change every second or everytime the current session expires. This means that even if a session expires, Microsoft doesn't always delete your container immediately.

Due to this reason, it is imperative that one checks the IP address in the terminal before beginning work or continuing where you left off. This practice ensures that if the IP Address of the Cloud Shell has changed, one updates the NSG rules to whitelist the newly assigned IP Address. By doing so, the admin will be able to make an SSH request into the VM, as the previous IP Address will be a dead rule and as an admin, you do not want to be locked out of your environment.

This may sound tiresome, but from a cybersecurity perspective, it is very secure because the "door" is only open for that specific, temporary session. To reduce the manual labor of having to update the NSG rules everytime to whitelist the new IP Address, this process can be automated so that before starting or continuing any work, one only runs the script that will make these updates. One must be willing to trade a little bit of convenience for a lot of safety.


In a corporate environment, Port 22 is not even open. Instead, Azure Bastion is used which is out of scope for this project since I am using the Free Tier account. Azure Bastion costs money per hour, but it is so much better because no NSG rules are needed for your IP, no Port 22 open, and it is fully encrypted.
