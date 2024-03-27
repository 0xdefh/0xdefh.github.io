---
title: Fresh off the boat - for new Blue Teamer & SOC Analyst
author: Nguyen Dang "Zeroska" Khuong
date: 2024-03-27 
categories: [BlueTeam, Security, SOC, ]
tags: [begineer]   
---

When you are on the new system and don't know a thing about it, here is a checklist to improve your visibility and its condition, or you are just a fresher blue team and want to learn.


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

