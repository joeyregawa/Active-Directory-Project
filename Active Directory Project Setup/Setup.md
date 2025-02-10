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
### **2.2.1. Setup Splunk Server Connection**

At VirtualBox Home, select Splunk server > settings > Network > change the network adapter to the NAT network that we created earlier and click ok. after that we can start the Splunk Server to configure manually the IP address for the Splunk Server based on the Diagram we create.

        sudo nano /etc/netplan/50-cloud-init.yaml

![alt text](<../Images/Splunk Server Configuration (2).png>)

change to

![alt text](<../Images/Splunk Server Configuration (3).png>)

then type:

        sudo netplan apply

![alt text](<../Images/Splunk Server Configuration (1).png>)

### **2.2.2. Download and Setup Splunk on Splunk Server**

- Choose Splunk Enterprise and Click ‘Get My Free Trial” (https://www.splunk.com/en_us/download.html). Select the Linux .deb file and download it.

![alt text](<../Images/Splunk Installation and Config (1).png>)

- At virtual box install the guest add-ons for virutalBox and install it.

        sudo apt-get install virtualbox-guest-additions-iso

- Now navigate to Devices > Shared Folders > Shared Folders Settings > Create new Shared Folder. Navigate to the directory where you installed Splunk, check all three boxes, and click ok.

![alt text](<../Images/Splunk Installation and Config (2).png>)

- After Shared Folders is setup, type:

Reboot the virtual machine with `sudo reboot`. 

- Add user to vboxsf group

Run `sudo apt-get install virtualbox-guest-utils` then reboot once more, and then `sudo adduser <your username> vboxsf`. Run `mkdir share` to create a new directory called "share".

![alt text](<../Images/Splunk Installation and Config (3).png>)

- run `sudo mount -t vboxsf -o uid=1000,gid=1000 <directory name where .deb file is located> share/`. to mount user share folder to our directory called share, then type ls -la. the “Share” folder should be highlighted.

![alt text](<../Images/Splunk Installation and Config (4).png>)

- move to the share directory, and we can see our splunk installer.

![alt text](<../Images/Splunk Installation and Config (5).png>)

- Install Splunk

        sudo dpkg -i splu<hit tab to auto-complete>

- Change directory to where is Splunk is located, and run `ls -la`. 

        cd /opt/splunk/

![alt text](<../Images/Splunk Installation and Config (6).png>)

- Switch to the Splunk user by executing `sudo -u splunk bash`. Then, navigate to the `bin` directory by running `cd bin/`. Start Splunk with `./splunk start`, and when prompted, press `q`, then `y`, and hit `[ENTER]` to proceed.
- To complete this process, exit the current session, go back to the `bin` directory, and run `sudo ./splunk enable boot-start -user splunk`. This will configure Splunk to launch automatically at boot as the Splunk user.

![alt text](<../Images/Splunk Installation and Config (7).png>)

# **3. Windows Target Machine**
## **3.1. Setup Windows Target Machine Connection and Name**

- Rename the Windows Target Machine. In this project, the target machine will be named as target-PC. then restart the system.
- Change the static IP to the designed IP from Active Directory Diagram

        IP: 192.168.10.100
        subnet mask: 255.255.255.0
        default gateway: 192.168.10.1
        DNS (for now): 8.8.8.8

- you can visit your Splunk using: `<your splunk ip>:8000 `

## **3.2. Setup Windows Target Machine Connection and Name**

- On the target machine, go to https://www.splunk.com/ and select Products > Free Trials & Downloads > Universal Forwarder > Get my free download. Then, download the appropriate version for your target machine.
- Double-click the installed MSI file and enter the basic information, but do not set a password. Skip the deployment server setup, and for the Receiving Indexer, specify the IP/port as 192.168.10.10:9997, then proceed with the installation.

## **3.3. Install Sysmon and add Sysmon Configuration**
- Download Sysmon from https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
- open  https://github.com/olafhartong/sysmon-modular scroll down and select sysmonconfig.xml. Click "raw", and save the file.
- Extract the Sysmon zip file and move the Sysmon config file to the extracted Sysmon zip folder. Run `.\Sysmon64.exe -i .\sysmonconfig.xml`, then click agree.

## **3.4. Configure inpunts.conf File for Splunk Universal Forwarding on Windows Machine**

        [WinEventLog://Application]
        index = endpoint
        disabled = false

        [WinEventLog://Security]
        index = endpoint
        disabled = false

        [WinEventLog://System]
        index = endpoint
        disabled = false

        [WinEventLog://Microsoft-Windows-Sysmon/Operational]
        index = endpoint
        disabled = false
        renderXml = true
        source = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational

- save this file as all file types in the local folder accessed previously as "inputs.conf".  Then restart the splunk service. Before restart splunk, double click at the Log On and change it to Local System Account. Then Restart it.

![alt text](<../Images/Splunk Universal Forwarding Configuration.png>)

- Open Splunk at 192.162.10.100:8000 and login to your splunk account. Then click Settings dropdown menu > Indexes > New Index > name it “endpoint” > save.
- Ensure Splunk server is enable to receive data.  Click Settings dropdown menu > Forwarding and receiving > Configure receiving > New Receiving Port > set port to 9997 > save.
- Check the data coming in from our machine. Click Apps > Search & Reporting > search for "index=endpoint".

# **4. Windows Server Configuraion**

*note: Step for Network and Configuration Setup for Windows server with sysmon and Splunk Universal Fowrarding is the same as windows target machine. (Remember to change the windows server name, in this project we will name it as ADDC01)*

objective:

- Install & configure windows server active directory then promote domain controller.
- configure target machine to join the domain

## **4.1. Install and Configuration Active Directory and Control Domain**

- open your windows Server manager.
- Navigate to Manage > Add Roles & Features > select “Next” > select Role-based for feature-based installation > click “Next” > click “Next” > Select ”Active Directory Domain Services” > click “Add Features” > keep on clicking “Next” until you can select Install.

![alt text](<../Images/Windows Server Configuration (1).png>)

- After receive the message Configuration required. Installation succeeded on ADDC01, click the flag icon beside manage.

![alt text](<../Images/Windows Server Configuration (2).png>)

- select "Promote this server to a domain controller” > Select "Add a new forest” (because we’re creating a brand new domain in this project) > create name at Root domain name (`<your domain name>`.local) > Next > Create a password > Next until the Configuration Wizard validates prerequisites, and then hit install. This should trigger you to be signed out and have the server restart.

![alt text](<../Images/Windows Server Configuration (3).png>)

![alt text](<../Images/Windows Server Configuration (4).png>)

- the backslash indicate that we have successfully installed adds and promoted our sever to a domain controller.

![alt text](<../Images/Windows Server Configuration (5).png>)

- Next step is to create some users. Login to server > navigate to Tools > Active Directory Users and Computers

![alt text](<../Images/Windows Server Configuration (6).png>)

- Right-click explorelearn.local > New > Organizational Unit > Name: "IT". Right-click in the space of this new Organizational Unit > New > User. First name: "Jenny", Last name: "Smith", Full name: "Jenny Smith", User logon name: "jsmith". Create a password, uncheck user must change password at next log (because this is lab environment), then finish. Create a new Organizational Unit called "HR" and create another different user.

![alt text](<../Images/Windows Server Configuration (7).png>)

![alt text](<../Images/Windows Server Configuration (8).png>)
*note: username: jsmith, pass: adsf1234QWER*

![alt text](<../Images/Windows Server Configuration (9).png>)
*note: username: tsmith, password: ASDFqwer1234*

## **4.2. Windows 10 Target Machine Joins New Domain**

- Search This PC > properties > select “Advanced system Settings” > Computer Name > Change > Select "Domain" > enter your domain name >  

![alt text](<../Images/Windows Server Configuration (10).png>)

![alt text](<../Images/Windows Server Configuration (11).png>)

- We will get this error because the machine doesn’t know to resole the domain name. to fix this navigate to network adapter by clicking the network icon at the bottom right of the window > Open Network & Internet Settings > Change Adapter Options > Right-click adapter > Properties > Double-click Internet Protocol Version 4 (TCP/IPv4). Change the DNS to the Server (`192.168.10.7`). Head back to Computer Name/Domain Changes (this window should still be open), and select "OK". Login with the administrator credentials and restart the machine.

![alt text](<../Images/Windows Server Configuration (12).png>)

![alt text](<../Images/Windows Server Configuration (13).png>)

![alt text](<../Images/Windows Server Configuration (14).png>)

- After restart the machine, we will login to the target machine using our newly create user. In this project we will use user Jenny Smith. Simply select other user > login using Jenny Smith credential (username: jsmith, password: adsf1234QWER) and make sure our sign in to is pointing to our domain.

![alt text](<../Images/Windows Server Configuration (15).png>)

![alt text](<../Images/Windows Server Configuration (16).png>)

![alt text](<../Images/Windows Server Configuration (17).png>)

# **5. Kali Linux Brute Force Attack on the Target Machine, View Telemetry via Splunk, Setup & Install ART (Atomic Red Team)**
## **5.1. Configure Kali Linux Network**

- Change Connection on Kali Linux to static IP address (`192.168.10.250`) based on Diagram we designed.
- Right Click “Ethernet Icon” > Select “Edit Connection” > Wired connection 1 > Click the Setting Icon > IPv4 Settings > change the “Method” to “Manual” > Add >Address: `192.168.10.250` > Netmask: `24` > Gateway: `192.168.10.1` > DNS servers: `8.8.8.8` > Save.

![alt text](<../Images/Kali Linux Configuration and Crowbar Installation (1).png>)

![alt text](<../Images/Kali Linux Configuration and Crowbar Installation (2).png>)

![alt text](<../Images/Kali Linux Configuration and Crowbar Installation (3).png>)

- To apply the change we need to Disconnect from the network and rejoin again. Then check the static IP from terminal. 

![alt text](<../Images/Kali Linux Configuration and Crowbar Installation (4).png>)

- We can check for connectivity by pinging `[google.com](http://google.com)` or our splunk server `192.168.10.10`

## **5.2. Install Crowbar to Simulate Brute Force Attack Attack**

- Update and Upgrade Kali Linux `sudo apt-get update && sudo apt-get upgrade -y`
- move to desktop, make a folder called ad-project (`mkdir ad-project`)
- install crowbar (`sudo apt-get install -y crowbar`)
- navigate to `cd /usr/share/wordlists`  .
- type ls and gunzip the `rockyou.txt.gz`  using  `sudo gunzip rockyou.txt.gz` . type ls again and we will have the `rockyou.txt` file.

![alt text](<../Images/Crowbar Installation.png>)

- copy `rockyou.txt` file to ad-project folder using  `cp rockyou.txt ~/Desktop/ad-project`
- take the first 20 line by typing `head -n 20 rockyou.txt > passwords.txt`

## **5.3. Enable Remote Desktop**

- On our target machine we will enabling the remote desktop by searching “This PC” > Properties > Advance System Settings > log-in using administrator > click “Remote” > Click Allow remote connections to this computer > Select User > add > enter our user username (tsmith, jsmith)> click ‘Check’ > ok > ok > apply.

![alt text](<../Images/Enable RDP (2).png>)

![alt text](<../Images/Enable RDP (1).png>)

## **5.4. Simulate Attack**
- Navigate back to our Kali Machine, then type `crowbar -h`  to see the help menu.
- Crowbar is a brute force tool which supports OpenVPN, Remote Desktop Protocol, SSH Private Keys and VNC Keys. (That’s why we enable the remote desktop and using crowbar)
- In this simulation we will targeting tsmith. Run `crowbar -b rdp -u tsmith -C passwords.txt -s 192.168.10.100/32`
    - -b : to choose protocol
    - -u : to choose the username of target
    - -C : to specify a password list file
    - -s : specify source target IP
    - /  : CIDR (Classless Inter-Domain Routing) is a method for representing IP addresses and their associated network masks.
    - /32,  indicates that there is no room for other hosts in the network; it is a single IP address. This is often used for specific routing purposes, such as when you want to route traffic to a particular device or when configuring firewall rules.
    - if **/24** would mean that the first 24 bits of the address are used for the network, which would allow for 256 addresses (from **`192.168.10.0`** to **`192.168.10.255`**). This is typically used for a subnet that can accommodate multiple hosts.

## **5.5. Analyze Telemetry Using Splunk**

- Open splunk server on browser and login
- Search endpoint index using `index=endpoint` key word
- Splunk will provide us with information of something happened to Terry's account we can also add `tsmith`.
- Scroll down and select `EventCode` there is an event with Value `4625` stands out.

![alt text](<../Images/Crowbar Bruteforce Attack (1).png>)

- Using your search engine to search value 4625, https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4625
- 4625 indicates Account Failed to Log on, and it can be noted all of the counts are occurring at approximately the same time which is an indication of brute force activity

![alt text](<../Images/Crowbar Bruteforce Attack (3).png>)

- Using your search engine to search value 4624, https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4624 , it indicate Account was successfully logged on.

![alt text](<../Images/Crowbar Bruteforce Attack (2).png>)

## **5.6. Run Tests on the Target Machine using Atomic Red Team (ART)**

- On target machine, open Powershell using administrator. Run `Set-ExecutionPolicy Bypass CurrentUser` > `Y`
- Navigate to Windows Security > Virus & threat protection > Manage Settings > Add or Remove Exclusions > Add an exclusion > Folder > This PC > Local Disk (C:).
- Navigate back to Powershell, run: `IEX ( IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing);` >`Install-AtomicRedTeam -getAtomics` and `Y`.
- Next, go to the (C:) drive > AtomicRedTeam > Atomics. You can also visit https://attack.mitre.org/ to explore adversary attacks and techniques, which can serve as a reference for the "T" values.
- In this example we will use `T1136.001` which is test for persistence by creating a local account. (`Invoke-AtomicTest T1136.001`)

![alt text](<../Images/Atomic Test T1059 (2).png>)

- Check to splunk, by searching index=endpoint NewLocalUser 

![alt text](<../Images/Atomic Test T1059 (3).png>)

- This indicate that we have just identified a gap in our protection to detect this activity. if an attacker compromise our system and created local account with current settings, we won’t be able to detect it.
- AtomicRedTeam help us to indentify gaps and visibility and generate Telemetry to see if our system can actually detect that activity.
- Next we will try using T1059 (Command and Scripting Interpreter).  `Invoke-AtomicTest T1059.001`

![alt text](<../Images/Atomic Test T1059 (4).png>)

- Defender is catching some threat.
- Bypass no profile

![alt text](<../Images/Atomic Test T1059 (2).png>)

- At splnuk we get the bypass noprofile by searching powershell

![alt text](<../Images/Atomic Test T1059 (1).png>)

- If we search for NewLocalUser

![alt text](<../Images/Atomic Test T1059 (5).png>)