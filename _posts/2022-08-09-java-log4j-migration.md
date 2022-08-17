---
layout: post
title: "[Java] log4j Migration - Maven,Gradle 없이 순수 jar 파일로 마이그레이션하는 방법"
date: 2022-08-09 15:12:09 +0600
categories: [JAVA]
author: EuiSangYu
post_image: "/assets/images/java/java.png"
---

우선 여러가지 방법이 있지만 회사에서 내가 적용에 성공한 방법을 토대로 작성

---

우리 부서는 솔루션 설치 시 고객사의 외부망 관련 보안 문제 때문에 Maven이나 Gradle 같은 외부 빌드를 이용하지 않고, jar 파일로 로컬에서 직접 관리하는 방식으로 업무를 진행한다.

사실 기존에 프로젝트들이 `자바7` 버전 베이스라 Log4j `1.2.16` 버전을 사용하고 있었기에 이번 보안 이슈 취약점 대상에선 제외되었지만, 이번 기회에 최신버전으로 마이그레이션 하자는 의견이 나와 진행하게 되었다.

내가 선택한 마이그레이션 버전은 `2.12.3` 버전이다.

-   Java 7을 사용하는 몇몇 프로젝트가 있기 때문에 Java 7을 지원하는 보안 취약점 문제가 해결 된 가장 최신 버전이기 때문
-   `[2.12.3 버전 jar 다운로드](https://logging.apache.org/log4j/2.x/download.html)`

![](https://velog.velcdn.com/images/clothes/post/507e9c58-0f59-450c-a175-228894f74810/image.png)

~~참고로 회사 코드는 노출시킬 수 없으므로 log4j -> log4j2 로 변경했을 시 log 객체의 메소드 파라미터 타입이 변경되는 점은 눈치껏 알아서 수정해야 함.~~

## 기존 프로젝트에서 WebContent/WEB-INF/lib 디렉토리에서 다음 항목들을 제거

![](https://velog.velcdn.com/images/clothes/post/4dbb0266-81c1-4248-98d1-16d657b7eb1b/image.png)

## 기존 log4j.xml 파일을 제거하고 다른 경로에 log4j2.xml 파일을 추가

-   기존의 log4j.xml 파일은 src 바로 하위 경로에 위치하고 있지만 log4j2.xml 파일은 WebContent/WEB-INF 하위에 classes 라는 디렉토리를 생성해서 그 안에 추가하면 된다.

![](https://velog.velcdn.com/images/clothes/post/b8793475-6ca7-45ec-a958-4daa44e2931f/image.png)

![](https://velog.velcdn.com/images/clothes/post/bf126040-1504-4d91-a186-0101a01083bc/image.png)

## log4j2.xml 예시


코드 구성 방법은 `[https://coding-plant.tistory.com/78](https://coding-plant.tistory.com/78 "링크")` 참조


## 새로운 버전의 jar 파일들 추가

> 2022.01.17 기준 추가 취약점 발견으로 인해 `2.12.4` 버전으로 첨부 파일 수정

![](https://velog.velcdn.com/images/clothes/post/fa57e8ba-b8ac-4a21-87c0-c35d4bbcfd7e/image.png)

## 코드 변경 사항

```java
// 변경 전
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;

//변경 후
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

---------------------------------------------------------------------

//변경 전
//변수이름과 (“??”)안의 클래스명은 기존 코드에 맞게 알아서 수정
protected static final Log log = LogFactory.getLog(“??”)

//변경 후
protected static final Logger log = LoggerFactory.getLogger(“??”)
```

---

추가로 JAVA8 버전 이상을 지원하는 경우엔 어떡하지? 라는 생각에 2.17.0 버전도 한번 시도해봤다.

JAVA8 프로젝트에 Log4j 1.2.16 으로 세팅되어있는 프로젝트에 진행해봤는데 위에 2.12.3 을 진행했던 방법과 정확히 동일하게해서 문제없이 동작되는걸 확인했다.

차이점이 있다면

![](https://velog.velcdn.com/images/clothes/post/1e79273a-df90-4b96-9c6b-1992a4f64d70/image.png)

사실 차이점까지는 아니고 혹시나 2.12.3 과 동일한 방법으로 진행했는데 에러가 난다면

해당 이클립스의 `Preferences - Java - Installed JREs` 설정에서 제대로 버전이 일치하는지 확인해보면 좋을 것 같다.
