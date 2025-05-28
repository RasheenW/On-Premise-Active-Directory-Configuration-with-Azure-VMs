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

 <h2>Objectives </h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Install Active Directory</h2>

To start things off, We're going to set our DC-1 VM as our Domain Controller and install Active Directory within it
Open the start menu, Click on "Server Manager" and this window should open 
<img src=https://i.imgur.com/GKJ8O9u.png>

Now Select "Add Roles and Features", click next until you get to "Server Roles" and check "Active Directory Domain Services"

<img src=https://i.imgur.com/adWtWCT.png>

Continue to click next until you reach 'Confirmation" and check the box to restart then click install

<img src=https://i.imgur.com/w2dMGy6.png>

Now that Active Directory is installed, You need to actually promote it to be a Domain Controller. Click the flag in the top right, Then proceed to click "Promote this server to a Domain Controller"

<img src=https://i.imgur.com/J3pyF9B.png>

When this window appears, Click on 'Add New Forest" and for the Root Domain Name type in "mydomain.com". Once you proceed to click next

<img src=https://i.imgur.com/gdVQJeM.png>

On this screen for the password we're just gonna go with "Password1", (This feature won't be used for this lab anyway)

<img src=https://i.imgur.com/BY4KYqv.png>

Proceed to DNS Options and Unchecked the box for Create DNS Delegattion 

<img src= https://i.imgur.com/S46fTGo.png>

Continue to click next unil you get to "Prerequisites Check" and press install

<img src=https://i.imgur.com/QW2GGny.png>
