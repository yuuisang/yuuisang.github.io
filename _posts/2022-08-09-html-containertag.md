---
title:  "[HTML] 컨테이너 태그(div, span) - 시멘틱 구조"
layout: post
author: EuiSang Yu
categories: HTML
tags: [HTML]
---

콘텐츠나 레이아웃에 아무런 영향도 주지 않고, 여러 요소들을 하나로 묶어 관리하기 편하게하는 태그를 <code>컨테이너 태그</code>라고 한다. 콘텐츠 내용을 구분하거나, 특정 영역마다 공통적인 스타일(css)를 적용하고자 할 때 개발자는 컨테이너태그를 사용하는 것이 좋다.

컨테이너 역할을 담당하는 태그는 크게 <code>시멘틱(Semantic) 태그</code>와 <code>논-시멘틱(non-Semantic) 태그</code>로 나뉜다.

## 시멘틱(Semantic) 태그

![](https://velog.velcdn.com/images/clothes/post/47f0293b-02ac-4190-a84d-91fb5752f5ca/image.png)

시멘틱 태그란 브라우저, 개발자와 사용자에게 태그에 종속되어있는 내용을 직설적으로 알려주는 태그이다.

태그의 종류로는 header, nav, section, article, aside, footer 가 있다.

-   **header** : 전체 사이트의 헤더, article에 관련된 헤더이다.
-   **nav** : 로그인, 목차 네비게이터 등으로 사용된다.
-   **section** : 뉴스헤드라인, 컨텐츠 분류, 본문바디에서 구간을 나눌 때, 본문안에서 본문끼리의 그룹을 지을 때 사용
-   **article** : 페이지의 주요 내용정보를 담을 때 사용
-   **aside** : 분몬 내용을 서포트 할 때 사용, aside가 어디에 포함되냐에 따라 사용 용도가 다르다.
-   **article 내 aside :** article에 종속되어있는 내용을 서포트해주는 정보를 담을 때 사용, 사용검색엔진이 스캐닝을 할때 article에 관련된 aside인지 알수있다.
-   **외부 aside :** 사이트 전체의 해당 되는 내용을 서포트 할 수 잇는 정보를 담은 aside, 간단한 네비 넣을 수 있음
-   **footer** : 회사소개, 저작권 약관등의 정보를 넣음

## 논-시멘틱(non-Semantic) 태그

아무런 의미가 부여되지 않는 태그이다. 스타일(css)을 주거나, 서버에서 데이터를 받아서 그룹형 컨테이너(혹은 모듈)로 manipulate를 해야할 때 컨테이너형 태그를 사용한다. 논 시멘틱 태그는 div 와 span 이 있다.

-   div /div
-   span /span

## div 와 span 비교

### div

-   박스 형태로 영역이 설정되고 그 안에 정렬된다.
-   width, height 크기 지정이 가능함.
-   자동으로 줄바꿈이 된다.
-   margin 속성이 4방향 모두 적용이 되며 위 아래 겹쳐지는 여백은 상쇄된다. 즉 여백의 크기가 더해서 2배가 되는 것이 아니라 겹쳐지는 것.

### span

-   span 은 줄 단위로 영역이 설정된다.
-   inline 속성을 가지기 때문에 width 와 height 를 속성값으로 정해 줄 수 없다.
-   줄바꿈이 되지 않고 옆으로 나열된다.
-   margin 속성이 양 옆으로만 적용되며 겹쳐지지 않는다. 가시적으로 더 넓어 보임.