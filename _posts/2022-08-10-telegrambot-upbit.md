---
layout: post
title: "[Telegram] 텔레그램 코인 알림봇 개발 (Node.js 를 이용한 Rest 방식)"
date: 2022-08-10 15:12:09 +0600
categories: [Telegram]
author: EuiSangYu
post_image: "/assets/images/telegram/telegram.png"
---

나는 평소 코인을 거래할 때 [김프가](https://kimpga.com/) 라는 사이트를 자주 이용하는데, 매번 띄워놓고 확인하기 너무 번거롭다고 느껴서 차라리 내가 원하는 특정 상황이 되었을때 **텔레그램 봇이 실시간 가상화폐(코인) 가격을 채팅으로 알려주는 프로그램**을 직접 개발해봐야겠다고 생각했다.

2022.04.24 어제 새벽에 시작했고, 현재 내가 시도한 방법이 몇몇 코인들의 정보를 가져오는데는 전혀 문제가 없지만 업비트의 **API Request 수 제한**에 걸리기 때문에 전체를 대상으로는 부적합한 방법이라는 걸 깨닫고 전체 데이터를 실시간으로 조회할 새로운 방법을 찾아 시작하기 전에 내가 시도한 방법에 대한 정리를 하려고 한다.

## [Node.js](https://nodejs.org/ko/download/) 설치

node.js 를 설치(본인 운영체제에 맞게)

![](https://velog.velcdn.com/images/clothes/post/b84b72ba-d950-4c21-b226-1930cf018cef/image.png)

package.json 파일을 설정

![](https://velog.velcdn.com/images/clothes/post/4e748443-92fd-4a23-ba24-3faa5f96cc98/image.png)

추후에 필요한 모듈들은 필요할 때마다 터미널에 'npm install \_\_ ' 해서 사용!

## 프로그램 올릴 개인용 무료 서버 [Heroku](https://dashboard.heroku.com) 가입 및 등록

![](https://velog.velcdn.com/images/clothes/post/6c262617-fc08-4996-add7-48206442292f/image.png)

여기서도 설정할 것들이 꽤나 있었다.

![](https://velog.velcdn.com/images/clothes/post/856c3118-f9b6-4651-b60b-bda9a1c0891a/image.png)


해당 Settings 메뉴에서 Config Vars 에 텔레그램에서 발급받은 키를 입력했다.(**중요**!)

INTERVAL은 몇초마다 결과를 받을지 테스트할겸 적용한 값이다.(중요하지 않음)

![](https://velog.velcdn.com/images/clothes/post/80d20113-b943-4950-ba50-05922010565c/image.png)


Heroku에 올릴 때도 깃 명령어는 다른 깃 사용법과 동일하다.

```
# 깃 기본 세팅
git init
# 깃 저장소 세팅
heroku git:remote -a test-mv
# 현재 프로젝트 파일을 깃 현재 저장소에 등록
git add .
# 현재 저장소에 저장
git commit -am "make it better"
# Heroku 서버 마스터로 푸시
git push heroku master
```

## Heroku 서버 자동 Sleep 방지 모니터링

Heroku는 일정 시간 동안 deploy한 앱에 접속 요청이 없을 경우, 앱을 sleep 시켜버린다. 

물론 sleep 이 된다고 해서 영원한 잠에 빠지거나 하는 건 아니고, 다음 요청이 있을 때까지 죽여 놓는 것이다. 새로운 요청을 받으면 앱을 새로 구동한 다음 웹 페이지를 보여준다. 평범한 블로그나 웹 사이트라면 sleep 상태라고 해도 10~30초 정도만 기다리면 되는 것이다.  
하지만 텔레그램 봇은 웹이 아니어서 그런지 한 번 sleep 상태로 빠져들면 다시는 깨어나지 않았다.  
  
그래서 나온 꼼수가 http end point를 만든 다음, 주기적으로 ping을 보내주는 서비스에 봇의 http end point를 등록해서 봇이 잠들지 않도록 해주는 것이다. 이런 서비스들 중 하나가 바로 [uptimerobot](https://uptimerobot.com) 이다.

무료로 가입할 수 있고, 사용법도 단순하다.

가입후 대시보드에서 **New Monitor** 클릭한 뒤 본인이 원하는 도메인을 세팅하면 된다.

![](https://velog.velcdn.com/images/clothes/post/929b05ea-3341-4a41-83c6-098d66b5b3cf/image.png)

## 텔레그램 봇 API key 발급

텔레그램에서 **@BotFather** 채널을 검색해서 채팅창에 **/start** 를 입력하면 설명이 나온다.

순서대로 기술하자면

1.  /newbot
2.  본인이 정한bot 이름 입력 

## bot.js

```javascript
/*
    텔레그램 김프 봇
    EuiSang Yu
    2022.04.25
*/

// 업비트 조회
// 2022.04.25 기준 총 113개
const Upbit = require('./upbit')

// 업비트 정보 가져오기
async function upbit_start() {
    const upbit = new Upbit('시리얼키 자리', '액세스키 자리')

    let market_all = await upbit.market_all()
    let market_krw = [];
    for(let i=0; i<market_all.data.length; i++){
        if(market_all.data[i].market.includes("KRW")){
            market_krw.push({"data" : market_all.data[i]});
        }
    }
    console.log("원화 상장 코인 총 개수 : " + market_krw.length)

    for (let i=0; i< market_krw.length; i++){
        {
            let {'data': data} = await upbit.market_ticker(market_krw[i].data.market)
            console.log(data)
        }

        //result.push({"market" : data[i].market, "trade_price" : data[i].trade_price})
    }
}

upbit_start()


// 바이낸스 정보 가져오기
const Binance = require('node-binance-api');
const binance = new Binance().options({
    APIKEY: '액세스키 자리',
    APISECRET: '시크릿키 자리',
    useServerTime: true,
    test: true
})


//사용자 id 저장
var  idSet  =  new  Set();

// Telegram Api 연동
const TelegramBot = require('node-telegram-bot-api');
var  http  =  require('http');
var  request  =  require('sync-request');

// 텔레그램 정보 가져오기
const getToken = (function(){
    const token = process.env.TELEGRAM_TOKEN;
    return function() {
        return token;
    };
})();

const bot = new TelegramBot(getToken(), {polling: true});

bot.onText(/\/start/, (msg, match) => {
    if(idSet.has(msg.chat.id) ==  false) {
        idSet.add(msg.chat.id);
    }
});

bot.onText(/\/stop/, (msg, match) => {
    if(idSet.has(msg.chat.id)) {
        idSet.delete(msg.chat.id);
    }
});

setInterval(function() {
    
    // res.map(coin  => {
    //     for(let  id  of  idSet) {
    //         bot.sendMessage(id, "현재 " + coin.market +" 가격은 ["  +  coin.trade_price +  "] 원 입니다.");
    //     }
    // });

}, process.env.INTERVAL);
```

## upbit.js

```javascript
const rp = require("request-promise")
const sign = require("jsonwebtoken").sign
const queryEncode = require("querystring").encode

async function request(url, qs, token, method) {
    if (!method) {
        method = 'GET'
    }
    let options = {
        method: method, 
        url: url,
        json: true,
        transform: function (body, response) {
            let remain_min = 0
            let remain_sec = 0
            if (response.headers && response.headers['remaining-req']) {
                let items = response.headers['remaining-req'].split(';')
                for (let item of items) {
                    let [key, val] = item.split('=')
                    if (key.trim()=='min') {
                        remain_min = parseInt(val.trim())
                    } else if (key.trim()=='sec') {
                        remain_sec = parseInt(val.trim())
                    }
                }
            }
            return {
                'success': true,
                'remain_min': remain_min, 
                'remain_sec': remain_sec, 
                'data': body
            }
        }
    }
    if (method=='POST') {
        options.json = qs
    } else {
        options.qs = qs
    }
    if (token) {
        options.headers = {Authorization: `Bearer ${token}`}
    }
    let result = {'success': false, 'message': null, 'name': null}
    try {
        result = await rp(options)
    } catch(e) {
        result.data = null
        if (e.error.error) {
            result.message = e.error.error.message
            result.name = e.error.error.name
        } else {
            result.message = e.message
        }
    }

    return result
}

//전체 계좌 조회
async function accounts() {
    const url = 'https://api.upbit.com/v1/accounts'

    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, {}, token)
    return result
}

// 주문 리스트
async function order_list(market, state, uuids, page) {
    //market: null KRW-BTC
    //state: wait done
    const url = 'https://api.upbit.com/v1/orders'
    let qs = {state:state, page:page}
    if (market) qs['market'] = market
    if (uuids) qs['uuids'] = uuids

    const query = queryEncode(qs)
    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
        query: query
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, qs, token)
    return result
}

// 주문(매수)
async function order_bid(market, volume, price) {
    //market: KRW-BTC
    const url = 'https://api.upbit.com/v1/orders'
    let qs = {market:market, side:'bid', volume:volume, price:price, ord_type:'limit'}

    const query = queryEncode(qs)
    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
        query: query
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, qs, token, 'POST')
    return result
}

// 주문(매도)
async function order_ask(market, volume, price) {
    //market: KRW-BTC
    const url = 'https://api.upbit.com/v1/orders'
    let qs = {market:market, side:'ask', volume:volume, price:price, ord_type:'limit'}

    const query = queryEncode(qs)
    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
        query: query
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, qs, token, 'POST')
    return result
}

// 주문 상세
async function order_detail(uuid) {
    const url = 'https://api.upbit.com/v1/order'
    let qs = {uuid:uuid}

    const query = queryEncode(qs)
    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
        query: query
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, qs, token)
    return result
}

// 주문 취소
async function order_delete(uuid) {
    const url = 'https://api.upbit.com/v1/order'
    let qs = {uuid:uuid}

    const query = queryEncode(qs)
    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
        query: query
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, qs, token, 'DELETE')
    return result
}

// 주문 가능 정보
async function order_chance(market) {
    const url = 'https://api.upbit.com/v1/orders/chance'
    let qs = {market:market}

    const query = queryEncode(qs)
    const payload = {
        access_key: this.accessKey,
        nonce: (new Date).getTime(),
        query: query
    }
    const token = sign(payload, this.secretKey)

    let result = await request(url, qs, token)
    return result
}

// 시세종목정보
async function market_all() {
    const url = 'https://api.upbit.com/v1/market/all'
    let result = await request(url)
    return result
}

// 분 캔들
async function market_minute(market, unit, to, count) {
    //unit:  1, 3, 5, 15, 10, 30, 60, 240
    //to: yyyy-MM-dd'T'HH:mm:ssXXX
    const url = 'https://api.upbit.com/v1/candles/minutes/'+unit
    let qs = {market:market}
    if (to) qs.to = to
    if (count) qs.count = count

    let result = await request(url, qs)
    return result
}

// 일 캔들
async function market_day(market, to, count) {
    //to: yyyy-MM-dd'T'HH:mm:ssXXX
    const url = 'https://api.upbit.com/v1/candles/days'
    let qs = {market:market}
    if (to) qs.to = to
    if (count) qs.count = count

    let result = await request(url, qs)
    return result
}

// 주 캔들
async function market_week(market, to, count) {
    //to: yyyy-MM-dd'T'HH:mm:ssXXX
    const url = 'https://api.upbit.com/v1/candles/weeks'
    let qs = {market:market}
    if (to) qs.to = to
    if (count) qs.count = count

    let result = await request(url, qs)
    return result
}

// 월 캔들
async function market_month(market, to, count) {
    //to: yyyy-MM-dd'T'HH:mm:ssXXX
    const url = 'https://api.upbit.com/v1/candles/months'
    let qs = {market:market}
    if (to) qs.to = to
    if (count) qs.count = count

    let result = await request(url, qs)
    return result
}

// 채결 정보
async function market_trade_tick(market, to, count) {
    //to: yyyy-MM-dd'T'HH:mm:ssXXX
    const url = 'https://api.upbit.com/v1/trades/ticks'
    let qs = {market:market}
    if (to) qs.to = to
    if (count) qs.count = count

    let result = await request(url, qs)
    return result
}


// 시세 Ticker
async function market_ticker(markets) {
    // markets: KRW-BTC,KRW-ETH
    const url = 'https://api.upbit.com/v1/ticker'
    let qs = {markets:markets}

    let result = await request(url, qs)
    return result
}


// 호가 정보
async function trade_orderbook(markets) {
    // markets: KRW-BTC,KRW-ETH
    const url = 'https://api.upbit.com/v1/orderbook'
    let qs = {markets:markets}

    let result = await request(url, qs)
    return result
}

// class Upbit
function Upbit(s, a) {
    this.secretKey = s
    this.accessKey = a
}

Upbit.prototype.accounts = accounts
Upbit.prototype.order_list = order_list
Upbit.prototype.order_bid = order_bid
Upbit.prototype.order_ask = order_ask
Upbit.prototype.order_detail = order_detail
Upbit.prototype.order_delete = order_delete
Upbit.prototype.order_chance = order_chance
Upbit.prototype.market_all = market_all
Upbit.prototype.market_minute = market_minute
Upbit.prototype.market_day = market_day
Upbit.prototype.market_week = market_week
Upbit.prototype.market_month = market_month
Upbit.prototype.market_trade_tick = market_trade_tick
Upbit.prototype.market_ticker = market_ticker
Upbit.prototype.trade_orderbook = trade_orderbook

module.exports = Upbit
```

## web.js

```javascript
/*
    http end-point
*/
const express = require('express');
var packageInfo = require('./package.json');

var app = express();

app.get('/', function (req, res) {
    res.json({ version: packageInfo.version });
});

var server = app.listen(process.env.PORT, function () {
    var host = server.address().address;
    var port = server.address().port;

    console.log('Web server started at http://%s:%s', host, port);
});
```

## index.js

```javascript
require('./bot');
require('./web');
```

## 텔레그램 봇으로 채팅 받는 것까지 성공!!

이렇게 구성을해서 테스트 중이었고 실제로 텔레그램 봇으로 코인 정보를 10초마다 실시간으로 채팅 받는 것까지 성공했다...

![](https://velog.velcdn.com/images/clothes/post/fca5aaf9-60dd-4913-8fbd-3640328aad69/image.png)


![](https://velog.velcdn.com/images/clothes/post/c795d370-8c83-45c5-9060-fe050d703474/image.png)


~~하지만...원화 마켓에 있는 총 113개의 코인의 이름과 현재 종가(trade\_price)를 한번에 받아오려고 하니 업비트의 Rest API 요청 수 제한이 있다는 사실을 뒤늦게 깨달아 버렸다...😡😡~~

![](https://velog.velcdn.com/images/clothes/post/c740c6eb-fa6c-4810-a094-65265adc602d/image.png)


![](https://velog.velcdn.com/images/clothes/post/98be74a5-9904-4799-96c8-08c818882e21/image.png)


그리하여 나의 8시간을 불태운 작업은 여기서 마무리 되었다.

지금 머리속에 드는 계획은 새로 환경구축하고 파이썬을 새로 배워볼 겸 파이썬으로 처리할 생각인데, 김프가 사이트를 **크롤링**해서 텔레그램에 보낼 메세지에 입혀야겠다.

그리고 생각해보니 가능하면 트위터 API도 같이 끌어와야겠다... 매번 트위터켜서 코인들 소식 검색하는것도 귀찮으니ㅜ

![](https://velog.velcdn.com/images/clothes/post/84d50146-c8fe-4ac3-ae76-e0a9a7ba51d9/image.png)


지금 굉장히 허무해서 설명을 너무 대충적은거 같은데 밑에 내가 참고한 사이트들을 전부 링크에 걸어둘테니 참고하면서 하면 될 것같다.

혹시 지금 이글을 보고 '나는 모든 코인 가격은 다 필요없고 간단하게 그때 그때 알고싶은 코인 몇개 정보면 돼! ' 라고 생각하는 사람들도 있을텐데 그렇다면 내가 시도한 방법으로도 무리없이 충분히 완성 가능하니 참고하면 좋을 것 같다.

그럼 다음 글은 파이썬으로 adios.............

## Ref

[https://johngrib.github.io/blog/2017/03/12/telegram-bot/](https://johngrib.github.io/blog/2017/03/12/telegram-bot/)

[https://note.heyo.me/%EC%97%85%EB%B9%84%ED%8A%B8api-%ED%8A%B8%EB%A0%88%EC%9D%B4%EB%94%A9-1-%EC%A4%80%EB%B9%84-%EB%B0%8F-%ED%85%8C%EC%8A%A4%ED%8A%B8/](https://note.heyo.me/%EC%97%85%EB%B9%84%ED%8A%B8api-%ED%8A%B8%EB%A0%88%EC%9D%B4%EB%94%A9-1-%EC%A4%80%EB%B9%84-%EB%B0%8F-%ED%85%8C%EC%8A%A4%ED%8A%B8/)

[https://steemit.com/kr-dev/@asinayo/nodejs-heroku](https://steemit.com/kr-dev/@asinayo/nodejs-heroku)

