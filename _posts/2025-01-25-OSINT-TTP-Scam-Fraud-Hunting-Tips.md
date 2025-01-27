---
title: [OSINT TTPs] Impersonate Website
date: 2025-01-25
author: khuong
layout: post
categories: [Security]
tags: [beginner,threatintelligence]   
toc: true
---

## Overview

During my investigation I have expose to investigate few of the Impersonate website, such as webiste that fake Facebook & website that fake such type of login panel, these website is use in phishing, fraud or scam campain

My job is to tracking those website to reported to the phishing pool or just discover the potential owner of these websites or domains

Today, I'll show you a few TTPs that I use during my investigation. 

Most of these TTPs is refer to finding an unique identifer label (UIL) which is a unique thing about the website or domain, these thing could be wording, html content, a piece of javascript code, overlap in whois historical data or any general unique thing that you can use to pivot

So let's start with a study case rather than a showing all the tools and theoratical cases. OSINT is a mindest not the tools. 


## General Knowledge | Finding the seed information | Asking questions

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

-> These are the cases that know about 

So in order to tracking these type of stuff we need to find where can information told 

## Study Case 1: Telegram Login Panel 

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
- [Whois Database]()
- [Threat Fox](https://threatfox.abuse.ch/)
- Python 

Notable Mention: Validin, 

I know, I know, a bunch of tools, remember the first step of CTI or Intelligence is COLLECTION, we must collect information. So those are sources of information. 

These tools allow me to search for those information (but with some limitation but that's okay)



## Study Case 2: Gmail or Microsoft


## Study Case 3: General Caess


