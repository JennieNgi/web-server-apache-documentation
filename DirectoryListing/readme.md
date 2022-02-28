# **Disable Directory Listing**


## Table of contents

* Disable Directory Listing
    * [Configuration of the httpd.conf file](#directoryConf)
    * [Testing Directory Listing Disabling](#directoryTest)

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
* [Configuration files](../Configurationfiles)
    * [hosts]
    * [httpd.conf]
    * [httpd-vhosts.conf]
    * [php.ini]
    * [my.ini]

<br>

# Disabling Directory Listing <a id="directory"></a>

## Configuration of the httpd.conf file <a id="directoryConf"></a>
As a security best practice, it is recommended to disable directory listing.
> Directory listing is a web server feature that, when enabled, lists the content of a directory with no index file (e.g. index.php or index.html) Therefore, if a request is made to a directory on which directory listing is enabled and there is no index file such as index.php or index.asp, the web server will return a directory listing, even if the directory contains files from a web application. 

1. Go to `C:\Apache24\conf\` directory
2. Open the `httpd.conf` file
3. Find the content below: 
```
Options Indexes FollowSymLinks
```
change to

```
Options -Indexes +FollowSymLinks
```
4. Restart Apache24 after the configuration 

<br>

## Testing Directory Listing Disabling <a id="directoryTest"></a>
1. Create few folders in the `C:\Apache24\htdocs\siteone.tbd` and `C:\Apache24\htdocs\sitetwo.tbd` directories without any index file.

2. Open your web browser > go to http://siteone.tbd or http://sitetwo.tbd
3. You should be able to see message as below:

Site One

![Site One Disable Directory Listing](/images/siteone_directory.png)

Site Two

![Site Two Disable Directory Listing](/images/sitetwo_directory.png)

