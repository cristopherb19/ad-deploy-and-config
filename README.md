<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployment and Configuration</h1>
Welcome back!  In this project we will continue to build upon the Active Directory environment created in the previous project.  This project will focus on the installation and organization of active directory, domain administration, domain integration, and remote desktop access permissions.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Prerequisites</h2>

-  Please complete <a href="https://github.com/christianDCdev/active-directory-setup">Setup for Active Directory Infrastructure</a> before beginning this project

<h2>Objectives</h2>

- Install Active Directory
- Create an Active Directory Forest
- Create a Domain Admin User
- Join Client-1 to the Domain
- Set up Remote Desktop for non-administrative users

<h2>Configuration Steps</h2>

<h3>&#9312; Install Active Directory</h3>
<p>

- Connect to your DC-1 VM via Remote Desktop
- Open Server Manager Application
- Click "Add Roles and Features"
- Click "Next" until you reach "Server Roles"
- Select "Active Directory Domain Services" and click "Add Features"
<img src="https://i.imgur.com/GiPCO9P.png" height="80%" width="80%" alt="AD Domain services"/>

- Click "Next" until you reach "Confirmation"
- Check box that says "Restart the destination server automatically if required"
- Click "Install" to complete installation
  
</p>

<h3>&#9313; Promote DC-1 to a Domain Controller</h3>

<p>

- Within the Server Manager Dashboard, click on the flag at top right and click "Promote this server to a domain controller"
<img src="https://i.imgur.com/dXntZsV.png" height="80%" width="80%" alt="domain controller promotion"/>

- Select "Add a new forest" option
- Set "Root domain name:" to "mydomain.com"
<img src="https://i.imgur.com/OtjZXv7.png" height="80%" width="80%" alt="domain controller promotion"/>

- Under "DNS options", uncheck "Create DNS delegation"
- Complete forest installation and your VM should automatically restart once installation is finished
- Log back into DC-1 VM as a domain user by typing "mydomain.com\(your username)" as your username (Example: mydomain.com\labuser)

</p>
<br />

<h3>&#9314; Create a Domain Admin user within the domain</h3>

<p>

- Within DC-1 VM, open Active Directory Users and Computers application
- Right click "mydomain.com" on the right side of window
<img src="https://i.imgur.com/h7KNfAb.png" height="80%" width="80%" alt="AD user mydomain"/>

- Click "New" then click "Organizational Unit"
- Fill in the name as "_EMPLOYEES" and click "Ok"
- Create another organizational unit
- Fill in the name as "_ADMINS"
- Click on the "_ADMINS" folder
- Within the empty field on the right, right click -> click "New" -> then click "User"
<img src="https://i.imgur.com/eknzFYE.png" height="80%" width="80%" alt="new user"/>

- Fill out fields for a new user named "Jane Doe" with username "jane_admin"
<img src="https://i.imgur.com/Ze0cl5V.png" height="80%" width="80%" alt="jane doe info"/>

- Proceed and finish user creation (NOTE: Feel free to uncheck "User must change password at next logon" box for your convenience)
- Next we will add jane_admin to the built-in "Domain Admins" Security Group
- Right click on "Jane Doe" and click "Properties"
- Navigate to "Member of" tab -> click "Add"
- Type "Domain Admins" in the empty field
- Click "Check Names" to confirm you found the correct object name, click "Ok", then click "Apply"
<img src="https://i.imgur.com/MwxvjCA.png" alt="add jane to domain admins"/>

- Close or logout of the DC-1 VM connection
- Log back into DC-1 VM as "Jane Doe" (mydomain.com\jane_admin)
- From now on user "jane_admin" will be used as the admin account
  
</p>
<br />

<h3>&#9315; Join Client-1 to your Domain</h3>

<p>

- Login to Client-1 VM as original local admin (in my case username = "labuser")
- Within the Client-1 VM, right click Windows start button -> then click "System"
- Click "Rename this PC (advanced)" on the right side of window
<img src="https://i.imgur.com/VMU4jgm.png" height="80%" width="80%" alt="Rename PC"/>

- Under "Computer Name" tab, click "Change
- Check "Domain" bubble, type "mydomain.com" in the field, then click "Ok"
<img src="https://i.imgur.com/CHRciZK.png" alt="Domain change"/>

- A "Windows Security" window should pop up
- Fill in the username and password with "Jane Doe" information (Username: mydomain.com\jane_admin)
- Click "Ok" and if done correctly, you will see the following window pop up
<img src="https://i.imgur.com/35CF1Mr.png"  alt="Successfully joined domain"/>

- Click "Ok" and your VM will restart
- Within DC-1 VM, open "Active Directory Users and Computers" application
- Expand "mydomain.com" -> then click on "Computers" to verify if Client-1 is there
  
</p>
<br />

<h3>&#9316; Setup Remote Desktop for Non-administrative users</h3>

<p>

- Log into Client-1 VM as "Jane Doe" (mydomain.com\jane_admin)
- Navigate to "Settings" -> "System" -> "Remote Desktop"
- Click on "Select users that can remotely access this PC" at the bottom of window
- Click "Add"
- Type "Domain Users" in empty field
- Click "Check Names" to confirm you found the correct object name and click "Ok"
<img src="https://i.imgur.com/a6nHqwn.png" alt="Successfully joined domain"/>

- Now all normal users within the domain can log into Client-1
  
</p>
<br />

<h2>Conclusion</h2>

<p>
  
Congratulations on completing the deployment and configuration of this Active Directory project!  We should now have an active directory forest installed, a domain admin user, and our Client-1 VM should now be inside our domain.  In the next project we will populate our domain with generated users.

- If you would like to continue to the next step in this series of Active Directory projects, please click <a href="https://github.com/christianDCdev/ad-user-generation">here</a>

</p>
