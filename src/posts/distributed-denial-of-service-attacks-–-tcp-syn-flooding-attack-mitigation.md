---
title: Distributed Denial of Service Attacks – TCP Syn Flooding Attack Mitigation.
description: The most dangerous attacks on internet services and networks are
  Distributed Denial of Service Attacks (DDoS), as discussed in the article "
  Distributed Denial of Service Attacks - TCP Syn Flooding Attack Mitigation ".
  The TCP syn flood DDoS attacks on the Apache server are mitigated using a
  method that is given. With a chosen time period, the effect of syn flooding
  will be lessened.
author: Cyber Operator
date: 2022-12-30T18:34:36.218Z
tags:
  - Security Article Review
---
The most dangerous attacks on internet services and networks are Distributed Denial of Service Attacks (DDoS), as discussed in the article " Distributed Denial of Service Attacks - TCP Syn Flooding Attack Mitigation ". The TCP syn flood DDoS attacks on the Apache server are mitigated using a method that is given. With a chosen time period, the effect of syn flooding will be lessened. 

The TCP syn flooding DDoS attack is described after the distributed denial of service attacks. In a SYN flooding attack, the attacker floods the victim server with SYN requests. Incomplete TCP connections made by the attack use network resources. To lessen the server's vulnerability to TCP syn flooding and to block specific IP addresses, we implemented RST.

DDoS assaults are being used by skilled hackers to harm the huge corporation's income cycle. The most harmful and persistent assault that renders servers unavailable to authorized users or clients is TCP SYN flooding. Because of how effectively this attack can halt server operations, we used shell script to create our detection strategy.

## Methodology 

The methodology of the researcher is  known as TCP three-way handshake method. When a client wants to begin a TCP connection to a server, the client and the server exchange a series of messages. We require the following test environment in order to practice DDoS SYN flood detection and mitigation, these steps include  installing a test environment, use VMware Workstation, the number of Ubuntu or Windows computers that can produce DDoS SYN flood attacks (by acting as attackers or authorized clients/users), A machine running Ubuntu 14.04.1 with an Apache2 server installed that will function as a server or victim and the NMAP or ZENMAP utility for locating open ports on the victim or server machine. 

Some of the steps the researcher used includes Using the Wireshark tool, the attacker's suspicious traffic may be collected, and the network's captured traffic can be analyzed after mitigation, the PuTTY tool to check the server's SSH connection following an attack, a TCP SYN flooding attack using the Hping3 or Scapy script on the server or target and Iptables chain set.

## Strengths and Weakness 

Some of the strength of the research is the way it was written and carried out. By capturing attackers' IP addresses and setting TCP - RST over the continuous flow of SYN+ACK, a mitigation approach for TCP syn flood DDoS attacks on the Apache server serves as an example of the research's strength. With a chosen time period, the effect of syn flooding will be lessened. Legitimate users can continue to access their connections using this technique.

An example of the research weakness is to create an application that can be used to counter a TCP SYN attack and lessen its impact, shell code can be utilized and TCP SYN flooding DDoS attack is one of the DDoS attacks that the network has experienced,which  the future research the researcher is going to focus on improving. 

## Citation 

 Snehal Sathwara, and Chandresh Parekh. “Distributed Denial of Service Attacks – TCP Syn Flooding Attack Mitigation.” International journal of advanced research in computer science 8.5 (2017): 2392–. Web.