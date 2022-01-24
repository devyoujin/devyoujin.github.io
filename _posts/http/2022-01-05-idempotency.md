---
title: "[HTTP] 멱등성(indempotency)"
categories:
  - HTTP
tags:
  - HTTP
  - Web
---

> 

# [1] 멱등성이란?
- [네이버 국어사전](https://ko.dict.naver.com/#/entry/koko/3b4f7ca2ddb64633a9607112fb4af0e0)에 의하면 멱등성은 **'연산을 여러 번 적용하더라도 결과값이 달라지지 않는 성질'**을 의미한다.

🎓 **TMI - 冪(덮을 멱)** 🎓 네이버 사전에 수학용어라고 나와있길래 '엇, 내가 아는 수학용어 중에서도 `멱` 들어가는 게 있었는데...' 싶어서 찾아보니까 멱급수였고 두 용어가 같은 한자를 쓰고 있었다. [네이버 한자사전](https://hanja.dict.naver.com/#/search?query=%E5%86%AA&range=all)에는 **거듭제곱**의 의미도 있다고 나온다. 
{: .notice--info}

# [2] 멱등성과 안전함
**<u>"HTTP 메서드가 멱등성을 가진다."</u>**
- **동일한 요청을 한 번 보낸 것과 여러번 보낸 것이 같은 효과**를 보이고, **여러번 요청에 의한 서버의 상태가 동일**할 때 HTTP 메서드가 멱등성을 가진다고 말할 수 있다.
- 멱등성을 가지는 HTTP 메서드: `GET`, `HEAD`, `PUT`, `DELETE` 

**<u>"HTTP 메서드가 안전하다."</u>**
- **서버의 상태를 바꾸지 않을 때** 즉, 읽기 작업을 하는 HTTP 메서드는 안전하다고 말할 수 있다.
- 안전한 HTTP 메서드: `GET`, `HEAD`, `OPTIONS`

![멱등성과 안전함]({{ site.url }}{{ site.baseurl }}/assets/img/http/http-idempotency-and-safety.jpg)
- MDN에 보면 모든 HTTP 메서드마다 멱등성과 안전함을 확인할 수 있다.
- <u>모든 안전한 메서드는 멱등성을 가지지만, 멱등성을 가진 메서드라고 해서 모두 안전한 것은 아니다.</u>

# [3] DELETE 메서드와 멱등성
> 'DELETE 메서드는 여러 번 호출하면 응답이 다르게 내려올텐데 멱등성을 가진다고?' 라는 의문을 품은 저 같은 사람이 있다면 보십쇼...🤧

데이터베이스에 저장된 하나의 아이템을 삭제하는 DELETE 메서드를 연달아 3번을 호출한다고 생각해본다. 올바르게 설계되었다면 첫 번째 요청에는 `200(OK)`을 반환하고, 두 번째 요청부터는 이미 삭제된 아이템에 대해서 요청을 보내기 때문에 `404(Not Found)`를 반환할 것이다.

```terminal
# 100번 아이템을 삭제한다
DELETE items/100/delete HTTP/1.1   #200
DELETE items/100/delete HTTP/1.1   #404
DELETE items/100/delete HTTP/1.1   #404
```

여기서 중요한 것은 해당 메서드가 멱등성을 가지는 지 따져볼 때 응답의 일치여부가 아닌 **첫 번째 요청과 그 이후의 요청을 처리한 후 서버의 상태에 변동이 없는지**가 기준이 된다는 것이다.

# 참고
- [MDN Docs](https://developer.mozilla.org/ko/docs/Glossary/Idempotent)