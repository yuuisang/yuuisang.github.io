---
layout: post
title: "[Blog] 티스토리에 쿠팡파트너스 배너 넣기"
date: 2022-08-15 15:12:09 +0600
categories: [Blog]
author: EuiSangYu
post_image: "/assets/images/blog/coopang.png"
---

평화로운 일요일 점심... 티스토리 블로그를 운영한지 반년이 넘어가는데 구글 애드센스만 등록하고 아직 쿠팡파트너스를 등록하지 못했다는걸 깨닫고 급하게 등록하고 블로그에 적용하는 것까지 성공했다!

특별히 어려운 부분은 없고, 마지막에 티스토리 블로그 스킨 편집에서 코드로 넣어야하는 부분이 비 개발자들에게는 조금 어려울 수 있다고 생각하기 때문에 설명과 함께 정리해두려고 한다.

## 1. 쿠팡 파트너스 사이트에 접속

쿠팡 파트너스(쿠팡 계정과 별도) 가입이 필요.

[https://partners.coupang.com/](https://partners.coupang.com/)


## 2. 쿠팡 파트너스 로그인

![image](https://user-images.githubusercontent.com/58925978/187123088-2b2b6d1f-19e3-4531-b969-7199d3ab62fe.png)

여기서 `가입하는 과정`부터 보자면

### 2-1. 쿠팡 파트너스 회원가입

![image](https://user-images.githubusercontent.com/58925978/187123115-36759eba-c92d-4153-a472-1a816978af02.png)


![image](https://user-images.githubusercontent.com/58925978/187123134-66e2b075-5849-4d5f-bc13-daa5cb6832be.png)


`추천인 ID`

```
AF6600364
```

![image](https://user-images.githubusercontent.com/58925978/187123155-9d20c4c2-30ec-406c-b731-98b3e523340f.png)

![image](https://user-images.githubusercontent.com/58925978/187123176-f8c3728f-7dc1-4452-8145-f24641cca1fe.png)


## 3. 쿠팡 파트너스 로그인 후 #링크 생성

![image](https://user-images.githubusercontent.com/58925978/187123193-023b911d-a796-4556-b6bf-c75b0332ac04.png)


## 4. 배너 만들기

![image](https://user-images.githubusercontent.com/58925978/187123216-01ed5b7a-e117-4a19-942c-ad4dcfa60bc9.png)

설정값은 마음대로 해도 괜찮고, 크기는 `본인 블로그에 이 배너가 들어갈 공간의 크기`에 맞게 설정해주면 된다.

참고로 잘못설정해도 추후에 얼마든지 변경하거나 다시 만들 수 있으니 걱정할 필요는 없다.

---

우선 여기까지 하면 쿠팡 파트너스에서 작업할 것은 끝난다.

이 뒤 부터는 `티스토리`라는 플랫폼에 적용하는 방법이다.

이건 개개인마다 코드 구성이 다르기 때문에 차이가 있을 수 있지만, 최대한 공통적인 부분 위주로 작성하려고 한다.

## 5. 티스토리 스킨 편집에 생성한 쿠팡파트너스 배너 추가

![image](https://user-images.githubusercontent.com/58925978/187123242-3331732d-62cb-4c75-8d05-9be0b6566d31.png)


```html
<div class="searchP-ad-container flex" style="border-top: 3px solid #e5e5e5;height:150px">
    <div class="searchP-ad position-relative width-100">
      <!-- 검색바 하단 광고 -->
      <script src="https://ads-partners.coupang.com/g.js"></script>
      <script>
        new PartnersCoupang.G({
          "id":591916,
          "template":"carousel",
          "trackingCode":"AF6600364",
          "width":"99%",
          "height":"150"
        });
        try {
          setTimeout(function() {
            var iframeNode = document.querySelector('iframe[id^="591916"]');
            document.querySelector('.searchP-ad').appendChild(iframeNode);
          }, 1000);
        } catch (e) {
          console.error(e);
        }
      </script>
    </div>
</div>
<span class="coupang-notice">이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.</span>
```

개발자들은 아마 쉽게 바로 사용할 수 있겠지만, 비 개발자들은 조금 난해할 수 있으니 설명하자면

위 캡처에서 `"id": 591916` 이랑 `"trackingCode": "AF6600364"` 그리고 `'iframe\[id^="591916"\]'` 이렇게 총 3 부분이 나의 쿠팡파트너스 고유 식별 정보를 담고 있는 부분이다.

캡처와 별도로 코드도 적어두었으니 잘 모르겠다면 코드를 전부복사해서 원하는 위치에 붙여넣기 한 후

저 3 부분의 숫자만 본인의 값으로 변경해서 사용하면 된다.

## 6. 결과물

![image](https://user-images.githubusercontent.com/58925978/187123258-b1ae1fb3-c5df-4920-9a08-089519e58c85.png)

