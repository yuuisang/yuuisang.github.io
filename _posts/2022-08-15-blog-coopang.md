---
layout: post
title: "[Blog] 스토리에 쿠팡파트너스 배너 넣기"
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

![](https://velog.velcdn.com/images/clothes/post/7cc68377-d04a-4353-b93e-6a9a28158792/image.png)

여기서 **가입하는 과정**부터 보자면

### 2-1. 쿠팡 파트너스 회원가입

![](https://velog.velcdn.com/images/clothes/post/763babd5-6a9b-47ea-a633-cbbfed9efedb/image.png)


![](https://velog.velcdn.com/images/clothes/post/04d7e31f-4a17-4701-99e7-01d66e8cebd6/image.png)


**추천인 ID**

```
AF6600364
```

![](https://velog.velcdn.com/images/clothes/post/f095efe4-810d-4117-aa32-ccf40b169ada/image.png)

![](https://velog.velcdn.com/images/clothes/post/7ba1c609-a3af-4917-bb5d-8a9c403eabdd/image.png)


## 3. 쿠팡 파트너스 로그인 후 #링크 생성

![](https://velog.velcdn.com/images/clothes/post/6915a038-8a42-4e6f-941f-4e7c21a19633/image.png)


## 4. 배너 만들기

![](https://velog.velcdn.com/images/clothes/post/0797df33-01e5-4eca-b568-6e2671b4d6c6/image.png)

설정값은 마음대로 해도 괜찮고, 크기는 **본인 블로그에 이 배너가 들어갈 공간의 크기**에 맞게 설정해주면 된다.

참고로 잘못설정해도 추후에 얼마든지 변경하거나 다시 만들 수 있으니 걱정할 필요는 없다.

---

우선 여기까지 하면 쿠팡 파트너스에서 작업할 것은 끝난다.

이 뒤 부터는 **티스토리**라는 플랫폼에 적용하는 방법이다.

이건 개개인마다 코드 구성이 다르기 때문에 차이가 있을 수 있지만, 최대한 공통적인 부분 위주로 작성하려고 한다.

## 5. 티스토리 스킨 편집에 생성한 쿠팡파트너스 배너 추가

![](https://velog.velcdn.com/images/clothes/post/07d12ddc-2c70-4061-a113-8cfa9079a501/image.png)


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

위 캡처에서 **"id": 591916** 이랑 **"trackingCode": "AF6600364"** 그리고 **'iframe\[id^="591916"\]'** 이렇게 총 3 부분이 나의 쿠팡파트너스 고유 식별 정보를 담고 있는 부분이다.

캡처와 별도로 코드도 적어두었으니 잘 모르겠다면 코드를 전부복사해서 원하는 위치에 붙여넣기 한 후

저 3 부분의 숫자만 본인의 값으로 변경해서 사용하면 된다.

## 6. 결과물

![](https://velog.velcdn.com/images/clothes/post/26bf6f1e-5ffd-4a74-b50d-3acd86914bee/image.png)

