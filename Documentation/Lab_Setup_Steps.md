# Active Directory Home Lab Setup

## Overview
This document details the setup of an Active Directory (AD) home lab using VMware Workstation. The lab includes a pfSense firewall, an Active Directory Domain Controller, a file server, Windows clients, and a Linux client.

## Lab Topology
```
                 Internet
                     │
                 Router
                     │
               pfSense Firewall
               (192.168.2.1)
                     │
    ┌───────────────┴───────────────┐
    │                               │
 Active Directory Server         SRV1 (File Server)
 (192.168.2.10)                  (192.168.2.20)
    │                               │
 ┌───────────────┬───────────────┐
 │               │               │
Win Client 1   Win Client 2   Linux Client
```

## Virtual Machines
| VM Name           | Role                 | OS                  | IP Address    |
|------------------|---------------------|---------------------|--------------|
| pfSense          | Firewall/Gateway    | pfSense             | 192.168.2.1  |
| AD Server        | Domain Controller   | Windows Server 2019 | 192.168.2.10 |
| SRV1             | File Server         | Windows Server 2019 | 192.168.2.20 |
| Windows Client 1 | Workstation         | Windows 10          | DHCP         |
| Windows Client 2 | Workstation         | Windows 10          | DHCP         |
| Linux Client     | Workstation         | Ubuntu              | DHCP         |

## Setup Steps

### 1. **Install pfSense as Firewall**
- Assign **WAN** (Bridged to Router) and **LAN** (192.168.2.1/24)
- Enable **DHCP on LAN** (to distribute IPs to clients)
- Set **DNS Forwarding** to use AD DNS

### 2. **Install & Configure Active Directory Server**
- Install Windows Server 2019
- Assign static IP **192.168.2.10**
- Install **Active Directory Domain Services (AD DS)**
- Promote Server to **Domain Controller** (Domain: `jack.local`)
- Configure **DNS** to forward to pfSense
- Configure **DHCP Server** for automatic client IP assignment

### 3. **Configure SRV1 as File Server**
- Assign static IP **192.168.2.20**
- Install **File Server Role**
- Create a shared folder `\srv1\public` with domain user access

### 4. **Join Clients to AD Domain**
#### Windows Clients:
1. Set DNS to **192.168.2.10**
2. Join domain via **System Properties → Change Settings → Domain: `jack.local`**
3. Restart and log in with **domain credentials**

#### Linux Client (Ubuntu):
```bash
sudo apt update && sudo apt install -y realmd sssd adcli
sudo realm join jack.local -U Administrator
```

### 5. **Group Policy Management**
- Configure a **GPO** to map `\srv1\public` as `Z:` drive for all domain users:
  1. Open **Group Policy Management**
  2. Create a new **GPO: "Map Public Drive"**
  3. Go to **User Configuration → Preferences → Drive Maps**
  4. New Drive Map → Path: `\srv1\public` → Assign letter `Z:`
  5. Link GPO to **domain users OU**

### 6. **Testing & Verification**
- Check domain join with:
  ```powershell
  Get-ADComputer -Filter *
  ```
- Test file server access from Windows clients:
  ```cmd
  net use Z: \\srv1\public
  ```
- Test Linux access:
  ```bash
  smbclient -L //srv1 -U DOMAIN\User
  ```

## Additional Enhancements
- Implement **Remote Desktop (RDP) for Admin PC**
- Automate **GPO Export & Backup** with PowerShell
- Document all configurations in a GitHub repository

## Summary
This lab simulates a **corporate IT infrastructure** with:
✅ **Active Directory for centralized authentication**
✅ **pfSense as a firewall & network manager**
✅ **File server for shared access across domain users**
✅ **Windows & Linux client domain integration**

This setup provides practical hands-on experience for **System Administration & Cybersecurity** roles.


