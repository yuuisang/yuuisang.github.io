---
layout: post
title: "[Javscript] JSON 데이터 [object object] alert 나 console.log 함수로 출력하는 방법"
date: 2022-08-09 15:12:09 +0600
categories: [Javascript]
author: EuiSangYu
post_image: "/assets/images/javascript/javascript.png"
---

기본적으로 JS에서 JSON 데이터는 콘솔이나 Alert 로 출력시 <code>[Object object]</code> 로만 출력되고 내용은 보이지 않는다.

이럴 경우 데이터를 제대로 갖고있는지 확인하려면 다음 함수를 사용하면 된다.

## JSON.stringify()

```javascript
//data == 확인할 JSON 데이터
console.log(JSON.stringify(data));
alert(JSON.stringify(data));
```