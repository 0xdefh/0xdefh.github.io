---
title: ENG - OSINT Techniques | How to find impersonate website
date: 2025-01-25
author: khuong
layout: post
categories: [Security]
tags: [beginner,threatintelligence]   
toc: true
image:
    path: /assets/img/arctrooper.jpg
---

## Overview

During my investigation I have expose to investigate few of the Impersonate website, such as webiste that fake Facebook & website that fake such type of login panel, these website is use in phishing, fraud or scam campain

My job is to tracking those website to reported to the phishing pool or just discover the potential owner of these websites or domains

Today, I'll show you a few TTPs that I use during my investigation. 

Most of these TTPs is refer to finding an unique identifer label (UIL) which is a unique thing about the website or domain, these thing could be wording, html content, a piece of javascript code, overlap in whois historical data or any general unique thing that you can use to pivot

So let's start with a study case rather than a showing all the tools and theoratical cases. OSINT is a mindest not the tools. 


## General Knowledge | Finding the seed information | Phishing

I've always said this quotes so many time, master youself master the enemy. 

Let's start with the original Telegram Web Page, examinate the original one first to help us understand what is the legit website

How we identify which website is legit?

1. Domain / IP address 
2. HTML Content
3. Urghh what else? 

So yes, domain/ip address and HTML content.

Let's understand how attacker can spread (distubution) these type of impersonate website

- Email Phishing
- Direct message phishing
- SMS Phishing
- Google / Youtube / Facebook Ads or Ads in General 

-> These are the cases that know about, these most likely is a product of what's known to be phishing kit 

So in order to tracking these type of stuff we need to find where can information will store 

## Study Case 1: Telegram Login Panel 

### Requirement or Investigation Objective

* Find any Impersonate Telegram Login Page
* Check if those website belong to a mass phishing campain or not
* 


### Collection 

Alright, let'start tracking telegram login panel, but there is a problem, you can scan the whole internet and then store all that data and query for those information
to track html contents and domains that are different from the original website but has the logo mark something but that will cost you a lot of time

So I'll use a free internet scanner tools (hmm probably some day I'll build my own database for that because I love build thing)

