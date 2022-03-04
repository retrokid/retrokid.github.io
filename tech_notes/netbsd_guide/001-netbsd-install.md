# NetBSD Installation

--------------------------

### Summary

These are the step by step instructions of installing a minimal NetBSD on a virtual machine. I'm using NetBSD as a mini server. So this installation has no graphical packages. I'm also using 32bit version. A bit slower but less demanding. 

I'm publishing this for the future reference. Because i'm sure i'm going to forget how i've installed and configured this OS.

You can download NetBSD 9.2 CD image from this site:

[https://www.netbsd.org/releases/formal-9/NetBSD-9.2.html](https://www.netbsd.org/releases/formal-9/NetBSD-9.2.html)

The VM has this configuration:

1 core cpu
1024mb ram
8gb ide hdd
no soundcard

-----------------------------

### Instructions

1- Boot your vm from cd image and wait until you see this screen. Press enter and continue next screen.

![001-netbsd-install-001.png](/images/001-netbsd-install-001.png)


2- Select your keyboard and press enter.

![001-netbsd-install-002.png](/images/001-netbsd-install-002.png)

3- Select install to hard disk and continue.


![001-netbsd-install-003.png](/images/001-netbsd-install-003.png)

4- Select yes and continue.

![001-netbsd-install-004.png](/images/001-netbsd-install-004.png)

5- Select 8.0G disk.

![001-netbsd-install-005.png](/images/001-netbsd-install-005.png)

6- Select "Guid Partition Table"

![001-netbsd-install-006.png](/images/001-netbsd-install-006.png)

7- Select correct and continue.

![001-netbsd-install-007.png](/images/001-netbsd-install-007.png)

8- Select sizes of NetBSD partitions.

![001-netbsd-install-008.png](/images/001-netbsd-install-008.png)

9- Press x to select go on and then press enter.

![001-netbsd-install-009.png](/images/001-netbsd-install-009.png)

10- Press x to select go on and then press enter.

![001-netbsd-install-010.png](/images/001-netbsd-install-010.png)

11- Select yes and continue.

![001-netbsd-install-011.png](/images/001-netbsd-install-011.png)

12- Select BIOS console and continue.

![001-netbsd-install-012.png](/images/001-netbsd-install-012.png)

13- Select custom installation and continue.

![001-netbsd-install-013.png](/images/001-netbsd-install-013.png)

14- Set "Manual pages" to Yes. (Man pages are always better than google searches)

![001-netbsd-install-014.png](/images/001-netbsd-install-014.png)

15- Select "Install selected sets" and continue.

![001-netbsd-install-015.png](/images/001-netbsd-install-015.png)

16- Select CD-ROM and continue.

![001-netbsd-install-016.png](/images/001-netbsd-install-016.png)

17- Wait for extraction to end.

![001-netbsd-install-017.png](/images/001-netbsd-install-017.png)

18- Press enter to start configuration.

![001-netbsd-install-018.png](/images/001-netbsd-install-018.png)

19- First thing is to set "root" user password. Select Change root password.

![001-netbsd-install-019.png](/images/001-netbsd-install-019.png)

20- Select yes.

![001-netbsd-install-020.png](/images/001-netbsd-install-020.png)

21- Enter new root password.

![001-netbsd-install-021.png](/images/001-netbsd-install-021.png)

22- Set "Enable raidframe" to No. Because i'm not going to use any RAID implementations. Look here for more info: [NetBSD Raidframe](https://www.netbsd.org/docs/guide/en/chap-rf.html)

![001-netbsd-install-022.png](/images/001-netbsd-install-022.png)

23- Set "Enable cgd" to No. Because im not going to encrypt any disks. Look here for more info: [NetBSD cgd](https://www.netbsd.org/docs/guide/en/chap-cgd.html)

![001-netbsd-install-023.png](/images/001-netbsd-install-023.png)

24- Select "Add a user" and press enter.

![001-netbsd-install-024.png](/images/001-netbsd-install-024.png)

25- Enter username and add this user to wheel group. (Wheel group means privileged users)

![001-netbsd-install-025.png](/images/001-netbsd-install-025.png)

26- Select bin/sh and continue.

![001-netbsd-install-026.png](/images/001-netbsd-install-026.png)

27- Set your user password.

![001-netbsd-install-027.png](/images/001-netbsd-install-027.png)

28- Select finished configuration and hit enter.

![001-netbsd-install-028.png](/images/001-netbsd-install-028.png)

29- Installation is completed. Hit enter.

![001-netbsd-install-029.png](/images/001-netbsd-install-029.png)

30- Select reboot the computer and hit enter.

![001-netbsd-install-030.png](/images/001-netbsd-install-030.png)

31- After boot, you should be able to see this login screen. 

![001-netbsd-install-031.png](/images/001-netbsd-install-031.png)

Congratulations,

You've successfully installed a minimal NetBSD 32bit operating system.

###### Copyright © Efe Ertuğrul. Free for personal use.

------------------------------

[download this page as .md]()

[download this page as .pdf]()

[back to NetBSD Guide](./netbsd-guide)
