---
title: "SOLID 원칙, 직접 예제 만들어 이해하기"
categories:
  - Design-Pattern
tags:
  - OOD
---

> 온라인 숍이라는 익숙한 도메인으로 SOLID 원칙의 예제를 만들어 보았다. 각각의 원칙을 전제 조건, 원칙을 위배하는 설계, 원칙을 만족하는 설계로 나누어 설명해보았다.

답답해서 직접 만든 예제🤓 혹시 틀린 부분, 개선할 부분이 있다면 댓글 남겨 주시면 감사하겠습니다. ('-')(,_,)
{:.notice--primary}

# 개요
Clean Code의 저자로 잘 알려진 Robert C. Martin이 2000년도 그의 논문 "Design Principles and Design Patterns"에 소개한 개념이다. 후에 Michael Feathers가 각 원칙의 첫 글자를 따서 `SOLID`라는 명칭을 만들었는데, Robert C. Martin도 이름이 있으니 대단한 원칙처럼 느껴진다며 `SOLID`라고 부르기 시작했다.

SOLID 원칙은 OOD(Object Oriented Design)를 위한 개념이다. 이 원칙을 따르면 가독성과 확장성이 좋고 유연하며 유지보수가 쉬운 소프트웨어를 설계할 수 있다. SOLID를 구성하는 각각의 원칙은 다음과 같다.

- S: Single Responsibility Principle(SRP)
- O: Open Closed Principle(OCP)
- L: Liskov Substitution Principle(LSP)
- I: Interface Segragation Principle(ISP)
- D: Dependency Inversion Principle(DIP)

