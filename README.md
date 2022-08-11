# Apache_on_CentOS
**Install Apache Web Server on CentOS 7**


**(Update Software Versions List)**
sudo yum update 
 
**(Install Apache)**
sudo yum install httpd

**( Activate Apache)**
sudo systemctl start httpd 
sudo systemctl enable httpd

**(Verify Apache Service)**
sudo systemctl status httpd

**Configure firewalld to Allow Apache Traffic**

**Modify your firewall to allow connections on these ports using the following commands:**
sudo firewall-cmd ––permanent ––add-port=80/tcp
sudo firewall-cmd ––permanent ––add-port=443/tcp

**Once these complete successfully, reload the firewall to apply the changes with the command:**
sudo firewall-cmd ––reload
 
**Configure Virtual Hosts on CentOS 7 (optional)**
Virtual hosts are different websites that you run from the same server. Each website needs its own configuration file.

Make sure these configuration files use the .conf extension, and save them in the /etc/httpd/conf.d/ directory.

There are a couple of best practices to use when you’re setting up different websites on the same server:

Try to use the same naming convention for all your websites. For example:
/etc/httpd/conf.d/MyWebsite.com.conf
/etc/httpd/conf.d/TestWebsite.com.conf
Use a different configuration file for each domain. The configuration file is called a vhost, for a virtual host. You can use as many as you need. Keeping them separate makes troubleshooting easier.

**To create a virtual host configuration file, enter the following into a terminal window:**
sudo vi /etc/httpd/conf.d/vhost.conf
**In the editor, enter the following text:**

NameVirtualHost *:80
<VirtualHost *:80>
ServerAdmin webmaster@MyWebsite.com (change into your server admin)
ServerName MyWebsite.com (change into your server name)
ServerAlias www.MyWebsite.com (change into site name)
DocumentRoot /var/www/html/MyWebsite.com/public_html/ **(change into whare the file is located located in your pc)**
ErrorLog /var/www/html/MyWebsite.com/logs/error.log **(change into whare the log file located located in your pc)**
CustomLog /var/www/html/MyWebsite.com/logs/access.log **combined (change into whare the custom log file located in your pc)**
</VirtualHost>
 
sudo mkdir /var/www/MyWebsite/{public_html, logs}
sudo systemctl restart httpd

Once the system finishes, you should be able to open a browser window to MyWebsite.com and see a default Apache test page.

You can replace MyWebsite above with the name of your domain. If you are hosting more than one domain, make sure you create a new directory in /var/www/ for each one. You can copy the code block in your /etc/httpd/conf.d/vhost.conf file, and replace MyWebsite with another domain name that you’re hosting.

**Apache Directories and Files**

One of the main ways Apache functions is through configuration files. They are located at /etc/httpd.

Apache has a main configuration file: /etc/httpd/conf/httpd.conf .

If there are any other configuration files, they are included in the main configuration file. They should use the .conf extension and should be stored in the **/etc/httpd/conf.d/ directory.**

You can enhance Apache’s functionality by loading additional modules.

The configuration files for these modules should be stored in: **/etc/httpd/conf.modules.d/ directory.**

Log files record all the activity of the Apache service, including client activity on the websites your system is hosting. These logs can be found in:  **/var/log/httpd/.**

**Commands For Managing Apache Service**
Stop Apache Service:
sudo systemctl stop httpd

Prevent or disable Apache from starting when the system boots:
sudo systemctl disable httpd

Re-enable Apache at boot:
sudo systemctl enable httpd

Restart Apache and apply any changes you have made:
sudo systemctl restart httpd

Enjoy with appache server...............
