---
title:  "[HTML] 텍스트 관련 태그(p, hr, em, strong, u, b, mark, br ...) 사용법"
layout: post
author: EuiSang Yu
categories: HTML
tags: [HTML]
---

## p 태그

문단을 표시하는 태그(단락을 구분)

```html
<html>
    <head>
    </head>
    <body>
    	<p>단락1 입니다.</p>
        <p>단락2 입니다.</p>
    </body>
</html>
```

## h1, h2 ... h6 태그

헤드라인을 표시하는 태그이며, 숫자가 작을수록 크기가 크다.

```html
<html>
    <head>
    </head>
    <body>
    	<h1>제일 큰 제목</h1>
        <h2>2번째로 큰 제목</h2>
        <h3>3번째로 큰 제목</h3>
        <h4>4번째로 큰 제목</h4>
        <h5>5번째로 큰 제목</h5>
        <h6>가장 작은 제목</h6>
    </body>
</html>
```

## hr 태그

수평선을 표시하는 태그로 주제 변경이나 내용 구분시에 사용하는 태그이다.

```html
<html>
    <head>
    </head>
    <body>
    	<p>첫 단락</p>
        
        <hr>
        
        <p>두번째 단락</p>
    </body>
</html>
```

## br 태그

줄바꿈(==Enter) 을 적용해주는 태그이다. br 태그 하나당 1줄씩 줄바꿈 처리 된다.

```html
<html>
    <head>
    </head>
    <body>
    	첫 줄 내용    
        <br>        
        두번째 줄 내용
    </body>
</html>
```

## b 태그

해당 b ~~ /b 안의 텍스트에 Bold(강조) 를 적용한다.

```html
<html>
    <head>
    </head>
    <body>
    	일반 글씨
        
        <br>
        
        <b>강조된 Bold 글씨</b>
    </body>
</html>
```

## strong 태그

해당 strong ~~ /strong 안의 텍스트를 굵게 만든다.

```html
<html>
    <head>
    </head>
    <body>
    	일반 텍스트
        
        <br>
        
        <strong>폰트 굵게 적용된 텍스트</strong>
    </body>
</html>
```

## u 태그

해당 u ~~ /u 안의 텍스트에 언더바( \_ ) 를 적용한다.

```html
<html>
    <head>
    </head>
    <body>
    	일반 내용
        
        <br>
        
        <u>밑줄 쳐진 내용</u>
    </body>
</html>
```

## em 태그

해당 em ~~ /em 안의 텍스트에 이탈릭체(폰트)를 적용한다.

```html
<html>
    <head>
    </head>
    <body>
    	일반 텍스트
        
        <br>
        
        <em>이탈릭체 적용 텍스트</em>
    </body>
</html>
```

## mark 태그

해당 mark ~~ /mark 안의 텍스트에 형광펜 표시를 적용한다.

```html
<html>
    <head>
    </head>
    <body>
    	일반 텍스트
        
        <br>
        
        <mark>형광펜 효과 적용 텍스트</mark>
    </body>
</html>
```

## &nbsp

태그는 아니지만 HTML에서 띄어쓰기(==SpaceBar) 1칸을 의미한다.

```html
<html>
    <head>
    </head>
    <body>
    	띄어쓰기전문구 &nbsp 1칸띄어쓰기후문구
    </body>
</html>
```