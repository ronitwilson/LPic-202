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
