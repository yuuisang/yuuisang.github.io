---
layout: post
title: "[Network] HTTP(HyperText Transfer Protocol) 개념 정리"
date: 2022-08-15 15:12:09 +0600
categories: [Network]
author: EuiSangYu
post_image: "/assets/images/network/http.png"
---

## HTTP란

HTTP(Hypertext Transfer Protocol)하이퍼텍스트 전송 규약. 웹 브라우저(web browser) 같은 응용프로그램을 통해 웹 클라이언트(사용자)와 웹 서버(서비스 제공자) 사이 데이터를 전송하는 프로토콜이다. 인터넷 통신을 위해 사용 되는 Protocol이며, HTML뿐만 아니라, 각종 이미지, 동영상, 음성 데이터 전송이 가능하다. 웹 서버와 사용자 컴퓨터에 설치된 웹 브라우저 사이에 문서를 전송하기 위한 `통신 규약`이다.

## HTTP의 특징

-   HTTP 클라이언트와 HTTP 서버에 의해서 해석이 된다.
-   TCP/IP를 이용하는 응용 프로토콜(application protocol)이다.
-   연결 상태를 유지하지 않는 비연결성 프로토콜이다.
-   요청/응답(Request/Response) 방식으로 동작한다.
-   HTTP는 기본 포트인 `80번 포트`에서 서비스 대기한다.

연결 상태를 유지하지 않기 때문에 정보를 저장하기 위한 수단으로 `쿠키(Cookie)`와 `세션(Session)`이 등장했다.

## HTTP의 통신 과정

![image](https://user-images.githubusercontent.com/58925978/187123035-51c524f7-c960-46e4-b960-e81834faa180.png)


클라이언트(사용자)가 서버에 `HTTP Request (요청) 전송`  
서버가 사용자의 요청을 받고 `HTTP Response (응답) 회신`

클라이언트의 요청이 없으면 응답하지 않는게 기본 상태이다.

## HTTP 상태 코드

상태 코드는  IETF (Internet Engineering Task Force)에서 정의한 인터넷 표준에 따라 개발되며, 총 5가지 클래스로 분류된다.

1.  `1xx`: Informational - 요청 정보 처리 중
2.  `2xx`: Success - 요청을 정상적으로 처리함
3.  `3xx`: Redirection - 요청을 완료하기 위해 추가 동작 필요
4.  `4xx`: Client Error - 서버가 요청을 이해하지 못함
5.  `5xx`: Server Error - 서버가 요청 처리 실패함

### 1xx: Informational 정보

서버가 요청을 클라이언트에서 성공적으로 수신했으며 서버 끝에서 처리 중이라는 정보를 나타낸다. 서버의 임시 응답이며 일반적으로 상태 줄과 선택적 헤더 만 포함하며 빈 줄로 끝난다. 현재는 거의 사용하지 않는다.

### 2xx: Success 성공

서버가 요청을 받고 성공적으로 처리되었음을 나타낸다.

### 3xx: Redirection 리디렉션

브라우저는 자동으로 다른 URL로 리디렉션되므로 브라우저 창에는이 코드가 표시되지 않지만, 이미지 파일처럼 캐싱된 파일을 새로고침 후 확인하면 3xx 코드를 확인할 수 있다.

### 4xx: Client Error 클라이언트 오류

서버가 해결할 수 없는 클라이언트 측 에러 코드다. 주로 클라이언트(사용자)가 서버에 잘못된 요청을 했을 경우 발생한다.

### 5xx: Server Error 서버 오류

서버가 클라이언트의 요청을 처리하지 못했을 때 발생한다. 서버는 보안 상 통신하지 않는 것이 가장 좋으므로 대부분의 에러 코드를 500 Error로 처리한다.

## HTTP 응답 코드(자세히)

| 100 | Continue (클라이언트로 부터 일부 요청을 받았으며 나머지 정보를 계속 요청함) |
| --- | --- |
| 101 | Switching protocols |
| 200 | OK(요청이 성공적으로 수행되었음) |
| 201 | Created (PUT 메소드에 의해 원격지 서버에 파일 생성됨) |
| 202 | Accepted(웹 서버가 명령 수신함) |
| 203 | Non-authoritative information (서버가 클라이언트 요구 중 일부만 전송) |
| 204 | No content, (사용자 요구 처리하였으나 전송할 데이터가 없음) |
| 301 | Moved permanently (요구한 데이터를 변경된 타 URL에 요청함) |
| 302 | Not temporarily |
| 304 | Not modified (컴퓨터 로컬의 캐시 정보를 이용함, 대개 gif 등은 웹 서버에 요청하지 않음) |
| 400 | Bad request (사용자의 잘못된 요청을 처리할 수 없음) |
| 401 | Unauthorized (인증이 필요한 페이지를 요청한 경우) |
| 402 | Payment required(예약됨) |
| 403 | Forbidden (접근 금지, 디렉터리 리스팅 요청 및 관리자 페이지 접근 등을 차단) |
| 404 | Not found, (요청한 페이지 없음) |
| 405 | Method not allowed (혀용되지 않는 http method 사용함) |
| 407 | Proxy authentication required (프락시 인증 요구됨) |
| 408 | Request timeout (요청 시간 초과) |
| 410 | Gone (영구적으로 사용 금지) |
| 412 | Precondition failed (전체 조건 실패) |
| 414 | Request-URI too long (요청 URL 길이가 긴 경우임) |
| 500 | Internal server error (내부 서버 오류) |
| 501 | Not implemented (웹 서버가 처리할 수 없음) |
| 503 | Service unnailable (서비스 제공 불가) |
| 504 | Gateway timeout (게이트웨이 시간 초과) |
| 505 | HTTP version not supported (해당 http 버전 지원되지 않음) |

## HTTP Method

### GET

GET 요청 방식은 URI(URL)가 가진 정보를 검색하기 위해 서버 측에 요청하는 형태

### POST

POST 요청 방식은 요청 URI(URL)에 폼 입력을 처리하기 위해 구성한 서버 측 스크립트(ASP, PHP, JSP 등) 혹은 CGI 프로그램으로 구성되고 Form Action과 함께 전송되는데, 이때 헤더 정보에 포함되지 않고 데이터 부분에 요청 정보가 들어가게 된다. 

### PUT

POST와 유사한 전송 구조를 가지기 때문에 헤더 이외에 메시지(데이터)가 함께 전송된다.원격지 서버에 지정한 콘텐츠를 저장하기 위해 사용되며 홈페이지 변조에 많이 악용되고 있다.

### DELETE

원격지 웹 서버에 파일을 삭제하기 위해 사용되며 PUT과는 반대 개념의 메소드

### PATCH

부분적인 수정을 위해 사용

### TRACE

원격지 서버에 Loopback(루프백) 메시지를 호출하기 위해 사용된다. 

### HEAD

HEAD 요청 방식은 GET과 유사한 방식이나 웹 서버에서 헤더 정보 이외에는 어떤 데이터도 보내지 않는다.웹 서버의 다운 여부 점검(Health Check)이나 웹 서버 정보(버전 등)등을 얻기 위해 사용될 수 있다. 

### OPTIONS

해당 메소드를 통해 시스템에서 지원되는 메소드 종류를 확인 가능

### CONNECT

웹 서버에 프락시 기능을 요청할 때 사용된다.