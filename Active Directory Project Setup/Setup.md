# **Active Directory Project Setup**

# **1. VM Installation**
## **1.1. Install Windows 10 Machine**

Go to https://www.microsoft.com/en-ca/software-download/windows10 and download the "Create Windows 10 installation media" tool by clicking "Download tool now." Choose the option to "Create installation media (USB flash drive, DVD, or ISO file) for another PC," then select "ISO file" and save it.

In VirtualBox Manager, click on "Add" to set up a new virtual machine. Assign it a name, select the downloaded Windows 10 ISO file, allocate 4096MB of RAM, assign 1 CPU, and create a 50GB virtual disk, then finish the setup process. Start the virtual machine, follow the installation instructions, select "Custom: Install Windows only (advanced)," and allow Windows 10 to install.

## **1.2. Kali Linux**

Download Kali Linux from https://www.kali.org/ and get the VM version. Also, download and install 7-zip from https://www.7-zip.org/. Use 7-zip to extract the Kali Linux file, then import it into Oracle VM VirtualBox Manager and start the VM.

## **1.3. Windows Server**

Download the Windows Server 2022 ISO from https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022, fill out the required form, and download the "64-bit edition." In VirtualBox, create a new virtual machine using the ISO, allocate 4096MB of RAM, assign 1 CPU, and set up a 50GB virtual disk, then finish the setup. Start the virtual machine, click "Install now," choose "Windows Server 2022 Standard Evaluation (Desktop Experience)," customize the settings, set a password, and complete the installation process.

## **1.4. Windows Server**

Visit https://ubuntu.com/server to download Ubuntu Server, specifically version 24.04.1 LTS for this lab. In Oracle VM VirtualBox Manager, create a new virtual machine using the ISO, allocate 8192MB of RAM, assign 2 CPUs, and set up a 100GB virtual disk, then complete the setup. Start the virtual machine, select "Try or Install Ubuntu Server," and navigate through the series of "Done" and "Continue" prompts, filling out the required form before proceeding with the installation. After the installation, reboot the system. You may encounter error messages. Once the system has rebooted, log in and execute the command `sudo apt-get update && sudo apt-get upgrade -y`. After the process finishes, press "Enter."

# **2. VM and Network Configuration**
## **2.1. Create a Network using NAT Network**
Click Tools and select network, than select the NAT Networks tabs than click create. In this project we will use 192.168.10.0/24 as our Network.

![alt text](<../Images/Nat Network.png>)

## **2.2. Splunk Server**
### **2.2. Setup Splunk Server Connection**

At VirtualBox Home, select Splunk server > settings > Network > change the network adapter to the NAT network that we created earlier and click ok. after that we can start the Splunk Server to configure manually the IP address for the Splunk Server based on the Diagram we create.

        sudo nano /etc/netplan/50-cloud-init.yaml

![alt text](<../Images/Splunk Server Configuration (2).png>)

change to

![alt text](<../Images/Splunk Server Configuration (3).png>)

then type:

        sudo netplan apply

![alt text](<../Images/Splunk Server Configuration (1).png>)