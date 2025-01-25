Lab Objective
The purpose of this lab is to set up a small network environment for practicing system administration tasks. The lab consists of essential components such as Active Directory, DNS, DHCP, file sharing, and client-server communication. It is designed to simulate real-world scenarios for IT professionals to practice and enhance their skills.

Lab Components
PfSense Firewall

IP Address: 192.168.2.1
Role: Provides network routing, NAT, and internet access for the lab.
Active Directory Server (AD01)

Hostname: AD01
IP Address: 192.168.2.10
Role: Primary Domain Controller for jack.local domain. Configured with DNS and DHCP.
File Server (SRV1)

Hostname: SRV1
IP Address: 192.168.2.20
Role: Configured as a file server with shared folders accessible to domain users.
Windows Clients (CLIENT01 & CLIENT02)

IP Addresses: Dynamically assigned via DHCP.
Role: Domain-joined clients for testing GPOs and file share access.
Linux Client (LINUX01)

IP Address: Dynamically assigned via DHCP.
Role: Simulates cross-platform compatibility and domain authentication.
Admin PC

IP Address: 192.168.1.10
Role: Used to remotely manage the lab environment, including Active Directory and PfSense.
Network Diagram
Refer to the diagram provided for a visual representation of the network setup.

Setup Steps
1️⃣ Configure PfSense
Assign LAN and WAN interfaces.
Set LAN IP to 192.168.2.1.
Configure NAT to allow internet access.
Set up DNS forwarders to ensure AD DNS queries resolve.
2️⃣ Configure Active Directory (AD01)
Install Active Directory Domain Services (AD DS).
Promote AD01 as the primary Domain Controller for jack.local.
Configure DNS:
Set forwarders to PfSense (192.168.2.1).
Install and configure DHCP:
Define a scope (192.168.2.50 - 192.168.2.100).
Set the default gateway to 192.168.2.1.
Set DNS server to 192.168.2.10.
3️⃣ Configure File Server (SRV1)
Add SRV1 to the domain jack.local.
Configure shared folder Public:
Path: C:\Public.
Permissions: Allow read/write access to all domain users.
4️⃣ Configure Clients
Windows Clients:
Join the jack.local domain.
Verify GPO and shared folder access.
Linux Client:
Install necessary tools (realmd, sssd, etc.).
Join jack.local domain using:
bash
Copy
sudo realm join jack.local -U Administrator
Test domain user authentication.
5️⃣ Configure Group Policy Objects (GPOs)
Create a GPO to map the shared folder as a network drive:
Drive Letter: Z:
Path: \\SRV1\Public.
Testing and Validation
Ensure all clients receive IPs via DHCP.
Verify domain authentication on all machines.
Test file access from both Windows and Linux clients.
Test RDP access to servers.
