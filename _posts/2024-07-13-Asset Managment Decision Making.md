---
title: Asset Management Decision Making
date: 2024-07-13
author: khuong
layout: post
categories: [Security]
tags: [beginner]
image:
    path: /assets/img/binarysunset.jpg 
comments: true
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
- [CSF Framework v2.0](https://csf.tools/reference/nist-cybersecurity-framework/v2-0/)

## 0. Overview

In the IDENTIFY of the NIST we'll plit it into stages:
- Plan for asset management
- Identify the services 
- Identify the assets
- Document the assets
- Manage the assets

Note: **A service is a set of activities that the organization carries out in the performance of a duty or in the production of a product.**

## 1. Plan for asset managment

First step is to prepare all the necessary documents that support the Asset Managment process and getting the approval from the upper managment in order to determined the scope of the assets management.

Asset management is significantly more complex for Managed Security Service Providers (MSSPs) than in-house enterprise teams. This is due to the necessity of obtaining customer agreement on asset management procedures, storage methods, and scope. Often, MSSPs manage only specific zones rather than entire sites, limiting their overall visibility.


## 2. Identify and prioritize the services

Services that are critical to organization, services that if something bad happen to it will impact the organization business

### Why You Identify Services?

Why identified services first? from the top-down level prespective, Organizaion provide services for the customer, asset exist to support the services to run smoothly and generate capical for the organization or just keep it operational

I undetstand this while I take the CISA Critical Infrastructure Course (401v) which show me how to analyze business purpose, which it is apply to ICS but we can take a page from that, here is the refs: [ICS CISA Training](https://ics-training.inl.gov/). Which this type of analysis is call **Criticality Analysis** (You could take a look at [Risk Assessment - Criticality Analysis RA-9](https://csf.tools/reference/nist-sp-800-53/r5/ra/ra-9/)). 

### How to Identify Services

You have to understand:
1. What are the services that the business provide for the customer?
    - Internal services (Interal service that support in-direct to the external service)
    - External services (Mostly the service that the business provide for the customer)
2. Which are the most important services?.
3. Does those services has a any relationship with each other (does it support each other to fulfill the business goal).
4. What are the order of criticality of those services.

For example:

Imagine that we are working as a security engineer for a company that provide crypto exchange (probably Binance, OKX,...), let ask those questions to ourself. Please remember this is just an example. I found this on the internet [How does a centralised crypto exchange actually work ?](https://medium.com/coinmonks/how-does-a-centralised-crypto-exchange-actually-work-84a574fe0a1) which have a diagram of crypto exchange system, Let's us try to dissect it and do Assest Managment on it.

![Cryto Exhange System](/assets/img/crypto-exchange-system.png)

Now we answer those questions above:

1. Provide a platform that trader could trade and exchange crypto, customer will deposit an amount of money, and the compnay will take that money and start trading on behave of the customer, or act as a broker.
2. These will be:
    - Deposit Money to Trading Account
    - Sell / Buy Crypto
    - Store Crypto
3. Yes! It all related to each other, you can buy or sell cryto if you don't have money, and if the crypto balance doesn't show up on your app while you have a bunch of them -> the customer are not going like it.

> These information could be taken from Business Impact Analysis (BIA) or any activities that the GRC had conducted, you should leverage that information.
{: .prompt-info }

After you identify the services and the supported services you should have a diagram look like this:

![Critical Services](/assets/img/critcal-services.png)

These are the critical services that support the business goal which is crypto exchange, if we prioritize which is the most critical services it would be like this: (tbh it is very hard to decide which services is more important than the other) - If I'm wrong please have a comment
1. Sell / Buy Crypto
2. Deposit Money 
3. Store Crypto / Could be a database that store all the transaction

![Identify and Prioritize the Services](/assets/img/identify-the-services.png)

By properly prioritizing services, an organization can proportionately allocate budget and resources for
resilience activities with the services that matter most, such as identifying assets.

**Asset definition**

After these step you should have a list of
- List of prioritized services
- Definition of Asset

## 3. Identify the assets

After you have all the necessary document, you have define the process and the definition of the asset that you want trying to manage. Now you need to break down the services in to assets

Assets that support the services are **people, technologies, informations, and facilities**. 

> Every services has the assets that support it mission, assets that support critical services are extremely important.
{: .prompt-info }

These are the step that you need to conduct when identify the assets:

- Assign responsibility for identifying assets supporting critical services.
- Identify people assets.
- Identify information assets.
- Identify technology assets.
- Identify facility assets.

For the purposes of this hypothetical scenario, let's assume that we don't have specific individuals in mind to own or manage the assets. In reality, these roles would need to be assigned.

These are the step I use during the identify the assets phase

![Identify The Assets](/assets/img/identify-the-assets.png)

Notes:
- Create an RACI matrix that outlines each person's responsibility for specific assets.


> I'll add the example RACI matrix soon, which it is the foundation of how we document our asset.
{: .prompt-info }
## 4. Document the assets

Alright now you have the services and the assets that you want to manage, now you need to create a document that standardlize the asset's information 

### Create an asset inventory

Every company has its own standard and information that they want to put in the Asset's information but for me a good asset information should have:

| Information of the Asset                                                                                      |
| :------------------------------------------------------------------------------------------------------------ |
| Asset type (people; information; technology; or facilities)                                                   |
| Categorization of asset by sensitivity (generally for information assets only)                                |
| Asset location (typically where the custodian is managing the asset)                                          |
| Asset owners and custodians (especially if assets are external to the organization)                           |
| Format or form of the asset (particularly for information assets that might exist on paper or electronically) |
| Location of asset backups or duplicates (particularly for information assets)                                 |
| Services that are dependent on the asset                                                                      |
| Value of the asset; either qualitative or quantitative                                                        |
| Asset protection and sustainment requirements                                                                 |

> I believe it takes time to determine the specific information your company needs to document for each asset. In the case of a Crypto Exchange Platform, the above details seem sufficient.
{: .prompt-info }

I don't like spreadsheet but it will you start going quite easily rather than trying to build a database for it, for the long run you will probably need a DB.

While spreadsheets can be a starting point for asset information, consider using [Retool](https://retool.com/) in the long run. Retool allows you to build a self-hosted or cloud-based portal or dashboard specifically for asset management. You can easily connect your existing database or spreadsheet and build a user-friendly interface for adding assets and tracking their lifecycle.

Example:

| **Number of Assets** |
| :------------------- |
| People:              |
| Information:         |
| Technology:          |
| Facilites:           |
| **Total Assets:**    |


| ID  | Name | Services Supported | Type | Location | Owner | Custodian | Format | Security Classification | Backup Location | Asset Value |
| :-- | :--- | :----------------- | :--- | :------- | :---- | :-------- | :----- | :---------------------- | :-------------- | :---------- |
|     |      |                    |      |          |       |           |        |                         |                 |             |


Asset Value can be: 


| Loss of Revenue | Additional Expenses | Legal | Customer Service | Good Will |
| :-------------- | :------------------ | :---- | :--------------- | :-------- |
|                 |                     |       |                  |           |



On a scale of 1 to 10, how likely is it that any disruption to the asset will significantly impact its value?

Refs: [CRR Implementation Guide Assets Management](https://www.cisa.gov/sites/default/files/c3vp/crr_resources_guides/CRR_Resource_Guide-AM.pdf) Appendix A. Asset Profile Catalog


### Document the relationship between assets and critical services

I read this [Specification for Asset Identification 1.1](https://nvlpubs.nist.gov/nistpubs/Legacy/IR/nistir7693.pdf) a document from 2011, in this document it said something that very true: `Unfortunately, neither a unified method nor a published specification for performing asset identification exists at this time` and I think till this time I can't find a unified method for it. 


But here a notes for you:
-  An asset could support multiple critical services.
-  Document any protection around the asset

## 5. Manage the assets

Organizational assets are dynamic. As assets change, their resilience requirements and protection strategies change as well. For the organization to effectively manage its assets, it must actively monitor for changes that significantly alter assets, identify new assets, or call for the retirement of assets for which there is no longer a need.

> This will be another blog soon, I'll publish any SOPs that I use during my jobs and hopefully you guy could take inspration from it, or not haha
{: .prompt-info }

## 6. Use case

Once you've spent 3-6 months compiling your asset inventory, consider using Retool or another tool to create a searchable interface for analysts. Integrating this inventory with your existing ticketing system can improve alert information, leading to faster and more efficient triage. Combining this with alert use cases and other relevant data can further streamline your processes