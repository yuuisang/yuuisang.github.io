---
title:  "[Javscript] Object.keys - 객체의 Key 값 가져오기, Object.value - value값 가져오기"
layout: post
author: EuiSang Yu
categories: Javascript
tags: [Javascript]
---

데이터를 객체로 다루다보면 key값만 추출해서 따로 사용하거나 value값만 추출해서 사용해야하는 경우가 종종 생긴다.  
이럴 때 배열에 돌려서 일일이 꺼내 쓰는건 굉장히 귀찮은 작업이기 때문에,

JS에서는 **Object.keys()**, **Object.values()** 라는 메서드를 제공해준다.  
  
쉽게 설명하자면 특정 객체를 대상으로 key, value 값들만 뽑아서 **배열로 리턴**하는 함수다.

```javascript
var obj = { a: 1, b: 2, c: 3 }; 
var keys = Object.keys(obj); 
var values = Object.values(obj);

console.log("결과1:"+keys);
console.log("결과2:"+values);

// 결과1 : [a, b, c]
// 결과2 : [1, 2, 3]
```

참고로 Object 이다보니 **순서는 명확하지 않다.**

해당 데이터에 명확한 인덱스(순서)를 알아야 한다면 조금 투박한 방법이지만

```javascript
var obj = { a: 1, b: 2, c: 3 }; 
var keys = Object.keys(obj); 
var values = Object.values(obj);

console.log("결과1:"+keys);
console.log("결과2:"+values);

// 결과1 : [a, b, c]
// 결과2 : [1, 2, 3]

// 순서 확인
var keys_arr = [];
var vals_arr = [];
keys.sort(); // 이름순으로 정렬
for(var i=0; i < keys.length; i++){
    vals_arr.push(values[keys[i]]);
}

console.log("keys 순서대로 정렬된 value 값들 : "+vals_arr);
```

이런식으로 해서 명확한 인덱스를 찾아도 된다.