- [URLScan.io](https://urlscan.io/)
- [Censys](https://censys.com/)
- [Shodan](https://www.shodan.io/)
- [Hunt.io](https://hunt.io/)
- [Fofa](https://en.fofa.info/)
- [Virustotal](https://virustotal.com/)
- [Hybrid Analysis](https://www.hybrid-analysis.com/)
- [AnyRun](https://any.run/)
- Whois Database
- [URLHaus](https://urlhaus.abuse.ch/)
- Python 
- Google Dorking 
- PhishTank 
- [PhishStat](https://phishstats.info/)
- StalkPhish OSS

Notable Mention: Validin 

I know, I know, a bunch of tools, remember the first step of CTI or Intelligence is COLLECTION, we must collect information. So those are sources of information.
These tools allow me to search for those information (but with some limitation but that's okay)

Alright we got ourself a bunch of data source that can look for

Let's take a look at the real Telegram Login page to understand what is normal and use that to pivoting and make searches

![Telegram QR Code Login](/assets/img/teleqrlogin.png)

Telegram Legit QR Code Login

![Telegram Phone Number Login](/assets/img/telephonelogin.png)

Telegram Phone Number Login 

![Telegram Title](/assets/img/teletitle.png)

Telegram Title

### Google Dork 
Let's begin and start with a simple keywords list and Google dorks 

**Keyword List:**

* Telegram 
* Please confirm your country code and enter your phone number

**Google Dork:**

This dork will list out all the domain 

```shell
intext:"Please confirm your country code and enter your phone number" -site:*.telegram.org telegram
intext:"Log in to Telegram by QR code" -site:*.telegram.org telegram
intext:"Open Telegram on your phone" -site:*.telegram.org
```

> This could be sometimes useful for us, just to check if are there any Fake website that has already index by our beloved Google. This could apply to others website as well
for me I'll just use a Google Alert just to monitor these stuff if any new website that show up
{: .prompt-info } 

Here you can see just a few search we could find a few potential fake website (which there is a bias here not every impersonate is malicous and not) most impersonate website has a short time to live
so probably it will not gonna be indexed

![Telegram Potential Fake Website](/assets/img/telefakeweb.png)

We could take a look at every website or you write google dork type of automation and crawl all the content of the search result. and then extract interesting javascript or weird html content, for me I just pick a random and **start using URLScan to find if are there any similar.**

Well if you not sure if the domain is legit or not or want to gain more information you could check for more information such as whois records, html content, javascript or just use a burpsuite intercept request just to be sure if are there anything interesting.

Or maybe conduct a vuls scan on that server. It depends.


After the dorking you can try other data source. In this cases I'll try URLScan.Io and any free and open reported phishing data (such as phish tank and phish stat)

### Phish Tank & Phish Stats

By using PhishStat.info API, which you can take a look at it right here: [API Documentation](https://phishstats.info/#apidoc) by default it will return 20 results, but I'll but the _size=100

This command will use the api from the phishstats to get some phising site that has reported as impersonate Telegram and we will pivoting from that
```shell
curl --insecure -XGET -H "Content-type: application/json" 'https://phishstats.info:2096/api/phishing?_where=(title,like,~Telegram~)&_sort=-id&_size=100' | jq
```

Example output:

```json
{
    "id": 11228739,
    "url": "http://www.guzi945.top/",
    "ip": "104.21.1.88",
    "countrycode": "",
    "countryname": "",
    "regioncode": "",
    "regionname": "",
    "city": "",
    "zipcode": "",
    "latitude": "0.0000",
    "longitude": "0.0000",
    "asn": "AS13335",
    "bgp": "104.16.0.0/12",
    "isp": "CLOUDFLARENET, US",
    "title": "Telegram",
    "date": "2025-01-21T02:29:27.000Z",
    "date_update": "2025-01-21T05:39:39.000Z",
    "hash": "1482c96533fdc5ce06952c36d55af966218da8919f75e523025f4abec64a559f",
    "score": 6.3,
    "host": "www.guzi945.top",
    "domain": "guzi945.top",
    "tld": "top",
    "domain_registered_n_days_ago": null,
    "screenshot": null,
    "abuse_contact": "abuse@guzi945.top",
    "ssl_issuer": null,
    "ssl_subject": null,
    "alexa_rank_host": null,
    "alexa_rank_domain": null,
    "n_times_seen_ip": 1,
    "n_times_seen_host": 1,
    "n_times_seen_domain": 1,
    "http_code": 403,
    "http_server": "cloudflare",
    "google_safebrowsing": "No",
    "virus_total": "Yes",
    "abuse_ch_malware": "No",
    "threat_crowd": null,
    "threat_crowd_subdomain_count": null,
    "threat_crowd_votes": null,
    "vulns": null,
    "ports": "80, 443, 2082, 2083, 2086, 2087, 2096, 8080, 8443",
    "os": null,
    "tags": "cdn",
    "technology": null,
    "page_text": null
}
```

The website that we found in the phishstats and still active is **hxxps://www.guzi945[.]top/**

**Addtional Information:**

* 40 days old
* Created on 2024-12-23
* Expires on 2025-12-23
* Updated on 2025-01-15
* Registrar WHOIS Server: www.gname.com

The search result from URLScan.io: [https://urlscan.io/result/59f0bf0e-a8ea-4d5b-8a16-8edfd8527b36/](https://urlscan.io/result/59f0bf0e-a8ea-4d5b-8a16-8edfd8527b36/)

**URLScan.io search query:**

The search query syntax is [here](https://urlscan.io/docs/search/).

```shell
page.url: guzi945.top
page.url: guzi*.top
page.url: *945.top
page.url: guz*.top
```

These search query aim to find more domain that potential using this techniques call , you can read more about that at here: [Mass Telegram account hijacking via supply-chain phishing campaign](https://izoologic.com/threat-advisory/mass-telegram-account-hijacking-via-supply-chain-phishing-campaign/)


This for to check if any malicious side has been indexed by the Google. 


Using a tool to gather all information from all those sources (API), Well you have to registered their services and use their free API. Or you can just use MISP to have the data flow in every day 


## Study Case 2: Gmail or Microsoft


## Study Case 3: General Caess


## Refs for Hunting Impersonate Website or Phishing

These are the article that I read in order to obtain this knowledge also inspired by it and in the end create this blog, to show case the action that I took upon this information.

* [StalkPhish - Use Case Hunting for Phishing 2022](https://stalkphish.com/2022/09/05/use-case-hunting-for-phishing/)
* [Cisco Talos - New Phishing as a Services Tool Greatness](https://blog.talosintelligence.com/new-phishing-as-a-service-tool-greatness-already-seen-in-the-wild/)
* [Brand Protection Hunting for Phishing Kit](https://loungefly84.medium.com/brand-protection-hunting-for-phishing-kits-34df8740989a)
