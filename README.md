<link rel="stylesheet" href="style.css">

# Active Directory and Splunk Network Lab

This project demonstrates the configuration and management of an Active Directory environment integrated with Splunk for log monitoring and analysis. The lab environment was built using VirtualBox and includes the following components:
- **Splunk Server**: Centralized logging server to collect and analyze data from other machines.
- **Windows Active Directory Server**: Provides directory services for the domain environment.
- **Windows 10 Target Machine**: A client machine joined to the domain.
- **Kali Linux Attacker Machine**: A penetration testing machine used to simulate attacks against the network.

## Project Overview

This project involves setting up an Active Directory environment with multiple virtual machines and configuring a network for security monitoring and analysis. Key components of the project include:

1. **Network Setup:**
   - Four virtual machines (Ubuntu Server, Windows Server, Kali Linux, and Windows 10) configured on VirtualBox.
   - Static IP addresses manually assigned to each machine for predictable communication.
   - Tools like **ping**, **ipconfig**, and **ifconfig** used to validate network connectivity.

2. **Active Directory Configuration:**
   - Windows Server set as the Domain Controller.
   - Created Organizational Units:
     - **I.T** with user **jsmith**.
     - **H.R** with user **tsmith**.

3. **Security Monitoring with Splunk and Sysmon:**
   - Installed **Sysmon** by Olaf Hartong for detailed system logging.
   - Logs from the Active Directory server and Windows 10 machine forwarded to the Splunk server for analysis.

4. **Brute Force Attack Simulation:**
   - Performed a brute force attack using **Crowbar** on the **tsmith** account.
   - Used a `rockyou.txt` file with 22 password combinations, one of which was correct.
   - Observed and analyzed the logs in Splunk to identify evidence of the brute force attack.


## Components

- **VirtualBox**: Virtualization platform used to create the virtual network.
- **Windows Server 2019**: Operating system for the Active Directory server.
- **Windows 10**: Client machine integrated into the Active Directory domain.
- **Kali Linux**: Attacker machine used for penetration testing in the environment.
- **Splunk**: Tool for collecting and analyzing log data across the network.

## Steps Taken

**Network Design**: Designed the network topology with two servers, a client, and an attacker machine. Configured all virtual machines to communicate using static IPs.
<div align="center">
  <img src="https://i.imgur.com/zwyRFuv.png" alt="Network Diagram" width="600">
</div>

**Downloaded and Configured Virtual Machines**: Obtained ISO images for the required operating systems:
- Ubuntu Server (for Splunk).
- Windows Server (for Active Directory).
- Kali Linux (as an attacker machine).
- Windows 10 (as a target machine).
- Set up each machine within VirtualBox.

**Assigned Static IP Addresses**: Configured network interfaces manually for consistent and predictable communication.
Static IP Assignments:
- Splunk Server: 192.168.10.10
- Active Directory Server: 192.168.10.7
- Windows 10: 192.168.10.100
- Kali Linux: 192.168.10.250

<p align="center">
  <strong>Ex: Active Directory IP</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/JgURU2B.png" alt="Active Directoy IP" width="400">
</div>

**Validated Network Connectivity**: Used ping to ensure all machines could communicate effectively.
Verified network configurations using:
- ipconfig on Windows-based machines.
- ifconfig on Linux-based machines.

**Active Directory Setup**: Configured the Windows Server as a domain controller, setting up the Active Directory environment.

**Splunk Configuration**: Installed and configured Splunk Universal Forwarders on both the Active Directory and Windows 10 machines to forward logs to the Splunk server. Make sure to create a Inputs.conf file in the Local directory with the following instructions.

<p align="center">
  <strong>Inputs Configuration to send to Endpoint</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/VRXpgWR.png" alt="Inputs conf" width="600">
</div>

<p align="center">
  <strong>Splunk Forwarder Setup</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/IWMPyqi.png" alt="Splunk Setup" width="800">
</div>

<p align="center">
  <strong>Splunk Server Setup</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/vUGPDp3.png" alt="Splunk Server Setup" width="800">
</div>

**Installed Sysmon for Enhanced Logging**: 
- Installed Sysmon, a system monitoring tool developed by Olaf Hartong, to capture detailed system activity, including process creation, network connections, and changes to file creation time.
- Sysmon was configured to enhance the logging capabilities of the environment, helping to monitor and log key events for analysis and security auditing in the Active Directory setup.

