---
title:  "[Java] log4j 보안 취약점 이슈 동작 원리 및 해결법"
layout: post
author: EuiSang Yu
categories: JAVA
tags: [JAVA]
---

요며칠 log4j 보안 이슈때문에 아주 난리도 아니다..

다들 고생하고 있을테니 나도 정리해두면 누군가에게 조금이라도 도움이 되겠지라는 생각에 정리해본다.

우선 **[보호나라](https://www.boho.or.kr/data/secNoticeView.do?bulletin_writing_sequence=36389)** 사이트에 들어가보면

![](https://velog.velcdn.com/images/clothes/post/abaad36c-3c0d-4e86-8f88-e99cd9e54b7b/image.png)

그럼 이번 보안 취약점 이슈는 왜 발생한걸까?

우선 그걸 알려면 Log4j 가 무엇인지부터 알아야 한다.

> Log4j는 Ceki Gülcü가 처음 개발한 자바 기반 로깅 유틸리티이고,  
> 아파치 소프트웨어 재단의 프로젝트 아파치 로깅 서비스(Apache Logging Services)의 일부이다.  
> 또 Log4j는 여러 자바 로깅 프레임워크들 가운데 하나이다.  
> 최종 사용자가 제품의 문제나 정보를 식별하기 위해, 그리고 소프트웨어 개발자가 프로그램을 개발하는 도중에 디버깅 등을 위해 타임스탬프 등 정해진 양식에 맞추어 화면 상이나 파일로 로그를 남길 목적으로 사용된다.  
>   
> ...**[위키백과](https://ko.wikipedia.org/wiki/Log4j)**

<br>
해당 버그는 2021년 11월 24일, 알리바바 클라우드 보안팀의 Chen Zhaojun가 발견했다.

그리고 얼마 있지 않아 세계적인 온라인 게임 '마인크래프트'의 기술 책임자가 본인 트위터를 통해 "마인크래프트에 영향을 미치는 중요한 보안 문제가 발견되어 수정하였다."고 발표를 하면서 마인크래프트는 시작일 뿐이라는 것을 알게했다.

해당 취약점 이슈가 이 정도로 큰 문제가 되는 주된 이유는 "서버에 로그인한 것 만으로 해커가 사용자의 컴퓨터를 사실상 원격 조종할 수 있는 것 이기 때문이다.

그래도 빠르게 해결방법이 제시되어 큰 피해를 줄일 수 있다는게 참 다행이다👍

그럼 이제 기존에 사용중이던 Log4j 버전 별로 해결방법을 확인해 보자.

사실 복잡할 게 없는 방법이라 아래 보호나라의 **[공지사항](https://www.boho.or.kr/data/secNoticeView.do?bulletin_writing_sequence=36389)**을 참조하면 될 것같다.

그리고 오래된 레거시로 계속 이어가며 사용중인 상황이라면 가급적 이번 기회에 마이그레이션(**[마이그레이션 방법 - 링크](https://coding-plant.tistory.com/59))**하는걸 추천한다.

오래된 버전은 아파치에서 지원도 끝나고 시간이 지나면 또 다른 보안 취약점에 노출될 확률이 높기 때문이다.

![](https://velog.velcdn.com/images/clothes/post/39f7bd84-6339-4278-8767-959639bda40a/image.png)