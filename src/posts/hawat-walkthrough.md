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

\--- TO BE CONTINUED ---