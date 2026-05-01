## VNet, Subnet, and NSG Configuration

First, I had to confirm that the work from phase 1 was still there and not wiped when the previous session expired. This is to ensure environmental consistency, as everything in this project will be built inside the resource group, and prevent resource sprawl.

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

### Vnet and Subnet Overview
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







