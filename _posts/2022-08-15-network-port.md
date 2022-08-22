---
layout: post
title: "[Network] 포트(Port)의 개념"
date: 2022-08-15 15:12:09 +0600
categories: [Network]
author: EuiSangYu
post_image: "/assets/images/network/port.png"
---

## 포트(Port)의 개념

우편물 배송에 비유하자면 집 주소 만으로는 누구에게 전달할지 명확히 알 수 없기 때문에, 집 주소와 함께 받는 사람의 이름까지 적어줘야 정확한 배송을 받을 수 있다.

이 때, 집 주소에 해당 하는 것이 `IP`이며, 받는 사람 이름이 `Port`다.

## 포트(Port)범위

`0 ~ 65535` : 16비트 숫자로 구성됨  
`0 ~ 1023` : 잘 알려진 포트 번호로 웹 서버, 메일 서버 같은 프로그램들이 사용한다.  
`1024 ~ 49151` : 잘 알려지지 않은 프로그램들이 사용한다.  
`49152 ~ 65535` : 서버가 클라이언트를 식별 할때 사용이 된다.