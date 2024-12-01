<link rel="stylesheet" href="style.css">

# Active Directory and Splunk Network Lab

This project demonstrates the configuration and management of an Active Directory environment integrated with Splunk for log monitoring and analysis. The lab environment was built using VirtualBox and includes the following components:
- **Splunk Server**: Centralized logging server to collect and analyze data from other machines.
- **Windows Active Directory Server**: Provides directory services for the domain environment.
- **Windows 10 Target Machine**: A client machine joined to the domain.
- **Kali Linux Attacker Machine**: A penetration testing machine used to simulate attacks against the network.

## Project Overview

In this project, I designed and built a network in a virtualized environment with the following goals:
1. Set up two servers (Splunk and Windows Active Directory) alongside a Windows 10 client and a Kali Linux attacker machine.
2. Install Splunk Universal Forwarders on both the Active Directory and Windows 10 target machines to send log data to the Splunk server.
3. Manually assign static IP addresses to all machines in the network after disabling DHCP.
4. Troubleshoot network configuration issues, including resolving IP assignment problems on the Splunk server by editing its YAML configuration file.

## Components

- **VirtualBox**: Virtualization platform used to create the virtual network.
- **Windows Server 2019**: Operating system for the Active Directory server.
- **Windows 10**: Client machine integrated into the Active Directory domain.
- **Kali Linux**: Attacker machine used for penetration testing in the environment.
- **Splunk**: Tool for collecting and analyzing log data across the network.

## Steps Taken

1. **Network Design**: Designed the network topology with two servers, a client, and an attacker machine. Configured all virtual machines to communicate using static IPs.
2. **Active Directory Setup**: Configured the Windows Server as a domain controller, setting up the Active Directory environment.
3. **Splunk Configuration**: Installed and configured Splunk Universal Forwarders on both the Active Directory and Windows 10 machines to forward logs to the Splunk server.
4. **Static IP Assignment**: Disabled DHCP and manually configured static IP addresses for all machines to ensure consistent network communication.
5. **Troubleshooting**: Encountered and resolved issues with static IP assignment on the Splunk server by editing the YAML configuration file.

## Key Challenges & Solutions

- **Static IP Configuration**: Initially faced issues with the Splunk server not accepting the static IP. Resolved by editing the YAML configuration file to manually assign the correct IP address.
- **Network Communication**: Ensured all virtual machines were able to communicate by troubleshooting and assigning IP addresses manually.

## Tools and Technologies

- VirtualBox
- Windows Server 2019
- Windows 10
- Kali Linux
- Splunk Enterprise
- Splunk Universal Forwarders
- YAML Configuration Files
- Networking (Static IP, DHCP, Routing)

## Installation

1. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/Active-Directory-Splunk-Lab.git
