---
title: Asset Management Decision Making
date: 2024-07-13
author: khuong
layout: post
categories: [Security]
tags: [beginner]
toc: true
---

## Introduction

When I start and learn about Cyber Security in general, while reading NIST and how to create a better defend plan for a company, I realize you can't win a battle against threat actor if you don't know and understand what are you protecting.

In NIST, the first step a of Cyber Security program that is IDENTIFY. The assets managment seem like a easy task but it is not trust me, it is not something you can plug a tool and then it magically map out all your assets and show you what are the most critical assets (high value) in your envinronment. It not just technology but it's depend on the people the culture and the platfrom you are using (Cloud, Hybrid, On-prems).

`IT asset management (ITAM) is foundational to an effective cybersecurity strategy and is prominently featured in the SANS Critical Security Controls and NIST Framework for Improving Critical Infrastructure Cybersecurity `

`"If you know the enemy and know yourself, you need not fear the result of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer a defeat. If you know neither the enemy nor yourself, you will succumb in every battle." - Sun Tzu, The Art of War"`


Refs:
- [CRR Resource Guide - CISA](https://www.cisa.gov/sites/default/files/c3vp/crr_resources_guides/CRR_Resource_Guide-AM.pdf)
- [NIST 1800-5](https://www.nccoe.nist.gov/publication/1800-5/index.html)
- ...

## Overview

In the IDENTIFY of the NIST we'll plit it into stages:
- Plan for asset management
- Identify the services 
- Identify the assets
- Document the assets
- Manage the assets

Note: **A service is a set of activities that the organization carries out in the performance of a duty or in the production of a product.**

## Plan for asset managment

First step is to prepare all the necessary documents that support the Asset Managment process and getting the approval from the upper managment in order to determined the scope of the assets management.


## Identify and prioritize the services

**Why You Identify Services?**

Services that are critical to organization, services that if something bad happen to it will impact the organization business

Why identified services first? from the top-down level prespective, Organizaion provide services for the customer, asset exist to support the services to run smoothly and generate capical for the organization or just keep it operationa


I undetstand this while I take the CISA Critical Infrastructure Course (401v) which show me how to analyze business purpose, which it is apply to ICS but we can take a page from that, here is the refs: [ICS CISA Training](https://ics-training.inl.gov/). Which this type of analysis is call **Criticality Analysis**. 

You have to understand:
1. What are the services that the business provide for the customer?
    - Internal services (Interal service that support in-direct to the external service)
    - External services (Mostly the service that the business provide for the customer)
2. Which are the most important services that the business reply on? 
3. Which are the services that support the most important services? 

Example:

Imagine we are doing security engineer for a company that provide crypto exchange (probably Binance, OKX,...), let ask those questions to ourself. Please remember this is just an example. I found this on the internet [How does a centralised crypto exchange actually work ?](https://medium.com/coinmonks/how-does-a-centralised-crypto-exchange-actually-work-84a574fe0a1) which have a diagram of crypto exchange system.

![Cryto Exhange System](/assets/img/Screenshot%202024-08-06%20at%2019.29.09.png)

Now we answer those questions above:

1. Provide a platform that trader could trade and exchange crypto, customer will deposit an amount of money, and the compnay will take that money and start trading on behave of the customer, or act as a broker
2. These could be:
    - Trading Engine
    - 
3. Trading, deposit, withdraw function

> These information could be taken from Business Impact Analysis (BIA) or any activities that the GRC had conducted, you should leverage that information.
{: .prompt-info }

After you identify the services and the supported services you should have a diagram look like this:




Then you have to define which information should you have to 


![Identify and Prioritize the Services](/assets/img/identify-the-services.png)


## Identify the assets

After you have all the necessary document, you have define the process and the definition of the asset that you want trying to manage. Now you need to break down the services in to assets

Assets that support the service, such as people, technologies, informations, and facilities. 


## Document the assets



## Manage the assets

