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
* rndc flush domain name
