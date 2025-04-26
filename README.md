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

 2. On your Windows 10 virtual machine, Download the ProtonVPN client on the account just created. Navigate to www.whatismyipaddress.com. Observe changes in the ip, location, and ISP. They are different because Azure has created its own secure tunnel similar to how Proton VPN creates its own VPN tunnels.


![win-10](https://imgur.com/bvfrKIX.png)

3. On the ProtonVPN client click 'get connected'. Your VPN server will make it appear as if it is in a different location. Mine appeared as if they were in The Netherlands and Japan. Observe the changes in the ip, location, and ISP. Try going to different websites and observe changes in the appearance, language, currency, etc.



![netherlands](https://imgur.com/wfxgjeA.png)
![netherlands](https://imgur.com/qvcxFO6.png)
![japan](https://imgur.com/vw0bqsW.png)
![japan](https://imgur.com/LZimggP.png)




