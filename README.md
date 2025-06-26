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



<h2>Deployment and Configuration Steps</h2>


In this Lab, we will create two VMs in the same VNET. One will be a Domain Controller and the other will be a Client Virtual machine. The client VM,  which is going to serve as Client  will be joined to the Domain Controller .
We will control the DNS settings on the Client to use the Domain Controller as its DNS server. Note: We will change the DC (Domain Controller) from dynamic to  a static  private IP Address which will not change no matter if the computer is restarted.
The reason is because it's offering Active Directory services to the Client Machine.

<p>
<img src="https://i.imgur.com/eFkGDVS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

 <img src="https://i.imgur.com/3yRgKKv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
After the VM is created, we are going to turn off the firewall. Right click on the start menu on the Domain Controller and click run and type wf.msc for windows firewall and turn off the firewall. We are going to set Client-1's DNS settings
to DC-1'S Private Address. We are simply going to use the private IP Address of DC-1 and go to Client-1 network interface/IP configuration. On the left go to DNS servers and change it from inherent from vitual network from AZure to custom
and paste our private IP Address we copied from DC-1. So whenever the computer wants to look up anything it will look to DC-1 for it instead of Vnet DNS servers.
</p>

<br />

<p>
<img src="https://i.imgur.com/JHHKrtY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/7XSCqcX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Next is to go to Azure portal and restart Client-1 and try to ping DC-1  private IP Address from Client-1 and it should work. 
</p>
<img src="https://i.imgur.com/6Dwglkx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<img src="https://i.imgur.com/EXGCMeo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
</p>
Next is to install Active Directory Domain Services from DC-1. Click start menu > Server manager > Add features/roles-Next-Next, in the Server selection there should be only DC-1 that is there. On server roles we will install Active Directory
Domain services. Click Add Features > Next > Next > Next click restart  if required and install. Next is to configure the installed Active Directory into a Domain controller and name it as my Domain.com. After installation is completed, DC-1 automatically
logs me off. Next, log back in DC-1 as user: mydomain.com\labuser. The reason is because we basically turned this VM into Domain Controller. The context of this is when people log in now the user account show in the Domain we are going to use to log
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
Next, we are going to create a new employee named "Jane Doe" as Admin. Add her to Domain Admin security group. Next log out  from DC-1 and log back again as mydomain.com\Jane_admin. Next Login to Client-1 and join it to the domain (computer will restart) 
Login to the Domain Controller and verify Client-1 shows up in ADUC (Active Directory Users and Computers). Create a new Organizational Unit  named “_CLIENTS” and drag Client-1 into there.


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
Next: Create non-administrative user on Client-1 by logging into Client-1 as mydomain.com\jane_admin and open System Properties. Allow Domain Users access to Remote Desktop we can now log into Client-1 as a normal, non-administrative user now.
<img src="https://i.imgur.com/WW5PFvh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
</p>
Next: We are going to use powershell to create a whole bunch of users inside  Active Directory. To do that, we are going to login to DC-1 as jane_admin and open powershell_ise as an administrator. Create a new file and paste the information of the script
into it and run the script and observe the account being created. When we are done, we will open Active Directory Users and Computers and we will observe the account in the approprriate organizational unit "_EMPLOYEE" section. finally we are going to 
pick one user (redu.figu) created and attempt to login with it in Client-1  remote desktop and see if it works (take note of the password in the script).
 
<img src="https://i.imgur.com/7kYTtiq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/tFn88lX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/OIH7AUc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Gmrz5Fo.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
</p>
Next: We will be working on Group policy and Managing Accounts. We will be dealing with Account Lockouts. To do that,  we first need to set up Account Lockout Policy in Active Directory, so we are going to use Group Policy to configure it. We are going to login into the Domain
Controller and to the search bar and type gpmc.msc and open Group Policy Management Console. Go to my domain.com and expand and right click to edit Default Domain Policy. In the Group Policy Management Editor, expand Computer Configuration - Policy -Window settings - Security Settings - Account Policies - Account Lockout Policy and configure Account Lockout Policy Settings. we will then pick a random user account we  created previously in DC-1 and attempt to login with it in Client-1 10 times with a bad password and observe that the account has been locked out within Active Directory. We will then go to Domain Controller and right click on mydomain.com and find the Account and   unlock the account, Reset the password and attempt to log in with the right password  in Client-1 and it should work.

<img src="https://i.imgur.com/MtqpqAl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/D0iRplO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/kutaCoO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/9wMues7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/64uCz16.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/uierh0Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/bNt1Ggu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Wy5C7hq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
</p>
Next: We will be disabling and enabling accounts in Active Directory. To do that right click on the account and disable the account. To activate the account  right click on the account to eanble it back.

<img src="https://i.imgur.com/4WerXI7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/sXwvU5A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
