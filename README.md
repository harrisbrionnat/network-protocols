<p align="center">
    <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines
In this tutorial, we observe various network traffic to a Windows 10 vm with Wireshark and explore Network Security Groups.


## Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, DHCP, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used 
- Windows 10 (21H2)
- Ubuntu Server 20.04

## High-Level Steps
- Create two Azure virtual machines: one running Windows 10 and another running Ubuntu Linux.
- Examine ICMP traffic with Wireshark.
- Examine SSH traffic with Wireshark.
- Examine DHCP traffic with Wireshark.
- Examine DNS traffic with Wireshark.
- Examine RDP traffic with Wireshark.

## Actions and Observations

### 1. Examine ICMP Traffic
Within your Windows 10 virtual machine, download and install Wireshark. Open the Wireshark app and click on the 'Ethernet' interface. Click the shark fin in the top left corner. Filter for ICMP traffic (what the ping command uses) by typing `ICMP` in the box that says 'Apply a Display Filter'. 

In Windows PowerShell, ping the private IP address of the Linux VM. Observe the ICMP traffic in Wireshark where you can see requests from the source VM (Windows 10) and replies from the destination VM (Linux Server 24).

![ICMP Traffic](https://imgur.com/wK7By1G.png)

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





