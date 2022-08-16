---
layout: post
title: "[Javscript] jQuery UI datepicker 사용법(ex_날짜 제한)"
date: 2022-08-09 15:12:09 +0600
categories: [Javascript]
author: EuiSangYu
post_image: "/assets/images/javascript/javascript.png"
---

## 기본 세팅 옵션

```javascript
$.datepicker.setDefaults({
        dateFormat: 'yy-mm-dd',	//날짜 포맷이다. 'yy-mm-dd' 를 보편적으로 사용
        prevText: '이전 달',	// 마우스 오버시 이전달 텍스트
        nextText: '다음 달',	// 마우스 오버시 다음달 텍스트
        closeText: '닫기', // 닫기 버튼 텍스트 변경
        currentText: '오늘', // 오늘 텍스트 변경
        monthNames: ['1월', '2월', '3월', '4월', '5월', '6월', '7월', '8월', '9월', '10월', '11월', '12월'],	//한글 캘린더중 월 표시를 위한 부분
        monthNamesShort: ['1월', '2월', '3월', '4월', '5월', '6월', '7월', '8월', '9월', '10월', '11월', '12월'],	//한글 캘린더 중 월 표시를 위한 부분
        dayNames: ['일', '월', '화', '수', '목', '금', '토'],	//한글 캘린더 요일 표시 부분
        dayNamesShort: ['일', '월', '화', '수', '목', '금', '토'],	//한글 요일 표시 부분
        dayNamesMin: ['일', '월', '화', '수', '목', '금', '토'],	// 한글 요일 표시 부분
        showMonthAfterYear: true,	// true : 년 월  false : 월 년 순으로 보여줌
        yearSuffix: '년',	
        showButtonPanel: true,	// 오늘로 가는 버튼과 달력 닫기 버튼 보기 옵션
        buttonImageOnly: true,	// input 옆에 조그만한 아이콘으로 캘린더 선택가능하게 하기
        buttonImage: "images/calendar.gif",	// 조그만한 아이콘 이미지
        buttonText: "Select date"	// 조그만한 아이콘 툴팁
    });
```

## 오늘 날짜 구하기

```javascript
var today = $.datepicker.formatDate('yy-mm-dd', new Date());
```

## 선택할 수 있는 날짜 제한

```javascript
$("#datepicker1").datepicker({
	maxDate : "+1m +1w",	//선택할 수 있는 최대 날짜  +1m +1w 은 1달 1주일 뒤 까지 선택가능  [+,-][숫자][y,m,w,d] 
	minDate : "-1y"	//선택할 수 있는 최소 날짜 
    //maxDate : new Date('2022-05-05'), // 이런식으로 사용해도 됨
    //minDate : new Date('2022-01-01') //
});
```
