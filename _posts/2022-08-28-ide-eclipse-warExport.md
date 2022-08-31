---
layout: post
title: "[IDE] 이클립스 War Export 추출 시 오류 Module name is invalid"
date: 2022-08-28 22:00:00 +0600
toc: true
toc_sticky: true
categories: [IDE]
author: EuiSangYu
post_image: "/assets/images/ide/warExportError.png"
---

회사에서 업무중 배포할 일이 있어 war 파일을 추출하려는데 갑자기 이상한 에러가나서 당황스러웠다.

다행히 쉽게 해결할 수 있는 환경설정 문제였어서 나중에 까먹을까봐 정리해둔다.

## WAR 파일 Export 시도
![image](https://user-images.githubusercontent.com/58925978/187122183-7f1a0d01-eab9-4b26-a2a5-a3063ab16aed.png)

## Module name is invalid 에러 발생
![image](https://user-images.githubusercontent.com/58925978/187122203-716c385d-ebb2-4e85-a1bd-68677136481f.png)

## 프로젝트 설정 변경
1. `Properties` 진입
![image](https://user-images.githubusercontent.com/58925978/187122219-28b3c495-3ca8-4c63-9636-5775a243186e.png)

2. `Project Facets` -> `Dynamic Web Module` 체크 후 Apply
![image](https://user-images.githubusercontent.com/58925978/187122242-193bb942-ba48-4dd1-bf1d-b2f22e7b4765.png)

3. 적용 중 모습
![image](https://user-images.githubusercontent.com/58925978/187122257-8503a968-df33-4905-834c-ef19a1844193.png)

4. 완료 후 다시 Export 시도
![image](https://user-images.githubusercontent.com/58925978/187122283-f75040f3-bf02-4cb6-b669-26597164cc70.png)

5. 정상적으로 추출 완료!
![image](https://user-images.githubusercontent.com/58925978/187122296-78b4ac1f-3e39-4945-ba56-f65437305599.png)


## 마무리
생각보다 간단하게 해결할 수 있는 문제였다.

