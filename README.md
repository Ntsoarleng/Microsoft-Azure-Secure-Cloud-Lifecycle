# Microsoft Azure: Secure Cloud Lifecycle

### A practical IaaS Migration and Security Lab

## Project Overview

This project demonstrates a full birth-to-deletion lifecycle of a cloud asset. Moving beyond the theory of AZ-900, I built a functional Infrastructure as a Service (IaaS) environment to host a WordPress site. By applying a security-first mindset and blue team defenses, I navigated real world migration failures to ensure data integrity and infrastructure resilience.

## The Tech Stack

- **Model**: Infrastracture as a Service (IaaS)
- **Cloud**: Microsoft Azure (Virtual Machines, VNETs, NSGs)
- **Operating Systenm**: Linux (Ubuntu)
- **App/DB**: WordPress and MySQL
- **Security**: Resource Locks and Network Security Groups
- **Governance**: Azure Cost Management and Budgets

## The 7-Phase Execution

- [**Phase 1: Governance and the Safety Net**](https://github.com/Ntsoarleng/Microsoft-Azure-Lab/blob/main/Documentation/Phase%201%3A%20Governance%20and%20the%20Safety%20Net.md#resource-group-and-lock-configuration): Establishing Resource Groups and Administrative Locks.
- [**Phase 2: Networking**](https://github.com/Ntsoarleng/Microsoft-Azure-Lab/blob/main/Documentation/Phase%202%3A%20Networking.md#vnet-subnet-and-nsg-configuration): Designing the VNET, Subnet, and NSG firewall rules.
- [**Phase 3: Compute (The hardware)**](https://github.com/Ntsoarleng/Microsoft-Azure-Lab/blob/main/Documentation/Phase%203%3A%20Compute%20(The%20hardware).md#virtual-machine-vm-configuration): Configuration and deployment of the Ubuntu Virtual Machine.
- [**Phase 4: Inside the VM**](https://github.com/Ntsoarleng/Microsoft-Azure-Lab/blob/main/Documentation/Phase%204%3A%20Inside%20the%20VM.md#the-lamp-linux-apache-mysql-php-stack): Installing the LAMP stack and manual MySQL configuratin.
- [**Phase 5: The Migration**](https://github.com/Ntsoarleng/Microsoft-Azure-Lab/blob/main/Documentation/Phase%205%3A%20The%20Migration.md#data-migration-and-content-integrity): Solving a data integrity issue caused by XML schema mismacth.
- **Phase 6: Budget and Alerts**: Implementing financial guardrails and automated cost alerts.
- **Phase 7: Final Cleanup**: Secure decommissioning and zero-footprint resource deletion.

## Why this Matters
- Beyond Fundamentals: Practical application of Azure services in a manual IaaS build.
- Problem solver: Proven ability to remediate migration errors and database conflicts.
- Defense oriented: Security was not an afterthought, it was the foundation.
