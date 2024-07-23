---
title: " Article Summary: A Kernel Rootkit Detection Approach Based on
  Virtualization and Machine Learning"
description: " A Kernel Rootkit Detection Approach Based on Virtualization and
  Machine Learning"
author: Cyber Operator
date: 2022-12-20T17:19:17.169Z
tags:
  - Security Article Review
  - Cyber Security
---
The kernel plays a huge role in operating system resource management. The operating system kernel can be compromised by a kernel rootkit. A kernel rootkit, once loaded, can carry out malicious operations on a system with high privilege. VKRD is proposed to address the limitations that other methods used to defect kernel rootkits suffer. VKRD is based on hardware assisted virtualization technology. VKRD provides transparent execution environment for kernel module in order to view its runtime behavior. VKRD leverages the stealth breakpoint technique to hook the kernel module loading. The key functionality is performed at VMM level and to retrieve the kernel’s module behavior, virtual machine introspection is performed. VKRD has moderate performance cost that are much smaller than DECAF’s monitoring. Some weaknesses are related to the security assumptions. VKRD assumes the operating system kernel is trusted before the kernel rootkit gets executed and VMM is trusted for its small TCB. Also, the methods used in VKRD may not identify some sophisticated kernel rootkits that rely on specific events for execution.

Tian, Donghai et al. “A Kernel Rootkit Detection Approach Based on Virtualization and Machine Learning.” IEEE access 7 (2019): 91657–91666. Web.