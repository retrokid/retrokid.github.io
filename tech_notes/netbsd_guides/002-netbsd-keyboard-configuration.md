# NetBSD keyboard configuration

----------------------

# Summary

In this part i'm going to configure my non-us keyboard by changing or adding some system configuration files for keyboard. **US** keyboard users can skip this part.

This part requires you to know basic usage of **vi** program. If you don't know how to use **vi** or **vim** check this website first: [NetBSD vi tutorial](https://www.netbsd.org/docs/guide/en/chap-edit.html#chap-edit-vi-tut)

**vi** is almost always pre-installed in every operating system. Learning **vi** is never a bad idea.

**vi** basic usage cheatsheet:

|Command|     Meaning     |
|-------|-----------------|
|h      |move cursor left |
|j      |move cursor down |
|k      |move cursor up   |
|l      |move cursor right|
|a      |add after char   |
|i      |add before char  |
|A      |add end of line  |
|I      |add start of line|
|o      |add below line   |
|O      |add above line   |
|dd     |delete one line  |
|x      |delete one char  |
|:w     |save             |
|:q     |quit             |
|:wq    |save and quit    |
|:w!    |force save       |
|:q!    |force quit       |


----------------------------

# Instructions

1- Start your system and login.

![002-netbsd-keyboard-configuration-001.png](/images/002-netbsd-keyboard-configuration-001.png)

2- Changing the system configuration requires privilege. So switch to **`root`** user with **`su`** command.

![002-netbsd-keyboard-configuration-002.png](/images/002-netbsd-keyboard-configuration-002.png)

3- Open **`wscons.conf`** file with **`vi`** editor. 

![002-netbsd-keyboard-configuration-003.png](/images/002-netbsd-keyboard-configuration-003.png)

4- I'm using **`tr`** keyboard. So im going to add **`encoding tr`** configuration in this file.

![002-netbsd-keyboard-configuration-004.png](/images/002-netbsd-keyboard-configuration-004.png)

5- I'm also going to edit keymaps because my current keyboard doesn't have a less, greater key.(These characters: "<>|").This requires me to go to **`/usr/share/wscons/keymaps/`** folder.And create a new file named **`overlay.tr`** with **`vi`** editor.(You can use anything as file name but do not forget it. We're gonna need it)

![002-netbsd-keyboard-configuration-005.png](/images/002-netbsd-keyboard-configuration-005.png)

6- What i'm going to do in this file that i'm going to set some unusable turkish character buttons to bar '|' less '<' and greater '>' characters. For example there is a 'ş' character in my keyboard. It's unusable in console but i might need '|' character so i've added **`keycode 39 = bar`** line in this file to set 'ş' button to bar '|' character. I've also set 'ö' and 'ç' buttons to use less '<' and greater '>'. (You can check your full keymap with this command: **`wsconsctl map | less`**)

![002-netbsd-keyboard-configuration-006.png](/images/002-netbsd-keyboard-configuration-006.png)

7- Again, open your **`wscons.conf`** file with **`vi`** editor. 

![002-netbsd-keyboard-configuration-003.png](/images/002-netbsd-keyboard-configuration-003.png)

8- Add **`mapfile /usr/share/wscons/keymaps/overlay.tr`** configuration and save it.

![002-netbsd-keyboard-configuration-007.png](/images/002-netbsd-keyboard-configuration-007.png)

9- Restart the system with **`shutdown -r now`** to load these new keyboard configurations.

![002-netbsd-keyboard-configuration-008.png](/images/002-netbsd-keyboard-configuration-008.png)

![002-netbsd-keyboard-configuration-009.png](/images/002-netbsd-keyboard-configuration-009.png)

10- When system starts, login with user and try your configured buttons. If you can see your characters it means that your keyboard configurations are working.

![002-netbsd-keyboard-configuration-010.png](/images/002-netbsd-keyboard-configuration-010.png)

------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/netbsd_guides/002-netbsd-keyboard-configuration.md)

[download this page as .pdf](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/netbsd_guides/002-netbsd-keyboard-configuration.pdf)

[back to NetBSD Guides](./netbsd-guides)

------------------------------

###### COPYRIGHT © 2022 EFE ERTUGRUL. ALL RIGHTS RESERVED. FREE FOR PERSONAL USE.