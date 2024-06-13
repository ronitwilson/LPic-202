# LPic-202
# 24-02-24
## Basic DNS Server configuration
* /etc/resolv.conf
*  process in Linux calls the getaddrinfo function to translate a domain name into its corresponding IP address.
*  supports a list of search domains in the form of a search directive.
```
$ cat /etc/resolv.conf
search departmentA.org departmentB.org
nameserver 8.8.8.8
```
* When the resolver tries to resolve a domain name nodeA, it will first form the FQDN using departmentA.org into nodeA.departmentA.org
![image](https://github.com/ronitwilson/LPic-202/assets/9934360/2fe55fd2-f8e4-471e-b228-f70252babbab)
* Foreward and Reverse lookup
  * domain name to ip
  * ip to domain name

* tools like **bind** **dnsmasq** are dns resovlers installed in the linux pc, for local dns caching, forewarding etc
* For bing dns listens on port 53 by default, defined in file vi **/etc/named.conf**
![image](https://github.com/ronitwilson/LPic-202/assets/9934360/d1c138a5-2cb5-4b20-8b94-db536b365b21)
* what is dump-file ? kind of used for debugging i think
 * gets generated when using rndc command
    
# 16-03-24
* **rndc**,
* ability to use tcp to communicate with a remote name servier and send cmds authenticated ** with digital signature**
* use this rndc to control the nameD service
* this depends on the /etc/rndc file
* rndc-cofgen -> command to create the conf file
 *  this generated conf file with keys must be mapped to nameD service conf in /etc/named.conf
 *  rndc conf file must have the right permissions

# 26-03-24
* dig commnad
* /etc/resolv.conf -> shows which dns resolver to use
* dig @localhost cnn.com -> force dig to use localhost to resolve for dns
* rndc flush <domain name>
* there is a bin /sbin/named-checkconf -> verifies syntax of named.conf
* dns zones
 *  zone defines what a domain name server has authority over
  * foreward zone and reverse zone 


# 01-04-24
* dns record types
* SOA - Start of Authority, A record (host to ip), cname alias  to a record name server
  ![image](https://github.com/ronitwilson/LPic-202/assets/9934360/9ac29b00-0ad8-4d0d-a192-07a81e901ff3)
  ![image](https://github.com/ronitwilson/LPic-202/assets/9934360/9eda4f9e-81e3-48fb-92c9-10a96ad9bc1e)


# 05-04-24
* named-checkzone -> check your zone files for the right syntax
* named-compilezone -> covert named zone file to compiled zone
  * if we use binary format we need to change the masterfile-format

# 18-04-24
* The usage of httpd
    * /etc/httpd
    * httpd.conf
        * ServerRoot - base directory for config files
        * DocumentRoot -> base directory for document files files
        * can choose things like debug level
        * can choose maxclients
* use of **Lynx** command line http browser

# Hosting dynamic web applications
* there are moudles which are installed into the httpd
  * these are present in the moudles folder with file name similar to mod-modulename.so
  * There are then conf files for these modules which five customization options
* The **Common Gateway Interface**
    * The way to  invoke another program to process some code
    *  The CGI feature uses the filename extension to detect when a web page file has embedded code, and then it passes the file off to an external program language interpreter based on the filename extension
    *  To make use of it the CGI module must be installed
*  

# 4-may-24
##  using htpasswd and mod_auth
* mod_auth module needs to be installed and the httpd conf has to have a entry to use the authentication to refer to the password file
* Use the httpasswd tool to create the password file

### option to use .htaccess directive in the config

## Using virtual servers
* Having more than one website in one physical server
* Configuring which files belong to which website
* We can have more than 1 ip address to a single webserver to serve the right website
* Or use diff domain name

#### Example of using a domian name to serve a wesite
* create file inside /etc/apache2/sites-available
* Notice the Document Root shows which files are used
![image](https://github.com/ronitwilson/LPic-202/assets/9934360/e3717161-32a5-409f-bcaa-dfe5665fdc30)


# 8-may-24
## Using ssl with Apache
* SSL have been replaced by TLS
* Inside /etc/ssl
  * There is certs folder -> all certs we trust
  * private -> all our gen certs
* Creating a certificate using openssl
  * creating private key
  * creating a certificate signed request
  * creating a certifcate
* Attach it to apache server
### Example screenshot
![image](https://github.com/ronitwilson/LPic-202/assets/9934360/d3913077-8b7f-47fb-8ed0-2c2f21437da3)


# 12 may redirect website from apache
### Example screenshot
![image](https://github.com/ronitwilson/LPic-202/assets/9934360/78402d30-66c5-4853-b1fa-98eda70e1f2a)

# 15-05-24
## Using a reverse proxy squid
### protecting the clients which does the request
* Squid was initally ment to be a cache proxy
* There are acl to control access to the sites to domain(dstdomain) or ip(source)
* we can set the time where it can connect to the sites
* apache virtual hosts is nothing but we can serve seperately several websites for diff ip:port combination

### Various authentication from squid
* One way to look for squid libs which are installed(to know the authentication types which are supported)
  *  Is to look at the /usr/lib/squid/ folder

#### LDAP and Active directory
* **Lightweight Directory Access Protocol LDAP** is a protocol that makes it possible for applications to query user information rapidly.Companies store usernames, passwords, email addresses, printer connections, and other static data within directories  it iss an open, vendor-neutral application protocol for accessing and maintaining that data. 
* **Active Directory** is a proprietary directory tool that is used to organize IT assets, such as computers, printers, and users. It can be used for authentication, and/or storing information about network resources. LDAP is one of the protocols that is used to create or query objects in Active Directory., LDAP is a language to talk to directory services, and Active Directory is one such directory service

#### using bssic auth pic
![image](https://github.com/ronitwilson/LPic-202/assets/9934360/c6d4cfab-fa38-4a30-9ed1-b30c7e36c4f0)




## Using a NGINX
* nginx can be used as a server and reverse proxy
* Similar to apache conf

# 27-may NGINX as reverse proxy
### Main use case
* It helps in caching
* Services like Aws cloud front (Content delivery nodes) are nothing but NGINX servers

### Other use cases
* Provides an entry point example things can connect in https or a particular port till nginx and from ngingx can be http etc
* Reduces the surface of attack area for security, since only Nginx is exposed outside
* Can provide load balancing

### disadvantage
* Not all information about the client reaches the backend since the nginx is the one who forwards the packtes
* Make use of HTTP extra headers to foreward this information

#### example of configuring the HTTP header forwarding
![image](https://github.com/ronitwilson/LPic-202/assets/61230302/21e72744-b19e-4bc4-8ee8-1dbe59d1ee28)


# 13-jun DHCP
  * Mostly DHCP is not installed by default
  * Many libs are there the most popular one ISC DHCP
  * The reference conf is there in /usr/share/doc/isc-dhcp-server/examples/server.conf
  * but it should be placed at /etc/dhcpsd
  * the /var/lib/dhcp/dhcp.leases to see the ip leases
  * The dhcp uses udp at port 67

### add picture at 11:40 mins
pass

