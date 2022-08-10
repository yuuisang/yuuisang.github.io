---
layout: post
title:  "[블로그] 티스토리 업비트 실시간 가격 띄우기"
categories: [ 티스토리 ]
image: assets/images/blog/upbit.png
---

코인 매매와 공부하는 걸 좋아하다보니 내 블로그에도 업비트의 실시간 가격이 떴으면 좋겠다는 생각이 들었다.

궁금해서 찾다보니 [참고할만한 블로그(꾸생님)](https://juni-official.tistory.com/)가 있어서 신기하기도하고 공부하는 목적도 겸해서 적용해보았다.

필요한 사람에게 도움이 되길 바라며 정리해본다.

## 결과물

![](https://velog.velcdn.com/images/clothes/post/70e1ae13-c1a4-495d-9a67-4a5d79a4f00c/image.png)


## HTML 코드

```
<div class="price-wrap">
  <div class="slide-wrap">
    <span class="item-BTC">
      <i class="bx bxl-bitcoin"></i>
      <span class="ticker-price-rise">33,415,000</span>
    </span>
    <span class="item-ETH">
      <!--<span class="ticker-txt">ETH : </span>-->
      <i class="bx bxl-ethereum"></i>
      <span class="ticker-price-rise">1,769,500</span>
    </span>
    <span class="item-ADA">
      <!--<span class="ticker-txt">ADA : </span>-->
      <i class="bx bxl-ada"></i>
      <span class="ticker-price-rise">500</span>
    </span>
  </div>
  <script>
    var slideBar = document.querySelector(".slide-wrap");
    setInterval(function() {
      var upbit = "https://api.upbit.com/v1/ticker?markets=";
      var crypto = "KRW-BTC,KRW-ETH,KRW-ADA";
      axios.get(upbit + crypto).then(function(res) {
        var data = res.data;
        res.data.forEach(function(el, idx) {
          var pirceBar = el.market.substr(4, 4) === "BTC" ? "<span class=\"ticker-txt\"><i class='bx bxl-bitcoin bx-xs'></i></span><span class=\"ticker-price-rise\">".concat(el.trade_price.toLocaleString(), "</span>") : "<span class=\"ticker-txt\">".concat(el.market.substr(4, 4), " :</span><span class=\"ticker-price-rise\">").concat(el.trade_price.toLocaleString(), "</span>");
          if (el.change === "RISE") {
            slideBar.children[idx].innerHTML = pirceBar;
          } else if (el.change === "FALL") {
            slideBar.children[idx].innerHTML = pirceBar;
          } else {
            slideBar.children[idx].innerHTML = pirceBar;
          }
        });
      })["catch"](function(err) {
        console.log(err);
      });
    }, 1200);
  </script>
</div>
```

스크립트 부분이 코드가 길지 않아 따로 **분리하지 않고** 해당 엘리먼트 안에 작성했다.

밑에 Javascript 코드 영역은 따로 기술해 두었다.

## Javascript 코드

```
<script>
    var slideBar = document.querySelector(".slide-wrap");
    setInterval(function() {
      var upbit = "https://api.upbit.com/v1/ticker?markets=";
      var crypto = "KRW-BTC,KRW-ETH,KRW-ADA";
      axios.get(upbit + crypto).then(function(res) {
        var data = res.data;
        res.data.forEach(function(el, idx) {
          var pirceBar = el.market.substr(4, 4) === "BTC" ? "<span class=\"ticker-txt\"><i class='bx bxl-bitcoin bx-xs'></i></span><span class=\"ticker-price-rise\">".concat(el.trade_price.toLocaleString(), "</span>") : "<span class=\"ticker-txt\">".concat(el.market.substr(4, 4), " :</span><span class=\"ticker-price-rise\">").concat(el.trade_price.toLocaleString(), "</span>");
          if (el.change === "RISE") {
            slideBar.children[idx].innerHTML = pirceBar;
          } else if (el.change === "FALL") {
            slideBar.children[idx].innerHTML = pirceBar;
          } else {
            slideBar.children[idx].innerHTML = pirceBar;
          }
        });
      })["catch"](function(err) {
        console.log(err);
      });
    }, 1200);
</script>
```

나는 현재 에이다만 분할로 매수하는 중이기 때문에 **비트코인**, **이더리움**, **에이다** 총 3개의 코인의 가격만 실시간으로 받아오고자 스크립트를 구성했다.

## CSS 코드

```
/* 업비트 API */
@media (min-width: 992px) {
  .price-wrap {
    height: 35px;
    /*background: #f8f8f8 url(images/bg.svg);*/
  }
}

.price-wrap {
  position: sticky;
  top: -15px;
  display: inline-block;
  padding: 0;
  margin: 35px 15px 0 15px;
  box-sizing: border-box;
  width: 280px;
  background-color: #161a1e;
  /*box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 2px 6px 2px;*/
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  overflow: hidden;
  z-index: 9998;
  font-size: 1.0rem !important;
  color: #fff !important;
  border: 0 solid #d0d0d0;
  background: #f1f1f191;
  border-radius: 10px;
  box-shadow: 0 1px 10px rgb(0 0 0 / 18%);
}

.price-wrap:after {
  content: 'Upbit';
  display: inline-block;
  /*position: absolute;*/
  top: 0;
  left: 0;
  height: 100%;
  background-color: #093687;
  z-index: 9999;
  padding: 10px;
  font-size: 15px;
  color: #fff;
  font-weight: bold;
  font-style: italic;
  font-family: 'IBM Plex Sans', sans-serif;
}

.ticker-txt {
  color: #333 !important;
  font-weight: bold;
  font-family: Maplestory-Light !important;
}

.bxl-bitcoin {
  color: #ef8e18;
  margin-top: 2px;
}

.bxl-ethereum {
  color: #3b3f52d8;
  margin-top: 2px;
}

.bxl-ada {
  color: #3f18ef;
  margin-top: 2px;
}

.slide-wrap>span {
  position: absolute;
  top: 50%;
  left: 110%;
  transform: translate(0, -50%);
  display: -ms-flexbox;
  display: flex;
  -ms-flex-pack: center;
  justify-content: center;
  -ms-flex-align: center;
  align-items: center;
  width: 110px;
  height: 20px;
  white-space: nowrap;
  text-align: center;
  color: #333;
  font-size: 1.1rem;
  font-family: 'IBM Plex Sans', sans-serif;
  z-index: 9997;
}

.slide-wrap>span span {
  font-size: 13px;
  margin: 2px;
  display: inline-block;
  vertical-align: middle;
}

.ticker-price-fall {
  color: #f6465d;
  margin: 0;
}

.ticker-price-rise {
  color: #0ecb81;
  margin: 0;
}

.ticker-price-same {
  color: #fff;
  margin: 0;
}

.item-BTC {
  animation: slidingSlow 15s 0s linear infinite;
}

.item-ETH {
  animation: slidingSlow 15s 5s linear infinite;
}

.item-ADA {
  animation: slidingSlow 15s 10s linear infinite;
}

@keyframes slidingSlow {
  0% {
    left: 100%;
  }

  100% {
    left: 5%;
  }
}
```

**HTML** 과 **CSS** 는 본인 블로그 스킨에 맞게 유동적으로 고쳐서 적용하면 된다.

끝!

## Ref

[juni-official.tistory.com](https://juni-official.tistory.com/)

![](https://velog.velcdn.com/images/clothes/post/95e593ac-5fed-48be-ad89-1a9ab34208f8/image.png)


넘나 친절하신 꾸생님