**Troubleshooting**: Encountered and resolved issues with static IP assignment on the Splunk server by editing the YAML configuration file.

### Configured Active Directory Domain Controller and Organizational Units

**Objective:** Set up the Windows Server as the main Domain Controller for Active Directory.

**Promoted Windows Server to Domain Controller:**
   - Made the Windows Server the primary **Domain Controller** for the Active Directory environment.
   - Signed in as **Administrator** to perform the necessary configurations.

**Created Organizational Units (OUs):**
   - Created two **Organizational Units** (OUs) to structure the directory:
     - **I.T** OU with the user **jsmith**.
     - **H.R** OU with the user **tsmith**.
   - This organizational structure helps streamline management by grouping users according to their departments.

### Final Step Brute Force Attack Simulation and Splunk Analysis

**Objective:** Simulate a brute force attack to observe and analyze log details in Splunk. 

**Important Note:** Make sure to enable RDP on the windows machine before attacking.

1. **Installed Crowbar on Kali Linux:**
   - Used the following command to install Crowbar:

     sudo apt-get install -y crowbar


2. **Executed Brute Force Attack:**
   - Targeted the **tsmith** account on the Active Directory domain.
   - Used a modified **rockyou.txt** file called passwords.txt containing 22 password combinations, one of which was correct.

     crowbar -b rdp -u tsmith -C passwords.txt -s 192.168.10.100/32

   - Observed and documented the behavior and response of the system.

3. **Log Analysis in Splunk:**
   - Analyzed the attack logs in Splunk to identify key details.
<p align="center">
  <strong>Splunk Index Search</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/rhx5XPg.png" alt="Splunk Search" width="800">
</div>
   - Observed Event Code **4625**, which indicates failed login attempts and detailed summary.
<p align="center">
  <strong>Event codes</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/hNV8T1T.png" alt="Event Code" width="700">
</div>

<p align="center">
  <strong>Event Details</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/7ajK15w.png" alt="Event details" width="700">
</div>

## Key Challenges & Solutions

**Static IP Configuration**: Initially faced issues with the Splunk server not accepting the static IP. Resolved by editing the YAML configuration file to manually assign the correct IP address. 

<p align="center">
  <strong>My YAML Solution</strong>
</p>
<div align="center">
  <img src="https://i.imgur.com/RioE2J2.png" alt="YAML Solution" width="600">
</div>

## 🛠 Skills Gained

This project has helped me develop and refine the following skills:

### 🔧 Technical Skills
- **Active Directory**: Designed and configured a Windows-based Active Directory domain with organizational units and user accounts.
- **Network Configuration**:
  - Assigned static IP addresses manually and configured network settings.
  - Disabled DHCP and validated network communication using tools like `ping`, `ipconfig`, and `ifconfig`.
- **Log Monitoring with Splunk**:
  - Installed and configured Splunk Universal Forwarders for log collection.
  - Analyzed logs in Splunk for security events (e.g., brute force attacks) and interpreted Event ID 4625.
- **System Hardening**:
  - Installed and configured Sysmon to enhance system logging capabilities.
- **Virtualization**: Set up multiple virtual machines (Windows Server, Windows 10, Ubuntu, and Kali Linux) using VirtualBox.
- **Brute Force Testing**: Simulated brute force attacks with Crowbar to analyze security logs and test defenses.

### 💡 Soft Skills
- **Troubleshooting**: Resolved network configuration issues, including editing YAML configuration files.
- **Documentation**: Created a detailed network diagram and recorded all processes for reproducibility.
- **Project Management**: Planned, executed, and documented a complex multi-system cybersecurity project.
- **Critical Thinking**: Interpreted system logs and identified patterns related to potential attacks.

### ⚙️ Tools and Technologies
- **Operating Systems**:
  - Windows Server
  - Windows 10
  - Kali Linux
  - Ubuntu Server
- **Networking Tools**:
  - `ping`, `ipconfig`, `ifconfig`
  - Static IP Addressing
- **Security Tools**:
  - Splunk
  - Sysmon
  - Crowbar
- **Virtualization**:
  - Oracle VirtualBox
- **Other**:
  - `rockyou.txt` for brute force testing

### 🌟 Summary
This project has significantly improved my understanding of Active Directory, log analysis, and network security. It has also provided me with hands-on experience in detecting and responding to security events.

