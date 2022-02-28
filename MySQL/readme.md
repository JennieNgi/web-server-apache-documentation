# **Installing MySQL Community Server**

## Table of contents
* Installing MySQL Community Server
    * [Downloading the noinstall ZIP Archive](#mysqlZIP)
    * [Editing Environment Variables](#mysqlConfOne)
    * [Creating the Data Directory to Store Database Data](#mysqlConfTwo)
    * [Initializing the Data Directory](#mysqlConfThree)
    * [Testing the MySQL Community Server](#mysqlTest)
    * [Optional - Securing the Initial MySQL Account](#mysqlSecure)
    * [Optional - Registering MySQL as a Windows Service](#mysqlService)

### If you are looking for other contents:

* [Installing Apache HTTP Server](../ApacheHTTPServer)
    * Prerequisites
    * Downloading the Apache HTTP Server
    * Testing the Apache HTTP Server installation
    * Optional: Registering Apache as a Windows Service
* [Creating Multiple Sites with Name Based Hosting on a Single IP Address](../MultipleSites)
    * Configuration of the httpd.conf file
    * Configuration of the httpd-vhosts.conf file
    * Configuration of the hosts file
    * Testing the New Created Sites
* [Disable Directory Listing](../DirectoryListing)
    * Configuration of the httpd.conf file
    * Testing Directory Listing Disabling
* [SSL Certificates Configuration](../SSL)
    * Prerequisites
    * Generate SSL Certificate and Key
    * Configuration of the httpd.conf file
    * Configuration of the httpd-vhosts.conf file
    * Testing SSL Certificates
* [Installing PHP](../PHP)
    * Downloading PHP 8 x64 Thread Safe ZIP
    * Configuration of php.ini
    * Edit Environment Variables
    * Configure PHP as an Apache module
    * Testing a PHP file
* [Configuration files](../Configurationfiles)
    * [hosts]
    * [httpd.conf]
    * [httpd-vhosts.conf]
    * [php.ini]
    * [my.ini]


# Installing MySQL Community Server <a id="mysql"></a>

## Downloading noinstall ZIP Archive <a id="mysqlZIP"></a>
1. Go to <em>https://dev.mysql.com/downloads/</em>
2. Click MySQL Community Server
3. Download the latest version `Windows (x86, 64-bit), ZIP Archive`

![Download MySQL](/images/dlSQL.PNG)

4. Create a new `MySQL8.0` folder in the root of your `C:\` directory and extract the contents of the ZIP into it.

<br>

## Editing Environment Variables <a id="mysqlConfOne"></a>
1. Click the Windows Start button and type `environment`
2. Click `Edit the system environment variables`
3. Select the `Advanced` tab
4. Click the `Environment Variables` button
5. Scroll down the System variables list and click `Path` followed by the `Edit` button
6. Click New and add `C:\MySQL8.0\bin`
7. Click OK

<br>

## Creating the Data Directory to Store Database Data <a id="mysqlConfTwo"></a>
1. Open File Explorer and go to `c:\`
2. Create a new folder named `mysqldata`

<br> 

## Initializing the Data Directory <a id="mysqlConfThree"></a>
1. Create a `my.ini` file in `C:\MySQL8.0\bin`
2. Add below code to the file

```
[mysqld]
# installation path
basedir=C:/mysql
# data directory
datadir=C:/mysqldata
```

3. Open a Command Prompt as administrator
4. Run below command:
```
C:\mysql\bin\mysqld.exe --initialize-insecure --user=mysql
```
5. The server can now be started by running below command:
```
C:\mysql\bin\mysqld.exe --console
```

<br>

## Testing the MySQL Community Server <a id="mysqlTest"></a>
1. Open another Command Prompt and run below command:
```
C:\mysql\bin\mysql.exe -u root 
```
If you have set a password for the root user, run this command instead:
```
C:\mysql\bin\mysql.exe -u -p root 
```
2. You will then log in as the root user in MySQL

![log in sql](/images/sqllogin.png)

3. Test SQL commands:
```
show databases;
```
4. The databases on the MySQL server host will be displayed

![show databases](/images/showdatabases.png)

5. To exit mysql, run below command:
```
exit
```
6. To safely shut down the server, run below command:
```
C:\mysql\bin\mysqladmin.exe -u root shutdown
```

If you had set a password for the root user, run this command instead:
```
C:\mysql\bin\mysqladmin.exe -u -p root shutdown
```
<br>

## Optional - Securing the Initial MySQL Account <a id="mysqlSecure"></a>
1. Log in as the root user in MySQL 
2. Run below command:
```
FLUSH PRIVILEGES
```
3. You should be able to see below message

![FLUSH PRIVILEGES](/images/FLUSHPRIVILEGES.png)

4. Run below command:
```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'yourpassword';
```
5. You should be able to see below message

![ALTER USER](/images/ALTER.png)

6. Exit mysql
7. Log in again to test the password by running below command:
run this command instead:
```
C:\mysql\bin\mysql.exe -u -p root 
```
8. You should be required to enter a password to log in this time

<br>

## Optional - Registering MySQL as a Windows Service <a id="mysqlService"></a>
MySQL can be installed as an auto-starting Windows service.
1. Open a Command Prompt as administrator
2. Run below command:
```
C:\mysql\bin\mysqld.exe --install
```
