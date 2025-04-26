<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>


- You will need to have created two Azuzre virtual machines. One running Windows 10 and another running Ubuntu Linux.
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>
<p>
Within your Windows 10 virtual machine, download and install WireShark. Open the Wireshark App and click on the 'Ethernet' interface. Click on the shark fin in the top left corner. Filter for ICMP traffic (what the ping command uses) by typing 'ICMP' in the box that says 'Apply a Display Filter'. In Windows Powershell, ping the private ip address of the Linux vm. Observe the ICMP traffic in Wireshark. We can see the requests from the source vm (Windows 10) and the reply from the destination vm (Linux Server 24)
</p>
<br />

<p>
<img src="https://imgur.com/wK7By1G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we will configure the Linux vms firewall to block ICMP traffic. Initiate a nonstop ping from the Windows vm to the Linus vm. type the command ping (the private ip of the Limux vv) -t. 
  <p>
<img src="https://imgur.com/nwmvNDA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<br />

<p>
Within the Azure portal, go to the Linux vm. Go to the 'Networking' tab. then to 'Network Settings'. Click the link under 'Network Security Group'. CLick 'Settings' and then 'inbound security rules'. Click 'Add'. Put an asterisk under Source port ranges and destination port ranges. Put 'any' for destination. Set the priority to 290. Set the  action to 'deny'. Then click 'add'. The requests from the Windows Machine will start to time out because of the configured firewall.
  <p>
<img src="https://imgur.com/ZGSCMYz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<br />
<p>
Delete the rule in the Azure portal on the Linux vm to resume ICMP traffic. 
</p>
<br />
<p>
Now, we will observe SSH traffic in WireShark. Start another packet capture and filter for ssh traffic this time. From the Windows 10 vm SSH into the Linux Server 24 vm. Type in: ssh username@<private ip address> (This is for the Linux vm). Then enter the password for the linux machine. Note that the prompt changed and we are now 'in' the Linux machine.
  
  <p>
<img src="https://imgur.com/undefined.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
 <p>
<img src="https://imgur.com/w7JpJaG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<br />
<p>
