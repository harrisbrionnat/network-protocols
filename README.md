<p align="center">
    <img src="https://imgur.com/YG6yT33.png" alt="Traffic Examination"/>
</p>

# Installing a VPN Server on a Windows 10 Virtual Machine
In this tutorial, we use Azure to create a virtual machine. On which, we will install ProtonVPN and analyze differences in ip address, location, and common websites.


## Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- MacOS Sonoma 14.0
- ProtonVPN



## Operating Systems Used 
- Windows 10 (21H2)
- MacOS Sonoma

  You will need to have created a Windows 10 virtual machine in Azure and set the location to West US 2.

## Actions and Observations

 1. Within your OWN pc, go to wwww.whatismyipaddress.com. Observe the following: ip address, location, ISP. Then go to the ProtonVPN website and create a free account. Do not download.

![myPC](https://imgur.com/daHIGrc.png)

### 2. Block ICMP Traffic
Next, we will configure the Linux VM's firewall to block ICMP traffic. Initiate a nonstop ping from the Windows VM to the Linux VM by typing the command:

ping  -t


![Block ICMP](https://imgur.com/nwmvNDA.png)

### 3. Configure Network Security Group
Within the Azure portal, navigate to the Linux VM. Go to the **Networking** tab, then to **Network Settings**. Click the link under **Network Security Group**. Click **Settings** and then **Inbound security rules**. Click **Add** and configure the following:
- **Source port ranges**: *
- **Destination port ranges**: any
- **Priority**: 290
- **Action**: Deny

After adding this rule, the requests from the Windows machine will start to time out due to the configured firewall.

![Network Security Group Configuration](https://imgur.com/ZGSCMYz.png)

### 4. Resume ICMP Traffic
Delete the blocking rule in the Azure portal on the Linux VM to resume ICMP traffic.

### 5. Observe SSH Traffic
Now, we will observe SSH traffic in Wireshark. Start another packet capture and filter for SSH traffic. From the Windows 10 VM, SSH into the Linux Server 24 VM by typing:

ssh@username< private ip address >

Enter the password for the Linux machine. The prompt will change, indicating you are now in the Linux machine's command line using TCP port 22. End the connection by typing `exit`.
</p>
<p>
    <img src="https://imgur.com/w7JpJaG.png" height="80%" width="80%" alt="SSH Traffic"/>
</p>
<p>
    <img src="https://imgur.com/tTUttbJ.png" height="80%" width="80%" alt="SSH Command Prompt"/>
</p>

### 6. Observe DHCP Traffic
<p>
Start another packet capture in Wireshark and filter for DHCP. Open Notepad and type the following commands:

ipconfig /release
ipconfig /renew

Save this as `dhcp.bat` in `C:\ProgramData`. In PowerShell, navigate to `C:\ProgramData`, list the folder contents, and run `dhcp.bat`.
</p>
<p>
    <img src="https://imgur.com/C
      
### 7. Observe DNS Traffic
Start another packet capture in Wireshark and filter for DNS. In PowerShell, type each:

nslookup 8.8.8.8 
nslookup www.google.com

Observe the DNS traffic. You can also filter by its TCP and UDP port, which is 53.

![DNS Traffic](https://imgur.com/PqtO4NM.png)

### 8. Observe RDP Traffic
Now, we will observe RDP traffic in Wireshark. Start another packet capture and filter for RDP. Since we are remotely connecting to our two Azure VMs, we use RDP over TCP port 3389. To filter for this traffic, type: tcp.port == 3389

We will seemingly be spammed with traffic as RDP is constantly streaming a picture.

<p>
    <img src="https://imgur.com/rUMfpKJ.png" height="80%" width="80%" alt="RDP Traffic"/>
</p>





