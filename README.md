# Active Directory Project

Welcome to the Active Directory Project repository!

This project will run a virtual environment using Oracle VM VirtualBox, including VMs for Windows 10, Kali Linux, Windows Server, and Ubuntu Server. Network settings are configured to allow communication through IP addresses and NAT Networks. For security, Splunk Server is used for log analysis, Universal Forwarder for data forwarding, and Sysmon for endpoint monitoring. Testing involves Crowbar for brute force attacks, Atomic Red Team (ART) for general assessments, and Splunk for log analysis. The Windows machines are integrated into an Active Directory domain with Remote Desktop enabled. PowerShell scripting automates various tasks, facilitating a hands-on approach to exploring cybersecurity concepts and tools in a controlled environment.

This project was greatly enhanced by the insights and tutorials from the [MyDFIR](https://www.youtube.com/playlist?list=PLEd_qaF8wpnXgdngqfsQtYYGM-IdtuxmC) YouTube channel. Their detailed videos played a crucial role in understanding and executing the different elements of the Active Directory Project.

# **1. Introduction**
## **1.1. Overview**
Active Directory Project is focused on creating an Active Directory.  Active Directory is used as database contain user computers groups  etc. In order to use active directory, a Server must install a service called Active Directory domain services /ADDS and than the server must be promoted to Domain Controller / DC. so it can do authentication using protocol called Kerberos and authorization for our domain.

### Active Directory Project Diagram: ###

![alt text](<Images/Active Directory Diagram.jpg>)

## **1.2. Project Objectives:**

 - The lab aims to offer a hands-on learning experience in establishing a virtualized environment for cybersecurity testing and exploration.
 - Create and configure various virtual machines (VMs), including Windows 10, Kali Linux, Windows Server, and Ubuntu Server.
 - The lab provides practical experience in network setup, security tool installation (such as Splunk and Sysmon), endpoint monitoring, and security testing (using Crowbar for brute force attacks).
 - Windows machines will be integrated into an Active Directory domain, and Remote Desktop access will be enabled to enhance the learning experience.
 - Automation tasks will be managed through PowerShell scripting.
 - Overall, the lab equips participants with practical knowledge of cybersecurity concepts, tools, and techniques in a controlled environment.

# **2. Requirement and Tools**

- **Oracle VM VirtualBox Manager**: For creating and managing virtual machines (VMs).
- **Splunk Server**: For analyzing and monitoring logs.
- **Splunk Universal Forwarder**: For forwarding data to Splunk.
- **Sysmon**: For monitoring endpoints on Windows machines.
- **Crowbar**: For simulating brute force attacks.
- **Atomic Red Team (ART)**: For security testing and validation.
- **PowerShell**: For scripting and automating tasks.
- **Microsoft Windows Event Logs**: Analyzed in Splunk for security monitoring.
- **Windows Server 2022**: Used for setting up Active Directory Domain Services.
- **Ubuntu Server**: Deployed as a Splunk server in the lab environment.
- **Microsoft Windows 10**: The target operating system for the lab machine.
- **Kali Linux**: Acts as the attacker machine in the lab setup.

# **3. Study Case**

This project will showcase the use of Active Directory, which is used as database contain user computers groups  etc. Splunk will be integrated to the Active Directory Server and Target Machine for log analysis. Testing involves Crowbar for brute force attacks, Atomic Red Team (ART) for general assessments.

## **3.1. Visual Representation**









