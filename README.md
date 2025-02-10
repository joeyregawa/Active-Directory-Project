# Active Directory Project

Welcome to the Active Directory Project repository!

This project will run a virtual environment using Oracle VM VirtualBox, including VMs for Windows 10, Kali Linux, Windows Server, and Ubuntu Server. Network settings are configured to allow communication through IP addresses and NAT Networks. For security, Splunk Server is used for log analysis, Universal Forwarder for data forwarding, and Sysmon for endpoint monitoring. Testing involves Crowbar for brute force attacks, Atomic Red Team (ART) for general assessments, and Splunk for log analysis. The Windows machines are integrated into an Active Directory domain with Remote Desktop enabled. PowerShell scripting automates various tasks, facilitating a hands-on approach to exploring cybersecurity concepts and tools in a controlled environment.

This project was greatly enhanced by the insights and tutorials from the [MyDFIR](https://www.youtube.com/playlist?list=PLEd_qaF8wpnXgdngqfsQtYYGM-IdtuxmC) YouTube channel. Their detailed videos played a crucial role in understanding and executing the different elements of the Active Directory Project.

# **1. Introduction**
## **1.1. Overview**
Active Directory Project is focused on creating an Active Directory.  Active Directory is used as database contain user computers groups  etc. In order to use active directory, a Server must install a service called Active Directory domain services /ADDS and than the server must be promoted to Domain Controller / DC. so it can do authentication using protocol called Kerberos and authorization for our domain.

### Active Directory Project Diagram: ###!

![alt text](<Images/Active Directory Diagram.jpg>)



















