---
title: Fresh off the boat - for new Blue Teamer & SOC Analyst
date: 2024-03-27 
author: khuong
layout: post
categories: [BlueTeam, Security, SOC]
tags: [begineer]   
toc: true
---

When you are on the new system and don't know a thing about it, here is a checklist to improve your visibility and its condition, or you are just a fresher blue team and want to learn. 

> Cyber Kill Chain is the keyword you should look at -> it describes how an attacker will normally do, MITRE ATT&CK will help you know about the detail of each step of the Kill Chain (the ATT&CK  is not a list of all threat actor techniques in the world but it is a list of known techniques)
{: .prompt-info }

> NIST Framework is the place you want to look for first, get the guideline clear and correct, and play it to your system, for me the first important step is to IDENTIFY your environment. 
{: .prompt-info }

> Learn about [OODA Loop](https://en.wikipedia.org/wiki/OODA_loop) and read about [how to use OODA Loop to design your cyber security defense](https://csrc.nist.gov/CSRC/media/Presentations/The-Cyber-OODA-Loop-How-Your-Attacker-Should-Help/images-media/day3_security-automation_930-1020.pdf)
{: .prompt-info }

## Overview

This checklist is what I used to review new systems and networks. While it won't provide a complete picture, it will prompt you to think critically about the system and gain valuable insights. This will help you identify areas for improvement or potential issues.

It's important to go beyond this checklist and delve deeper into system audits. Reading dedicated books and following best practices will provide a more comprehensive understanding. This was my approach before I learned about formal system audits.

## What is Cyber Security in my opinion

The need for security and defense is an age-old concept. From the very beginning, humans have sought to protect what's valuable to them – loved ones, possessions, anything of importance. This instinct led to the development of defensive strategies and tools.

Today, those valuable things are increasingly digital. Whether it's a Facebook account or a company database with millions of records, the information we hold online can be incredibly precious.

Cyber Security take a lot of concept from the military and physical world defenses concept for example:
- Intelligence 
- Threat Hunting
- Least Privilege
- Deception or counter-intelligence 
- ...

So when doing Cyber Security, you think of yourself is a solder or a general, warchief and you are at war, you need to use all your exising resource and make the defenses work just like Sun Tzu said

`"If you know the enemy and know yourself, you need not fear the result of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer a defeat. If you know neither the enemy nor yourself, you will succumb in every battle." - Sun Tzu, The Art of War  `

---

## Know Yourself 
###  Internet-facing servers/services

This is the first thing attackers can get their hands on (look at the Kill Chain - Recon). It is public to the internet so it is crucial that you understand and know these things (How many are there in your system)
- Server's operating system (How many Linux, Windows, Mac, and its versions?)
- Number of Web application services (What are the technologies that are being used to build those websites?)
- Number of Web servers (IIS, Apache, Nginx) 
- Domain (how many subdomains?) 
- 5-tuples (Src, Dest IP Address, Src, Dest Port, Protocol)
- Are there any remote access services that are public to the internet (RDP, VNC, VPN, SSH)
- Firewall

### Understand Windows and Linux 

Set up a lab and start poking around, you can create a lab as below, don't mind the AWS part just use VMware or VirtualBox or Docker Container to do it, and you will learn a lot.

If you wondering what operating system that you should focus on, go with Windows first and then Linux (or mix up but always pay more time for Windows) 



### Email 

Most of the attacks come from BES (Business Email Compromise). 

Small companies don't have the luxury of buying email services, they will self-hosted and will not have a protection system so there will be no filter or any security measure against the top vector of attack which is Email Phishing -> You need to look for Email system and its data flow.

Understand Email Header and how to investigate a phishing ticket


### Logging

That is the data that you are collecting for your SIEM (If you don't have one, build one) -> ELK is a great start, and start ingesting logs to that instance and play around with it, such as what if you use PowerShell what logs does it generate? what is event ID, and what are the best practices to use that log -> any detection that could use this log source

Ref:

- https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html#introduction (Logging for application)
- https://csrc.nist.gov/publications/detail/sp/800-92/final (NIST about logging management)

It is essential, logging is an act of mercy for you and your company, if you do not collect enough logs you will lose your visibility on your system. If your SIEM can handle the sheer amount of logs that pour in then good -> You will learn a lot by analyzing those data 

A better understanding of the log source or the data source will better your detection and your DFIR process later on. I mean you should know what the data source provides you information as IP Address, process execution time when it first appears on the system, does the process communicates to the Internet, and so on. 


`Don't be scare, you will have time and mentor to guide you, and if not then it is ok, you still have a lot of time to familiar yourself with all of this 😘.`

#### Log Format

You must learn about the log format

- Syslog
    - Snare
    - BSD
    - IETF 
- Windows Event Log 
- Product Logs -> which is the log that is generated specifically for your company's product or vendor's product

#### How much log is enough?

You need to understand which log has high value and what are their use case, for example why you collect Event ID 4688 (search the internet and come back to these blogs and tell me why) 

After you understand those concepts, now you need to understand how much data is enough.

#### What should I look for

In Windows you can reference to this article: 
- [Monitoring AD for signs of compromise](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise) which show which log (artifact) that you could use during your investigate and value that provided by the Windows 
- 

### Build your own dashboard

So you don't know how to do data analysis, but you have an account on SIEM and you can create your own shit then "Hell Yah" -> Create your own shit.

So why build your own dashboard and why can I use the default or someone else dashboard, oh you could use the default and be done with it but that's not why you're here, you want to be better, you hunt for hackers not the other way around -> BUILD YOU OWN DASHBOARD (For a small scope first -> build dashboard for a VLAN first).

**The benefit of that is that:**

- You know what you are looking at, the data source, you know what you are monitoring 
- You can quickly learn how the data in that VLAN or System
- You can statistically create a baseline (What computer is talking to, how often it does that, and many more questions that you could come up with your own)


### Familiar with the ticketing system

Most of the time if you are a young analyst you will have to do ticketing (case management) I don't like this but this is something you must do, although it is the simplest form of security task it is also one of the most important ones

### Get to know the people 

Okay, It is true that you need to have a list of systems and who is the owner of it, and learn by asking what is normal to them. 

Join a community and follow people on Twitter, here are some channels, and people you need to follow

**Twitter**

- [Black Hills Information Security](https://twitter.com/BHinfoSecurity) -> Great Team 10/10, a lot of tutorials and helpful videos, good community
- [vx-underground](https://twitter.com/vxunderground) 
- [Netresec](https://twitter.com/netresec)
- [Mandiant](https://twitter.com/Mandiant) 
- [The DFIR Report](https://twitter.com/TheDFIRReport) 
- [Cyber Monk](https://twitter.com/Cyb3rMonk)
- [Shadow Server](https://twitter.com/Shadowserver)
- [CISA](https://twitter.com/CISACyber)
- SANS (all of the accounts that belong to SANS Institute)
- [Florian Roth](https://twitter.com/cyb3rops)
- [Sergio Caltagirone](https://twitter.com/cnoanalysis)
- [Red Canary](https://twitter.com/redcanary)
- [Sekoia](https://twitter.com/sekoia_io)

After you follow a bunch of people, Twitter Algorithm will suggesst you even more yay!

**Discord**

- [Gynvael](https://discord.gg/JXyKVpxzgf)
- [Black Hills Information Security](https://discord.gg/bhis)
- [DFIR](https://discord.gg/digitalforensics)
- [OALabs](https://discord.gg/oalabs)
- [Threat Hunter](https://discord.gg/threathunter)

These channel provide me with huge amount of knowledge and links to article that help me to get my job and stay relevant in the Cyber Security scene.

### Learning Structured Analytic (optional but not too optional)

### Learning Data Analytic (Important)

Know how to do programming would greatly improve you skill

When I first landed my job to do cyber security, I was shocked that there are so many data that flowing to our SIEM.

---
## Know the Enemy

Knowning what are the enemny (threat actor, hackers) are doing, what CVE are they using and what are the 

### Conclusion and How to to get your training

Leaning Cyber Security is hard, there are a lot of concept you need to know and understand, a lot of 