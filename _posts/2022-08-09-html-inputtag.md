---
title:  "[HTML] input 태그 총 정리"
layout: post
author: EuiSang Yu
categories: HTML
tags: [HTML]
---

<code>input</code> 태그는 사용자로부터 값을 입력받을 수 있는 대화형 컨트롤(=필드)를 나타낸다. 기본적으로 인라인 요소이고, 닫는 태그가 없는 단일태그이다. input 태그는 type 속성을 통해 입력받는 요소의 데이터 유형이 달라진다. 사용가능한 type 은 20여 가지이며, 기본값은 text 이다.

## 다양한 type

### text

디폴트 값. 한줄의 텍스트 필드이다. 새줄 문자는 입력값으로부터 자동으로 제거 됨.
![](https://velog.velcdn.com/images/clothes/post/21bde81f-c0e8-4859-b2a2-441007fc5dad/image.png)


### password

값이 가려진 한줄 텍스트 필드. 사이트가 안전하지 않으면 사용자에게 경고

![](https://velog.velcdn.com/images/clothes/post/ccd7af7d-9ee9-4b85-b0dc-0714eeabaa1a/image.png)

### radio

**같은 name 값**을 가진 여러개의 선택중에서 하나의 값을 선택하게 하는 라디오 버튼

![](https://velog.velcdn.com/images/clothes/post/7df3f73a-3ace-411e-b2f4-090561677b42/image.png)

### submit

form ~ /form 내에 있는 정보들을 서버로 전달하는 버튼

![](https://velog.velcdn.com/images/clothes/post/c90694a2-bcde-43c1-b3cb-0a8df761babc/image.png)

### range

값이 가려진 숫자를 입력하는 컨트롤. 디폴트 값이 중간값인 범위 위젯으로 표시하고, 접속사 min 와 max 사이에 사용되며 수용가능한 값의 범위를 정의한다.

![](https://velog.velcdn.com/images/clothes/post/e6dc1932-0929-43e8-8d99-c6ae3bd862b9/image.png)

### button

기본 행동을 가지지 않으며 value을 레이블로 사용하는 푸시 버튼.

![](https://velog.velcdn.com/images/clothes/post/159419e3-b3ae-4b68-867a-dcfaf9af72be/image.png)

### checkbox

단일 값을 선택하거나 선택 해제할 수 있는 체크박스.

![](https://velog.velcdn.com/images/clothes/post/f1e1bcad-69e4-4a14-904a-a5aa515f39a1/image.png)

### date

날짜(연월일, 시간 없음)를 지정할 수 있는 컨트롤. 브라우저가 지원하는 경우, 활성화 시 날짜를 선택할 수 있는 달력 등을 열어준다.

![](https://velog.velcdn.com/images/clothes/post/aaee5aaa-ca91-4162-8948-8fe184c767b7/image.png)

![](https://velog.velcdn.com/images/clothes/post/72f0d4c7-b884-40ee-96ee-1061e2a69425/image.png)

### file

파일을 지정할 수 있는 컨트롤. accept 특성을 사용하면 허용하는 파일 유형을 지정할 수 있다.

![](https://velog.velcdn.com/images/clothes/post/89c972e1-8884-45cd-8889-7286cd174c7e/image.png)

![](https://velog.velcdn.com/images/clothes/post/ac8e5f05-04c1-40a3-9e64-86eebf485736/image.png)

### hidden

형태가 보이지 않지만 값만 서버로 전송하는 타입이다. 자주 사용되는 타입!

![](https://velog.velcdn.com/images/clothes/post/69f877eb-0575-40fc-9415-12f0d6cb98c2/image.png)

### image

src 특성에 지정한 이미지로 나타나는 시각적 제출 버튼. <img> 태그와 동일

![](https://velog.velcdn.com/images/clothes/post/ea3f7c53-45cd-475d-9372-9ee4ee644ad9/image.png)

~이 외에도 몇개 더 있지만 딱히 중요한 것은 없다.~

## name 지정

**radio** 타입에서는 반드시 name 지정 필수!

```
<input type="radio" name="age" value="1">1
<input type="radio" name="age" value="2">2
<input type="radio" name="age" value="3">3
<input type="radio" name="age" value="4">4
```

## 다양한 전역 속성

**input 요소**는 전역 속성(Global Attributes)과 다음 특성을 포함한다.

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| [accept](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefaccept) | file | 파일을 업로드 컨트롤에서 기대하는 파일 유형을 암시 |
| [alt](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefalt) | image | 이미지 유형에 대한 대체 속성. accessibiltiy 측면에서 필요. |
| [autocomplete](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefautocomplete) | all | 양식 자동생성 기능 (form autofill) 암시 |
| [autofocus](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefautofocus) | all | 페이지가 로딩될때 양식 제어에 오토포커스 |
| [capture](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefcapture) | file | 파일 업로드 제어에서 input 방식에서 미디어 capture |
| [checked](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefchecked) | radio, checkbox | 커맨드나 컨트롤이 체크 되었는지의 여부 |
| [dirname](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefdirname) | text, search | 양식 전송시 요소의 방향성을 전송할 때 양식 필드의 Name |
| [disabled](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefdisabled) | all | 양식 컨트롤이 비활성화되었는지의 여부 |
| [form](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefform) | all | 컨트롤을 양식 요소와 연결 |
| [formaction](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefformaction) | image, submit | 양식 전송시 URL 사용하기 |
| [formenctype](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefformenctype) | image, submit | 양식의 데이터 인코딩 유형이 양식 전송시 사용될 것 |
| [formmethod](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefformmethod) | image, submit | 양식 전송시 HTTP 방식을 사용 |
| [formnovalidate](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefformnovalidate) | image, submit | 양식 전송시 양식 컨트롤 확인을 무시하기 |
| [formtarget](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefformtarget) | image, submit | 양식 전송시 브라우징 맥락 |
| [height](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefheight) | image | 이미지 높이에서 height 속성과 같음 |
| [list](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdeflist) | almost all | datalist 자동입력 옵션의 id 속성값 |
| [max](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefmax) | numeric types | 최대값 |
| [maxlength](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefmaxlength) | password, search, tel, text, url | value의 최대 길이 (문자수) |
| [min](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefmin) | numeric types | 최소값 |
| [minlength](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefminlength) | password, search, tel, text, url | value의 최소 길이 (문자수) |
| [multiple](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefmultiple) | email, file | 불리언값. 여러 값을 허용할지의 여부 |
| [name](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefname) | all | input 양식 컨트롤의 이름. 이름/값 짝(name/value pair)의 일부로서 양식과 함께 전송된다 |
| [pattern](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefpattern) | password, text, tel | value 가 유효하기 위해 일치해야 하는 패턴 |
| [placeholder](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefplaceholder) | password, search, tel, text, url | 양식 컨트롤이 비어있는 때 양식 컨트롤에 나타나는 내용 |
| [readonly](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/readonly) | almost all | 불리언값. 이 값은 수정이 불가능함 |
| [required](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/required) | almost all | 불리언값. 양식이 전송되기 위해서 반드시 입력하거나 확인이 필요한 값 |
| [size](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefsize) | email, password, tel, text | 컨트롤의 크기 |
| [src](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefsrc) | image | 이미지 출처의 주소에서 src 와 같은 속성 |
| [step](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefstep) | numeric types | 유효한 증분적인 (Incremental)값 |
| [type](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdeftype) | all | input 양식 컨트롤의 유형 |
| [value](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefvalue) | all | 양식 컨트롤의 현재 값. 이름/값 짝(name/value pair)의 일부로서 양식과 함께 전송된다 |
| [width](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#htmlattrdefwidth) | image | 이미지의 width 속성과 같다 |