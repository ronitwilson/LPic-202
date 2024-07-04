# Building Router with iptables 25th jun 2024
* Iptables
* Packet forewarding
* Netward address translation (NAT)
 
## Terms
*  IPtables
*  ufw -> written on top of iptables for ease
*  firewald, nftables -> alternative to iptalbes
*  iptable-persistent -> make iptable changes persistant

## Features of IPtables
* Routing
* NAT
* Filtering
* Logging
* Redirecting

## Packet Forewarding
* Kernel does not allow packets to move b/n interfaces by default
* can be enabled
    * /etc/sysctl.conf -> net.ipv4.ip_forward=1

## Further configuration
- `iptables` Rules
  - `cat /etc/iptables/rules.v4`
  - Processing Chains
    - Input: Traffic destined for the localhost
    - Output: Traffic leaving the localhost
    - Forward: Traffic being routed elsewhere

- Enabling NAT
  - Configure NAT rule
    - `sudo iptables -t nat -A POSTROUTING -j MASQUERADE`
    - `sudo iptables -t nat -s 10.222.0.0/24 -A POSTROUTING -j MASQUERADE`
  
  - Save configuration
    - `sudo iptables-save | sudo tee /etc/iptables/rules.v4`

##  4 July port forwarding IP tables
- Connection tracking
- Destination NAT
- Source NAT

