---
title: ENG - Investigation using OSINT Case 0x00 - One of the Viet Nam MMO 
date: 2024-07-05
author: khuong
layout: post
categories: [Security]
tags: [beginner]
toc: true
mermaid: true

---

## Overview

I was tasked to investigate a Vietnamese person that was doing MMO and accidencly cause damage to some people. I was given a domain and nothing more, these are the question that I need to anwser:

1. What is the Google Analytics ID of this website?
2. What is the origin hosting IP address of the website?
3. What did the website’s owner claim as the reason the website closed forever
4. This website used to have an alternative login method. What was the login
method and the application ID associated with it?
5. Identify a potential admin of the website or the related community

The domain is: mymin.net

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
- [Whois](who.is)
- [DNS Checker](https://dnschecker.org)
- [Web Archive](http://web.archive.org/)
- 

For faster time to gather this information, you should have a script to automate this porcess for you, which we do use during our investigation but for the sake of clarity we will be doing manual for this case.

#### Domain Information

By using who.is: https://who.is/whois/mymin.net 

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

This is easy but finding the true IP Address of the domain will take more time, because some domain will sit behind cloudflare or some CDN services.

By using who.is: https://who.is/whois/mymin.net  there are tab DNS records which has all the information such as 

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
s Information](https://www.virustotal.com/gui/domain/mymin.net/details) -> if you scroll down you will also find the `45.32.121.177` which is mymin.net true IP address

Later I'll show you how to find the true IP address behind cloudflare using another technique which I find that it is very fundamental and can be apply to any case.


Alright after we have such information such as:

- IP Address: 45.32.121.177

#### Examinate 


## Conclusion
