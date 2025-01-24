# Active Directory Home Lab
This repository contains a guide to setting up an AD lab environment using VMware Workstation, Windows Server, and pfSense.

## 📌 Features
- Active Directory Domain Services (AD DS)
- Dedicated File Server
- DHCP, DNS, and Group Policy (GPO) configurations
- pfSense firewall and network segmentation
- Windows and Linux client integration

## 🛠️ Lab Components
| Component       | IP Address       | Role                          |
|---------------|------------------|-------------------------------|
| pfSense       | 192.168.2.1      | Firewall & Router             |
| Domain Controller | 192.168.2.10 | Active Directory & DNS        |
| SRV1          | 192.168.2.20     | File Server                   |
| Windows Clients | DHCP Assigned  | Domain-Joined Workstations    |
| Linux Client  | DHCP Assigned    | Ubuntu Client (AD Integrated) |
| Admin PC      | RDP to AD Server | RDP to AD Server              |

## 📖 Setup Instructions
See the [Lab Setup Steps](Documentation/Lab_Setup_Steps.md) for a detailed guide.
