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

It'll automatically restart afterwards and once it does, We will relog into DC-1 now as a Domain User. In username type in "mydomain.com\labuser"

<img src=https://i.imgur.com/vbZXx8d.png>

<h2> Domain Admin User Creation </h2>

Now within Active Directory we will be creating an Orginazational Unit that we will call "_Employees", "_Admins" & "_Clients" within DC-1 (These names are important, Within the next section we will be utilizing a script that uses _EMPLOYEES)
The first step to navigate there, Click start, Open "Windows Administrative Tools" Folder & Click "Active Directory Users and Computers"

<img src=https://i.imgur.com/Nr4ryFS.png>

Within here you want to right click "mydomain.com", proceed to click "New" then "Orginzational Unit". Once thats done input "_EMPLOYEES" for our first unit and repeat the same process for "_ADMINS" & "_CLIENTS"

<img src=https://i.imgur.com/Vu8HX3e.png>
<img src=https://i.imgur.com/SFqjF3e.png>

Now we will create an actual employee, For this example I'll just use "Jane Doe" but feel free to use any name you want. Now right click the "_ADMINS" folder we just created, Click "New" then "User". The username will be "jane_admin", Password "Cyberlab123!"; For this lab click "Password never expires" box just for convienency (In a real setting you wouldn't do this)

<img src=https://i.imgur.com/a1flNLy.png>
<img src=https://i.imgur.com/BvmvLBT.png>
<img src=https://i.imgur.com/attzO9Y.png>

Even though we created our admin within the group they actually aren't one yet, So now we will give them the permissions of one. Right click your employee name within "_ADMINS" then click "Properties". 

<img src=https://i.imgur.com/kFMp36A.png>

Click "Member of", Click "Add", Type in "Domain Admins", Click "Check Names", Click "Ok" then "Apply" Now your employee should be a Domain Admin.

<img src=https://i.imgur.com/WVIk3sx.png>

Now we will log out of our DC-1 rdp and relog as our new Domain Admin (mydomain.com\jane_admin), For the rest of this lab we will use this account from this point on.

<img src=https://i.imgur.com/QuFrwkh.png>

<h2> Client-1 Connection To Domain </h2>

This part has roughly been set up prior to what we did previously in Azure when we changed the DNS setting to DC's Private IP Address, Now we will just log into Client-1 as "labuser". Once logged in right click "Start", click "System" and click "Rename this PC (advanced)" 

<img src= https://i.imgur.com/J6y9gnL.png>

Then click "Change" and for Member of type in "mydomain.com"

<img src= https://i.imgur.com/6S9PX8c.png>

Now we will simply log into as our Domain Admin User, Once done we will need to restart the RDP

<img src=https://i.imgur.com/NJPUI0v.png>

Now we will open our DC-1 VM and confirm that Client-1 shows up in ADUC (Active Directory Users and Computers)
Simply dropdown "mydomain.com", click "Computers", Client-1 should appear and from there we will drag Client-1 into the "_CLIENTS" OU we made earlier

<img src=https://i.imgur.com/55v5uAw.png>

<h2> RDP Setup for Non-admin Users </h2>

Within Client-1 we will allow Domain Users to access it through RDP, So right click the Start menu, click "System" then click "Remote Desktop". After that click "Select Users that can remotely access this PC", Click "Add, proceed to type in "Domain Users" & click "Check Names". Once done, Click OK multiple times until the pop up window closes, Normally we would provide User Access through a Group Policy but we will tinker with that later on in the lab

<img src=https://i.imgur.com/4D9ERnz.png>
<img src=https://i.imgur.com/m5hlZAc.png>

I will conclude the lab here, The next portion will touch on User Creation, Account Management & Group Policy
