---
title: "[VSCode] Leetcode 확장 프로그램"
categories:
  - VSCode
tags:
  - VSCode
  - 🔨Tool
---

> ✨ Visual Studio Code Extension for Leetcode ✨

요즘 Leetcode를 열심히 푸는데,,, 풀려고 출석은 매일 하는데,,, 마침 우연히 Github 추천 레포지토리에 떠서 다운받게 된 Extension이다. 너무 멋진 프로그램이라 소개해보고자 한다.🙆‍♀️
{: .notice}

# [1] 다운로드
- Visual Studio Code에서 Extensions에 `Leetcode`라고 검색하면 여러개가 나오는데 나는 다운로드수가 제일 많은 걸로 선택해서 받았다.
- [해당 확장 프로그램 Github 페이지](https://github.com/LeetCode-OpenSource/vscode-leetcode)

# [2] 실행
## 로그인
우선 로그인을 해야 메뉴를 둘러볼 수 있다.

좌측에 `Leetcode 로고` 선택하고, Explorer 상단에 `대문버튼🚪`을 눌러 로그인한다. **Leetcode 계정뿐만 아니라 Github이나 Linkedin 계정**으로도 로그인할 수 있다.
![VSCode Leetcode 로그인]({{ site.url }}{{ site.baseurl }}/assets/img/vscode/vscode-leetcode-plugin.jpg)

## 메뉴 구성
![VSCode Leetcode Overview]({{ site.url }}{{ site.baseurl }}/assets/img/vscode/vscode-leetcode-plugin-overview.jpg)
커뮤니티 제외하고 Leetcode 홈페이지에서 문제풀 때 제공하는 기능 대부분이 지원된다.
- `Explorer`란에 **난이도, 주제, 회사로 분류**가 되어있다. Leetcode 홈페이지에서는 문제마다 회사를 확인하려면 프리미엄 구독을 해야하는데 플러그인에서 제공하는 게 신기했다. 버근가...

- 제출해서 통과한 문제 옆에는 **녹색체크**✅가 표시되고, **하트**🤍를 누르면 `Favorite`폴더에서 따로 관리할 수 있다.

- 문제 하나를 클릭해서 `Code Now` 버튼을 클릭하면 풀이를 시작할 수 있다. 소스코드가 파일 단위로 만들어지기 때문에 파일이 저장되는 폴더를 Github Repository로 관리하고자 할 때 쉽게 직관적으로 가능하다. 

- 하단 바에 `LeeCode:아이디` 클릭하면 **세션을 관리**할 수 있다.

## 테스트&제출
테스트 혹은 제출 버튼은 소스 코드 작성하는 곳 밑에 주석처럼 존재하고 있다.
![VSCode Leetcode 제출&테스트 버튼]({{ site.url }}{{ site.baseurl }}/assets/img/vscode/vscode-leetcode-plugin-submit-test-buttons.jpg)

Leetcode 홈페이지에서처럼 테스트 케이스를 직접 입력해서 테스트해볼 수 있다.
![VSCode Leetcode 테스트]({{ site.url }}{{ site.baseurl }}/assets/img/vscode/vscode-leetcode-plugin-test.jpg)

제출해서 통과하면 제출 결과도 보여준다.
![VSCode Leetcode 제출]({{ site.url }}{{ site.baseurl }}/assets/img/vscode/vscode-leetcode-plugin-submission.jpg)