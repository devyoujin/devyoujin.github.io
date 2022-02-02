---
title: "[Jekyll Blog] favicon 생성 및 설정"
categories:
  - Jekyll-Blog
tags:
  - Jekyll
  - Blog
  - Github-Pages
---

> 💎Jekyll + Github Pages로 개발 블로그 만들기 / Minimal-Mistakes 테마 커스터마이징하기💎

# [1] favicon 생성
favicon 설정을 쉽게 도와주는 사이트들이 있다.
- [favicon.io](https://favicon.io/): 이미지뿐만 아니라 텍스트나 이모지도 파비콘으로 바꿔주는 사이트
- [realfavicongenerator](https://realfavicongenerator.net/): 이미지를 파비콘으로 바꿔주고 html 코드를 제공해주는 사이트

나는 이미지를 직접 만들었기 때문에 첫 번째 사이트는 필요하지 않았지만, 간단하게 텍스트나 이모지를 선택해 파비콘으로 만들고자 한다면 유용할 것 같다.🙃

realfavicongenerator에서는 웹 브라우저뿐만 아니라 모바일 아이콘, 데스크탑 아이콘으로 어떻게 표현되는지까지 미리보기로 보여주고, 배경색상도 설정할 수 있다.

주의해야할 건 마지막 부분에 파비콘 경로 설정 부분이다. 만약 파비콘을 루트에 저장할 것 아니라면 경로를 설정해주어야한다. 나는 `recommended`를 무시하고 두 번째 것을 선택하고 경로를 `assets/img/favicon`로 설정하였다.

![favicon 경로]({{ site.url }}{{ site.baseurl }}/assets/img/jekyll-blog/path-to-favicon.png)

# [2] favicon 적용

1. 다운로드 받은 파비콘 압축을 풀어 위에서 지정한 경로에 옮긴다.
2. 생성된 html 코드를`<head>...</head>`사이에 붙여넣는다.

지킬 블로그는 큰 뼈대 구조는 똑같지만 테마에 따라 파일 구조가 조금씩 다르기 때문에 해당하는 부분을 잘 찾아서 넣어주어야 한다. 보통 `_includes` 디렉토리 밑에 `header.html` 혹은 `head.html`일 가능성이 높다.

내가 사용하는 `minimal-mistakes` 테마 같은 경우에는 `_includes/head/custom.html`에 붙여넣으면 된다.

# [3] favicon 적용 확인
Github에 push하기 전에 Jekyll server만 켜도 확인할 수 있다. 타-다!🎉

```
bundle exec jekyll serve
```