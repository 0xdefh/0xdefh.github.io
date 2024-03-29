---
title: Stealer Logs
date: 2024-03-28
author: khuong
layout: post
categories: [Security]
tags: [stealer, cybersecurity, threat intelligence, research]   
toc: true
---

I don't know how to describe this thing called, but I guess it is OSINT

> Info stealer monitoring isn't a new idea, and I know others have explored it before. I'm thankful for the information they've shared online, which helped me learn how to do it myself. This blog focuses specifically on monitoring Telegram for stolen information, but the techniques could be applied to websites and forums as well.

> While writing this, I worried that someone might misuse this information for malicious purposes. It's important to remember that info stealers are bad actors, and this information should only be used for defensive purposes.

## Stealer Logs

Stealer or Info Stealer -> Malicious software designed to steal your data and credentials. Success stealer family

There are a lot of forums, telegram, and discord groups where these threat actors sell data and credentials. Usually, they will provide sample data on their channel to show that the data is legit.

## How do I find these stuffs?

First of all if not because of this SANS webcast, I could never know about this: https://www.sans.org/webcasts/setting-up-osint-watchdogs-create-free-persistent-monitoring-tools-python/, and exchange information with "Konoha" give me an idea that I could do something like that for myself to, so my journey to find Information Stealer Channels began.


### Existing List

By following this list or this list: https://github.com/fastfire/deepdarkCTI/blob/main/telegram.md You can participate in many sources, but the problem is you don’t have the full-time to monitor these chat channels. The need for automation and crawlers is real. (This list is just a starting point for you,; we will develop the OSINT skill to find more channels)

### OSINT

I use various search engines to find these channels and invitation links, and from there I can develop more keywords to search for more chat channels.

[Tips how to find private, hidden, personal groups and channels TelegramPrivateChatLeaks](https://telegra.ph/Tips-how-to-find-private-hidden-personal-groups-and-channels---TelegramPrivateChatLeaks-08-10)

In this post there are a few things I like about it
- About the invitation link of Telegram (the private links) 
- Using google dork, and telegram dork to find channels that private

Combined with the keyword and understanding of the Telegram channel URL we can craft a few dorks to search for these leak channels. There are some basic search queries:

- site:t.me/joinchat access
- site:t.me/joinchat logs
- site:t.me/joinchat txt
- site:t.me/joinchat
- intext:t.me/
- intext:t.me/joinchat {keyword}
- t.me/joinchat/AAA
- site:t.me/ {keyword}

Some keywords that might be relevant: redline, logs, cloudlogs, logsfree, free logs, hacking software, rat, ddos, trojan, botnet, infect, virus, spyware, cloud extractor, bltools, pegasus, cve, dcrat, venom, aurora, stealer, free stealer, dropper, binder, blackhat, fud, asyncrat.

I try to build keywords full of this in different languages to wider my results

> You can pivot and search for even more Telegram channels from these channels. By using telegram built-in search or using Google search
{: .prompt-info }

## Automate the crawling process

After I got into quite a few Info Stealer Channels I started to download it manually

-> Well you can be manually crawling for data can't you? Here is the control flow of my script which is drawn by my friends, you should code yourself to learn more and can tweak it if you like (using Telethon):
Using python telethon (which is a python lib used to interact with Telegram, which needs a phone number), we could set a pipeline something like this:

**Crawl Messages/ Files → Store in Splunk/Elastic DB → Crawl and Search Keywords/ Create Alerts on those datasets → Monitore/ Triage/ Investigate → Report to Customer**
There are some paid channel that I don’t know that is worth following because you have to pay → defeat the purpose of OSINT

Also, the channel doesn’t last for a long time so if the source dies then you will have to find another → that’s why we must find the correlation between each channel, think about it, this type of selling is a market and market will have the same characteristic just like a real-life market, they will have a supplier and a distributor.

Refs:
- [Overview of the Russian speaking infostealer ecosystem - the distribution](https://blog.sekoia.io/overview-of-the-russian-speaking-infostealer-ecosystem-the-distribution/)
- [Overiew of the Russian speaking infostealer - the logs](https://blog.sekoia.io/overview-of-the-russian-speaking-infostealer-ecosystem-the-logs/)


Why am I detecting a new telegram channel in the URL, it is because some channels will post a link the their new telegram channel or they create a telegram channel to publish their sample leak data, to download those I need to follow that channel quickly and download it before the link expired.

> Notes: There are other tools but I like to build my own, well at least for now, maybe I'll switch to these tools soon:
> - [Tex](https://github.com/guibacellar/TEx)
> - [AIL Framework](https://github.com/CIRCL/AIL-framework)
{: .prompt-info }

## How can we use data leak information?

### Build your own breached/stealer logs database

You have ever heard of [Have I Been Pwned](https://haveibeenpwned.com/) and [Breach Directory](https://breachdirectory.org/), right? they have a pool of breached data and stealer logs of their own, and you wonder how the hell they have that information and why don't you have it

So this is how you can build your own, by collecting all the sample leaked data. 


### Pivot for OSINT investigation

Have you ever felt stuck in a detective rut? Stuck with just a name or email and no way to crack the case? Well, imagine having a secret weapon – a treasure chest full of clues!

That's kind of what information stealer data is like for investigators. It's packed with things people might not want you to see – passwords, usernames, even where they surf the web. This info can be a game-changer, making investigations way smoother than sifting through social media.

Of course, with great power comes great responsibility! Using this data can be a bit of a gray area, but hey, that's why we have experts to figure it all out.

Here's a fun fact: Say you're hunting down an email address. Traditional detective work might not tell you much. But with this special data, you could find a treasure trove! Login details, computer info, maybe even their location (think detective gadgets!).

Remember, this is just the tip of the iceberg! Information stealer data is a fascinating (and sometimes tricky) tool that helps investigators solve mysteries.

## References and credits

In this section, I'll give you my understanding of these channels during my learning (I just re-learn this knowledge from the best OSINT practitioner around the world) thanks https://twitter.com/matt0177 (Matt Edmondson) for sharing his knowledge. Also Michael Bazzel for the Inteltechniques and many other OSINT practitioners.

Also "N" who together with me built the script, reinvented quite a lot of wheels but it was quite fun and the best part is that we learned something new. I appreciate your help, contributions, and support

Refs I'll update this list regularly.
- https://therecord.media/redline-stealer-identified-as-primary-source-of-stolen-credentials-on-two-dark-web-markets
- https://www.youtube.com/watch?v=gFp1XOmssAg&ab_channel=FIRST (Very good talk, I like it)
- https://www.first.org/resources/papers/conf2023/FIRSTCON23-TLPCLEAR-Kim-Info-Stealer-Most-Bang-for-the-Buck-Malware.pdf (The slide from the above talk)
- https://start.me/p/DPYPMz/the-ultimate-osint-collection
- https://medium.com/@nijithneo/guide-to-osint-in-person-investigation-bd2a38cd3616
- https://inteltechniques.com/blog/2022/07/06/new-breach-data-lesson-ii-stealer-logs/
- https://arstechnica.com/security/2023/11/hackers-spent-2-years-looting-secrets-of-chipmaker-nxp-before-being-detected/ (Just someone of many reasons why you should monitor data leak)

## What's next
I guess finishing the script and publishing that small script, storing all that data, keep researching on Info Stealer, tracking their C2 infrastructure and deception. To be honest I got a lot of ideas. 

Find the relations between telegram channels.

Learn about data breaches and how to obtain them. In this Telegram Monitoring, I'm talking about breaches that much.

Learn more from others. 