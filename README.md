**Goal** Create a Windows 10 VM to host osTicket and supporting software (IIS, PHP, MySQL).

## Step 1 — Create the Windows 10 VM (Azure Portal)

**Exact steps and UI paths**

1. Azure Portal → **Create a resource** → **Compute** → **Virtual machine**.
   - On **Basics** tab:
     - Subscription: `AZURE subscription 1`
     - Resource group: `osticket-vm` (create new)
     - Virtual machine name: `osticket-vm`
     - Region: **East US 2**
     - Image: **Windows 10 Enterprise - 22H2**
     - Size: **Standard_E2s_v3**
     - Administrator account: `labuser` 

   ![VM Basics](/basics.png)

2. On **Disks** tab:
   - OS disk type: `Premium SSD`
   - Data disk: none added for this lab
   ![Disks](/disks.png)

3. On **Networking** tab:
   - Virtual network: `vnet-eastus2(osticket-vm)` (create new)
   - Subnet: `default`
   - Public inbound ports: **RDP (3389)** — restricted to your public IP address `X.X.X.X/32`
   ![Networking](/networks.png)

4. Review + Create → Confirm the validation passed → **Create**.
   - Screenshot: `/review.png` (shows the review page and validation).

5. After deployment, open the VM **Overview** page:
   - Verify public IP address and status **Running**.
   ![VM Overview](/overview.png)

6. Connect via RDP:
   - Download RDP → RDP → Click the "+" → Add PC → Put in the public IP address → click "add" → then enter the login: "labuser" and password: "Cyberlab123!"
   ![RDP Desktop](/connection.png)

## Step 2 Confirguring osTicket

1. Within the VM download ZIP file and unzip it.
- Download osTicket-Installation-Files.zip within VM
- Then on the ZIP file right click it and click extract all then click extract.
![ZIP File](/zip.png)

2. Enable IIS
- Go to the Control Panel In the VM
- Under Programs click on "Uninstall a program" 
- Then on the side of the panel click on "Turn windows features on or off"
- Then find "Internet Information Service" and click it 
- Then expand IIS by clicking the "+" button then expand "World Wide Web Service"
- Then expand "Application Developement Features" and check it
- Then click ok in the bottom right corner
![Enable IIS and CGI](/IIS.png)

## Step 3 Installing PHP Manager

1. Go to the "osTicket-Installation-Files"
- Double click on PHPManagerForIIS_V1.5.0
- Click "next" then "I agree" once installed close the tab
![Install PHP](/PHP.png)

2. Install "rewrite_amd64_en-US"
- Then within the same folder we will install rewrite_amd64_en-US
- Agree to the terms then click install
![Install "rewrite_amd64_en-US"](/rewrite.png)

## Step 4 Create the directory C:\PHP
- Go to (C:) drive and create a folder named PHP
- Then we will unzip the "php-7.3.8-nts-Win32-VC15-x86" file from the "osTicket-Installation-Files" folder to the new PHP folder
- Then right click on the "php-7.3.8-nts-Win32-VC15-x86" file and click extract all
- Then click browse and click on the new PHP folder we created and extract "php-7.3.8-nts-Win32-VC15-x86" to the C:\PHP folder
![PHP](/PHP.png)

## Step 5 Install VC_redist.x86
- Double click and agree to the terms and condtions and click install
![VC_redist.x86](/VC.png)

## Step 6 Install mysql
- Double click on the "mysql-5.5.62-win32" file
- Click "next" then accept the liscense agreement then click "next"
- Then for the setup type select "typical" then click "next"
- Then click "Install"
- Also make sure to check "Launch the MySQL instance configuration wizard" and then click "finish"

## step 7 Configure mysql
- Click "next" then choose "Standard Configuration" then click "next"
- Then click "next" agian
- Then for the root password we will set it to "root" so type root for the password then "next"
- The click "execute"
![mysql-5.5.62-win32](/sql.png)

## Step 8 Register PHP within IIS
- Open IIS as an admin click start type in IIS and right click it and select "Run as an administrator"
- Then double click "PHP Manager" and select "Register new PHP version"
- Then browse to it click the the "..." on the right
- Then go to the (C:) drive and click on "php-cgi.exe" and click "open" then click "ok"

## Step 9 Reload IIS
- Then in the IIS Manager right click on the "osticket-vm(osticket-vm\labuser)" and click "stop"
- Then Right click it agian and click "start"
![IIS](/IIS.png)

## Step 10 Install osTicket
- Back in the "osTicket-Installation-Files"
- Right click on the "osTicket-v1.15.8" file and click "extract all" then click "extract"
- Then in the "osTicket-v1.15.8" folder their will be a "scripts" and "upload" folder within "osTicket-v1.15.8"
- Then copy the "upload" folder to the "c:\inetpub\wwwroot"
- Then within the "c:\inetpub\wwwroot" rename the "upload" folder to "osTicket"

## Step 11 Reload IIS Manager agian 
- Open IIS manager and right click it and "Run as Administrator Agian"
- Right click on "osticket-vm" click "stop" and then click "start"
- Then click on the dropdown arrow on "osticket-vm" and then click on the dropdown button on "Default Web Sites" then on the right click on "browse *:80(http)"
![Reload IIS](/Reload.png)
---
- Now you should be able to see the osTicket Installer page
![osTicket Page](/page.png)

## Step 12 IIS Configurations
- Go back to IIS and make sure to "Run as Administrator"
- Go back to IIS, sites -> Default Web Site -> osTicket
- Double click on PHP manager
- Then under PHP extensions click on "enable or disable extensions"
- Then Enable: php_imap.dll, php_intl.dll, and php_opcache.dll
- Then refresh the osTicket site and we should see the changes

![osTicket Page Refresh](/Refresh.png)

## Step 13 Rename ost-config.php and assign permissions
- Rename: ost-config.php, From: "C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php" To: "C:\inetpub\wwwroot\osTicket\include\ost-config.php"
- Right click on ost-config.php click "properties" go to the "security" tab
- Assign Permissions: ost-config.php, click advance then click "Disable inheritance" -> Remove All,
- Then click "add" New Permissions then add Everyone and basic permissions select all basic permissions
- Click "apply" and "ok"
![ost-config.php](/config.png)

## Step 14 Install HeidiSQL
- Double click hit "next" and then click "install" and then "finish"
- Then in HeidiSQL at the bottom click "new"
- User: root
- Password: root
- Then click "open"
- Right click on unamed and then "create new" then select "database"
- Then for the name use "osTicket" then click "ok"
![HeidiSQL](/heidi.png)

## Step 15 Setting up osTicket in the browser
- Then go back to the osTicket and click "continue"
- For Help Desk Name: "My Help Desk"
- Then for email: lukasemail@gmail.com
- Admin username: "adminuser" Admin password: "Password1"
- Database settings: mySQL Database: osTicket, MySQL Username: "root", mySQL Password: "root"
- Then click "Install Now" at the bottom of the page
![osTicket](/baisc.png)

## Step 16 Go to your osTicket URL:
- Now we will go to our help desk Agemt login page "http://localhost/osTicket/"
- And Access the end user page http://localhost/osTicket/
![osTicket](/admin.png)
![osTicket](/enduser.png)






