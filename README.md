<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />






<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>


In this Lab we will create two VMs in the same VNET. One will be a Domain Controller and the other will be a Client Virtual machine. The client VM  which is going to serve as Cient  will be joined to the domain controller .
We will control the DNS settings on the Client to use the Domain Controller as its DNS server. Note: We will change the DC (Domain Controller) to  a static  private IP Address which will not change no matter if the computer is restarted.
The reason is because it's offering Active Directory services to the Client Machine.

<p>
<img src="https://i.imgur.com/WcMjiXR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the VM is created, we are going to turn off the firewall. Right click on the start menu on the Domain Controller and click run and type wf.msc for windows firewall and turn off the firewall. We are going to set Client-1's DNS settings
to DC-1'S Private Address. We are simply going to use the private IP Address of DC-1 and go to Client-1 network interface/IP configuration. On the left go to DNS servers and change it from inherent from vitual network from AZure to customs
and paste our private IP Address we copied from DC-1. So whenever the computer wants to look up anything it will look to DC-1 for it instead of Vnet DNS servers.
</p>

<br />

<p>
<img src="https://i.imgur.com/JHHKrtY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/7XSCqcX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Next is to go to Azure portal and restart Client-1 and try to ping DC-1  private IP Address from Client-1 and see if it works. 
</p>
<img src="https://i.imgur.com/6Dwglkx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/EXGCMeo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
