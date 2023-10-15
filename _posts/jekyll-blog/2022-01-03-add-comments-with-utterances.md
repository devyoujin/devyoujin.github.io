---
title: "[Jekyll Blog] 댓글 기능 추가하기(feat. Utterances)"
categories:
  - Tools
  - Jekyll-Blog
tags:
  - jekyll
  - blog
  - github_pages
---

> 💎Jekyll + Github Pages로 개발 블로그 만들기 / Minimal-Mistakes 테마 커스터마이징하기💎

# [1] 🔮 Utterances 소개
## 특징
- 오픈 소스다. -> 직접 테마 만들어서 블로그에 적용도 하고 오픈 소스에 기여도 할 수 있다!🤓
- 가볍다.
- 광고 없이 무료다.

## 동작방식
- Github Issue 기반으로 모든 댓글 데이터가 Github Issue에 저장된다.
- [Github issue search API](https://docs.github.com/en/rest/reference/search#search-issues)를 이용하여 사용자가 선택한 **이슈 맵핑 방식**에 따라 `url`이나 `pathname` 혹은 `title`로 연관된 이슈를 찾고 이슈가 없으면 Utterance bot🤖이 새로 생성해준다.

# [2] 🔮 Utterances 설정
[Utterances 공식페이지](https://utteranc.es/)에서 옵션을 선택하면 소스 코드를 제공해준다.

1. Github App으로 등록되어 있는 **[Utterances 설치](https://github.com/apps/utterances)**를 진행한다.
2. 댓글이 저장될 **Github Repository를 준비**하고 다음을 확인한다.
    - Repository는 **public**이어야한다.  
    (블로그 소스가 저장된 repository가 private일 경우, repository를 새로 하나 만든다.)
    - 테마를 **fork**해서 만든 블로그라면, **Github Issues가 활성화**되어 있는지 확인한다.  
    (Github Repository > Settings > Options > Features > ✅ Issues)
3. **Issue Mapping 방식**을 선택한다.
    > 나는 변경 가능성이 제일 적을 것 같은 **pathname**을 선택했다.
    - **Issue title contains page pathname**: 블로그 포스트의 URL 컴포넌트와 매칭된다.(예: `category/title`)
    - **Issue title contains page URL**: 블로그 포스트 URL 전체에 매칭된다.(예: `https://username.github.io/category/title`)
    - **Issue title contains page title**: 블로그 포스트 제목에 매칭된다.
    - **Issue title contains page og:title**: 페이지의 오픈 그래프 타이틀 메타데이터에 매칭된다.
    - **Specific issue number**: 특정 이슈 번호에 매칭된다. 이슈가 자동으로 생성되지 않는다.
    - **Issue title contains specific term**: 특정 키워드에 매칭된다. 이슈 제목은 설정한 키워드로 생성된다.
4. (선택사항) **Label을 설정**한다.
    - Utterances bot🤖이 이슈를 새로 생성할 때 라벨을 붙여주도록 설정할 수 있는데, **이미 존재하는 라벨만 설정이 가능**하므로, 아직 라벨을 안 만들었다면 Github Issue에서 먼저 만들어준다.
5. **테마를 선택**한다.
6. 생성된 **script 코드**를 복사한다.


# [3] 🔮 Utterances 적용
[2]에서 복사한 script 코드를 적용하는 방식은 블로그 테마에 따라 다양하다. 이론적으로는 포스트의 레이아웃이 되는 html 파일의 `<head>...</head>` 태그 사이에 넣어주면 된다. 하지만 지킬 테마 자체에서 Utterances를 사용할 수 있도록 제작된 테마같은 경우, `_config.yml`에서 설정할 수 있다. 내가 사용중인 **Minimal Mistakes 테마** 또한 `_config.yml`에서 설정이 가능하다.

🔽 _config.yml
```yml
comments:
  provider               : utterances
  utterances:
    theme                : "github-dark-orange"
    issue_term           : "pathname"
    label                : "comment"
```

# 참고
- [Utterances Docs](https://utteranc.es/)

