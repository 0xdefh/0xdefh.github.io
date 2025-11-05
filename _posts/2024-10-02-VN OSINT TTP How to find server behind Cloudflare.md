---
title: VN - OSINT Techniques | Làm thế nào để tìm server phía sau Cloudflare
date: 2024-10-02
author: zeroska
layout: post
categories: [Security]
tags: [investigation,osint,ttp]
toc: true
mermaid: true
image:
    path: /assets/img/startwar-osint.jpg
---


## Tổng quan
Trong quá trình điều tra OSINT hàng ngày của tôi, tôi đã gặp phải nhiều trang web cố gắng ẩn mình với Cloudflare. Họ nghĩ rằng họ an toàn vì địa chỉ IP của họ được bảo vệ bởi Cloudflare. 

Nhưng không đâu. 


## Bức tranh lớn và nền tảng
Internet với 3.706.452.992 địa chỉ IPv4 công cộng được quét hàng ngày bởi các dịch vụ khác nhau như Censys, Shodan, Fofa, ... và bao gồm tất cả các máy quét Internet tự lưu trữ của Pentester, tất cả các thợ săn mối đe dọa, tất cả các nỗ lực tấn công SSH, tất cả các Bot Mirai và nhiều hơn nữa.

Vì vậy, về cơ bản, quét Internet không phải điều gì quá mới mẻ.

Tìm một máy chủ đằng sau Cloudflare là tìm một thứ gì đó đặc biệt và duy nhất về trang web của họ được lưu trữ trên máy chủ đó và sau đó hy vọng các dịch vụ quét Internet sẽ thu thập thông máy chủ đó ngay tại thời điểm có điều đặc biệt đó, (favicon hash, TLS cert,...)

Giống như bạn đã có tất cả các địa chỉ IP được lập hồ sơ và đã có tất cả thông tin bạn chỉ cần một điểm xoay (pivoting point) để tìm ra viên ngọc trong đống IP đấy

Tôi sẽ chỉ cho bạn một vài cách để làm điều đó.

Điều này không có gì mới và không có gì kỳ diệu về nó. Chỉ cần cảm ơn các dịch vụ và cách Internet hoạt động.


## Dễ dàng: Hash của Favicon


## Dễ dàng: Banner hoặc Hash của Title hoặc Tên Title 


## Trung bình: Chứng chỉ TLS


## Xác minh thông tin bằng Curl



## Làm thế nào bạn có thể làm cho nó khó hơn cho những người làm OSINT.

