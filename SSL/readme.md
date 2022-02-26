# **SSL Certificates Configuration**


## Table of contents
* SSL Certificates Configuration
    * [Prerequisites](#sslPre)
    * [Generate SSL Certificate and Key ](#sslConfOne)
    * [Configuration of the httpd.conf file](#sslConfTwo)
    * [Configuration of the httpd-vhosts.conf file](#sslConfThree)
    * [Testing SSL Certificates](#sslTest)

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
* [Installing PHP](../PHP)
    * Downloading PHP 8 x64 Thread Safe ZIP
    * Configuration of php.ini
    * Edit Environment Variables
    * Configure PHP as an Apache module
    * Testing a PHP file]
* [Installing MySQL Community Server](../MySQL)
    * Downloading the noinstall ZIP Archive
    * Editing Environment Variables
    * Creating the Data Directory to Store Database Data
    * Initializing the Data Directory
    * Testing the MySQL Community Server
    * Optional - Securing the Initial MySQL Account
    * Optional - Registering MySQL as a Windows Service



# SSL Certificates Configuration <a id="ssl"></a>

## Prerequisites <a id="sslPre"></a>
The openssl library is required to generate your own certificate. 

<br>

## Generate SSL Certificate and Key <a id="sslConfOne"></a>
1. Go to `C:\Apache24\conf\` directory and copy the `openssl.cnf` to the `C:\Apache24\bin\` directory

2. Open a Command Prompt and cd to `C:\Apache24\bin\` directory
3. Generate private key and certificate signing request by running below command:
```
openssl req -config openssl.cnf -new -out server.csr -keyout server.pem
```
4. Enter you own PEM pass pharse

![PEM pass pharse](/images/pem.png)

5. Fill out the csr information

![fill out the csr information](/images/csr.png)

6. You will see the `server.csr` and `server.pem` files are created in the 
`C:\Apache24\bin\` directory

6. Here you can send the `server.csr` to any publicly trusted Certificate Authority to sign it

7. Or you can do a self-signed SSL certificate by running below command:

```
openssl rsa -in server.pem -out server.key
```

8. Enter your created PEM pass pharse
9. Generate the self-signed SSL certificate by running below command:
```
openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 3650
```
10. You will see the `server.crt` and `server.key` files are created in the 
`C:\Apache24\bin\` directory

11. Cut and paste all the four generated files  to `C:\Apache24\conf\SSL\siteone.tbd\` directory

<br>

## Configuration of the httpd.conf file<a id="sslConfTwo"></a>
1. Go to `C:\Apache24\conf\` directory
2. Open the `httpd.conf` file
3. Uncomment this line: #LoadModule ssl_module modules/mod_ssl.so
<br>You can uncomment a line in a configuration file by removing the # at the start of the line.
```
LoadModule ssl_module modules/mod_ssl.so
```

4. Save and close the file 

<br>

## Configuration of the httpd-vhosts.conf file<a id="sslConfThree"></a>
1. Go to `C:\Apache24\conf\extra\` directory
2. Open the `httpd-vhosts.conf` file
3. Add below code to the file:
```
Listen 443

<VirtualHost *:443>
    DocumentRoot "${SRVROOT}/htdocs/siteone.tbd"
    ServerName siteone.tbd
    SSLEngine On
    SSLCertificateFile "${SRVROOT}/conf/SSL/siteone.tbd/server.crt"
    SSLCertificateKeyFile "${SRVROOT}/conf/SSL/siteone.tbd/server.key"
</VirtualHost>

```
4. To redirect HTTP to HTTPS, add one line of code to VirtualHost *:80

```
<VirtualHost *:80>
    DocumentRoot "${SRVROOT}/htdocs/siteone.tbd"
    ServerName siteone.tbd
    Redirect permanent / https://siteone.tbd
</VirtualHost>

```

<br>
 
## Testing SSL Certificates <a id="sslTest"></a>
1. create an  `index.html` file in `C:\Apache24\htdocs\siteone.tbd` 
2. Open your web browser > go to http://siteone.tbd
3. It will automatically redirect you to the https://siteone.tbd. You should be able to see this page 

![SSL inserted](/images/ssl1.png)

You will see a "Not secure" warning message if you are using Self-signed certificates, which are inherently not trusted by the browser. It is recommended to send the SSL certificate to a Certificate Authority for signature.

4. Click Advanced > Continued to siteone.tbd (unsafe)

![click advanced](/images/ssl2.png)

5. Content of siteone.tbd will be displayed

![content of siteone.tbd](/images/ssl3.png)

