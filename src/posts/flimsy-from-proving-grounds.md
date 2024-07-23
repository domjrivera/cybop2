---
title: Flimsy from Proving Grounds
description: This is a walkthrough of the flimsy machine that can be found in
  offsec's Proving Grounds.  This machine is generally used for training for
  pentest certification exams, such as offsec's OSCP
author: CyberOperator
date: 2024-07-23T20:40:53.707Z
tags:
  - Tags
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