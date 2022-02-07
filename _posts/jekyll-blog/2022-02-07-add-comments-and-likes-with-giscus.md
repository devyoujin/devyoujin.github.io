---
title: "[Jekyll Blog] 댓글&좋아요 기능 추가하기(feat. Giscus)"
categories:
  - Jekyll-Blog
tags:
  - Jekyll
  - Blog
  - Github-Pages
---

> 💎Jekyll + Github Pages로 개발 블로그 만들기 / Minimal-Mistakes 테마 커스터마이징하기💎

# [1] 💎 Giscus 소개
Giscus는 Github Discussion을 기반으로 하는 프로그램이다. [Github discussion search API](https://docs.github.com/en/graphql/guides/using-the-graphql-api-for-discussions#search)를 이용하여 사용자가 선택한 **맵핑 방식**에 따라 `pathname`이나 `url` 혹은 `title`로 연관된 discussion을 찾고 없으면 Giscus Bot🤖이 새로 생성한다.


# [2] 💎 Giscus로 바꾼 이유
1. `Discussion` 글 자체에 누를 수 있는 reaction도 제공하는데 이를 좋아요 기능처럼 사용할 수 있기 때문이다. (이 기능을 사용하려면 기능 탭에서 `메인 포스트에 반응 남기기`에 체크해야한다.)
2. 커스텀 테마를 지원하기 때문이다.
2. '댓글'이라는 특성 자체가 `Issue`보다는 `Discussion`에 더 적합할 것 같았기 때문이다.
3. 나는 댓글 수가 제로였기 때문에😅 해당사항이 없지만 `Issue`를 `Discussion`으로 마이그레이션 할 수 있다고 한다.

# [3] 💎 Giscus 설정 및 적용
Giscus는 [한국어 공식 문서](https://giscus.app/ko)를 제공하고 있기 때문에 크게 어렵지 않게 진행할 수 있다.

내가 설정한 값들은 아래와 같다.
- Discussion 맵핑 방식: `pathname(경로)`
- Discussion 카테고리: 권장사항 처럼 Announcements 타입/`이 카테고리에서만 discussion 찾기`에 체크
- 기능: `메인 포스트에 반응 남기기`, `댓글 위에 댓글 상자 배치`에 체크
- 테마: Github Light

Discussion 맵핑 방식이나 script 코드를 적용하는 방식은 Utterances와 동일하다. 이전에 작성한 [[Jekyll Blog] 댓글 기능 추가하기(feat. Utterances)](https://dev-ujin.github.io/jekyll-blog/add-comments-with-utterances)에 자세하게 설명해두었니 참고할 수 있다.

조만간 블로그에 어울리는 💜보라보라한 테마💜를 하나 만들어봐야겠다.
