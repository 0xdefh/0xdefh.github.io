---
title: Fresh off the boat - for new Blue Teamer & SOC Analyst
date: 2024-03-27 
author: 1
layout: post
categories: [BlueTeam, Security, SOC, ]
tags: [begineer]   
toc: true
---

When you are on the new system and don't know a thing about it, here is a checklist to improve your visibility and its condition, or you are just a fresher blue team and want to learn.

> Cyber Kill Chain is the keyword you should look at -> it describes how an attacker will normally do, MITRE ATT&CK will help you know about the detail of each step of the Kill Chain (the ATT&CK  is not a list of all threat actor techniques in the world but it is a list of known techniques)
{: .prompt-info }

> NIST Framework is the place you want to look for first, get the guideline clear and correct, and play it to your system, for me the first important step is to IDENTIFY your environment. 
{: .prompt-info }


# Overview

This is the list that I would always check when I got to a new system/network. I know that this list can't give you a well-rounded look at the system but it will make you think and gain knowledge of the system that you are working with -> and plan the improvement or find something that is not right in the system

Reading the system audit checklist and book is good you should read it, the guide was my thought before I knew about system audits.


# 1. Internet-facing servers/services

This is the first thing attackers can get their hands on (look at the Kill Chain - Recon). It is public to the internet so it is crucial that you understand and know these things (How many are there in your system)
- Server's operating system (How many Linux, Windows, Mac, and its versions?)
- Number of Web application services (What are the technologies that are being used to build those websites?)
- Number of Web servers (IIS, Apache, Nginx) 
- Domain (how many subdomains?) 
- 5-tuples (Src, Dest IP Address, Src, Dest Port, Protocol)
- Are there any remote access services that are public to the internet (RDP, VNC, VPN, SSH)
- Firewall

# 2. Understand Windows and Linux

Set up a lab and start poking around, you can create a lab as below, don't mind the AWS part just use VMware or VirtualBox or Docker Container to do it, and you will learn a lot.

If you wondering what operating system that you should focus on, go with Windows first and then Linux (or mix up but always pay more time for Windows) 



# 3. Email

Most of the attacks come from BES (Business Email Compromise). 

Small companies don't have the luxury of buying email services, they will self-hosted and will not have a protection system so there will be no filter or any security measure against the top vector of attack which is Email Phishing -> You need to look for Email system and its data flow.

Understand Email Header and how to investigate a phishing ticket


# 4. Logs 

That is the data that you are collecting for your SIEM (If you don't have one, build one) -> ELK is a great start, and start ingesting logs to that instance and play around with it, such as what if you use PowerShell what logs does it generate? what is event ID, and what are the best practices to use that log -> any detection that could use this log source

Ref:

- https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html#introduction (Logging for application)
- https://csrc.nist.gov/publications/detail/sp/800-92/final (NIST about logging management)

It is essential, logging is an act of mercy for you and your company, if you do not collect enough logs you will lose your visibility on your system. If your SIEM can handle the sheer amount of logs that pour in then good -> You will learn a lot by analyzing those data 

A better understanding of the log source or the data source will better your detection and your DFIR process later on. I mean you should know what the data source provides you information as IP Address, process execution time when it first appears on the system, does the process communicates to the Internet, and so on. 


`Don't be scare, you will have time and mentor to guide you, and if not then it is ok, you still have a lot of time to familiar yourself with all of this 😘.`