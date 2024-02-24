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
* ![image](https://github.com/ronitwilson/LPic-202/assets/9934360/2fe55fd2-f8e4-471e-b228-f70252babbab)

