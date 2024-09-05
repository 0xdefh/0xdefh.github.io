---
title: ENG - Investigation using OSINT Case 0x00 - One of the Viet Nam MMO 
date: 2024-07-05
author: khuong
layout: post
categories: [Security]
tags: [beginner]
toc: true
mermaid: true
image:
    path: /assets/img/startwar-osint.jpg
---

## Overview

I was tasked to investigate a Vietnamese person that was doing MMO and accidencly cause damage to some people. I was given a domain and nothing more, these are the question that I need to anwser:

1. What is the Google Analytics ID of this website?
2. What is the origin hosting IP address of the website?
3. What did the website’s owner claim as the reason the website closed forever
4. This website used to have an alternative login method. What was the login
method and the application ID associated with it?
5. Identify a potential admin of the website or the related community

The domain is: `mymin.net`

## My Investigation 

### Gather basic information

I was given only the domain so it is my first pivoting point, first you have to know what kind of information you can have from the domain name: `mymin.net`, you can know it by reading [Pivot Atlas](https://gopivot.ing/), for the domain: 

 ```mermaid 
 flowchart LR
	%% define nodes
	IP_ADDRESS(IP Address)
	DOMAIN(Domain):::primary
	DOMAIN_(Domain):::secondary
	TLS_CERT(TLS Certificate)
	SAMPLE(Sample)
	
	%% define edges
	DOMAIN -- forward DNS --> IP_ADDRESS
	IP_ADDRESS -- reverse DNS ---> DOMAIN
	DOMAIN <-- DNS history --> IP_ADDRESS
	TLS_CERT -- CN ---> DOMAIN
	DOMAIN <-- similar name ---> DOMAIN_
	DOMAIN <-- registrant ---> DOMAIN_
	DOMAIN <-- registrar --> DOMAIN_
	DOMAIN <-- NS --> DOMAIN_
	DOMAIN <-- TLD --> DOMAIN_
	DOMAIN <-- reg. time --> DOMAIN_
	DOMAIN <-- URL path --> DOMAIN_
	SAMPLE -- references ---> DOMAIN
	SAMPLE -- queries --> DOMAIN
```
Refs: [Pivot Atlas](https://gopivot.ing/)


We will be using (this is the tool I prefer) you guys can check this out [Pivot Atlas Tools](https://gopivot.ing/tools/) 
- nslookup
- [Whois](https://who.is/)
- [DNS Checker](https://dnschecker.org)
- [Web Archive](https://web.archive.org/)
- Censys
- Shodan
- Google Search

For faster time to gather this information, you should have a script to automate this porcess for you, which we do use during our investigation but for the sake of clarity we will be doing manual for this case.

#### Domain Information

By using who.is: [mymin.net](https://who.is/whois/mymin.net)

| Registrant Contact Information:        | Administrative Contact Information     | Technical Contact Information          |
| :------------------------------------- | :------------------------------------- | :------------------------------------- |
| Name: None                               | Name: Hau Nguyen                        | Name: Hau Nguyen                             |
| Organization: None                      | Organization: None                      | Organization: None                      |
| Address 342A LE HONG PHONG - NHA TRANG | Address 342A LE HONG PHONG - NHA TRANG | Address 342A LE HONG PHONG - NHA TRANG |
| City Nha Trang                         | City Nha Trang                         | City Nha Trang                         |
| State / Province 34                    | State / Province 34                    | State / Province 34                    |
| Postal Code 718609                     | Postal Code 718609                     | Postal Code 718609                     |
| Country VN                             | Country VN                             | Country VN                             |
| Phone 1206020905                       | Phone 1206020905                       | Phone 1206020905                       |
| Email  ilgbt.net@gmail.com             | Email  ilgbt.net@gmail.com             | Email  ilgbt.net@gmail.com             |
|                                        |                                        |                                        |


| Date Time                |
| :----------------------- |
| Expires On 2025-12-27    |
| Registered On 2019-12-27 |
| Updated On 2024-02-08    |


From this information we have more information to pivoting from:
- Email: ilgbt.net@gmail.com
- Name: Hau Nguyen
- Geolocation: 342A LE HONG PHONG - NHA TRANG


> In this specific case we know that we easily found the Registrat email, name and geolocation but in most case this information probably will be redacted -> which make the case a little bit more challenging
{: .prompt-info }


#### IP Address / Name Server / TLS Certificate

This is easy but finding the true IP Address of the domain will take more time, because some domain will sit behind cloudflare or some reverse proxy.

By using **who.is**: https://who.is/whois/mymin.net  there are tab DNS records which has all the information such as 

- A records (which is IPv4)
- Name server 

| Hostname  | Type | Content                |
| :-------- | :--- | :--------------------- |
| mymin.net | NS   | lily.ns.cloudflare.com |
| mymin.net | NS   | tom.ns.cloudflare.com  |
| mymin.net | A    | 104.26.3.89            |
| mymin.net | A    | 104.26.2.89            |
| mymin.net | A    | 172.67.75.81           |

By using VirusTotal I found TLS Cert and even more information on the domain: [VirusTotal
s Information](https://www.virustotal.com/gui/domain/mymin.net/details) -> if you scroll down you will also find the `45.32.121.177` which is `mymin.net` true IP address. 

We verify this information by using **Censys** and **Shodan** to check whether this IP actually host the mymin.net website https://45.32.121.177/account/login.php -> is the mymin.net login portal

- Censys query: [Censys - 45.32.121.177](https://search.censys.io/hosts/45.32.121.177)
- Shodan: [Shodan - 45.32.121.177](https://www.shodan.io/host/45.32.121.177)

> By using Censys and Shodan, we understand mymin.net infastructure, hosted on vultr and has another hostname `ussv.net`
{: .prompt-info }


Later I'll show you how to find the true IP address behind cloudflare using another technique which I find that it is very fundamental and can be apply to any case.

Alright after we have such information such as:

- IP Address: 45.32.121.177

#### Examinate the website 

> Remember keep a good OPSEC, use a VM and use a VPN or change your User-Agent or using a Proxy, to examinate the Website because all your action will leave digital footprints so in order to keep yourself safe.
{: .prompt-info }

Alright we will start examinate the website by take a look at `mymin.net`, we will inspect the login screen and look for any pivoting point. Because we still need at much information as posible

Using Chrome DevTools to inspect all the element to find the Google analytics ID

> Google Analytic ID usually is written as UA-XXXXXXXX or GA-XXXXXX (The lastest Google analytics 4) Refs the different between it [UA to GA4](https://support.google.com/analytics/answer/10269537?hl=en)
{: .prompt-info }


Inspect and search for the `UA-` or `GA-` (Because in order for Google analytics to work, it will scan your website for such code), if you have adblock extention, you should disable it because it will remove the Google analytics from the website


Google analytics Code from the mymin.net:

![Mymin Google analytics](/assets/img/google-analytic-mymin.png)


Using [Web Archive](https://web.archive.org/) to check the historial data of `mymin.net` for any clues. 

![Mymin.net Login Page](/assets/img/mymin-net-login.png)

There are 29 times where web archive take a snapshot of this webpage, we will check it all the see if are there nay interesting stuffs

![Web Archive Timeline](/assets/img/webarchive-timeline.png)

From 2021 - 2024 this domain is puting to use to serve as as MMO login page, before that 2004-2016 this domain is belong to some Korean Highschool which is not interesting to us.

But when we poking arround the function and review all the link of this webstie we found a lot of interesting stuff

When we click on this USSV policies, its redirect us to another domain which call `mcare.me` where we found even more keywords and information.

![USSV Policies](/assets/img/ussv-policy.png)


`mcare.me` footer give us a lot of information and keywords (facebook, email address, another domain to look for)

![mcare.me footer](/assets/img/mcare-footer.png)

We also using Web Archive one more time to analyze the `mcare.me` for more information


Here is the summary of what we has found (include keywords and findings):
- USSV (on Register page there are a mention of USSV)
- Ucoin
- mcare.me 
- www.ussv.net (from contact)
- 2014 is timestamp when USSV was created
- Facebook: [ussvtools](https://www.facebook.com/ussvtools)
- Google UA ID: `UA-58475948-1`


### Pivoting from the information that we gathered

These are the summary of infomation that we has found:

- Email: `ilgbt.net@gmail.com`
- Name: `Hau Nguyen`
- Geolocation: `342A LE HONG PHONG - NHA TRANG`
- IP Address: `45.32.121.177`
- Domain: `mymin.net`, `mcare.me`, `www.ussv.net`, 
- Keywords: `USSV`, `Ucoin`, 
- Facebook:  [ussvtools](https://www.facebook.com/ussvtools)
- Google UA ID: `UA-58475948-1`
- TLS Cert

That's a lot of information, but now we going to see how these information related to each other and find the owner of mymin.net

#### Email 

This is the most important information in my opinion, you got an email you literaly have the identiy of the person, you can search the email address through multiple database such as:
- Information Stealer database (Using commercial database or you crawl your self [Information Stealer](https://0xdefh.github.io/posts/Stealer-logs/))
- Google Dork the the email on various platform or using tool to automate this process
- Data Breached Database  (you have to crawl it yourself because commercial tool is expensive)


Our checklist are:
- Dork (google, facebook, twitter, forums,...) 
- Search information stealer
- Search data leaked / breached
- Chat mentioned

We start dorking for `ilgbt.net@gmail.com` -> there is only one result 

![Dorking Result](/assets/img/dorking-result.png)

Which it is a [youtube video](https://www.youtube.com/watch?v=XWTdndQ6Vf8) from 10 years ago from "[Cộng Đồng ILNhaTrang](https://www.youtube.com/@AdminFriendlyUSS)" (Full URL: https://www.youtube.com/@AdminFriendlyUSS) Joined Mar 2 2012, this youtube channel contains these keywords which match with the previous information that we gathered:
- USS
- USSV
- Hau Nguyen

By crawling all data from the youtube description, transcript and search against the information we gathered will result more information (which it is to long to listed here, I'll only listed result that matter the most)

From these youtube we even found more keywords and information that I'll save for further investigation:
- `ILGBT.net`
- `cityuss.net`
- `lgbtuss.com`
- `Auto STR`
- `FastDo`
- ...

#### Name

We got a name: `Hau Nguyen`

#### Geolocation 

We got a Geolocation: `Nha Trang`


#### IP Addresse

#### Domains


#### Facebook 


#### TLS Cert

## Conclusion & The Gap in our Analyst & Report


1. What is the Google Analytics ID of this website? -> `UA-58475948-1`
2. What is the origin hosting IP address of the website? -> `45.32.121.177`
3. What did the website’s owner claim as the reason the website closed forever -> ``
4. This website used to have an alternative login method. What was the login 
method and the application ID associated with it? ->
5. Identify a potential admin of the website or the related community -> 