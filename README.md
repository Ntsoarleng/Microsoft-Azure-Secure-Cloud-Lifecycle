# Microsoft-Azure: Secure Cloud Lifecycle

## Project Overview

This project was built to bridge the gap between cloud theory and real-world application. I built a full Infrastructure as a Service (IaaS) environment, perfomed data migration. Throughout the process, I applied a security-first mindset and implemented Blue-team defenses to strengthen the security and resilience of the cloud resources. This lab proves that I can not only build in the cloud but can protect and manage the entire lifecycle of an asset.

## The Tech Stack

- **Model**: Infrastracture as a Service (IaaS)
- **Cloud**: Microsoft Azure (Virtual Machines, VNETs, NSGs)
- **Operating Systenm**: Linux (Ubuntu)
- **App/DB**: WordPress and MySQL
- **Security**: Resource Locks and Network Security Groups
- **Governance**: Azure Cost Management and Budgets

## What I did

1. **The IaaS Build (Total Control)**
   Instead of using a managed platform (PaaS), I chose IaaS. I deployed and configured a Linux Virtual Machine from scratch. This proves I can manage the Shared Responsibility Model, handling the OS, security patches, and database configuration myself.
2. **Real world Migration and Troubleshooting**
    AZ-900 explains what migration is, and I perfomed one.
   - **The challenge**: I moved website data using an XML file, but I hit a schema mismatch error. Automated migration resulted in a compromise of data integrity, where the imported information did not align correctly with the new environment's structure.
   - **The fix**: I analyzed the error logs, identified code conflict, and manually edited the XML schema to make the migration successful.
3. **Practical GRC (Governance, Risk, and Compliance)**
I treated this lab like a corporate environment by implementing:
- **Resource locks**: I applied "Lock-PreventDelete" lock to prevent accidental deletion of critical infrastructure.
- **Financial guardrails**: I set up a project budget with automated alerts at 50% and 90% to ensure zero billing surprises.
<br>

## Phase-by-Phase breakdown

- **Phase 1: Governance and the Safety Net** : Configured the NSG and administrative resource lock.
- **Phase 2: Networking** : 
