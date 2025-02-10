# Active Directory Project

Welcome to the Active Directory Project repository!

This project will run a virtual environment using Oracle VM VirtualBox, including VMs for Windows 10, Kali Linux, Windows Server, and Ubuntu Server. Network settings are configured to allow communication through IP addresses and NAT Networks. For security, Splunk Server is used for log analysis, Universal Forwarder for data forwarding, and Sysmon for endpoint monitoring. Testing involves Crowbar for brute force attacks, Atomic Red Team (ART) for general assessments, and Splunk for log analysis. The Windows machines are integrated into an Active Directory domain with Remote Desktop enabled. PowerShell scripting automates various tasks, facilitating a hands-on approach to exploring cybersecurity concepts and tools in a controlled environment.

This project was greatly enhanced by the insights and tutorials from the [MyDFIR](https://www.youtube.com/@MyDFIR) YouTube channel. Their detailed videos played a crucial role in understanding and executing the different elements of the Active Directory Project.

## **[Click here to visit Actvie Directory Project Setup!](./Active%20Directory%20Project%20Setup/Setup.md)**

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

### **3.1.1. WIndows Active Directory User Creation** 

![alt text](<Images/User Creation 1 .png>)

![alt text](<Images/User Creation 2.png>)

ref 1: Actvie Directory Settings

### **3.1.2. Enable Remote Desktop** 

![alt text](<Images/Enable RDP (1).png>)

![alt text](<Images/Enable RDP (2).png>)

ref 2: RDP Settings

### **3.1.3. Analyze Telemetry Using Splunk** 

*note: simulate attack with crowbar*

![alt text](<Images/Crowbar Bruteforce Attack (1).png>)

![alt text](<Images/Crowbar Bruteforce Attack (2).png>)

![alt text](<Images/Crowbar Bruteforce Attack (3).png>)

![alt text](<Images/Crowbar Bruteforce Attack (4).png>)

ref 3: Test for RDP Bruteforce Attack 

### **3.1.4. Atomic Red Team Test**

![alt text](<Images/Atomic Test T1136.001 (2).png>)

![alt text](<Images/Atomic Test T1136.001 (3).png>)
*this indicate that we have just identified a gap in our protection to detect this activity. if an attacker compromise our system and created local account with current settings, we won’t be able to detect it.*

ref 4.1: Test for Persistence by Creating a Local Account

![alt text](<Images/Atomic Test T1059 (2).png>)

![alt text](<Images/Atomic Test T1059 (3).png>)

![alt text](<Images/Atomic Test T1059 (1).png>)

ref 4.2: Test for Command and Scripting Interpreter

# **4. Conclusion**

We have successfully set up and configured a service called Active Directory domain services /ADDS and than the server must be promoted to Domain Controller / DC. So it can do authentication using protocol called Kerberos and authorization for our domain. Then successfully integrate it with Splunk to enable log analyst with Bructefore Attack Simulation (crowbar) and ART (Atomic Red Team) to perform general assessments of our system.

- Configuring and setting up a Windows 10 Server with Sysmon to generate comprehensive event data, splunk universal forwarder for forwarding data to Splunk and ADDS and promoted a Domain Controller so it can do authentication using protocol called Kerberos and authorization for our domain.
- Configuring and setting up a Windows 10 Target Machine with Sysmon to generate comprehensive event data, splunk universal forwarder for forwarding data to Splunk and join the Target Machine to Domain Server.
- Deploying Splunk server for analyzing and monitoring logs.
- Perfrom bruteforce attack using Crowbar and general assessment using ART / Atomic Red Team on Target Machine 

This project has provided valuable hands-on experience in implementing Active Directory workflow using powerful open-source tools. We can now apply this knowledge to enhance the organization's Active Directory System.

# **5. Refferences**
- https://youtu.be/mWqYyl89QaY?si=clMEfPK_5sLtnQeW
- https://youtu.be/2cEj3bS5C0Q?si=_5U9Ilp8aC8QobYD
- https://youtu.be/uXRxoPKX65Q?si=VMFiQvaMDRCzGXDv
- https://youtu.be/1XeDht_B-bA?si=eUlE4WOloqR-RKua
- https://youtu.be/orq-OPIdV9M?si=UMoVp8qovNSK-Y52