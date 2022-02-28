# **Installing Apache HTTP Server**


## Table of contents
* Installing Apache HTTP Server
    * [Prerequisites](#VS16)
    * [Downloading the Apache HTTP Server](#dlApache)
    * [Testing the Apache HTTP Server installation](#testApache)
    * [Optional: Registering Apache as a Windows Service](#serviceApache)

### If you are looking for other contents:
* [Creating Multiple Sites with Name Based Hosting on a Single IP Address](../MultipleSites)
    * Configuration of the httpd.conf file
    * Configuration of the httpd-vhosts.conf file
    * Configuration of the hosts file
    * Testing the New Created Sites
* [Disable Directory Listing](../DirectoryListing)
    * Configuration of the httpd.conf file
    * Testing Directory Listing Disabling
* [Installing PHP](../PHP)
    * Downloading PHP 8 x64 Thread Safe ZIP
    * Configuration of php.ini
    * Edit Environment Variables
    * Configure PHP as an Apache module
    * Testing a PHP file
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

# Installing Apache HTTP Server <a id="Apache"></a>

## Prerequisites<a id="VS16"></a>
Apache installation is required Windows® Visual Studio C++ 2019 aka VS16.
1. Click this download link: *[https://aka.ms/vs/17/release/VC_redist.x64.exe](https://aka.ms/vs/17/release/VC_redist.x64.exe)*
2. Run **VC_redist.x64.exe** and install with all default settings<br>
![Install VS16](/images/VS16.png)
3. Restart your computer after successful installation

<br>

## Downloading the Apache HTTP Server <a id="dlApache"></a>
1. Go to <em>https://www.apachelounge.com/download/</em>
2. Download **Apache 2.4.52 Win64** by clicking `httpd-2.4.52-win64-VS16.zip`<br>
![Install Apache 2.4.52 Win64](/images/Apache.png)
3. Open File Explorer
4. Extract the dowloaded zip file in `Downloads` directory
5. Copy the extracted Apache24 folder to `C:\` directory<br>
![Apache24 folder in C:\ directory](/images/Apache24.png)

<br>

## Testing the Apache HTTP Server installation <a id="testApache"></a>
1. Open IIS Manager > Make sure IIS Manager Service is turned off<br>
![Shut down IIS](/images/IIS.png)
2. Open Services > Make sure World Wide Web Publishing service is turned off<br>
![Shut down WWWPS](/images/World Wide Web Publishing service.png)
3. Open a Command Prompt as administrator and cd to `c:\Apache24\bin` directory 
```bash
httpd.exe
```
4. Open your web browser > go to http://localhost or http://server-ip:80. 
5. A page saying "It Works!" should show up. <br>
![It Works!](/images/localhost.png)

<br>

## Optional: Registering Apache as a Windows Service <a id="serviceApache"></a>
You may want to run Apache as a Window Service so that you can easily turn on and off Apache after configuration
1. Open a Command Prompt as administrator
2. cd to directory `c:\Apache24\bin`
3. Add Apache as a Windows Service
```bash
httpd.exe -k install 
```
<br>
