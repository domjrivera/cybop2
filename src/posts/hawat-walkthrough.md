---
title: Hawat Walkthrough
description: Walkthrough of the Hawat machine from Proving Grounds
author: Cyber Operator
date: 2024-08-02T17:57:25.045Z
tags:
  - Tags
---
# Hawat (Proving Grounds) Walkthrough

Next up is Hawat.  If you have seen my other vulnerable [practice pentest machine walkthrough](https://cyberoperator.com/tags/exploitable/), you know the drill, so let's go!

## Scanning

We'll start with the nmap scan

`nmap -sC -sV -p- --script vuln [target IP]`

We see that this is full of interesting services in unusual ports (that is why we use the -p- option in our nmap scan, we should scan all ports, not just the default subset.

![](/static/img/screenshot-2024-08-02-at-2.04.14 pm.png)

![](/static/img/screenshot-2024-08-02-at-2.04.41 pm.png)

## Additional Recon and Enumeration

Issue tracker web app in an unusual port, 17445, interesting...

![](/static/img/screenshot-2024-08-02-at-2.08.08 pm.png)

We used the option to create a user on this app (username "soyplant").  Looking at the list of registered user, we see the user we just created as well as a the other existing users (as part of our enumeration)

![](/static/img/screenshot-2024-08-02-at-2.10.06 pm.png)

And another web app on port 30455, also an non traditional port (looks like this is a badly executed attempt to hide apps using non-traditional ports, always a dumb idea!

![](/static/img/screenshot-2024-08-02-at-2.15.22 pm.png)

And another one in port 50080 (yawn?)

![](/static/img/screenshot-2024-08-02-at-2.18.07 pm.png)

And directory traversal over the Internet is allowed, another strike!

![](/static/img/screenshot-2024-08-02-at-2.20.59 pm.png)

With so many potential attack surfaces, the challenge is which one to pick first.  You don't want to go down a rabbit hole and waste a lot of time in what should be a pretty easy machine to exploit!

Let's enumerate some more then, gobuster to the rescue!

\--- TO BE CONTINUED ---