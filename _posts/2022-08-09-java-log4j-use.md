---
layout: post
title: "[Java] log4j 2 사용법"
date: 2022-08-15 15:12:09 +0600
categories: [JAVA]
author: EuiSangYu
post_image: "/assets/images/blog-img1.jpg"
---

## log4j2.xml 파일 코드 구성

APACHE 공식 래퍼런스 문서 기본 형태 + 업무에서 배운 형태

```
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="debug" name="RoutingTest" monitorInterval="30">
  <Properties>
    <Property name="filename">target/rolling1/rollingtest-$${sd:type}.log</Property>
  </Properties>
  <ThresholdFilter level="debug"/>
 
  <Appenders>
    <Console name="STDOUT">
      <PatternLayout pattern="%m%n"/>
      <ThresholdFilter level="debug"/>
    </Console>
    <Routing name="Routing">
      <Routes pattern="$${sd:type}">
        <Route>
          <RollingFile name="Rolling-${sd:type}" fileName="${filename}"
                       filePattern="target/rolling1/test1-${sd:type}.%i.log.gz">
            <PatternLayout>
              <pattern>%d %p %c{1.} [%t] %m%n</pattern>
            </PatternLayout>
            <TimeBasedTriggeringPolicy interval="1" modulate="true" />
            <SizeBasedTriggeringPolicy size="500" />
          </RollingFile>
        </Route>
        <Route ref="STDOUT" key="Audit"/>
      </Routes>
    </Routing>
  </Appenders>
 
  <Loggers>
    <Logger name="EventLogger" level="info" additivity="false">
      <AppenderRef ref="Routing"/>
    </Logger>
 
    <Root level="error">
      <AppenderRef ref="STDOUT"/>
    </Root>
  </Loggers>
 
</Configuration>
```

각각의 요소에 대해 하나씩 정리해보자.

우선 가장 상단의 Configuration 부터

## Configuration

```
<Configuration status="debug" name="RoutingTest" monitorInterval="30">
```

Configuration은 로그 설정의 최상위 노드이다.

Configuration은 Properties, Appenders, Loggers 요소를 자식 노드로 가지고 있다.  
status 속성은 log4j의 내부 이벤트에 대한 로그 레벨을 의미.

monitorInterval="30" 은 Log4j가 파일의 변경 여부를 확인하는 주기를 '30'분 주기로 하겠다는 뜻이다.

## Properties

```
<Properties>
    <Property name="filename">target/rolling1/rollingtest-$${sd:type}.log</Property>
  </Properties>
```

Properties는 해당 Configuration 영역 내에서 사용할 프로퍼티를 의미한다.

자바로 치면 전역변수같은 느낌

## Layout

```
<PatternLayout>
	<pattern>%d %p %c{1.} [%t] %m%n</pattern>
</PatternLayout>
```

날짜나 시간(12,24) 포맷, 색깔, 출력 요소 등을 결정할 수 있는 요소이다.

구체적인 사용 방법은 **[링크](https://logging.apache.org/log4j/2.x/manual/layouts.html)** 

## Appenders

Appender는 log 메세지를 특정 위치에 전달해주는 역할이다.

Appender는 layout을 통해 로그를 formatting 하고, 어떤 방식으로 로그를 제공할지 결정한다.

Appender에는 여러 종류가 있다. 소개되지 않은 나머지는 **[링크](https://logging.apache.org/log4j/2.x/manual/appenders.html)** 

-   ConsoleAppender
-   RollingFileAppender
-   FileAppender
-   JDBCAppender
-   등등...

여기서 가장 핵심이라고 생각하는 **RollingFileAppender** 만 따로 설명하자면, 

```
<RollingFile name="Rolling-${sd:type}" fileName="${filename}" 
	filePattern="target/rolling1/test1-${sd:type}.%i.log.gz">
       
       <PatternLayout>
       		<pattern>%d %p %c{1.} [%t] %m%n</pattern>
       </PatternLayout>
       <Policies>
       	<TimeBasedTriggeringPolicy interval="1" modulate="true" />
       	<SizeBasedTriggeringPolicy size="500" />
       </Policies>
       <DefaultRolloverStrategy max="10" fileIndex="min"/>
</RollingFile>
```

로그 파일에 문제가 생기면 로그가 전부 유실될 수 있기 때문에 **RollingFileAppender**에서 설정을 해줌으로서 미연에 방지할 수 있다.

RollingFileAppender 는 파일에 로그를 기록하고, 특정 기준에 따라 압축하여 저장하는 방식의 Appender 이다.

RollingFileAppender의 구체적인 속성들을 설명하자면

#### Policy

Policy는 간단하게 설명하자면 기준이되는 트리거를 정할 수 있고, 구체적인 제약사항을 정할 수 있다.

File Rolling Up 기준이고, 하나의 RollingFileAppender에는 여러 Policy를 적용할 수 있다.

예를 들어 TimeBasedTriggeringPolicy 를 삽입한다고 치면 설정한 interval=? 에 따라 주기가 달라진다.

-   **OnStartupTriggeringPolicy** : jvm start시 trigger
-   **TimeBasedTriggeringPolicy** : time에 따른 trigger
-   **SizeBasedTriggeringPolicy** : file size에 따른 trigger
-   **CronTriggeringPolicy** : Cron Expression(시간에 관한 표현)에 따른 trigger

#### DefaultRolloverStrategy

DefaultRolloverStrategy는 datetime 패턴과 File Pattern의 int값을 받아서 정해진다.

File Pattern 숫자는 DB에서 사용되는 자동증가 Sequence처럼 rollover 마다 1씩 증가한다.

datetime은 현재 시간으로 대체되고, 각각 rollover 이후에는 정해준 형식대로 아래 사진처럼(예시) 저장된다.

![](https://velog.velcdn.com/images/clothes/post/d9f9f71b-00d1-44e8-ad8a-040232299a82/image.png)

해당 **Strategy**에 부여할 수 있는 속성들

-   **fileIndex** : max로 설정 시 높은 index가 더 최신 파일이 됩니다. min으로 설정 시 작은 index가 최신 파일이 된다. 기존의 파일들을 rename하는 방식으로 동작.
-   **compressionLevel** : 0~9까지 정수값. 0은 압축하지 않고, 1은 최고 속도, 9는 최고 압축. ZIP파일만 가능함.
-   **tempCompressedFilePattern** : 압축하는 동안의 파일 이름 패턴.
-   **min** : counter 최소값. 기본값은 1
-   **max** : counter 최대값. 만약 최대값에 도달하면 오래된 파일을 삭제. 기본값은 7

## Logger

```
<Loggers>
	<!-- Additivity값은 중복된 로그를 남길 지에 대한 속성 -->
    <Logger name="EventLogger" level="INFO" additivity="false">
      <AppenderRef ref="Routing"/>
    </Logger>
 
    <Root level="error">
      <AppenderRef ref="STDOUT"/>
    </Root>
</Loggers>
```

Root패키지의 <Logger>는 필수이고, 여러개를 적용할 때에는 <Loggers> 내에 복수개의 <Logger>로 설정할 수 있다.

해당 로거는 name="EventLogger" 패키지에 해당하는 파일들에 대해서 INFO 이상 레벨의 로그를 콘솔에 남기는 로거이다.

그냥 여태까지는 로그를 찍어야하는구나하고 대충 사용할 줄만 알았었는데 이번 기회에 조금 자세히 공부할 수 있었다

---

## Ref

[https://logging.apache.org/log4j/2.x/manual/configuration.html#PropertySubstitution](https://logging.apache.org/log4j/2.x/manual/configuration.html#PropertySubstitution)
