---
title: "Article Summary: Detecting and Preventing Kernel Rootkit Attacks with
  Bus Snooping"
description: Detecting and Preventing Kernel Rootkit Attacks with Bus Snooping
author: Cyber Operator
date: 2022-12-20T02:52:42.586Z
tags:
  - Security Article Review
  - Cyber Law
---
Article cited: 

H. Moon, H. Lee, I. Heo, K. Kim, Y. Paek and B. B. Kang, "Detecting and Preventing Kernel Rootkit Attacks with Bus Snooping," in IEEE Transactions on Dependable and Secure Computing, vol. 14, no. 2, pp. 145-157, 1 March-April 2017, doi: 10.1109/TDSC.2015.2443803.

# Article Summary: 

The researchers in this article proposed a news hardware-based monitoring solution to detect and prevent kernel Rootkit attacks. The new system they presented, Vigilare system, is a kernel integrity monitor that is built to snoop the bus traffic of the host system from an independent  hardware.  

# Strengths and Weaknesses of research methodology: 

The strength of the new proposed system is that it detect transient attacks, something that is hard to detect using existing snapshot-based integrity monitor. It’s weakness is that it might not be as effective when it comes to dynamic kernel region manipulation rootkit technique.