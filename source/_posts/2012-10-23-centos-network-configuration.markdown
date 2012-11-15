---
layout: post
title: CentOS network configuration
tags:
- centos
- linux
- quickfire
- tips
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
This post is being made for me personal notes. Maybe it will assist others at some point. I am always forgetting the various configuration files involved with setting up networking on a [CentOS](http://www.centos.org) host. I have decided to document the process I go through each time to help me remember next time. Most of this information comes from various forums, CentOS documentation and the man pages.


##Device specific information

A configuration file exists for each interface under `/etc/sysconfig/network-scripts/`.  To change the configuration for _eth0_ we will need to edit `/etc/sysconfig/network-scripts/ifcfg-eth0`. 

###DHCP
Edit the file to match to the following, leave any lines that are not listed below in place
```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

###Static address
To use a static IP address, edit the configuration file as noted below.  Again, leave any lines already in the file not listed below in place.  The __NETWORK__, __NETMASK__, and __IPADDR__ should match your network settings.
```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
NETWORK=172.24.1.0
NETMASK=255.255.255.0
IPADDR=172.24.1.10
```

##System wide networking information:
Several system wide configuration settings can be found in `/etc/sysconfig/network`.  These include the hostname and gateway as well as the option to disable networking.

Edit `/etc/sysconfig/network` as necessary to match your local network settings.
```
NETWORKING=yes
HOSTNAME=server.example.com
GATEWAY=172.24.1.1
```

##DNS server information
Finally, we configure which nameservers to use for DNS resolution.  This is set in `/etc/resolv.conf` and again should match your network settings.  The example below will use [Google's Public DNS servers](https://developers.google.com/speed/public-dns/docs/using).
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

After all is set, `$service network restart` or a reboot for all settings to be applied.  If you have custom iptables rules, you will need to adjust them as necessary.