---
layout: post
title: "[개발] 이클립스 War Export 추출 시 오류 Module name is invalid"
date: 2022-08-28 22:00:00 +0600
toc: true
toc_sticky: true
categories: [Dev]
author: EuiSangYu
post_image: "/assets/images/dev/warExport.png"
---

회사에서 업무중 배포할 일이 있어 war 파일을 추출하려는데 갑자기 이상한 에러가나서 당황스러웠다.

다행히 쉽게 해결할 수 있는 환경설정 문제였어서 나중에 까먹을까봐 정리해둔다.

## WAR 파일 Export 시도
![](https://velog.velcdn.com/images/clothes/post/df89a088-2624-40af-8122-636292e16425/image.png)

## Module name is invalid 에러 발생
![](https://velog.velcdn.com/images/clothes/post/dfaec65c-3696-4074-9d98-8c639e1c701a/image.png)

## 프로젝트 설정 변경
1. `Properties` 진입
![](https://velog.velcdn.com/images/clothes/post/596a4d64-ff75-4fb3-9e7f-d6ca74266746/image.png)

2. `Project Facets` -> `Dynamic Web Module` 체크 후 Apply
![](https://velog.velcdn.com/images/clothes/post/80fe4cef-359f-47bf-82b5-ca9f8b089582/image.png)

3. 적용 중 모습
![](https://velog.velcdn.com/images/clothes/post/1ca45095-5d00-4448-baef-1962fce78d8f/image.png)

4. 완료 후 다시 Export 시도
![](https://velog.velcdn.com/images/clothes/post/282bf160-ef1f-44a0-9b92-abf418f126fd/image.png)

5. 정상적으로 추출 완료!
![](https://velog.velcdn.com/images/clothes/post/67979120-af04-4baf-83b7-7047c82c9ee0/image.png)


## 마무리
생각보다 간단하게 해결할 수 있는 문제였다.

