---
title: "[Spring] Spring 탄생 배경"
categories:
  - Spring
tags:
  - 🌱Spring
---

> `#EJB` `#POJO` `#Spring`

# Spring 탄생 배경
> 🧸 **요약**: Spring이 탄생하기 이전에는 EJB(Enterprise Java Bean)가 Java 진영의 대표기술이었다. 하지만 EJB는 여러 문제점을 가지고 있었다. 한 개발자가 EJB의 문제점을 지적하며 대체 방안을 소스코드로 작성하여 책을 출간하였다. 이 책을 본 다른 개발자들 몇몇이 모여 오픈소스화하며 Spring이 탄생하게 되었다.
{:.notice--primary}

## EJB(Enterprise Java Bean)
EJB는 Java EE(Enterprise Edition) 구현체 중 하나로 **Spring이 탄생하기 이전까지 Java 진영의 대표기술**이었다. '**비지니스 객체를 관리하는 컨테이너를 만들어서 필요할 때마다 컨테이너로부터 객체를 받아서 사용하자**'라는 아이디어에서 시작되었다.

다음 기술을 지원하며 기업용 어플리케이션 개발을 단순하게 했다.
- 트랜잭션 관리
- 세션 관리
- EJB 인스턴스 풀링
- 지속성
- 보안
- 병렬 처리
- 데이터베이스 커넥션 풀링
- 인증과 접근 제어

그럼에도 불구하고 EJB는 몇 가지 **문제점**을 가지고 있었는데, 이 문제를 해결하기 위해 대안을 고안하면서 Spring이 탄생하게 되었다.
- **객체 지향적 개발 불가능**: 프레임워크 패키지에 속한 인터페이스를 사용하여 개발을 해야했는데, 이 인터페이스가 tight coupling으로 설계되어있다. 즉, 인터페이스가 서로 의존하고 있기 때문에 유지보수가 어렵고 확장성이 떨어지며 Java라는 객체 지향 언어를 사용하면서 객체 지향의 장점을 이용하지 못했다.
- **기술 침투 현상**: 특정 기술에 한정적인 복잡한 개념들을 이해해야했다. 프로젝트 자체가 기술에 종속되는 기술 침투 현상이 발생했다.
- **불필요한 구현**: 필요하지 않더라도 몇몇의 콜백 함수들을 반드시 구현해야했다.
- **무거운 웹 서버 사용**: EJB 컨테이너는 JBoss, Websphere, Weblogic과 같은 서버의 일부분이었는데, Apache Tomcat과 비교했을 때 굉장히 무거운 서버이다.
- **단위 테스트가 어려움**: EJB 컨테이너 밖에서 어플리케이션을 실행하는 것은 거의 불가능했기 때문에 단위 테스트를 위해 전체 어플리케이션 컨테이너에 배포해야했다.

## POJO(Plain Old Java Object)
POJO는 **프레임워크에 종속되지 않은 Java 객체**를 의미한다.

POJO라는 용어가 탄생한 배경도 재미있다. 세 명의 개발자가 강연을 준비하면서 의도적으로 붙인 이름인데 그 중 한 개발자의 말을 빌리자면,

 💬 ... 그 강연에서 우리는 Entity Bean을 이용하는 것이 아닌 일반 Java 객체로 비지니스 로직을 구현하는 것의 장점에 대해 이야기했어. 우리는 사람들이 왜 그렇게 일반 객체 사용에 반대하는지 궁금했고, 그건 그럴 듯한 이름이 없기 때문이라고 결론지었어. 그래서 우리가 하나 지어줬지. 근데 그게 진짜 잘 먹혔더라고. - Martin Fowler
 {:.notice}

즉, 그냥 'Java 객체'라고 불러도 될 것을 사람들로 하여금 특별한 기술로 인식하도록 굳이 이름을 붙인 것이다. 그의 뜻을 따라 나도 POJO를 단순히 직역한 '간단한 오래된 방식의 자바 객체' 보다는 조금의 긍정적 뜻을 담아 '**전통적 순수 자바 객체**'라고 번역하고 싶다.🤓

POJO는 순수한 Java 객체 그 자체로, **Java가 본래 가지고 있는 가장 큰 특징인 객체지향적 개발**이 가능하도록 했다. 후에 탄생한 Spring은 POJO를 지원한다.

## Spring 고안
Rod Johnson이 EJB의 문제점을 지적하며 EJB 없이도 고품질의 확장 가능한 어플리케이션 개발이 가능하다는 것을 30,000 라인의 소스코드로 선보이며 [책](http://www.yes24.com/Product/Goods/798359)을 출간하였다. EJB로 고통받는 다른 개발자들에게 반응이 좋았다고 한다. Juergen Hoeller와 Yann Caroff가 Rod Johnson에게 오픈소스 프로젝트를 제안했다. Yan Caroff가 지은 이름 Spring은 '**EJB라는 추운 겨울을 지나 따뜻한 봄이 왔다**'라는 의미를 담고 있으며, 2004년 봄의 시작인 3월에 버전 1.0을 공식 배포되었다.

# 번외: JPA(Java Persistence API) 탄생 배경
JPA는 Java 진영의 표준 ORM 기술인데, 현재 널리 쓰이고 있는 Hibernate가 JPA 구현체 중 하나이다. 

Spring 이전에 EJB가 있었다면, Hibernate 이전에는 Entity Bean이 있었다. Entity Bean은 EJB가 지원하는 기능 중 하나였는데 이 또한 지옥이었는지 한 개발자가 앞장 서서 Hibernate라는 대안을 내놓았다. JPA는 Hibernate를 거의 복사+붙여넣기 해서 만들었다고 해도 과언이 아닐만큼 많은 부분 참고하여 만든 표준 인터페이스이다.


# 참고
- <https://javajee.com/ejb-programming-model-and-pojo-programming-model>
- <https://m.blog.naver.com/sillllver/220593543939>
- <https://martinfowler.com/bliki/POJO.html>
