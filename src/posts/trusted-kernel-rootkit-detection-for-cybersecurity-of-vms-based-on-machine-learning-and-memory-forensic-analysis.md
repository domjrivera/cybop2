---
title: Trusted Kernel Rootkit Detection for Cybersecurity of VMs Based on
  Machine Learning and Memory Forensic Analysis*
description: In summary, the journal presents a convincing method, a TKRD
  (Trusted Kernel Rootkit Detection), to detect known and unknown rootkits in
  VMs from private cloud environments. The method combines the memory forensic
  analysis and machine learning to detect viruses with proven experimental
  results. However, some assumptions are required for further study.
author: Cyber Operator
date: 2022-12-30T18:39:09.213Z
tags:
  - Security Article Review
---
*Summary of: Wang, Xiao et al. “TKRD: Trusted Kernel Rootkit Detection for Cybersecurity of VMs Based on Machine Learning and Memory Forensic Analysis.” Mathematical biosciences and engineering : MBE 16.4 (2019): 2650–2667. Web.*

This article is to demonstrate a solution, TKRD(Trusted Kernel Rootkit Detection), to detect known and unknown kernel rootkits based on the machine learning algorithm, to reduce the cyber security attack using rootkits on virtual machines running in a private cloud computing environment. Here are the steps explained in the article.

1. Memory dump from OpenStack platform - The first step is to take the memory snapshots from the controller node dashboard
2. Data Collect - The experiment takes ~100 rootkit samples uploaded to the VM. By using Python scripts, 2300 memory dumps are collected to capture different intervals and various application states including OS.
3. Memory Forensic - After the memory dumps, the article then dives into the feature extraction for memory forensic analysis by using a widely used memory forensic framework called Volatility. This framework includes different plugins for rootkit detection. Those plugins can detect abnormal behaviors based on the standard kernel metadata structure and normal processes, such as doubly linked list, orphan thread, device tree, etc. With the feature extraction, the article explains the step of calculating the Mutual Information using marginal probabilities of the frequency of occurrence and the boolean indicator of whether a rootkit is presented, and joint probabilities of both. At the end, the article applies the machine learning algorithm to train the classifier based on the human perception and bio-inspired models.  
4. Experiments and Evaluation - The article uses various algorithms supplied by Weka 3.9, a machine learning software and evaluates the performance, accuracy, and effectiveness of different machine learning models. Based on the results, the researchers conclude that Random Forest has the highest TPR and the most excellent classifier.  

Overall, the article proposes a justifiable theory with some the following convincing arguments:

1. Tools and techniques are widely used and recognized by different research groups, as the article also quoted the similar researches and results done by other colleagues.

   1. Open Source OpenStack and Kernel-Based VM Hypervisor
   2. Windows 7 Ultimate (x86)
   3. Volatility - GNU public licensed feature extraction tool
   4. Machine algorithm using human perception and bio-inspired models,RandomForect, J84, PART, etc
   5. Weka 3.9 - a suite of machine learning software written in Java for data analysis and predictive modeling
2. The Volatility plugins leveraged in the research provide a wide range of coverage to detect the malicious behaviors, from corrupted metadata structure, orphan thread, suspicious pointers, to unknown functions such as Callbacks/Timers. This wider scope of coverage increases the accuracy of rootkit detection. 
3. The classifiers used in the machine learning algorithm are based on human perception and bio-inspired models, such as Baysian and SVM. Those models are proven methods for probabilities and quadratic programming algorithms.  

From the assumptions and evidence presented in the article, some of the assumptions should be further explored as shown below. Future studies are required to validate those assumptions.

1. One of the assumptions is that the controller node VM will not be compromised by the rootkit. This should be validated as some virus can be replicated itself through the entire virtual machine, including the controller node. 
2. Driver Objects is one of the plugins to detect the rootkit. The plugin is to check the data from _DRIVER_OBJECT and KLDR_DATA_TABLE_ENTRY and detect any data corruption. The assumption here is that the rootkit can hook the functions of handling different requests from the OS user mode. However, whether the hook exists, it is stated that further analysis is required. 
3. SSDT is another plugin leveraged in the article to detect modified pointers from malicious modules. The assumption is based on the assumption of most rootkits using inline hook techniques instead of pointing out of the NT modules or win32k.sys. However, the inline hook technique theory needs to be validated.

In summary, the journal presents a convincing method, a TKRD (Trusted Kernel Rootkit Detection), to detect known and unknown rootkits in VMs from private cloud environments. The method combines the memory forensic analysis and machine learning to detect viruses with proven experimental results. However, some assumptions are required for further study.