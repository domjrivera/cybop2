---
title: Kevin Walkthrough - Proving Grounds
description: Walkthrough of the Kevin machine from Proving Grounds
author: Cyber Operator
date: 2024-07-25T16:55:50.565Z
tags:
  - Tags
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



\--- COMING SOON ---