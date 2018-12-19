# Table Of Contents

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Table Of Contents](#table-of-contents)
	- [Install ownCloud](#install-owncloud)
	- [Prerequisites](#prerequisites)
		- [Install Red Hat Repository](#install-red-hat-repository)
		- [Install EPEL repository](#install-epel-repository)
		- [Install LAMP](#install-lamp)
			- [Install Apache and PHP](#install-apache-and-php)
				- [Install Database](#install-database)
					- [Install MySQL](#install-mysql)
					- [Install the MariaDB database](#install-the-mariadb-database)
- [Create ownCloud repository](#create-owncloud-repository)
	- [Import the ownCloud Signing Key](#import-the-owncloud-signing-key)
	- [Add the ownCloud Repository in your system](#add-the-owncloud-repository-in-your-system)
	- [Install ownCloud in your system](#install-owncloud-in-your-system)
		- [Set the required permissions on ownCloud directory](#set-the-required-permissions-on-owncloud-directory)
		- [Enable Apache and Database](#enable-apache-and-database)
	- [Create a Database for ownCloud](#create-a-database-for-owncloud)
- [Configure SELinux and Firewall Rules for OwnCloud](#configure-selinux-and-firewall-rules-for-owncloud)
- [Setup ownCloud with the Installation wizard](#setup-owncloud-with-the-installation-wizard)
- [Allow access to ownCloud Server](#allow-access-to-owncloud-server)
- [Add users to ownCloud](#add-users-to-owncloud)
- [Connect client to the ownCloud server](#connect-client-to-the-owncloud-server)

<!-- /TOC -->

## Install ownCloud

This guide describes administration tasks for ownCloud, the flexible open source file synchronization and sharing solution. ownCloud includes the ownCloud server, which runs on Linux, client applications for Microsoft Windows, Mac OS X and Linux, and mobile clients for the Android and Apple iOS operating systems.

## Prerequisites

Check that your system fulfills the following prerequisites:



 - Red Hat software collection    repository enabled (only for RHEL 7)
 - EPEL repository enabled
 - Apache server and PHP extensions    installed (Lamp stack)
 - MariaDB installed

### Install Red Hat Repository

Install all the required software and utilities from the Red Hat repository.

To enable Red Hat software collection repository in RHEL7, use the following command:

`subscription-manager repos --enable rhel-server-rhscl-7-eus-rpms`



 **Note** This command is applicable only for RHEL. You can skip it for CentOS
 server.


### Install EPEL repository

Use the following command to enable EPEL repository and yum utils:

`yum install epel-release yum-utils -y`

### Install LAMP

Before installation, set up a running LAMP stack. A Lamp stack is combination of L- Linux Operating system, A – Apache Web Server, M-MySQL or MariaDB Database, and P-PHP or any other scripting language to display the data. If you already have a running LAMP stack, skip this step. Else, use the following commands to setup lamp stack:

#### Install Apache and PHP

Use the following command to install PHP:

	yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y

	yum-config-manager --enable remi-php72

	yum install httpd php php-mysql php-dom php-mbstring php-gd php-pdo php-json php-xml php-zip php-curl php-mcrypt php-pear php-intl setroubleshoot-server -y

##### Install Database

You can choose to either install MySQL or the MariaDB database for your requirement.

######Install MySQL

MySQL is a freely available open source Relational Database Management System (RDBMS) that uses Structured Query Language (SQL). It will enable adding, accessing and managing content in your database.

Use the following command to install MySQL:

	yum --enablerepo=remi,epel install mysql-server

	service mysqld start

	/usr/bin/mysql_secure_installation

######Install the MariaDB database

MariaDB is a fast, scalable, and robust database server that provides an SQL interface for accessing data.

Install the database server as MariaDB with the following command:

`yum install wget mariadb-server mariadb -y`

In the following example, the MariaDB database is used.

# Create ownCloud repository

Create your ownCloud repository by downloading and installing the ownCloud install file.

## Import the ownCloud Signing Key

Use Linux installer for the installation of ownCloud. Import the ownCloud signing key using the rpm command.

Use the following command to download the signing key on CentOS 7:

	rpm --import https://download.owncloud.org/download/repositories/production/CentOS_7/repodata/repomd.xml.key

Use the following command to download the signing key on RHEL 7:

	rpm --import https://download.owncloud.org/download/repositories/production/RHEL_7/repodata/repomd.xml.key

For more information on Code Signing, see [_ownCloud Code Signing_](https://doc.owncloud.org/server/10.0/developer_manual/app/advanced/code_signing.html?highlight=sign).

## Add the ownCloud Repository in your system

Use the following commands to add it on CentOS 7:

`cd /etc/yum.repos.d/`
`wget`
`http://download.owncloud.org/download/repositories/production/CentOS_7/ce:stable.repo`

Use the following code to add it on RHEL 7:

`cd /etc/yum.repos.d/`

`wget `

`http://download.owncloud.org/download/repositories/production/RHEL_7/ce:stable.repo`

## Install ownCloud in your system

Use the yum command to install the ownCloud Package:

`yum install owncloud -y`

### Set the required permissions on ownCloud directory

`chown -R apache.apache /var/www/html/owncloud/`

### Enable Apache and Database

Use the following commands to start and enable Apache and database service:

`systemctl start httpd`

`systemctl start mariadb`

`systemctl enable httpd`

`systemctl enable mariadb`


This command will enable services at startup.

## Create a Database for ownCloud

 1. Use the following command to set root password, remove test database, Remove anonymous users and disable remote root login on the new MariaDB server:

		mysql_secure_installation

 2. Logon to your database server and run the following command to create a database:

		mysql -u root -p

3. A MySQL or MariaDB prompt will appear.  The following example uses mariaDB. Use the following command to create a database called as “owncloud10db”:



	     `MariaDB [(none)]> create database owncloud10db;`

4. Grant the “clouddbuser” permission to access the “owncloud10db” database with a password that you can specify on the localhost:

		MariaDB [(none)]> grant all on owncloud10db.* to 'clouddbuser'@'localhost' identified by '{Passwd-here}';

5. Flush all privileges and exit:

		MariaDB [(none)]> FLUSH PRIVILEGES;
		MariaDB [(none)]> exit

# Configure SELinux and Firewall Rules for OwnCloud

Security Enhanced Linux or SELinux is a kernel security module that supports access control. If SELinux is enabled on your server, then write the following SE Linux rules for ownCloud:

`semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/owncloud/data'`

`restorecon '/var/www/html/owncloud/data'`

`semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/owncloud/config'`

`restorecon '/var/www/html/owncloud/config'`

`semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/owncloud/apps'`

`restorecon '/var/www/html/owncloud/apps'`

If a firewall is enabled and configured on your server then allow *http* and *https* ports using the following firewall-cmd command:

	firewall-cmd --permanent --add-service=http
	firewall-cmd --permanent --add-service=https
	firewall-cmd --reload

# Setup ownCloud with the Installation wizard

To configure OwnCloud, go to the following URL:

*_http://<Your-Server-Ip-address>/owncloud_*


![owncloudsetup1](//img/ownCloud_wizard_setup_1.jpg)

![owncloudsetup2](//img/ownCloud_wizard_setup_2.jpg)

Provide your user name, password, database information and the ownCloud folder details. Once you provide all the required details, Click on “Finish Setup”.

The ownCloud Logon Page appears:

![owncloudsetup3](//img/ownCloud_wizard_setup_3.jpg)

Enter the username and password and the ownCloud dashboard appears:

![owncloudsetup4](//img/ownCloud_wizard_setup_4.jpg)

The ownCloud is installed successfully on your system and you can start sharing files.

# Allow access to ownCloud Server

As an administrator, you can decide how the users must connect to the ownCloud server.  You must configure the webserver (Apache in this case ) to allow access to the desired port. The default port access is (80, 443). Edit the Apache configuration file at the path “/etc/httpd/conf/httpd.conf” to change the listening port to 8080.

1. Log on as the root user.

2. To change the ports use the following command:

>  `sudo vi /etc/httpd/conf/httpd.con`

 The configuration file opens. The default listening port is 80.

3. Find the following line:

> `Listen 80`

4. Change it to the following line to the configuration file:

> `Listen 8080`

5. Save and close the file.

6. Check that new port number 8080 is not blocked in SELinux and Firewall:

> `sudo semanage port -a -t http_port_t -p tcp 8080`

7. If the semanage command is not found, install the following package:

> `sudo yum install policycoreutils-python`

8. To allow port 8080 via the firewall, perform the following steps:

9. For RHEL 7 / CentOS 7:

  1. Add the port:

      sudo firewall-cmd --permanent --add-port=8080/tcp
      sudo firewall-cmd –reload`

  2. Restart the httpd service:
      sudo systemctl restart httpd

10. For RHEL 6 / CentOS 6:

	1. Edit the iptables:
      sudo vi /etc/sysconfig/iptables
  2. Add the new custom port line:
      -A INPUT -m state --state NEW -m tcp -p tcp --dport 8090 -j ACCEPT

  3. Save and exit the file and restart iptables service. 	
      sudo service httpd restart

11. Verify the port using command:

    sudo netstat -tulpn | grep :8090

12. If netstat command is not found, install the following package.

    sudo yum install net-tools

13. Verify the Apache test page from the browser using URL:
    http://IP-address:8080

# Add users to ownCloud

As an administrator, you can add users to ownCloud from the ownCloud dashboard.

Perform the following steps to add a user:

1. Go to the ownCloud server URL.

2. Enter your username and password.

The ownCloud dashboard appears:

![Dashboard](//img/ownCloud_dashboard.png)

3. Select **users** from the **Create** list.

4. Enter the username in the **Username** box

5. Enter the initial password for the user in the **Password** box.

6. You can also assign **Groups** membership to the user by selecting the group name from the list.

7. Click the **Create** button.

# Connect client to the ownCloud server

You can connect to the ownCloud server from a client such as your mobile or a desktop. You can access or synchronize files from your mobile or desktop to ownCloud. For this, you must install the ownCloud client on your system.

1. Download the ownCloud Desktop client from the [ownCloud Desktop Clients] (https://owncloud.com/download/#desktop-clients) download page.

2. Click the downloaded setup file. The installation wizard appears.

3. On the “Setup ownCloud server” screen, enter the server address and click **Next**.

4. On the “Enter user credentials” screen, enter the username and password, and click **Next**.

5. On the “Setup local folders options” screen, you can choose the folders from the server to sync. You can also sync all of your local files on the ownCloud server, or select individual folders. The default local sync folder is ownCloud, in your home directory. You may change this folder to any other required folder.

6. Click the **Connect** button.
