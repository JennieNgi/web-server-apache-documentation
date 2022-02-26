# **Creating Multiple Sites with Name Based Hosting on a Single IP Address**


## Table of contents
* Creating Multiple Sites with Name Based Hosting on a Single IP Address
    * [Configuration of the httpd.conf file](#multipleSitesConfOne)
    * [Configuration of the httpd-vhosts.conf file](#multipleSitesConfTwo)
    * [Configuration of the hosts file](#multipleSitesConfThree)
    * [Testing the New Created Sites](#multipleSitesTest)

### If you are looking for other contents:
* [Installing Apache HTTP Server](../ApacheHTTPServer)
    * Prerequisites
    * Downloading the Apache HTTP Server
    * Testing the Apache HTTP Server installation
    * Optional: Registering Apache as a Windows Service
* [Disable Directory Listing](../DirectoryListing)
    * Configuration of the httpd.conf file
    * Testing Directory Listing Disabling
* [Installing PHP](../PHP)
    * Downloading PHP 8 x64 Thread Safe ZIP
    * Configuration of php.ini
    * Edit Environment Variables
    * Configure PHP as an Apache module
    * Testing a PHP file]
* [SSL Certificates Configuration](../SSL)
    * Prerequisites
    * Generate SSL Certificate and Key
    * Configuration of the httpd.conf file
    * Configuration of the httpd-vhosts.conf file
    * Testing SSL Certificates
* [Installing MySQL Community Server](../MySQL)
    * Downloading the noinstall ZIP Archive
    * Editing Environment Variables
    * Creating the Data Directory to Store Database Data
    * Initializing the Data Directory
    * Testing the MySQL Community Server
    * Optional - Securing the Initial MySQL Account
    * Optional - Registering MySQL as a Windows Service

<br>

# Creating Multiple Sites with Name Based Hosting on a Single IP Address <a id="multipleSites"></a>

## Configuration of the httpd.conf file <a id="multipleSitesConfOne"></a>
1. Go to `C:\Apache24\conf\` directory
2. Open the `httpd.conf` file
3. Uncomment this line: #Include conf/extra/httpd-vhosts.conf 
<br>You can uncomment a line in a configuration file by removing the # at the start of the line.

```
#Virtual hosts
Include conf/extra/httpd-vhosts.conf
```
4. Save and close the file 
5. Restart Apache24 after configuration

<br>

## Configuration of the httpd-vhosts.conf file <a id="multipleSitesConfTwo"></a>
1. Go to `C:\Apache24\conf\` directory, you will see a folder named `extra` is created
2. Go to `C:\Apache24\conf\extra\` directory, open the `httpd-vhosts.conf` file
3. Add below code to the file:
```
<VirtualHost *:80>
    DocumentRoot "${SRVROOT}/htdocs/siteone.tbd/"
    ServerName siteone.tbd
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "${SRVROOT}/htdocs/sitetwo.tbd/"
    ServerName sitetwo.tbd
</VirtualHost>
```
Here siteone.tbd and sitetwo.tbd are used for the hostnames and directory names, but you also can specify a particular name you want. 

4. Go to `C:\Apache24\htdocs` directory
5. Create two directories with names as same as you specified as the `DocumentRoot` in the `httpd-vhosts.conf` file
6. Restart Apache24 after configuration

<br>

## Configuration of the hosts file <a id="multipleSitesConfThree"></a>
1. Run Notepad as administrator
2. Open the `C:\Windows\System32\drivers\etc\hosts` file
3. Add below code to the file to link your localhost IP address and the hostnames you created:
```
127.0.0.1   siteone.tbd
127.0.0.1   sitetwo.tbd
```
4. Save and close the file

<br>

## Testing the New Created Sites <a id="multipleSitesTest"></a>
1. Create an `index.html` file with different content in `C:\Apache24\htdocs\siteone.tbd` and `C:\Apache24\htdocs\sitetwo.tbd` directories. 
2. Open your web browser > go to http://siteone.tbd and  http://sitetwo.tbd
3. The content you created in each index.html should show up on each site.

Site One

![Site One](/images/siteone.png)

Site Two

![Site Two](/images/sitetwo.png)


