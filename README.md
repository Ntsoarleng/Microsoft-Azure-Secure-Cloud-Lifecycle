# Microsoft-Azure: Secure Cloud Lifecycle

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

- **Phase 1: Governance and the Safety Net**: Establishing Resource Groups and Administrative Locks.
- **Phase 2: Networking**: Designing the VNET, Subnet, and NSG firewall rules.
- **Phase 3: Compute (The hardware)**: Configuration and deployment of the Ubuntu Virtual Machine.
- **Phase 4: Inside the VM**: Installing the LAMP stack and manual MySQL configuratin.
- **Phase 5: The Migration**: Solving a data integrity loss caused by XML schema mismacth.
- **Phase 6: Budget and Alerts**: Implementing financial guardrails and automated cost alerts.
- **Phase 7: Final Cleanup**: Secure decommissioning and zero-footprint resource deletion.

## Why this Matters
- Beyond Fundamentals: Practical application of Azure services in a manual IaaS build.
- Problem solver: Proven ability to remediate migration errors and database conflicts.
- Defense oriented: Security was not an afterthought, it was the foundation.
