---
title: "[IntelliJ] 외부 라이브러리 import하기"
categories:
  - Tool
tags:
  - IntelliJ
  - 🔨Tool
---

> 인텔리제이 빌더를 사용하는 일반 프로젝트에서 외부 라이브러리를 추가하는 방법

🚧 네이티브 IntelliJ IDEA 빌더를 사용하는 프로젝트에서 유효한 방법이다. Maven이나 Gradle 같은 빌드 툴을 사용한다면, 빌드 파일을 통해 라이브러리를 추가할 수 있다.
{: .notice--warning}

두 가지 방법이 있다.
- 방법 1) jar 파일을 직접 다운로드 받아 프로젝트에 추가하기(혹은 직접 만들어서 jar 파일로 export한 라이브러리를 다른 프로젝트에서 사용하려고 할 경우)
- 방법 2) Maven을 통한 웹 검색으로 프로젝트에 주입하기

# [1] 라이브러리 얻기
[MVNRepository](https://mvnrepository.com/)에서 필요한 라이브러리를 검색하고 버전을 선택한다. 나는 예시로 `json simple`을 검색하고, `1.1.1`버전을 선택했다.

![MVNRepository]({{ site.url }}{{ site.baseurl }}/assets/img/intellij/intellij-mvnrepository-library.jpg)

- 방법 1) `jar` 혹은 `bundle`을 눌러 jar 파일을 다운로드 한다.
- 방법 2) dependency의 `groupId`와 `version`을 복사한다.


# [2] 프로젝트에 라이브러리 등록하기
IntelliJ > File > Project Structure > 왼쪽 메뉴에서 Libraries > `+` 버튼

- 방법 1) `Java` 선택 > 다운로드 받은 jar 파일 선택
- 방법 2) `From Maven` 선택 > 복사한 라이브러리 `groupId` 혹은 `groupId:version` 형태로 입력 > 🔍검색 버튼 > OK

- 여러 개의 모듈이 있는 경우에 라이브러리를 등록하고 나면 라이브러리를 적용할 모듈을 선택하라고 나온다. 여러 개의 모듈을 선택할 수도 있다.
- 등록된 라이브러리는 프로젝트 폴더 밑 `.idea` > `libraries` 에서 확인할 수 있다.
- 방법 1을 선택하여 jar 파일로 라이브러리를 등록한 경우, 파일을 삭제하면 IntelliJ에서도 삭제된다.

# [3] 라이브러리 관리하기
> 라이브러리를 등록한 시점 이후에 추가된 라이브러리를 해제하거나 추가로 다른 모듈에 라이브러리를 적용하고 싶은 경우

- 하나의 모듈에 대해서 라이브러리 관리할 때: IntelliJ > File > Project Structure > <u>Modules</u> > 모듈 선택 > Dependencies > `+` 버튼 > Library > 라이브러리 선택
- 여러 개의 모듈에 대해서 한 번에 라이브러리 관리할 때: Intellij > File > Project Structure > <u>Libraries</u> > 라이브러리에 마우스 오른쪽 클릭 > Add to Modules > 모듈 선택(다중 선택 가능)

🎓 정리하자면, **라이브러리 자체를 등록하고 삭제**할 때에는 `Libraries` 탭에서! **등록된 라이브러리를 모듈에 추가하고 삭제**하는 것은 `Modules` 혹은 `Libraries` 탭에서 가능하나, 여러 개의 모듈에 한꺼번에 적용하고 싶을 때에는 Libraries 탭에서 하는 것이 효율적이겠다!
{: .notice--info}

# 참고
- [IntelliJ Docs - Libraries](https://www.jetbrains.com/help/idea/library.html#define-library)

인텔리제이에서 라이브러리를 추가할 수 있는 경로도 여러가지고 추가할 수 있는 레벨도 여러가진데 요건 따로 공부해서 정리해야겠다.🤓