참고로 "Design Principles and Design Patterns"에서는 무슨 영문인지 단일 책임 원칙에 대한 내용을 찾을 수 없었다. 하지만 Robert C. Martin의 한 [강연](https://www.youtube.com/watch?v=TMuno5RZNeE)을 보면 그가 단일 책임 원칙에 대해 설명하는 것을 볼 수 있다.

# Single Responsibility Principle(SRP, 단일 책임 원칙)
*A class should have one and only one reason to change.*   
클래스는 변경되어야 할 단 하나의 이유만을 가져야 한다.
{:.notice--primary}

## 전제 상황
```
|------|        |-------------|
| Shop |------> |    Order    |
|------|        |-------------|
                | + ship()    |
                | + cancel()  |
                | + retour()  |
                |-------------|
```

- `Order` 클래스는 배송(`ship()`), 주문 취소(`cancel()`), 반품(`retour()`)의 메서드를 가지고 있다.

## 원칙 위배
하나의 클래스가 세 개의 책임을 가지고 있으므로 단일 책임 원칙을 위배한다.


## 원칙 만족
```
                                           |------------------|
                                           | CancelDepartment |
                                       |---|------------------|
                                       |   | + cancel()       |
|------|        |-------------| <------|   |------------------|
| Shop |------> |    Order    |
|------|        |-------------| <------|   |------------------|
                | + ship()    |        |---| RetourDepartment |
                |-------------|            |------------------|
                                           | + retour()       |
                                           |------------------|
```
책임을 분산시켜 표현한다. (⚠️ 단일 책임 원칙만 적용했기 때문에 최선의 설계가 아니다.) 이제 반품 정책에 바뀌면 `RetourDepartment` 클래스에만 변경이 일어난다.

# Open Closed Principle(OCP, 개방 폐쇄 원칙)

*A module should be open for extension but closed for modification.*  
모듈은 확장에는 열려 있고, 변경에는 닫혀있어야 한다.
{:.notice--primary}

OOD의 모든 원칙들을 통틀어 가장 중요한 원칙이다. **모듈의 소스코드를 변경하지 않으면서 모듈이 하는 일을 변경할 수 있어야 한다.** 모순 같아 보이지만 **추상화(abstraction)**를 이용하면 실현 가능하다.

## 전제 상황
```
|------|        |----------------------|   |-----------------|
| Shop |------> |        Order         |   | <<enumeration>> |
|------|        |----------------------|   |   ShippingType  |
                | - type: ShippingType |   |-----------------|
                |----------------------|   | + DOMESTIC      |
                | + ship()             |   | + INTERNATIONAL |
                | + cancel()           |   |-----------------|
                | + retour()           |
                |----------------------| 
                   ^                ^      
                   |                |      
            |----------|     |---------------|
            | DOMESTIC |     | INTERNATIONAL |
            |  ORDER   |     |     ORDER     |
            |----------|     |---------------|                
```

```
public class Order {
  private ShippingType type;
  ...
  public void ship() {
    if (type == ShippingType.DOMESTIC) {
      // Domestic shipping policy
    } else if (type == ShippingType.INTERNATIONAL) {
      // International shipping policy
    }
  }
  ...
}
```
- `Order` 클래스는 배송 타입(`ShippingType`)을 변수로 가지고 있다.
- 현재 배송 타입에는 국내(`DOMESTIC`)와 국제(`INTERNATIONAL`)가 있다.
- 같은 대륙 내 배송에 대해 별도의 배송 정책을 적용하기 위해 대륙(`CONTINENTAL`)을 추가하려고 한다.
- 배송 타입에 따라 적용되는 배송 정책이 다르기 때문에 배송 처리 메서드(`ship()`)에서 if문으로 구분지어 표현하였다.

## 원칙 위배
```
|------|        |----------------------|   |-----------------|
| Shop |------> |         Order        |   | <<enumeration>> |
|------|        |----------------------|   |   ShippingType  |
                | - type: ShippingType |   |-----------------|
                |----------------------|   | + DOMESTIC      |
                | + ship()             |   | + INTERNATIONAL |
                | + cancel()           |   | + CONTINENTAL   |
                | + retour()           |   |-----------------|
                |----------------------|
                     ^      ^      ^               
           |---------|      |      |-------|         
           |                |              |         
      |----------|  |---------------| |-------------|      
      | DOMESTIC |  | INTERNATIONAL | | CONTINENTAL |
      |  ORDER   |  |     ORDER     | |    ORDER    |
      |----------|  |---------------| |-------------|
```
```
public class Order {
  private ShippingType type;
  ...
  public void ship() {
    if (type == ShippingType.DOMESTIC) {
      // Domestic shipping policy
    } else if (type == ShippingType.INTERNATIONAL) {
      // International shipping policy
    } else if (type == ShippingType.CONTINENTAL) {
      // Continental shipping policy
    }
  }
  ...
}
```
요구 사항을 반영하기 위해 `ShippingType`에 대륙 필드를 추가하고, 배송 메서드(`ship()`)에 if문을 추가하였다.

개방 폐쇄 원칙을 만족하려면 배송 타입이 추가되었을 때, 기존의 소스 코드를 변경하지 않고 확장하는 방식으로 구현이 가능해야한다. 하지만 위의 설계에서는 배송 타입이 추가될 때마다 `ship()` 메서드에 변경이 발생하므로 개방 폐쇄 원칙을 위배한다.

## 원칙 만족
```
                |---------------| 
|------|        | <<interface>> |   
| Shop |------> |     Order     |  
|------|        |---------------|  
                | + ship()      |   
                | + cancel()    |   
                | + retour()    |   
                |---------------|
                   ^    ^    ^        
        |----------|    |    |-----------| 
        |               |                |
  |----------|  |---------------| |-------------|     
  | DOMESTIC |  | INTERNATIONAL | | CONTINENTAL |
  |  ORDER   |  |     ORDER     | |    ORDER    |
  |----------|  |---------------| |-------------|

```


```
public interface Order {
  void ship();
  void cancel();
  void retour();
}

public class DomesticOrder implements Order {
    ...
    @Override
    public void processOrder() {
        // Domestic shipping policy
    }
}

public class InternationalOrder implements Order {
    ...
    @Override
    public void processOrder() {
        // International shipping policy
    }
}

public class ContinentalOrder implements Order {
    ...
    @Override
    public void processOrder() {
        // Continental shipping policy
    }
}
```

`Order` 인터페이스를 만들고 배송 타입에 따른 각각의 클래스를 만들어 인터페이스를 구현(`implements`)하였다. 각 클래스에서 `ship()` 메서드를 오버라이딩 해서 배송 정책을 각각 적용하였다. 이제 새로운 배송 타입이 추가되더라도 기존의 코드를 변경하지 않고 새로 클래스를 만들고 인터페이스를 구현하는 방식으로 확장이 가능하게 되었다. 


# Liskov Substitution Principle(LSP, 리스코프 치환 원칙)

*Subclasses should be substitutable for their base classes.*   
하위 클래스는 상위 클래스를 대체할 수 있어야 한다.
{:.notice--primary}

```
|------|        |-------|
| Shop |------> | Order |
|------|        |-------|
                    ^
                    |
              |--------------|    
              | OrderDerived |
              |--------------|
```
`Shop`이 `Order` 클래스를 사용하고 있고, `OrderDerived`는 `Order`로부터 파생된 것을 표현한 다이어그램이다. 리스코프 치환 원칙을 만족하려면 `Order`가 `OrderDerived`로 대체되더라도 `Shop`은 정상 기능해야한다.

상속 관계에서는 자식 클래스가 부모 클래스의 모든 것을 상속 받기 때문에 당연하다고 생각할 수도 있지만 고려해야할 문제가 있다. 바로 Circle/Ellipse Dilemma이다.

## Circle/Ellipse Dilemma(원과 타원 딜레마)
> `is a` 관계에 놓인 두 객체를 모델링할 때 발생하는 딜레마로, Square/Rectangle Dilemma(사각형과 직사각형 딜레마)라고도 부른다.

`모든 원은 타원이다`. 원은 두 초점이 같은 타원이기 때문에 원은 타원에 속한다고 말할 수 있다. 이를 상속 관계로 나타내면 아래의 다이어그램과 같다.

```
|---------|
| Ellipse |
|---------|
     ^
     |
|--------|
| Circle |
|--------|     
```

타원을 아래와 같이 정의했다고 가정해본다.
```
|-------------------------------|
|  Ellipse                      |
|-------------------------------|
| - fociA: Point                |
| - fociB: Point                |
| - majorAxis: Double           |
|-------------------------------|
| + getFociA(): Point           |
| + getFociB(): Point           |
| + getMajorAxis(): Double      |
| + setFoci(a: Point, b: Point) |
| + setMajorAxis(axis: Double)  |
|-------------------------------|
```

원은 타원을 상속하기 때문에 초점이 한 개만 필요함에도 불구하고 초점 변수 두 개를 가지게 된다. 오버헤드를 감수한다면 원의 `setFoci(Point a, Point b)` 메서드를 오버라이딩해서 두 개의 초점이 같은 값을 가지도록 수정하면 타원을 상속하면서 원으로써 기능하도록 구현할 수는 있다.
```
void Ellipse::SetFoci(const Point& a, const Point& b)
{
  itsFocusA = a;
  itsFocusB = b;
}

// Override
void Circle::SetFoci(const Point& a, const Point& b)
{
  itsFocusA = a;
  itsFocusB = a;
}
```

`Ellipse`를 이용한 다음 함수를 통해 위의 원과 타원의 설계가 리스코프 치환 원칙을 만족하는지 생각해본다.
```
void f(Ellipse& e)
{
  Point a(-1,0);
  Point b(1,0);
  e.setFoci(a,b);
  e.setMajorAxis(3);
  assert(e.getFociA() == a);
  assert(e.getFociB() == b);
  assert(e.getMajorAxis() == 3);
}
```
리스코프 치환 원칙을 만족하려면 `Ellipse`를 `Circle`로 바꿨을 때 함수가 정상적으로 작동해야한다. 하지만 `Circle`로 바꾸면 두 번째 assert문인 `assert(e.getFociB() == b)`에서 에러가 난다. 

즉, **상속 관계에 있다고 해서 항상 리스코프 치환 원칙이 만족되는 것은 아니다.** 리스코프 치환 원칙을 만족하기 위해서 자식 클래스는 부모 클래스의 명세를 반드시 지켜야한다. 위의 예시에서는 `Circle`이 `Ellipse`의 "초점은 두 개이다."라는 명세를 지키지 않았다. 명세에서 다음 두 가지 조건이 충족되면 상속 관계에서 리스코프 치환 원칙이 만족된다고 할 수 있다.

1. 자식 클래스의 선행 조건(precondition)이 부모 클래스의 메서드보다 강하지 않다.
2. 자식 클래스의 후행 조건(postcondition)이 부모 클래스의 메서드보다 약하지 않다.

*\*선행 조건(precondition): 메서드가 호출되기 전에 참이어야 하는 것*  
*\*후행 조건(postcondition): 메서드가 완료된 후에 참이어야 하는 것*


위의 함수를 다음과 같이 수정하면 리스코프 치환 원칙을 만족하게 만들 수는 있다. 하지만 소스 코드의 변경은 또 다시 개방 폐쇄 원칙을 위반하게 한다. 즉, **리스코프 치환 원칙의 위반은 곧 개방 폐쇄 원칙의 위반으로 이어진다.**
```
void f(Ellipse& e)
{
  if (typeid(e) == typeid(Ellipse)) {
    Point a(-1,0);
    Point b(1,0);
    e.setFoci(a,b);
    e.setMajorAxis(3);
    assert(e.getFociA() == a);
    assert(e.getFociB() == b);
    assert(e.getMajorAxis() == 3);
  }
  else {
    throw NotAnEllipse(e);
  }
}
```


# Interface Segragation Principle(ISP, 인터페이스 분리 원칙)

*Many client specific interfaces are better than one general purpose interface.*   
특정 클라이언트만을 위한 인터페이스 여러 개가 하나의 범용 인터페이스보다 낫다.
{:.notice--primary}


## 전제 상황
```
|--------|
| Shop A |------|        |---------------|
|--------|      |------> | <<interface>> |   
                         |     Order     |
                |        |---------------|
|--------|      |------> | + ship()      |
| Shop B |------|        | + cancel()    |    
|--------|               | + detour()    |
                         |---------------|
```
- `Shop A`와 `Shop B` 모두 `Order` 인터페이스를 구현하여 사용하고 있다. 
- `Shop A`가 예약 배송(`schedule()`) 기능 추가를 요구했다. 
- `Shop B`는 예약 배송을 지원하지 않는다.

## 원칙 위배
```
|--------|
| Shop A |------|        |---------------|
|--------|      |------> | <<interface>> |
                         |     Order     |
                |        |---------------|
|--------|      |------> | + ship()      |
| Shop B |------|        | + cancel()    |    
|--------|               | + detour()    |
                         | + schedule()  |
                         |---------------|
```
Order 인터페이스에 schedule() 메서드를 추가해 요구 사항을 반영했다. 인터페이스 분리 원칙을 만족하려면 **인터페이스는 클라이언트로 하여금 불필요한 메서드를 구현하도록 강요하지 않아야한다.** 하지만 위의 예제에서 `Shop B`는 예약 배송 기능을 지원하지 않음에도 불구하고 해당 메서드를 구현해야한다.

## 원칙 만족
```
                |----------------|
                | <<interface>>  |  
|--------|      |   Schedulable  |
| Shop A |------|----------------|------|     |---------------|
|--------|      | + schedule()   |      |     | <<interface>> |
                |----------------|      |---> |     Order     | 
                                              |---------------|
                                        |---> | + ship()      |
|--------|                              |     | + cancel()    |
| Shop B |------------------------------|     | + detour()    |
|--------|                                    |---------------|
                                         
```
모든 클라이언트의 요구 사항을 하나의 인터페이스로 만드는 것보다 특정 클라이언트만을 위한 인터페이스를 만들게 되더라도 인터페이스를 분리하여야 한다.

# Dependency Inversion Principle(DIP, 의존관계 역전 원칙)

*Depend upon Abstractions. Do not depend upon concretions.*   
구체화가 아닌 추상화에 의존해야한다.
{:.notice--primary}

개방 폐쇄 원칙이 OO 아키텍처의 목표를 나타낸다면, 의존관계 역전 원칙은 주요 원리를 나타낸다. 의존관계 역전 원칙은 구체적인 함수나 클래스에 의존하기보다는 인터페이스나 추상적 함수, 추상적 클래스에 의존해야한다는 것이다.

## 전제 상황
```
        |------|
        | Shop |
        |------|    
            |
            v
     |--------------|
     | OrderService |
     |--------------|
       |          |
       v          v
|----------|   |------|
| Domestic |   | User |
|   Order  |   |------|
|----------|     
```
```
public class OrderService {
  private DomesticOrder Order;
  private User user;

  OrderService(DomesticOrder order, User user) {
    domesticOrder = new DomesticOrder();
    user = user;
  }
}
```
- `Shop`이 `OrderService`를, `OrderService`는 `DomesticOrder`와 `User` 클래스에 의존하고 있다. 
- `Shop`이 이제 국제 배송을 지원해 `InternationOrder`를 추가해야한다.

## 원칙 위배
```
             |------|
             | Shop |
             |------|    
                 |
                 v
          |--------------|
          | OrderService |
          |--------------|
           |    |      |
      |----|    |      |----------| 
      v         v                 v
|----------|  |---------------|  |------|
| Domestic |  | International |  | User |
|   Order  |  |     Order     |  |------|
|----------|  |---------------|
```
```
public class OrderService {
  private DomesticOrder domesticOrder;
  private InternationalOrder internationalOrder;
  private User user;

  OrderService(DomesticOrder domesticOrder, User user) {
    domesticOrder = new DomesticOrder();
    internationalOrder = null;
    user = user;
  }

  OrderService(InternationalOrder internationalOrder, User user) {
    internationalOrder = new InternationalOrder();
    domesticOrder = null;
    user = user;
  }
}
```
최상위 모듈 Shop은 어플리케이션 상위 정책들을 다룬다. 이 상위 정책들은 일반적으로 세부 구현 사항에 크게 관심을 갖지 않는다. 그럼에도 불구하고 상위 모듈이 하위 모듈에 의존하는 순차적 설계에서는 최상위 모듈이 세부 구현 사항을 다루는 최하위의 모듈에 직접적으로 의존한다.

요구 사항을 반영한 위 설계는 `OrderService`가 구체적 클래스인 `DomesticOrder`와 `InternationalOrder`에 직접적으로 의존하고 있어 의존관계 역전 원칙을 위배한다.

## 원칙 만족
```
              |------|
              | Shop |
              |------|    
                  |
                  v
            |--------------|
            | OrderService |
            |--------------|
               |          |
               v          v
    |---------------|    |---------------|
    | <<interface>> |    | <<interface>> |
    |     Order     |    |      User     |
    |---------------|    |---------------|
      ^          ^                   ^
      |          |                   |
|----------|  |---------------|   |------|
| Domestic |  | International |   | User |
|   Order  |  |     Order     |   |------|
|----------|  |---------------|
```
```
public interface Order() {...}

public class DomesticOrder implements Order {...}
public class InternationalOrder implements Order {...}
```
```
public class OrderService {
  private Order order;
  private User user;

  OrderService(Order order, User user) {
    order = new Order();
    user = user;
  }
}
```
`Order` 인터페이스를 만들고 `DomesticOrder`와 `InternationalOrder` 클래스에서 인터페이스를 구현한다. 상위 모듈 뿐만 아니라 하위 구현 클래스도 인터페이스에 의존하는 것을 **의존관계의 역전**이라고 표현한다. (위 다이어그램에서 화살표 방향 참고)

의존관계를 역전해야하는 이유는 간단하다. **구체적인 것에 비해 추상적인 것은 변경이 훨씬 적게 발생**하고, **추상적인 것은 변경 없이 설계를 바꾸는 것이 가능**하기 때문이다. 이는 곧 개방 폐쇄 원칙으로 이어진다.

# 참고
- <http://staff.cs.utu.fi/~jounsmed/doos_06/material/DesignPrinciplesAndPatterns.pdf>
- <https://www.baeldung.com/solid-principles>
- <https://www.youtube.com/watch?v=TMuno5RZNeE>