---
layout: post
title: "[Blog] Github 블로그 검색엔진에 등록 (구글/네이버/다음)"
date: 2022-08-15 15:12:09 +0600
categories: [Blog]
author: EuiSangYu
post_image: "/assets/images/blog-img1.jpg"
---

기존에 운영하던 [티스토리 블로그](https://coding-plant.tistory.com/)에서 GitHub 블로그로 이전해 본격적으로 사용하기 위해 검색엔진에 등록을 하기로 했다.

우선 우리나라에서 검색량이 많은 구글, 네이버, 다음에 등록을 해보려 한다. 각 포털사이트별로 검색엔진에 등록방법을 구글링을 해본 결과들을 정리해보려고 한다.


## sitemap.xml 생성하기
우선 검색엔진에서 GitHub 블로그의 글들을 긁어올 수 있도록, 사이트의 모든 페이지 정보를 모아두는 **sitemap.xml** 이 필요하다.

포스팅을 업로드 할 때마다 매번 추가해주는 건 너무 노가다일테니 한번에 세팅해서 넣어주도록 하자.

[사이트맵 코드 링크 이동](https://github.com/yuuisang/yuuisang.github.io/blob/main/sitemap.xml)


위 링크의 코드를 복사해서 루트 디렉토리에 sitemap.xml 파일을 만들고 **깃에 push** 하면 된다.

업로드 후, https://본인블로그주소/sitemap.xml 에 접속해서 내 블로그의 모든 페이지 주소를 정상적으로 출력하는지 확인되면 끝!

예시)
![](https://velog.velcdn.com/images/clothes/post/edec5f22-4387-4079-9e1d-70766387e789/image.png)

## robots.txt 생성하기
내 사이트를 검색엔진에 등록하면 구글 검색 엔진의 크롤러가 내 사이트에 방문하여 정보를 가져간다.

이 때, 크롤러가 방문했을 때 참고할 수 있는 정책을 명시해주면 좋다.

```
User-agent: *
Allow: /
Sitemap: https://yuuisang.github.io/sitemap.xml
```

위 코드를 복붙해서 robots.xml 파일을 만들고, 루트디렉토리에 추가하면 됨.
참고로 깃허브 주소는 본인껄로 변경해야함!

## feed.xml 생성하기
이건 필수는 아닌데 RSS Feed로도 등록될 수 있도록 feed.xml 까지 만들어본다.

[feed.xml 코드 링크 이동](https://github.com/yuuisang/yuuisang.github.io/blob/main/feed.xml)


위 링크내의 코드를 복사해서 feed.xml 파일을 만들고 **루트디렉토리**에 추가

<br><br>
여기까지 등록 전 준비단계는 전부 끝났다.
이제  각 포털사이트에 등록하러 가보자!

---

## 구글서치콘솔 등록
1. [구글 웹마스터 도구](https://search.google.com/search-console?resource_id=https%3A%2F%2Fyuuisang.github.io%2F&hl=ko) 접속 -> **URL 접두어** 탭으로 이동 -> 등록하고자하는 사이트의 **URL 입력** -> 계속 버튼 클릭
![](https://velog.velcdn.com/images/clothes/post/320966ba-3dd2-428a-bd3d-613beece8e76/image.png)

2. 본인의 url을 등록해야 한다. 방법은 여러가지 있는데 HTML 파일을 직접 저장시키는게 가장 권장사항이다.
![](https://velog.velcdn.com/images/clothes/post/e6af0472-c90e-4fdb-871f-7987232d41bb/image.png)

3. 이 파일을 깃허브 디렉토리 내 루트에 저장!
![](https://velog.velcdn.com/images/clothes/post/36fab3e7-4c76-493a-8af0-a9a4059e4045/image.png)
![](https://velog.velcdn.com/images/clothes/post/23168394-fd67-4dad-ab40-ca0cc92a6570/image.png)

4. 여기까지 됐으면 좌측 메뉴에서 Sitemaps 을 클릭 -> 새 사이트맵 추가 에 https://본인깃허브주소/sitemap.xml 을 입력 -> 제출 버튼 클릭
![](https://velog.velcdn.com/images/clothes/post/ee322542-062a-40f3-9f54-7b28d1b13a11/image.png)

5. 위 이미지처럼 뜨면 성공이다.

<br>

여기까지 구글서치콘솔 작업은 끝! 다음은 네이버...!

---
## 네이버 서치어드바이저
1. [네이버 서치어드바이저](https://searchadvisor.naver.com/) 에 접속.
2. **웹 마스터 도구** -> **사이트 관리** -> **사이트 등록 페이지**로 이동한다.
![](https://velog.velcdn.com/images/clothes/post/af4058e3-d1c9-43e5-907a-cb5d0e9e3e0f/image.png)
3. URL을 입력한다.
4. **사이트 소유확인 페이지**에서 **HTML 파일 업로드** 를 선택한다.
![](https://velog.velcdn.com/images/clothes/post/e0f2bbaf-2e81-4f27-a5a1-548fcabc4e97/image.png)

5. **HTML 확인 파일** 을 클릭하여 다운로드 한다.
6. 등록하고자하는 깃허브의 루트 디렉토리에 해당 파일을 업로드한다.
7. 가이드 되어있는 링크를 클릭하여 제대로 업로드 되었는지 확인한다.
8. **소유확인 버튼**을 누른 후 아래와 같은 팝업이 뜨는지 확인한다.
![](https://velog.velcdn.com/images/clothes/post/d04a0e7c-fb32-45ff-9e97-e4a90524ecb0/image.png)

> HTML 확인파일을 찾을수 없거나, 네이버 검색로봇 사이트 서버에 접근할 수 없습니다.

9. 이런 문구가 뜬다면 하루 정도 기다렸다가 다시 진행해보면 되는 경우가 많다.

10. 정상적으로 마무리가 되었다면 목록에 이렇게 뜬다.
![](https://velog.velcdn.com/images/clothes/post/4ead899e-797a-4e0c-88c7-cda22e1a3ff5/image.png)

---

1. 이제 **사이트맵** 을 제출해 보자!
(구글과 동일하게 제출만 하면 된다.)
2. 등록된 블로그 링크를 클릭하여 **사이트 관리** 페이지로 들어간다.
3. **요청** -> **사이트맵 제출** 메뉴로 들어간다.
4. 아까 만들어서 내 깃허브에 업로드했던 **sitemap.xml** 의 주소를 다음과 같이 입력하고 **확인** 버튼을 누른다.
![](https://velog.velcdn.com/images/clothes/post/6beef945-de63-4233-9c82-ebeaca11d157/image.png)
5. 잘 되었는지 확인해 본다.

---

## 다음 
1. [다음 검색등록](https://register.search.daum.net/index.daum) 에 접속한다.
2. **블로그 등록** 을 클릭하고 **블로그 URL**을 넣고 **확인** 을 클릭하면 끝!
![](https://velog.velcdn.com/images/clothes/post/b855b968-14e9-4771-94c8-98364c2d2d2d/image.png)
![](https://velog.velcdn.com/images/clothes/post/75cd176c-3270-4cd2-a806-157e0b0dff77/image.png)
![](https://velog.velcdn.com/images/clothes/post/cc480d45-224a-4f44-bafd-ddced1131394/image.png)

<br>
앞서 두 구글,네이버 사이트에 비해 엄청 간단하다.

---

## SEO 검색 엔진 최적화
https://tech.songyunseop.com/post/2016/09/seo-for-blog/

이분 포스트를 보면서 차차 진행해 볼 예정이다.


