## VNet, Subnet, and NSG Configuration

Firstly, I had to confirm that the work from phase 1 was still there and not wiped when the previous session expired. This is to ensure environmental consistency, as everything in this project will be built inside the resource group, and prevent resource sprawl.

**Command used to check if the resource group was still in place:**
```bash
az group list --output table
```

The output was:

<img width="687" height="100" alt="rg-check" src="https://github.com/user-attachments/assets/ca7d9c02-931a-43bb-a31e-1987e3b5de19" />

<br>

**Command used to confirm that the lock was still in place and configured correctly:**

```bash
az lock list --resource-group RG-Cyberporfolio-Prod --output table
```

Result:

<img width="764" height="77" alt="lock-confirmation" src="https://github.com/user-attachments/assets/f9c844a0-b5af-4fe1-9998-ef04ff44b886" />

<br>

Now that I was sure that the resources I created were still in place, I could then go on to configure the VNet, Subnet and NSG resources.
Think of it like checking your mirrors before you start driving a car. You know that they were there yesterday, but checking again takes 2 seconds and prevents a massive accident. This is why it is always important to confirm that the resources/assets that were created are still in place and configured properly.
<br>
<br>

### Vnet and Subnet Overview:
**Command used to create the Vnet and Subnet is:**
```bash
az network vnet create --resource-group RG-CyberPortfolio-Prod --name Vnet-Portfolio --location southafricanorth --address-prefix 10.0.0.0/16 --subnet-name Subnet-Web --subnet-prefix 10.0.1.0/24
```
The output showing successful configuration was:

<img width="1570" height="687" alt="vnet and subnet creation" src="https://github.com/user-attachments/assets/5b5fe9aa-c256-4e58-8ff1-d2758ba5ada7" />

<br>

What the command does is:
1. It defines a vnet network to be created inside the resource group, RG-Cyberportfolio-Prod.
2. It then assigns a name to this network, Vnet-Portfolio.
3. It specifies the location of the datacenter in which the VNet and Subnet are going to live and comply to Governance of that region, i.e POPIA. Note that since the VNet is inside the resource group whose location was also already configured to southafricanorth, this means that every resource that gets put into this resource group inherits the location in which it is housed. However, as a best practice, one must ensure that resources are configured fully and explicitly even if there is an implicit inheritance in place. This is to prevent any mistakes and misconfigurations that might creep in as we progress.
4. The address prefix used for the VNet, 10.0.0.0/16, defines the boundaries of the entire private network. The /16 means there are 65 536 available IP addresses, from 10.0.0.0 to 10.0.255.255.
5. In the same breadth, the subnet that will house my particular Virtual Machine was created. The subnet name is Subnet-Web with subnet-prefix, 10.0.1.0/24. The /24 gives 256 addresses, from 10.0.1.0 to 10.0.1.255.

<br>

In Azure, networking is hierarchical. Creating the VNet and Subnet in a single command is a clean way to build the entire network foundation at once, ensuring that specific IP address ranges are mapped correctly from the start and prevent misconfigurations, which is one of the most critical cybersecurity vulnerabilities according to OWASP Top 10 2025. If there was a need, one might also have one subnet for a Web Server and a different, more restricted subnet for a Database. 

By doing this configuration in one go, my network environment is instantly ready for the Compute (VM) phase.
<br>
<br>

### Network Security Group (NSG) Overview:

The NSG is essentially the cloud firewall, it defines the rules of engagement of who can interact with the reosurces within the resource group.

**Command used to create NSG:**
```bash
az network nsg create --resource-group RG-Cyberportfolio-Prod --name NSG-Web-Secure --location southafricanorth
```
<br>

To show successful configuration, the below was output, and there was no error:

<img width="1584" height="603" alt="nsg-creation" src="https://github.com/user-attachments/assets/8a470d2f-5341-4f69-9e38-fad2d423d5cc" />
<br>

The NSG was also created inside the resource group, its name: NSW-Web-Secure, and located in the southafricanorth region. This is consistent with the purpose of the project.

After creating the NSG, Azure blocks all incoming traffic from the internet by default. Inbound rules need to be created to "Allow" Port 80/443 so visitors can see my portfolio.

**Command used to allow web traffic into the network:**
```bash
az network nsg rule create --resource-group RG-Cyberportfolio-Prod --nsg-name NSG-Web-Secure --name AllowWebRedirect --priority 100 --destination-ranges 80 443 --access Allow --protocol Tcp
```
<br>

The result to show successful configuration without any error:

<img width="1580" height="452" alt="allow web-traffic" src="https://github.com/user-attachments/assets/9ef1ba9c-76e3-417e-b196-68c6026d1a9a" />

<br>

Because I explicitly allowed only specific ports, the NSG automatically drops everything else, like hackers trying to scan for open ports.

The reason why both Ports, 80 and 443 were allowed even though I would have only preferred to allow Port 443 for safety reasons; this is to ensure that whenever a user visits my website and they type the address/url of my portfolio in the search bar, a big warning does not appear that may suggest that the website is faulty or broken thus making the user skeptical. Security is great, but user experience (UX) must also be prioritized. 

By default, browsers try to connect via HTTP (Port 80) first. If Port 80 is closed, an error message appears when a person tries to go to my portfolio, "Site Not Found". When Port 80 is open, the request hits the server and then immediately gets redirected to HTTPS (Port 443). This is where actual communiation happens, and it is secure as its purpose is to ensure encryption and data integrity.

In summary, Port 80 was opened to strictly facilitate a 301 Redirect to Port 443. This ensures a seamless user experience (UX) while enforcing encryption in transit as the mandatory standard for all traffic, satisfying both usability and security requirements.

<br>
<br>
Since the only Ports allowed to access the network are Port 80 and 443 for the public, SSH needs to be enabled to allow me as the owner to manage my resources. If SSH is not enabled, I am basically locked out of my network.

**Command used to enable SSH:**
```bash
az network nsg rule create --resource-group RG-Cyberportfolio-Prod --nsg-name NSG-Web-Secure --name AllowRestrictedSSH --priority 110 --source-address-prefixes <YOUR-IP>/32 --destination-port-ranges 22 --access Allow --protocol Tcp --description "Allow SSH only from my home IP for management."
```

Result showing successful configuration without any errors:

<img width="1600" height="480" alt="ssh-enablement" src="https://github.com/user-attachments/assets/ff46a926-da0d-4109-9f81-523c944b273a" />

<br>

Because SSH gives one "Root" (total) control over the server, it is the number 1 target for hackers. This is why I only restricted it to my IP address. The /32 restricts it to the provided IP address. If Azure NSG sees a different IP address, it will drop the connection entrirely.

In summary, network traffic was segmented into two planes: The data plane (Port 80/443) for public access, and the Management plane (Port 22) for administrative tasks. The management plane was secured via IP-whitelisting to eliminate the attack surface for unauthorized SSH attempts.









