---
title: Wombo Walkthrough
description: Walkthrough of Wombo from Proving Grounds
author: Cyber Operator
date: 2024-07-29T14:46:36.787Z
tags:
  - Exploitable
---
Wombo is a machine labeled as "easy".  It is a Linux machine that you can use to practice pentesting in general or more specifically to practice for certification exams, such as OSCP.  With that, let's begin!

1. Scan

We normally do two nmap scans, a quick one to get a quick read and the more useful longer one.  We start with the quick one (we have the longer one running in another window):

![](/static/img/screenshot-2024-07-29-at-10.50.01 am.png)

We see that port 80 is open, so let's see if we can navigate to a web server:

![](/static/img/screenshot-2024-07-29-at-10.52.53 am.png)

So we have the nginx web server default page.  Now let's chack out if there is anything in port 8080, which is also open.

Now we have a NodeBB (a forum) installed.

![](/static/img/screenshot-2024-07-29-at-10.54.40 am.png)

While we were looking around these, our longer nmap scan finished, so let's see what we found there:

![](/static/img/screenshot-2024-07-29-at-10.57.02 am.png)

![](/static/img/screenshot-2024-07-29-at-10.57.52 am.png)

![](/static/img/screenshot-2024-07-29-at-10.58.41 am.png)

![](/static/img/screenshot-2024-07-29-at-10.59.29 am.png)

![](/static/img/screenshot-2024-07-29-at-11.00.12 am.png)

![](/static/img/screenshot-2024-07-29-at-11.00.48 am.png)

There are probably many rabbit holes that you can explore after looking at that scan.  For example, we do a searchsploit lookup for the OpenSSH version and for the Redis version:

![](/static/img/screenshot-2024-07-29-at-11.16.00 am.png)

While the username enumeration vuln from OpenSSH may be interesting, the Redis unauthenticated code execution seems more interesting.

You could finalize this exploit with a Metasploit module.  If you are practicing for a cert exam, such as OSCP, this is not an option.  Let's try to find an interesting redis rce exploit. After a brief Google search, we find a two-part possible useable one:

![](/static/img/screenshot-2024-07-29-at-11.31.48 am.png)

![](/static/img/screenshot-2024-07-29-at-11.34.54 am.png)

We then download the python exploit as well as the linux accompanying file:

![](/static/img/screenshot-2024-07-29-at-11.36.00 am.png)

Let's run it:

![](/static/img/screenshot-2024-07-29-at-11.53.18 am.png)

Pretty straightforward run of the exploit from there.
