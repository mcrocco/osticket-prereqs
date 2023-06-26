<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Installing IIS (Internet Information Services) and PHP Manager for IIS
- Download and Install Rewrite Module
- Download PHP
- Download VC executable
- Download MySQL and HeidiSQL

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/UnxODtv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In order for osTicket to function as a server, we first must enable IIS on our Windows machine. In the search bar next to the start button, search "add or remove programs" open the system settings, select Programs and Features on the top right, and then select "Turn Windows features on or off". Scrolling down to Internet Information Services, check that box, along with World Wide Web Services once it is expanded. In addition, make sure CGI is marked under Application Development Features. The picture above is what the Windows Features screen should look like after enabling everything. Click "OK" to install IIS. 
</p>
<br />

<p>
<img src="https://i.imgur.com/MVCKbJ2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This link will provide all of the installation files needed to properly install osTicket: https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6. The picture above represents all of the files in the google drive link.

First, install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi) and the Rewrite Module (rewrite_amd64_en-US.msi). 

Create the directory C:\PHP on File Explorer

Go back to the installation files and download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the file into the directory C:\PHP

Download and install VC_redist.x86.exe

Download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
  - Choose typical setup when installing MySQL
  - Choose Standard Configuration when MySQL launches and enter a password to remember
</p>
<br />

<p>
<img src="https://i.imgur.com/nk2maGo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After installing all of those files, we have to now register PHP from within IIS. To do this, go to the search bar and type "IIS", right click the application and select to run it as an administrator. Click on osTicket in the top left, and then find and select PHP Manager. The picture above is the screen that should appear. Select "Register new PHP version", click the three dots (...) to open the PHP directory that was created. Select php that is listed as an application, then open. The path should be as it is shown above. If it is, select OK. Go back to the main IIS menu and select Restart on the top right corner to reload IIS with the new PHP. 
</p>
<br />

<p>
<img src="https://i.imgur.com/a1eHMzM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After registering PHP, go back to the installation files and download osTicket v1.15.8. Once the zip file is extracted, copy the "upload folder" to c:\inetpub\wwwroot
  - Within wwwroot, rename "upload" to "osTicket" and restart IIS again
In IIS, go to Sites, Default and then osTicket
  - On the right-hand side click Browse *:80 to take you to the webpage that osTicket is running on. 

At this point the picture above is what should be showing on the web page, minus a couple of check marks. To enable more extensions, go to IIS, Sites, Default and then osTicket. Select PHP Manager and individually select php_imap.dll, php_intl.dll & php_opcache.dll and then select enable in the top right for each. Refreshing the osTicket webpage will show more checkmarks like what is shown above. 
</p>
<br />

<p>
<img src="https://i.imgur.com/j72YKDH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Before installing HeidiSQL, ost-sampleconfig.php needs to be renamed to ost-config.php. This can be found in the C:\inetpub\wwwroot\osTicket\include directory. Additionally, ost-config.php needs to have a permission of everyone having access to the file. So, right-click the file, select Properties, Security and then Advanced. Choose Disable Inheritance and Remove All to get rid of all of the default permissions, and then go to New Permissions, type in "everyone", check names, and give this all of the access privileges. 

Now we can go back to the installation files and install HeidiSQL
  - After opening HeidiSQL, create a new session and create a password to remember
  - "root" should already be displayed as the username
  - Open the session
  - Create a database titled "osTicket"
</p>
<br />

<p>
<img src="https://i.imgur.com/IaVFGuB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Selecting "Continue" on the osTicket webpage will bring you to a screen that is shown above. Feel free to name the Helpdesk whatever you would like, along with an email that will be used to receive ticket information from customers. Put in information for the Admin User as well. In this case, user_admin will be the username for the Admin User (remember the created password for this user, as it will be needed to login to osTicket itself). 

Go back to HeidiSQL to fill out the MySQL Database (osTicket), Username (root) and Password. Finally, you can click Install Now!
  - Note: once osTicket is fully installed, delete C:\inetpub\wwwroot\osTicket\setup and set the permissions of ost-config.php to read only for clean up purposes
</p>
<br />
