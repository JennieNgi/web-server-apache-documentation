# **Disable Directory Listing**


## Table of contents
* Installing PHP
    * [Downloading PHP 8 x64 Thread Safe ZIP](#phpConfOne)
    * [Configuration of php.ini](#phpConfTwo)
    * [Edit Environment Variables](#phpConfThree)
    * [Configure PHP as an Apache module](#phpConfFour)
    * [Testing a PHP file](#phpTest)

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
* [Installing MySQL Community Server](../MySQL)
    * Downloading the noinstall ZIP Archive
    * Editing Environment Variables
    * Creating the Data Directory to Store Database Data
    * Initializing the Data Directory
    * Testing the MySQL Community Server
    * Optional - Securing the Initial MySQL Account
    * Optional - Registering MySQL as a Windows Service


<br>

# Installing PHP <a id="php"></a>

## Downloading PHP 8 x64 Thread Safe ZIP <a id="phpConfOne"></a>
1. Go to <em>https://www.php.net/downloads.php</em>.
2. Click `Windows downloads`

![dl php](/images/dlphp.png)

3. Download the latest `PHP 8 x64 Thread Safe ZIP` package. Make sure you are NOT downloading the Non Thread Safe Version.

![Thread Safe](/images/phpthread.png)

4. Create a new `php` folder in the root of your `C:\` directory and extract the contents of the ZIP into it.
PHP can be installed anywhere on your system, but you’ll need to change the paths referenced below if `C:\php` isn’t used.

<br>

## Configuration of php.ini <a id="phpConfTwo"></a>
1. PHP’s configuration file is named php.ini and it doesn’t exist initially, so copy `C:\php\php.ini-development` to `C:\php\php.ini`. 
2. Open the `C:\php\php.ini` file
3. Enable any required extensions. You’ll need to remove a leading semicolon (;) to uncomment a setting. Find the content below:
```
;extension=curl
;extension=gd
;extension=mbstring
;extension=pdo_mysql
```

change to
```
extension=curl
extension=gd
extension=mbstring
extension=pdo_mysql
```

This will depend on the libraries you want to use, but the above extensions should be suitable for most applications.

<br>

## Edit Environment Variables <a id="phpConfThree"></a>
To ensure Windows can find the PHP executable, you need to change the PATH environment variable.
1. Click the Windows Start button and type `environment`
2. Click `Edit the system environment variables`
3. Select the `Advanced` tab
4. Click the `Environment Variables` button
5. Scroll down the System variables list and click `Path` followed by the `Edit` button
6. Click New and add `C:\php`
7. Click OK

<br>

## Configure PHP as an Apache module <a id="phpConfFour"></a>
1. Go to `C:\Apache24\conf\` directory
2. Open the `httpd.conf` file
3. Add below code to the bottom in the file: 
```
LoadModule php_module "C:/php/php8apache2_4.dll"
AddType application/x-httpd-php .php
PHPIniDir "C:/php"
LoadFile "C:/php/php8ts.dll"
```
4. Save and close the file.
5. Restart Apache24 after the configuration 

<br>

## Testing a PHP file <a id="phpTest"></a>
1. Create a new file named `index.php` in `C:\Apache24\htdocs\siteone.tbd` directory
2. Add below PHP code to the file:
```
<?php
phpinfo();
?>
```
3. Open a web browser and enter your server address: http://siteone.tbd/index.php
4. A “PHP version” page will appear showing the various PHP and Apache configuration settings.

![PHP testing](/images/php.png)

<br>

