---
title: "[Jekyll Blog] 블로그 시작하기"
categories:
  - Jekyll-Blog
tags:
  - Jekyll
  - Blog
  - Github-Pages
---

> 💎Jekyll + Github Pages로 개발 블로그 만들기💎

# [1] Ruby 설치하기

> 윈도우 환경을 기준으로 작성하였다. 다른 운영체제에서의 설치 방법은 [Jekyll Installation](https://jekyllrb.com/docs/installation/)에서 자세히 확인할 수 있다.

Jekyll를 사용하려면 아래의 세 가지가 먼저 필요하다.
  1. Ruby (2.5.0 버전 이상)
  2. RubyGems
  3. GCC와 Make

1. [Ruby Installer](https://rubyinstaller.org/downloads/)에서 <u>2.5.0 버전 이상</u>의 **Ruby+Devkit**을 다운받는다. (**Ruby+Devkit**으로 설치하면 위에 언급한 세 가지를 한 큐에 다운받을 수 있다.)
2. Ruby 설치가 완료되면 자동으로 터미널이 열리면서 MSYS2 설치 옵션을 묻는데, 엔터키를 눌러 기본값으로 진행한다.
  - 터미널을 그냥 종료해버린 경우 터미널에 `ridk install` 명령어를 입력하여 설치를 진행할 수 있다.
3. 터미널에 명령어를 입력하여 각각이 잘 설치되었는지 확인한다.
    - Ruby: `ruby -v`
    - RubyGems: `gem -v`
    - GCC와 Make: `gcc -v`, `g++ -v`, `make -v`

# [2] Jekyll과 Bundler 설치하기

```terminal
gem install jekyll bundler
```
터미널에 `jekyll -v`, `bundler -v`를 각각 입력하여 설치가 잘 되었는지 확인한다.

# [3] Sample Blog로 테스트하기

> Jekyll계의 **<u>Hello, World!</u>**라 해두겠다. 테스트용으로 블로그를 생성하고 로컬에서 실행시켜 <u>개발환경이 잘 구축되었는지 </u> 확인한다. 

```terminal
jekyll new helloBlog        # 사이트 생성
cd helloBlog                # 사이트 내로 이동
bundle exec jekyll serve    # 사이트 빌드
```

웹 브라우저에서 `localhost:4000`으로 접속한다.

🛑 **Trouble Shooting** 🛑 <br> 3.0.0 버전 이상의 Ruby를 설치했다면 빌드 과정에서 `webrick` 관련 에러가 발생할 수 있다. 터미널에 `bundle add webrick`를 입력해 의존성을 추가해주면 된다.
{: .notice--danger}

# [5] Jekyll Theme로 시작하기
> 지킬 테마를 입혀 기본 프로젝트 골격을 갖추고 로컬에서 실행해본다. 

1. 자신의 로컬에서 원하는 위치에 원하는 이름으로 블로그 폴더를 만든다.
2. [jekyllthemes.org](http://jekyllthemes.org/)에서 마음에 드는 지킬테마를 고른다.
3. 다운로드를 누르면 깃헙 레포지토리로 연결되는데, 해당 테마 소스코드를 다운받고 압축을 풀어 블로그 폴더에 넣는다.
4. 블로그 폴더로 이동해서 주입된 gem을 프로젝트에 설치한다.
```terminal
bundle install
```
5. 사이트를 빌드한다.
```terminal
bundle exec jekyll serve
```
6. 웹 브라우저에서 `localhost:4000`으로 접속한다.

🛑 **Trouble Shooting** 🛑 <br> 빌드 중에 `kramdown-parser-gfm` 관련 에러가 발생한다면, `Gemfile`에 `gem kramdown-parser-gfm`를 추가하고 `bundle install` 후 다시 빌드해본다. <br>  _*참고_: `kramdown-parser-gfm`는 gfm(Github Favored Markdown)의 마크다운 파일을 HTML로 변환해주는 역할을 한다.
{: .notice--danger}

## minimal-mistakes로 시작하기
> 나는 이용자도 많고 문서화가 잘 되어 있는 [minimal-mistakes](https://mmistakes.github.io/minimal-mistakes/collection-archive/) 테마로 시작하였다. 군더더기 없는 문서이지만 시작하는 단계에서 💡소소한 팁...(?)💡을 언급하고자 한다.

[minimal-mistakes 시작가이드](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)를 보면 
소스코드를 다운받고 압축을 푼 후, 다음 항목들을 삭제하라고 한다.
- .editorconfig
- .gitattributes
- .github
- /docs
- /test
- CHANGELOG.md
- minimal-mistakes-jekyll.gemspec
- README.md
- screenshot-layouts.png
- screenshot.png

하지만 `/docs/_posts`에는 **샘플 포스트**들이 있어서 글을 작성할 때 형식을 참고하기 좋다. 프로젝트 폴더 바로 밑(루트)에 `_posts` 폴더를 만들고 그 밑에 `samples` 폴더를 만들어 샘플 포스트들을 옮겨두었다. 그리고 `.gitignore`에 `_posts/samples`를 추가하여 블로그에는 보여지지 않도록 한다.

그렇게 설정하면 대략적인 전체 프로젝트 구조는 다음과 같다.
```bash
📁blog
|---📁_includes
|---📁_layouts
|---📁_sass
|---📁_assets
|---📁_posts
    |---📁samples
        |---📄2009-05-15-edge-case-nested-and-mixed-lists.md
        |---📄2006-06-01-edge-case-many-tags.md
        |---📄2009-07-02-edge-case-many-categories.md
        ...
|---⚙_config.yml
|---🔸.gitignore
|---🔺Gemfile
|---📄index.html
|---📄index.markdown
```

# [6] Github Pages로 호스팅하기
> 로컬에서 작업한 블로그를 이제 Github Pages를 이용하여 호스팅해본다.

1. Github에서 `<username>.github.io` 이름으로 Repository를 만든다.
2. 로컬에서 작업한 디렉토리와 방금 만든 레포지토리를 연결한다.
```bash
  git init
  git remote add upstream https://github.com/<username>/<username>.github.io
```
3. Gemfile에 `gem "github-pages"`를 추가한다.
4. `_config.yml`를 수정한다.
```yml
url                      : "https://<username>.github.io"
baseurl                  : ""
repository               : "<username>/<username>.github.io"
```

5. Github에 push한다.
```bash
git add .
git commit -m "complete initial setting"
git push origin master
```
6. 웹 브라우저에서 `https://<username>.github.io`로 접속한다.

# [7] 관련 개념 정리
## Jekyll
- **Jekyll**은 Ruby로 작성된 <u>정적 사이트 생성기</u>이다. 

## Gem
- **Gem**은 Ruby 생태계에서 하나의 <u>기능을 담당하는 모듈</u>을 의미한다.
- Jekyll도 Gem이고, Jekyll Plugin으로 사용되는 라이브러리도 모두 Gem이다.

## Gemfile
- **Gemfile**은 <u>Gem들을 나열한 파일</u>이다.

## Bundle
- **Bundler** 역시 하나의 Gem인데, <u>Gemfile에 나열되어 있는 모든 Gem들을 설치</u>하는 역할을 한다.

## Jekyll Cheat Sheet
**Gemfile에 새로운 Gem이 추가되었을 때**
```bash
bundle install
``` 

**Gemfile에 기존에 있던 Gem의 버전을 변경할 때**
```bash
bundle update
```

**로컬에서 사이트 빌드하기**
```bash
bundle exec jekyll serve
```

# 참고
- [Minimal Mistakes Jekyll Theme Docs](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)
- [Jekyll Docs](https://jekyllrb.com/docs/)