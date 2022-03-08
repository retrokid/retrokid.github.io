# NetBSD package manager

----------------------

# Summary

In this part i'm going to enable built-in package manager and install pkgin. Pkgin is the recommended package manager for NetBSD.
For more information see: [PKGIN Website](https://pkgin.net/)

This part requires active internet connection.

----------------------

# Instructions

1- Start and login to your system.

![004-netbsd-package-manager-001](/images/004-netbsd-package-manager-001.png)

2- Switch to **`root`** user with **`su`** command.

![004-netbsd-package-manager-002](/images/004-netbsd-package-manager-002.png)

3- Go to root's **homefolder** with **`cd`** command. Check with **`ls`** command that you're in **homefolder**. Open **`.profile`** dotfile with **`vi`** program.

![004-netbsd-package-manager-003](/images/004-netbsd-package-manager-003.png)

4- In this file find and uncomment **`export PKG_PATH`** line by deleting the **#** character at the start of the line. Save it using **`:w!`** command because this file is read-only.

![004-netbsd-package-manager-004](/images/004-netbsd-package-manager-004.png)

![004-netbsd-package-manager-005](/images/004-netbsd-package-manager-005.png)

5- This configuration don't require a system restart. It requires a re-login. So logout from all the logged-in users with **`exit`** command.

![004-netbsd-package-manager-006](/images/004-netbsd-package-manager-006.png)

![004-netbsd-package-manager-007](/images/004-netbsd-package-manager-007.png)

6- Login with **`root`** user. (Installing programs requires root privileges)

![004-netbsd-package-manager-008](/images/004-netbsd-package-manager-008.png)

![004-netbsd-package-manager-009](/images/004-netbsd-package-manager-009.png)

7- First, install **`pkgin`** package manager using command **`pkg_add -v pkgin`** .

![004-netbsd-package-manager-010](/images/004-netbsd-package-manager-010.png)

![004-netbsd-package-manager-011](/images/004-netbsd-package-manager-011.png)

![004-netbsd-package-manager-012](/images/004-netbsd-package-manager-012.png)

![004-netbsd-package-manager-013](/images/004-netbsd-package-manager-013.png)

8- From now on we can use pkgin. Update pkgin database with command **`pkgin update`** . Always update **`pkgin`** before installing programs.

![004-netbsd-package-manager-014](/images/004-netbsd-package-manager-014.png)

![004-netbsd-package-manager-015](/images/004-netbsd-package-manager-015.png)

9- Let's test **`pkgin`** by installing **`vim`** program. Use command **`pkgin install vim`** to install **`vim`**. Type Y to continue install. This will download and copy all the necessary files for **`vim`** program.

![004-netbsd-package-manager-016](/images/004-netbsd-package-manager-016.png)

![004-netbsd-package-manager-017](/images/004-netbsd-package-manager-017.png)

10- After installation is over, test-run the program with command **`vim`**. Check if it runs or not.

![004-netbsd-package-manager-018](/images/004-netbsd-package-manager-018.png)

![004-netbsd-package-manager-019](/images/004-netbsd-package-manager-019.png)

11- You can also delete installed programs. Remove **`vim`** with using **`pkgin remove vim`** command.

![004-netbsd-package-manager-020](/images/004-netbsd-package-manager-020.png)

![004-netbsd-package-manager-021](/images/004-netbsd-package-manager-021.png)

![004-netbsd-package-manager-022](/images/004-netbsd-package-manager-022.png)

12- After removal of a program you should also remove unnecessary packages by using **`pkgin autoremove`** command.

![004-netbsd-package-manager-023](/images/004-netbsd-package-manager-023.png)

![004-netbsd-package-manager-024](/images/004-netbsd-package-manager-024.png)

![004-netbsd-package-manager-025](/images/004-netbsd-package-manager-025.png)

13- Also use **`pkgin clean`** command to clean the cache after an install or uninstall operation.

![004-netbsd-package-manager-026](/images/004-netbsd-package-manager-026.png)

By the way you should always think programs as potential security vulnerabilities. Especially if you are running your system as a server. So never install any unnecessary programs to a server. Best is always use the programs those come with your operating system. For example use vi instead of vim. 

This is the end of NetBSD guide. Now you have a fully functioning minimal NetBSD system. Next is up to you. You can install a Graphical User Interface or configure a Firewall. For more information about NetBSD use the official guide here: [NetBSD Guide](https://www.netbsd.org/docs/guide/en/)

------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/netbsd_guides/004-netbsd-package-manager.md)

[download this page as .pdf](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/netbsd_guides/004-netbsd-package-manager.pdf)

[back to NetBSD Guides](./netbsd-guides)

------------------------------

###### COPYRIGHT © 2022 EFE ERTUGRUL. ALL RIGHTS RESERVED. FREE FOR PERSONAL USE.