---
title: "[GitHub] 여러 개의 GitHub 계정 SSH로 연결하기"
categories:
  - Tools
  - Git&GitHub
tags:
  - github
---

> how to manage multiple GitHub accounts with SSH

# [1] SSH 키를 생성
각 GitHub 계정에 대해 SSH 키를 생성한다.

```
ssh-keygen -t rsa -b 4096 -C "email_organization@example.com"
ssh-keygen -t rsa -b 4096 -C "email_personal@example.com"
```
- `-t`(type): 키 알고리즘 명시
- `-b`(bits): 키 사이즈 명시
- `-C`(comment): public key 뒤에 붙음.

두 개의 SSH 키를 구분짓기 위해 키 이름을 물을 때 **고유한 키 이름을 입력**한다. 회사용은 `org_id_rsa`, 개인용은 `per_id_rsa`로 생성했다고 가정하겠다.
```
> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

각 계정에 대해 각각 공개키(.pub)와 개인키가 생성된 것을 확인할 수 있다. 
```
ls ~/.ssh

org-id-rsa      per-id-rsa 
org-id-rsa.pub  per-id-rsa.pub  
```

# [2] SSH config 설정
설정 파일이 존재하지 않으면 `~/.ssh`에 `config` 이름으로 새로 파일을 만든다.

```
Host github.com-<개인용 GibHub username>
  HostName github.com
  User git
  AddKeysToAgent yes
  IdentityFile ~/.ssh/per-id-rsa

Host github.com-<회사용 GitHub username>
  HostName github.com
  User git
  AddKeysToAgent yes
  IdentityFile ~/.ssh/org-id-rsa
```
나는 `GitHub username`을 사용하여 Host를 구분지었는데,  `github.com123`처럼 의미 없는 값이어도 상관 없다. **두 Host 값이 다르도록 설정해주기만 하면 된다.** 

# [3] SSH client에 private key 등록
```
ssh-add -K ~/.ssh/org_id_rsa
ssh-add -K ~/.ssh/per_id_rsa
```
- `-K`: MAC Keychain에 비밀번호 저장

`-K` 옵션에 대해 에러가 나면 아래와 같이 실행한다. (참고: [GitHub Docs - Error: ssh-add: illegal option --K](https://docs.github.com/en/authentication/troubleshooting-ssh/error-ssh-add-illegal-option----k))
```
/usr/bin/ssh-add -K ~/.ssh/org_id_rsa
/usr/bin/ssh-add -K ~/.ssh/per_id_rsa
```

```
// 등록된 키 전부 조회
ssh-add -l

// 등록된 키 전부 등록 해제
ssh-add -D
```

# [4] 각 GitHub 계정에 SSH public key 추가
## 4-1. SSH 키 복사
```
pbcopy < ~/.ssh/org_id_rsa.pub
```
공개키를 클립보드에 복사한다.

## 4-2. GitHub에 SSH 키 붙여넣기
각각의 GitHub 계정에 로그인한다. `Settings > SSH and GPG keys > New SSH key`에 복사한 값을 붙여넣는다.


# [5] 로컬 레포지토리 설정
## 5-1. GitHub 계정 정보 설정
레포지토리마다 사용할 GitHub 계정을 설정한다. 여기서 설정한대로 커밋 로그가 남는다.
```
git config --local user.name "username"
git config --local user.email "email@example.com"
```

## 5-2. remote url 변경
remote에서 clone을 해온 경우 `remote url`의 기본 값은 `git@github.com:<username>/<repository_name>.git`이다. 여기서 `@`뒤에 붙는 `github.com`을 [[2]](#2-ssh-config-설정)에서 설정한 Host 값과 동일하게 설정해준다.

```
git remote set-url origin git@github.com-<GitHub username>:<username>/<repository_name>.git
```


# 참고
- <https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent>
- <https://gist.github.com/jexchan/2351996?permalink_comment_id=4179310#gistcomment-4179310>