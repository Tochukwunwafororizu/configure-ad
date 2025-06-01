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
</p>
Next is to install Active Directory Domain Services from DC-1. Click start menu- Server manager - Add features/roles-Next-Next, in the Server selection there should be only DC-1 that is there. On server roles we will install Active Directory
Domain services. Click Add Features-Next-Next-Next click restart  if required and install. Next is to configure the installed Active Directory into a Domain controller and name it as my Domain.com. After installation is completed, DC-1 automatically
logs me off. Next, log back in DC-1 as user: mydomain.com\labuser. The reason is because we basically turned this VM into Domain Controller. The context of this is when people log in now the user account essist in the Domain we are going to use to log
back in and the user.


<img src="https://i.imgur.com/9oBoqti.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SUDKHi7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/YMCbrow.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Next is to create Domain Admin User within the Domain.  Having a Domain User is such a big deal in real life because the Domain Admin has so many rights across the Domain which includes assigning permisions to Managing Organizational Units (OUS),
establishing group policy objects (GPOS) etc. We are going to create our Organizational Units  called _EMPLOYEES. Basically, we will create two folder one called _employees and another _Admins. We will create a Domain Admin inside of this Admin folder.

</p>
<br />
<img src="https://i.imgur.com/Bs0VPTP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
</p>
Next, we are going to create a new employee named "Jane Doe" as Admin. Add him to Domain Admin security group. Next log out  from DC-1 and log back again as mydomain.com\Jane_admin. Next Login to Client-1 and join it to the domain (computer will restart) 
Login to the Domain Controller and verify Client-1 shows up in ADUC. Create a new Organizational Unit  named “_CLIENTS” and drag Client-1 into there.


</p>
<br />
<img src="https://i.imgur.com/z7T0Op5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/eAyeCTS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/WZjJmpp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/lgQLxlB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Aa4x3Ca.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/xZdnqOn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
</p>
Next: Create non-administrative user on Client-1 by logging into Client-1 as mydomain.com\jane_admin and open system properties. Allow domain users access to remote desktop we can now log into Client-1 as a normal, non-administrative user now.
