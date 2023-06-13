# NetBSD network configuration

-------------------------

### Summary

In this part i'll show you how to enable NetBSD dhcp daemon for internet connection. Most of the time there is already a dhcp service in your network (your router, virtualbox). So there is no need for manual ip configuration. 

If you need to set manual ip configuration for your network or enabling dhcp daemon did not work for you, please visit this website for more information: [Setting up TCP/IP on NetBSD in practice](https://www.netbsd.org/docs/guide/en/chap-net-practice.html)

--------------------

### Instructions

1- Start and login to your system.

![003-netbsd-network-configuration-001](/images/003-netbsd-network-configuration-001.png)

2- Switch to **`root`** user with **`su`** command.

![003-netbsd-network-configuration-002](/images/003-netbsd-network-configuration-002.png)

3-Open **`/etc/rc.conf`** configuration file with **`vi`** program.

![003-netbsd-network-configuration-003](/images/003-netbsd-network-configuration-003.png)

4- At the end of the file, add **`dhcpcd=YES`** configuration and save the file.

![003-netbsd-network-configuration-004](/images/003-netbsd-network-configuration-004.png)

5- Restart your system with **`shutdown -r now`** command.

![003-netbsd-network-configuration-005](/images/003-netbsd-network-configuration-005.png)

![003-netbsd-network-configuration-006](/images/003-netbsd-network-configuration-006.png)

6- When your system starts again login and try to ping google with command **`ping google.com`** . If you are getting any response, you're connected to internet.

![003-netbsd-network-configuration-007](/images/003-netbsd-network-configuration-007.png)

------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/netbsd_guides/003-netbsd-network-configuration.md)

[download this page as .pdf](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/netbsd_guides/003-netbsd-network-configuration.pdf)

[back to NetBSD Guides](./netbsd-guides)

------------------------------

###### COPYRIGHT © 2022 EFE ERTUGRUL. ALL RIGHTS RESERVED. FREE FOR PERSONAL USE.