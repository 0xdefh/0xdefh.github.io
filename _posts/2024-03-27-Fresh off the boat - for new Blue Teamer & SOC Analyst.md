---
title: Fresh off the boat - for new Blue Teamer & SOC Analyst
date: 2024-03-27 
author: khuong
layout: post
categories: [Security]
tags: [beginner]   
toc: true
---


When you are on the new system and don't know a thing about it, here is a checklist to improve your visibility and its condition, or you are just a fresher blue team and want to learn. 

> Cyber Kill Chain is the keyword you should look at -> it describes how an attacker will normally do, [MITRE ATT&CK](https://attack.mitre.org/) will help you know about the detail of each step of the Kill Chain (the ATT&CK  is not a list of all threat actor techniques in the world but it is a list of known techniques)
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

In the realm of cybersecurity, you're not just a soldier, you're the general, the strategist. It's a constant battle, and just like Sun Tzu said, victory hinges on knowing both your defenses and your adversaries.

`"If you know the enemy and know yourself, you need not fear the result of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer a defeat. If you know neither the enemy nor yourself, you will succumb in every battle." - Sun Tzu, The Art of War  `

Mastering the strategic thinking of Sun Tzu's Art of War can transform you into a more effective cybersecurity defender.

The Cuckoo Egg by Cliff Stoll is a great resource for cybersecurity. Did you know there's a Vietnamese translation available? You might want to check it out!

---

## Know Yourself 

With the NIST framework by your side and the mindset of a general you now must get your hand dirty by actually doing the work. First know yourself -> know your IT/OT environment.

###  Internet-facing servers/services

The initial stage of an attack often involves reconnaissance, where attackers gather publicly available information. Understanding what data is exposed online is critical for your defense.  How much of your system's information is publicly accessible?

You as a defender always has a upper hand in this case, you have control over the asset far better than the attacker. So why not mapping out the network and understand how 

- Server's operating system (How many Linux, Windows, Mac, and its versions?)
- Number of Web application services (What are the technologies that are being used to build those websites?)
- Number of Web servers (IIS, Apache, Nginx,...) 
- Domain (how many subdomains?) 
- 5-tuples (Src, Dest IP Address, Src, Dest Port, Protocol)
- Are there any remote access services that are public to the internet (RDP, VNC, VPN, SSH)
- Firewall, IDS/IPS 

There are so many to understand but the easiest thing in my opinion is to understand this. 

### Understand Windows and Linux 

Hands-on learning is key! Set up a cybersecurity lab using a free tool like VMware, VirtualBox, or Docker containers. This lets you safely experiment with different scenarios and learn through exploration.

For operating systems, focus on Windows first.  Linux is valuable too, but mastering Windows vulnerabilities is crucial as it's a common target. You can eventually explore both, but prioritize Windows initially.

### Email 

Most of the attacks come from BES (Business Email Compromise). 

Small companies don't have the luxury of buying email services, they will self-hosted and will not have a protection system so there will be no filter or any security measure against the top vector of attack which is Email Phishing -> You need to look for Email system and its data flow.

Understand Email Header, Email  and how to investigate a phishing ticket. 

### Logging / Analyze Logs 

**Seeing Through the Fog: Understanding Your IT Environment with Logs**

Ever feel like you're flying blind in your IT environment?  Unsure what your servers are up to, or if they're harboring malicious activity?  The answer lies in a treasure trove of information often ignored: logs.

Logs are detailed records of system activity, capturing everything from successful logins to application errors.  By analyzing these logs, you gain valuable insights into the health and security of your IT infrastructure.  But unanalyzed logs are like locked treasure chests - useless until unlocked.

**Unlocking the Power of Logs with SIEM**

Security Information and Event Management (SIEM) systems are designed to do just that.  They centralize and analyze logs from various sources, helping you identify patterns and potential threats.

Don't have a dedicated SIEM? No worries!

Building Your Own Security Arsenal with ELK Stack

ELK Stack (Elasticsearch, Logstash, and Kibana) is a free and open-source platform that allows you to build your own powerful SIEM.

Taking Control with Hands-on Exploration

Once you have ELK set up, the fun begins! Start collecting logs from your systems and feeding them into ELK.  This lets you explore the data and ask critical questions like:

- What happens when you use PowerShell? What logs are generated?
- What information can an event ID tell me?
- How can I leverage these logs to identify and stop security threats?
- By actively analyzing logs, you gain a clear view of your IT environment, enabling you to detect suspicious activities and proactively secure your systems.

Ref:
- [OWASP Cheat Sheet - Logging](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html#introduction)
- [NIST about Logging ](https://csrc.nist.gov/publications/detail/sp/800-92/final)

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

It's important to prioritize log selection for your SIEM to ensure efficient operation and accurate threat detection. Not all logs are equally valuable.

#### What should I look for

In Windows you can reference to this article: 
- [Monitoring AD for signs of compromise](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise) which show which log (artifact) that you could use during your investigate and value that provided by the Windows 
- [IAN Research - SOC Logging and Monitoring Best Practises](https://www.iansresearch.com/resources/all-blogs/post/security-blog/2021/04/29/soc-logging-and-monitoring-best-practices)
- 

### Build your own dashboard

So you don't know how to do data analysis, but you have an account on SIEM and you can create your own shit then "Hell Yah" -> Create your own shit.

So why build your own dashboard and why can I use the default or someone else dashboard, oh you could use the default and be done with it but that's not why you're here, you want to be better, you hunt for hackers not the other way around -> BUILD YOU OWN DASHBOARD (For a small scope first -> build dashboard for a VLAN first).

**The benefit of that are:**

- You know what you are looking at, the data source, you know what you are monitoring 
- You can quickly learn how the data in that VLAN or System by looking at the metric that you are set up
- You can statistically create a baseline (What computer is talking to, how often it does that, and many more questions that you could come up with your own)

Just like a general or CEO you need glass panel of information ready for you to look at every morning and determined whether shit happend or not.

### Familiar with the ticketing system

Most of the time if you are a young analyst you will have to do ticketing (case management) I don't like this but this is something you must do, although it is the simplest form of security task it is also one of the most important ones.

But khuong, why? well because of this please read this: [Hexacorn - How to become the best SOC analyst e-v-e-r.](https://www.hexacorn.com/blog/2018/02/25/how-to-become-the-best-soc-analyst-e-v-e-r/)

### Get to know the people in your IT Envinroment and surround yourself with people who are in the security field

Absolutely, maintaining a system ownership list is crucial. It's much faster and likely more accurate to inquire about typical behavior from the owners themselves, rather than attempting to figure it out independently. However, be mindful of potential bias or misinformation - it's always wise to pursue verification for complete accuracy.

**Surround yourself with Cyber Security folks**

Join a community and follow people on Twitter, here are some channels, and people you need to follow:

**VN Cyber Security folks**

- A lot of people I want to mention here but I don't have their consent, probably I'll have them list right here soon.

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

**Discords**

- [Gynvael](https://discord.gg/JXyKVpxzgf)
- [Black Hills Information Security](https://discord.gg/bhis)
- [DFIR](https://discord.gg/digitalforensics)
- [OALabs](https://discord.gg/oalabs)
- [Threat Hunter](https://discord.gg/threathunter)
- ...

These channel provide me with huge amount of knowledge and links to article that help me to get my job and stay relevant in the Cyber Security scene.

**Blogs**

- [Tao Security](https://taosecurity.blogspot.com/)
- [The DFIR Report](https://thedfirreport.com/) - For the love of god please read this 
- [Hexacorn](https://hexacorn.com/)
- [AD Security](https://adsecurity.org/)
- [Elastic Security Lab](https://www.elastic.co/security-labs)
- ...

### Learning Structured Analytic (optional but not too optional)

### Learning Data Analytic (Important)

Programming skills are a powerful asset and can significantly boost your skillset and also makes you more valuable in the job market. also Data Analytic

In my first cybersecurity role, I was overwhelmed by the sheer volume of data flowing into our SIEM (Security Information and Event Management system). I felt lost amidst a sea of unfamiliar terms: Windows Event Logs, Application Logs, Firewall Logs, internal IP addresses, VLANs, server names... the list went on. The biggest challenge? Knowing where to even begin! 

Instead of relying solely on reactive ticketing systems, security professionals can leverage Jupyter Notebooks to become active threat hunters.  These notebooks can serve as a daily log, documenting security events and findings. 

Additionally, they can be used to visualize network activity through charts and maps, focusing on the specific VLANs under your responsibility. Most importantly, Jupyter Notebooks empower a proactive approach.  You can create routines that go beyond just responding to tickets.  These routines can involve actively searching for threats within your network and statistically analyzing security events to identify potential issues before they escalate.

By learning data analytics, you can apply various techniques to uncover insights from data. Here are some examples:
- **Frequency analysis**: This technique helps you understand how often certain values appear in your data.
- **Cluster analysis**: This technique allows you to group similar data points together, revealing hidden patterns.
- **Grouping**: This technique involves organizing data into categories based on shared characteristics.
- **Anomaly detection**: This technique helps you identify unusual data points that deviate from the expected patterns.
... (and many more!)"

By learning Python, you can use Jupyter Notebook to do various thing:
- [Threat Hunter Playbook](https://threathunterplaybook.com/tutorials/jupyter/introduction.html)
- [Data Exfiltration](https://pberba.github.io/security/2019/10/08/data-exfiltration/) this blog is amazing btw
- [Handbook of anomaly detection with python outlier detection 1 introduction](https://medium.com/dataman-in-ai/handbook-of-anomaly-detection-with-python-outlier-detection-1-introduction-c8f30f71961c)
- There are many more, I'll added soon

### But what about Malware Analysis, DFIR, Threat Intelligence, Threat Hunter, ... and other cool jobs

This is like the special forces in the Cyber Security, Cyber Security is broad and always changing. But the demand are not that much in VN, 

Vietnam's cybersecurity job market is still developing. While major players like Viettel and VinCSS offer opportunities, remote work for Singaporean companies is another option. But this limited scope shouldn't discourage you. Vietnam's cybersecurity landscape is rapidly improving. Public awareness is growing, and the demand for cybersecurity professionals is on the rise.

---
## Know the Enemy

Knowning what are the enemny (threat actor, hackers) are doing, what CVE are they using and what are the threat landscape by reading news and research paper. This is probably call **Cyber Threat Intelligence** (CTI)

It is seem that event Intelligence alone is also very difficult

---
## Conclusion and How to to get your training

Learning Cyber Security is hard, there are a lot of concept you need to know and understand, a lot of time is just compliance and doing data analysis, asset managment and spread sheet.

The key? Stay curious, stay active, and be proactive! There's always something new to learn, and that's what makes this field so dynamic.

My goal? To give you a clear picture of the industry's direction and how I approach running a Security Operations Center (SOC).