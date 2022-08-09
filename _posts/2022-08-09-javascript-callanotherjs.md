---
layout: post
title:  "[Javscript] Javascript 파일에서 다른 JS 함수 호출 하는법"
categories: [ Javascript ]
image: assets/images/javascript/javascript.png
---

Node.js 처럼 Module.import/export 로 하는 방법말고 그냥 js에서 하는 방법을 찾고 있었는데

정상 동작하는 방법을 찾았다.

## 호출한 파일 : calc\_forecasting.js

호출 대상 : erlangc.js

```
// 외부 js파일 호출(erlangc.js)
document.write('<script src="/com/js/erlangc.js"></script>');

// 외부 js파일에 있는 함수 호출(Agents)
// function Agents() --> erlangc.js 파일 내에 정의된 함수

// 사용 예시
var Agents_t = Agents(SLA, SERVICE_TIME, tempVal ,AHT);
```
