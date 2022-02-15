---
title: "[Java Live Study] 2-4. 리터럴(Literal)"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 자료형, <u>변수</u> 그리고 배열 사용하는 방법 익히기


# [1] Literal(리터럴)
리터럴은 기본형 변수에 값을 대입할 때 **대입연산자(`=`)를 기준으로 우변**에 사용되는 <u>고정 값</u>을 의미한다. 

```java
boolean result = true; // true가 리터럴
char ch = 'a'; // 'a'가 리터럴
int i = 100; // 100이 리터럴
```

## 숫자형 리터럴에 언더스코어(`_`) 사용하기
실생활에서 긴 숫자에 3자리씩 끊어서 콤마(`,`)를 찍듯이 **Java7**부터는 언더스코어(`_`)를 사용하여 **가독성을 높일 수 있다.**

- 숫자형 데이터 타입이면 사용 가능하다.
- 꼭 3자리씩 나누어야 하는 것은 아니다.
- 유효하지 않은 경우
  1. 숫자 리터럴 맨 앞이나 맨 뒤에 사용 불가능
  2. 소숫점 앞뒤에 사용 불가능
  3. 타입을 명시해주는 접미사(예. float에 F, long에 L) 앞에 사용 불가능
  4. 숫자를 String으로 입력하는 경우 사용 불가능

```java
// error: 1번에 해당
long l = _123000L;
int i = 456000_;

// error: 2번에 해당
float f = 12._345f;
float f = 12_.345f;

// error: 3번에 해당
double d = 89.000_d;

// error: 4번에 해당
int i = Integer.parseInt("650_000");

// ok 
int i = 9_____7;
```
