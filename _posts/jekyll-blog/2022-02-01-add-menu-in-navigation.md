---
title: "[Jekyll Blog] 네비게이션 메뉴 추가하기 (카테고리와 태그 메뉴 만들기)"
categories:
  - Jekyll-Blog
tags:
  - 🧪Jekyll
  - 💜Blog
  - Github-Pages
---

> 💎Jekyll + Github Pages로 개발 블로그 만들기 / Minimal-Mistakes 테마 커스터마이징하기💎

> 상단 네비게이션 바에 카테고리와 태그 메뉴를 추가하는 방법을 알아본다. 응용하여 자기소개, 포트폴리오 등 원하는 메뉴를 추가해도 좋을 것 같다.🌻


# [1] Navigation에 등록
`_data/navigation.yml`에 메뉴 이름과 눌렀을 때 연결될 url을 작성해준다.

🔽 navigation.yml
```yml
main:
  - title: "Category"
    url: /categories
  - title: "Tag"
    url: /tags
    ...
```
메뉴에 `Category` 버튼을 누르면 `https://{블로그 주소}/categories`로 연결된다는 의미인데, 해당 페이지를 아직 만들지 않았기 때문에 404 에러가 화면에 보일 것이다.


# [2] Page 만들기
1. 루트 경로 밑에 `_pages` 디렉토리를 만든다.
2. `_pages` 밑에 원하는 이름으로 `.md`파일을 만든다. (나는 `category_archive.md`, `tag_archive.md`로 지정했다.)
3. 아래 코드를 붙여 넣는다.

🔽 category_archive.md
```html
---
title: "Category"
layout: categories
permalink: /categories
author_profile: true
---
```

🔽 tag_archive.md
```html
---
title: "Tag"
layout: tags
permalink: /tags
author_profile: true
---
```

- `title`: 블로그에서 `Category` 메뉴를 눌렀을 때 화면에 보여진다.
- `layout`: minimal-mistakes 같은 경우에는 이미 `_layouts`에 구현이 다 되어있기 때문에 layout으로 지정만 해주면 된다.
- `permalink`: <u>[[1]](#1-menu-등록)에서 `url`에 적은 값과 같은 값을 넣어줘야한다.</u>
- `author_profile`: Category나 Tag 페이지에서도 좌측 프로필이 보여지게 할 것인지에 대한 여부이다.