---
title: Stealer Logs
date: 2024-03-28
author: khuong
layout: post
categories: [Security]
tags: [stealer]   
toc: true
---

I don't know how to describe this thing called, but I guess it is OSINT

> I know Info Stealer Monitoring isn't anything new, so this blog is just my way to rediscover how others people has done it, I'm very grateful that those guys share this knowlegde (some keywords) that I can found it on my own. In this blog I just focus on Telegram only, but it could be the same for webs and forums.
When I write this blog I afraid that if someone know about this could use this information in bad ways, or it could doing something harmful. 

## Stealer Logs

Stealer or Info Stealer -> Malicious software designed to steal your data and credentials. Success stealer family

There are a lot of forums, telegram, and discord groups where these threat actors sell data and credentials. Usually, they will provide sample data on their channel to show that the data is legit.

## How do I find these stuffs?

First of all if not because of this SANS webcast, I could never know about this: https://www.sans.org/webcasts/setting-up-osint-watchdogs-create-free-persistent-monitoring-tools-python/, and exchange information with "Konoha" give me an idea that I could do something like that for myself to, so my journey to find Information Stealer Channels began.


### Existing List

By following this list or this list: https://github.com/fastfire/deepdarkCTI/blob/main/telegram.md You can participate in many sources, but the problem is you don’t have the full-time to monitor these chat channels. The need for automation and crawlers is real. (This list is just a starting point for you,; we will develop the OSINT skill to find more channels)

### OSINT

I use various search engines to find these channels and invitation links, and from there I can develop more keywords to search for more chat channels.

Tips how to find private, hidden, personal groups and channels - TelegramPrivateChatLeaks[https://telegra.ph/Tips-how-to-find-private-hidden-personal-groups-and-channels---TelegramPrivateChatLeaks-08-10]

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

Crawl Messages/ Files → Store in Splunk/Elastic DB → Crawl and Search Keywords/ Create Alerts on those datasets → Monitore/ Triage/ Investigate → Report to Customer

There are some paid channel that I don’t know that is worth following because you have to pay → defeat the purpose of OSINT

Also, the channel doesn’t last for a long time so if the source dies then you will have to find another → that’s why we must find the correlation between each channel, think about it, this type of selling is a market and market will have the same characteristic just like a real-life market, they will have a supplier and a distributor.

Refs:
- https://blog.sekoia.io/overview-of-the-russian-speaking-infostealer-ecosystem-the-distribution/
- https://blog.sekoia.io/overview-of-the-russian-speaking-infostealer-ecosystem-the-logs/


Why am I detecting a new telegram channel in the URL, it is because some channels will post a link the their new telegram channel or they create a telegram channel to publish their sample leak data, to download those I need to follow that channel quickly and download it before the link expired.


> Notes: There are other tools but I like to build my own, well at least for now, maybe I'll switch to these tools soon:
> - [Tex](https://github.com/guibacellar/TEx)
> - [AIL Framework](https://github.com/CIRCL/AIL-framework)
{: .prompt-info }

