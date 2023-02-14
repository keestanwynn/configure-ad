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

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/YBlD51Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
Set Domain Controller’s NIC Private IP address to be static
Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet from previous steps.
Ensure that both VMs are in the same Vnet.
</p>
<br />

<p>
<img src="https://i.imgur.com/FaD3OoF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping). 
Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall. 
Check back at Client-1 to see the ping succeed. 
Login to DC-1 and install Active Directory Domain Services. 
Promote as a DC: Setup a new forest as mydomain.com. 
Restart and then log back into DC-1 as user: mydomain.com\labuser. 
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”. 
Create a new OU named “_ADMINS”. 
Create a new employee named “Jane Doe” with the username of “jane_admin”. 
Add jane_admin to the “Domain Admins” Security Group. 
Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”. 
User jane_admin as your admin account from now on. 


</p>
<br />

<p>
<img src="https://i.imgur.com/2zMLjxE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 as mydomain.com\jane_admin and open system properties. 
Click “Remote Desktop”. 
Allow “domain users” access to remote desktop. 
You can now log into Client-1 as a normal, non-administrative user now.  
Login to DC-1 as jane_admin. 
Open PowerShell_ise as an administrator. 
Run the script and observe the accounts being created. 
When finished, open ADUC and observe the accounts in the appropriate OU. 
Attempt to log into Client-1 with one of the accounts. 


</p>
<br />
