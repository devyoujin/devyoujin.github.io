---
title: "[Java Live Study] 1. JVM Architecture"
categories:
  - Java-Study
tags:
  - ☕Java
  - Java-Live-Study
---

> ⚓[백기선 강사님의 live study](https://github.com/whiteship/live-study)에 나온 주제들을 혼자 공부하고 정리하여 작성한 글입니다.⚓

📌 **1주차 목표**: Java 소스 파일(`.java`)을 JVM으로 실행하는 과정 이해하기

# [1] JVM이란?
<u>Java Virtual Machine</u>의 약자로 <u>자바 가상 머신</u>이라고 불린다.

컴퓨터가 이해할 수 있는 것은 0과 1로 이루어진 2진수의 기계어이다. 인간이 작성하는 **소스 코드를 컴퓨터가 이해하는 언어인 <u>기계어(Machine Code)</u> 혹은 <u>바이너리 코드(Binary Code)</u>로 변환하는 과정**을 <u>컴파일(Compile)</u>이라고 한다.

운영체제마다 요구하는 기계어가 다르기 때문에 Windows에서 컴파일해서 변환된 기계어를 Linux는 이해하지 못한다. 하지만 **JVM은 어떤 운영체제에서든 프로그램을 실행할 수 있도록 해준다.** <u>"Write Once. Run Anywhere."</u> JVM의 짧은 이 슬로건이 위 설명을 대신해준다. 

# [2] JVM 환경에서의 Compile & Execution
## C와 Java 비교
C와 Java로 작성된 각각의 소스 코드가 컴파일되고 실행되는 과정을 비교해본다.
![C와 Java에서 컴파일&실행]({{ site.url }}{{ site.baseurl }}/assets/img/java-live-study/compile-and-execution-in-c-and-java.jpg)
- **C**: **컴파일러**가 <u>소스 코드</u>(`.c`)를 <u>기계어를 포함하는 오브젝트 파일</u>(`.obj`)로 변환한다. **링커**가 오브젝트 파일을 통합해 하나의 <u>실행가능한 파일</u>(`.exe`)로 만든다.
- **Java**: **컴파일러**가 <u>소스 코드</u>(`.java`)를 <u>바이트코드를 포함하는 클래스파일</u>(`.class`)로 변환한다 

## 직접 해보기
Hello World 프로그램을 작성하고 터미널을 통해 직접 컴파일하고 실행해본다.
### Java 코드 작성하기
🔽 HelloWorld.java
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

### 컴파일하기
```terminal
javac HelloWorld.java
```
에러 없이 성공했다면 같은 위치에 `HelloWorld.class`가 만들어진다.

### 실행하기
```terminal
java HelloWorld
```

🛑**java.lang.ClassNotFoundException**🛑: HelloWorld.class를 찾을 수 없을 때 `ClassNotFoundException`이 발생한다.   1️⃣`.class`파일이 정말 만들어졌는지 확인해본다.
2️⃣해당 파일이 있는 디렉토리에서 명령어를 실행한 것이 맞는지 확인해본다.
3️⃣1번도 2번도 아니라면 `java -cp [class 파일이 있는 경로]` 명령어로 classpath를 명시하여 실행해본다.
{: .notice--danger}


# [3] Byte Code(바이트코드)
바이트코드는 <u>JVM이 이해할 수 있는 언어</u>이다. **바이트코드를 JVM 위에서 실행하면, 실행환경에 맞추어 JVM이 바이트코드를 알맞은 형태의 기계어로 변환해준다.** Java뿐 만 아니라 Groovy, Scala, Clojure 등 바이트코드로 컴파일이 가능한 언어라면 어느 운영체제 환경이던지 JVM이 설치되어 있기만 하면 해당 언어로 작성한 프로그램을 어디서든 실행할 수 있게 된다.

# [4] JVM 환경 전체 프로세스
![Java 전체 과정]({{site.url}}{{stie.baseurl}}/assets/img/java-live-study/java-entire-process.jpg)

JVM이 어떤 구조인지는 아래에서 자세히 설명할 것이기 때문에 이를 제외하고 특징을 나열해본다.
- <u>컴파일타임</u>과 <u>런타임</u>으로 나뉘어져 있고, JVM은 런타임에 속해 있다.
- **컴파일타임**에서는 Java 소스 코드(`.java`)를 `javac` 명령어를 사용해 바이트코드(`.class`)를 변환한다.
- **런타임**에서는 바이트코드(`.class`)를 `java` 명령어를 사용해 JVM이 실행환경에 알맞게 해석하도록 한다.  

# [5] JVM 구성
JVM은 Class loader, Runtime data area, Execution engine 세 가지 영역으로 구성되어 있다.
![JVM 구성]({{site.url}}{{site.baseurl}}/assets/img/java-live-study/jvm-architecture.jpg)

## Class Loader
### Loading
Loading은 세 종류의 class loader에 의해 진행된다.
1. **Bootstrap class loader**: 미리 컴파일된 신뢰할 수 있는 클래스 파일이 들어 있는 `RT.jar`에서 클래스 파일을 메모리로 로드한다.
2. **Extension class loader**: 추가적인 클래스 파일을 `/jre/lib/ext/`에서부터 메모리로 로드한다.
3. **Application class loader**: 프로그래머가 작성한 어플리케이션 파일을 메모리로 로드한다.

### Linking
Linking은 세 단계로 구성된다.
1. **Verify**: 바이트코드 클래스 파일이 표준에 부합하는지 검증한다.
2. **Prepare**: 정적 변수를 위한 메모리가 할당되고, 변수의 디폴트 값이 지정된다.
3. **Resolve**: symbolic reference가 actual reference로 교체된다.(실제 물리적인 메모리 주소를 가리키게 된다.)

🎓**Symbolic Reference**🎓: symbolic reference는 논리적 참조이다. 즉, 객체가 참조하는 실제 메모리 주소를 가리키는 것이 아니라 객체 자체를 반환한다.
{: .notice--info}

### Initialization
- 정적 변수에 실제 값이 할당된다.
- Static initializer(정적 초기자)가 실행된다.

🎓**Static Initializer**🎓: static initializer는 프로그램을 실행할 때 단 한 번만 실행이 된다. 1️⃣클래스의 객체를 생성하거나, 2️⃣객체가 아직 생성되지 않았더라도 static 멤버 변수나 static 멤버 함수에 최초 접근할 경우가 해당된다.
{: .notice--info}

## Runtime Data Area
- **Method Area**: 클래스 데이터가 여기 저장된다. (`Class Employee{...}`)
- **Heap Memory**: 객체와 인스턴스 변수가 저장된다. (`new Employee()`)
- **Stack Memory**: 지역 변수, 연산자 스택, 프레임 데이터(예외 발생, 일반 메서드 반환 등 담당)가 저장된다.
- **PC Register**: 현재 실행되는 명령어가 저장된다.
- **Native Method Stacks**: 네이티브 메서드에 대한 정보가 저장된다.

## JVM Execution Engine
- **Interprter**: 클래스 파일이나 바이트코드를 한줄씩 읽는다. 문제는 같은 메서드가 여러 번 호출되면, 인터프리터는 해당 줄을 도 다시 해석한다.
- **JIT(Just In Time) compiler**: 인터프리터의 문제를 극복하는 것을 돕는다. 메서드가 반복적으로 호출되면 JIT 컴파일러는 바이트코드를 네이티브 코드로 컴파일한다. 이 네이티브 코드는 반복적으로 호출되는 메서드에 바로 사용된다.
  - **Intermediate code generator**: 중간 코드 생성한다.
  - **Code optimizer**: 중간 코드의 성능을 개선한다.
  - **Target code generator**: 중간 코드를 네이티브 코드로 변환한다.
  - **Profiler**: 반복적으로 호출되는 지점을 찾는다.
- **Garbage collector**: 더이상 사용하지 않는 객체를 제거한다.
- **Java native method interface**: 네이티브 라이브러리와 상호작용하여 JVM 실행 엔진이 이를 사용할 수 있도록 한다.

# [6] JRE와 JDK
- **JRE(Java Runtime Environment)**: JVM + 표준 라이브러리
- **JDK(Java Development Kit)**: JRE + 개발자를 위한 도구(javac, jdb, jar 등)
- 프로그램 실행하기 위해서는 JRE만 설치해도 충분하지만, 개발을 목표로 한다면 JDK를 설치해야한다.
- Java 언어 자체는 무료이지만, JDK는 어느 것을 사용하느냐에 따라 무료로 사용할 수도 있고, 유료로 사용해야할 수도 있다. (Oracle JDK는 상업적으로 이용 시 유료, Open JDK는 무료 등)

# 참고
- <https://www.youtube.com/watch?v=QHIWkwxs0AI>
- <https://www.youtube.com/watch?v=G1ubVOl9IBw>
- <https://blog.jamesdbloom.com/JVMInternals.html>