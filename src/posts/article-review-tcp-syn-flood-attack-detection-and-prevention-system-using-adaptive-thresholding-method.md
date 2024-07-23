---
title: "Article Summary: Tcp Syn Flood Attack Detection and Prevention System
  using Adaptive Thresholding Method"
description: Tcp Syn Flood Attack Detection and Prevention System using Adaptive
  Thresholding Method
author: Cyber Operator
date: 2022-12-20T03:02:13.486Z
tags:
  - Security Article Review
  - Cyber Law
---
This article is about a way to counter TCP-SYN flood attacks using an adaptive threshold method. TCP-SYN flood attacks exploit the three-way handshake that the TCP protocol uses and creates a large issue with a DOS (Denial of Service) attack. The correlation between the two is that one makes the other one easier to perform. There have been many other approaches to detect or prevent this TCP-SYN flood attack but none that seem to have created a system of the two. 

	The methodology of this article is split between 5 different modules- attack generation module, SYN flood detection module, prevention module, adaptive threshold module and the alert module. This can be seen in Figure 1.  Too detect the TCP- SYN flood is by using python and scapy to detect the incoming packets based on a certain IP address. They compare the number sent by the IP source within a certain time interval and compare it to the adaptive threshold value from their adaptive threshold algorithm. If the value is high then the alert module is notified and the prevention module stops the attack. The results showed that the detection time decreased as the SYN per seconds increased. This clearly shows that the algorithm is working and can detect a large SYN flood attack. 

![](/static/img/38196a82-5a29-44ec-b789-1003ca9d503c.jpeg)

Figure 1- Detection and Prevention Design


The strength of this approach is that any large attack will be detected and will be detected faster with bigger attacks. On the downside the attacker could optimize his attack to be right under the threshold limit after testing the system to then perform his attack undetected. More parameters are needed, and they have stated that for their future work. 

References

1. Ramkumar, B. N., and T. Subbulakshmi. Tcp Syn Flood Attack Detection and Prevention System using Adaptive Thresholding Method. vol. 37, EDP Sciences, Les Ulis, 2021. ProQuest, http://proxygw.wrlc.org/login?url=https://www.proquest.com/conference-papers-proceedings/tcp-syn-flood-attack-detection-prevention-system/docview/2507662989/se-2, doi:<https://doi.org/10.1051/itmconf/20213701016>.