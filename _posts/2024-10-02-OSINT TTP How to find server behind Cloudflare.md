---
title: ENG - OSINT Techniques | How to find a server behind Cloudflare
date: 2024-10-02
author: khuong
layout: post
categories: [Security]
tags: [investigation,osint,ttp]
toc: true
mermaid: true
image:
    path: /assets/img/warhammergame.jpg
---


## Oveview

During my day doing OSINT investigation. I has encounter numerous of Website that trying to hide themself with Cloudflare. They think they are safe because their IP address got cloudflare protected.

## The Big Picture and the Fundamental

Internet with its **3,706,452,992 Public IPv4 addresses** is scanned everyday by various services such as Censys, Shodan, Fofa,... and include all the Pentester self-hosted Internet Scanner, all the threat hunter, all the SSH bruteforce attempts, all the Mirai Bot, and many more. So basically, Internet scanning isn't something new. 

Finding a server behind Cloudflare is all about finding something unique about their website that hosted on that server and then hopefully those internet scanner services pick up the server right at the momment the unique thing is there.

Just like you already have all the IP address getting profile and already has all the information you just need a pivoting point to find they needle in the haystack.


> Notes: But still there are some thing you can do to hide your server behind Cloudflare by reading this blog you will see with proper Cloudflare configuration you can securely hide you server
> [How To Bypass Cloudflare and How To Defend by Kerkour](https://kerkour.com/how-to-bypass-cloudflare-and-how-to-defend)
{: .prompt-info }


I'll show you a few way to do it.

This is nothing new and nothing magical about it. Just thank for the services and how the Internet work. 


```mermaid
flowchart LR
    %% define nodes
    USER(User)
    CLOUDFLARE(Cloudflare CDN)
    TRUESERVER(Origin Server)
    INTERNETSCANNER(Internet Scanner - Censys, Shodan,...)
    IP(IP Address)
    HTML(HTML)
    FAV(Favicon)
    OTHERS(Other Information)

    %% define edges    
    USER -- 1 - Access --> CLOUDFLARE
    CLOUDFLARE -- 2 - Serve Origin Server Content --> USER
    CLOUDFLARE -- 3 - Redirect --> TRUESERVER
    TRUESERVER -- 4 - Send Data --> CLOUDFLARE
    INTERNETSCANNER -- Scan --> TRUESERVER
    TRUESERVER -- Has --> IP
    TRUESERVER -- Has --> HTML
    TRUESERVER -- Has --> FAV
    TRUESERVER -- Has --> OTHERS
```

## Easy: Favicon Hash

**What is Favicon?** Favicon is a logo of the browser tab that you see everyday, this was the first unique thing about the Website because people create their logo, trademarks
and put 

So when identify which server is have that Favicon hash is the easiest way to identify the server behind Cloudflare. Censys and Shodan 

Script to caculate the favicon hash, you win will input the URL of the favicon hash, for example: `python3 script.py www.example.com/favicon.ico`

```python
#!/usr/bin/env python3
import mmh3
import requests
import codecs
import sys
from termcolor import colored
from requests.packages.urllib3.exceptions import InsecureRequestWarning
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)

if len(sys.argv) < 2:
	print("[!] Error!")
	print(f"[-] Use: python3 {sys.argv[0]} http://example.com/favicon.ico")
	sys.exit()

def main():

    try:
        response = requests.get(sys.argv[1], verify=False)
        if (response.status_code != 404):
            favicon = codecs.encode(response.content,"base64")
            hash_favicon = mmh3.hash(favicon)

            print(colored(f'http.favicon.hash:{hash_favicon}', "yellow"))
            print(colored(f'https://www.shodan.io/search?query=http.favicon.hash%3A'+str(hash_favicon), "green"))
            print(colored('http:s//www.censys.io/search/query'))
        else:
            print(colored(f'http.favicon.hash: not found', "red"))

    except Exception as e:
        print(colored(e, "red"))

if __name__ == '__main__':
	main()
```

After you got this information you go to shodan and search.

## Easy: Banner or Title Hash

Same fundamental techniques as the Favicon hash. Banner and Title hash also got index and scan by the these Internet Scanner. In HTML Page, there are always a title and a banner which you can 



## Medium: TLS Certificate 




## Verify Information using Curl

I learn how to use verify the origin server is owner of the domain or not by reading this blog: [Discovering the IP address of a Wordpress site hidden behind Cloudflare](https://blog.nem.ec/2020/01/22/discover-cloudflare-wordpress-ip/)

For a single IP address host a single domain

```shell
curl "IP Address" -H "Host: "
```

For an IP address that server multiple domain (shared IP address)

```shell
curl -k --resolve domain:port:ip_address https://<domain name>
```

The reason why you use the `--resolve` because of


## How can you make it harder for the OSINT guys.

I think you can't, just like your footprint of your C2 or anything of your server will get scan

## Refs

- [How To Bypass Cloudflare and How To Defend by Kerkour](https://kerkour.com/how-to-bypass-cloudflare-and-how-to-defend)
- [How to Bypass Cloudflare in 2024](https://scrapeops.io/web-scraping-playbook/how-to-bypass-cloudflare/)
- [Discovering the IP address of a Wordpress site hidden behind Cloudflare](https://blog.nem.ec/2020/01/22/discover-cloudflare-wordpress-ip/)


