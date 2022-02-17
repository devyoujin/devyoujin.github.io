---
title: "[Java Live Study] 2-3. 타입 추론(Type Inference)"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **2주차 목표**: Java의 <u>자료형</u>, 변수 그리고 배열 사용하는 방법 익히기

# [1] 타입 추론(Type Inference)
- 타입 추론은 컴파일러가 추론 알고리즘에 따라 타입을 결정하는 것이다.
- 타입 추론은 Generics를 지원하는 용도로 사용되다가, Lambda를 도입하면서 개선되었다.

🚧 Generics랑 Lambda 공부하고 돌아와서 타입추론 내용 보충하기 🚧

# [2] var
- var는 지역 변수로만 선언될 수 있으며, 지역 변수의 타입 추론을 위해 사용된다.
- 컴파일러가 변수의 초기값으로 타입을 추론해 명시해두기 때문에 변수를 읽을 때마다 추론을 위한 연산을 하지 않는다.
- 명시적 초기화(선언과 동시에 초기값을 부여하는 것)를 해야한다.
- null, 배열, 람다 표현식으로 초기화할 수 없다.

- <https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html>
- <https://catch-me-java.tistory.com/19>
- <https://www.baeldung.com/java-10-local-variable-type-inference>