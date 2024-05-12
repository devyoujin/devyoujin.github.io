---
title: "[Spring] HttpMessageNotReadableException 해결"
categories:
  - Language&Framework
  - Spring
tags:
  - spring
  - test
  - error
---

# [1] 문제 상황
스프링에서 MockMvc를 사용해 컨트롤러 레이어를 테스트하던 중 문제가 발생했다. 내가 예상한 작동은 상태코드 `200(Ok)`를 리턴하는 것인데 `400(Bad Request)`과 함께`HttpMessageNotReadableException` 예외가 발생했다.

⬇️ **에러 로그**
```
MockHttpServletRequest:
      HTTP Method = PUT
      Request URI = /api/v1/members/username
       Parameters = {}
          Headers = [Content-Type:"application/json;charset=UTF-8", Accept:"application/json", Content-Length:"18"]
             Body = {"username":"New Username"}
    Session Attrs = {}
...
Resolved Exception:
             Type = org.springframework.http.converter.HttpMessageNotReadableException
```


⬇️ **테스트 코드: MemberControllerTest**
```java
private MemberUsernameRequest memberUsernameRequest;

 @BeforeEach
public void setUp() {
    memberUsernameRequest = MemberUsernameRequest.builder()
                .username("New Username")
                .build();
}
...
@Test
void should_updateMemberUsername() throws Exception {
    Mockito.when(memberService.findMemberByOauthId(isA(String.class)))
            .thenReturn(member);
    Mockito.when(memberService.canUpdateUsername(isA(Member.class)))
            .thenReturn(true);
    Mockito.when(memberService.updateUsername(isA(Member.class), isA(MemberUsernameRequest.class)))
            .thenReturn(MemberUsernameResponse.of("New Username"));

    mockMvc.perform(put(MEMBER_BASEURL + "/username")
                    .contentType(MediaType.APPLICATION_JSON)
                    .content(objectMapper.writeValueAsString(memberUsernameRequest))
                    .with(user(OAuthUserPrincipal.of(member)))
                    )
                    .andExpect(status().isOk()); //에러 발생
}
```
테스트하고자 하는 컨트롤러는 username을 업데이트하는 기능을 한다. PUT 메서드를 사용하고, RequestBody에 username을 받는다.

⬇️ **메인 코드: MemberController**

```java
@Override
public ResponseEntity<MemberUsernameResponse> updateMemberUsername(OAuthUserPrincipal userPrincipal,
                                                                   MemberUsernameRequest memberUsernameRequest) {
    return new ResponseEntity<>(
                memberService.updateUsername(
                    memberService.findMemberByOauthId(userPrincipal.getOauthId(), memberUsernameRequest
                ),
                HttpStatus.OK);
}
```
인터페이스를 구현한 메서드 자체는 매우 간단하다. 서비스 레이어의 `findMemberByOauthId` 메서드를 호출하는 게 전부다.

⬇️ **메인 코드: MemberUsernameRequest**
```java
@Getter
public class MemberUsernameRequest {
    @JsonProperty("username")
    @NotNull
    private String username;

    @Builder
    public MemberUsernameRequest(String username) {
        this.username = username;
    }
}
```


# [2] 발생 원인
[스프링 공식 문서](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/http/converter/HttpMessageNotReadableException.html)를 보면 `HttpMessageNotReadableException`은 **HttpMessageConverter.read(...)가 실패할 때 발생하는 에러**라고 나와있다. 

⬇️ **HttpMessageConverter.read(...) 메서드에 대한 설명**
```
T read(Class<? extends T> clazz, HttpInputMessage inputMessage)
        throws IOException, HttpMessageNotReadableException
Read an object of the given type from the given input message, and returns it.

Parameters:
clazz - the type of object to return. This type must have previously been passed to the canRead method of this interface, which must have returned true.
inputMessage - the HTTP input message to read from

Throws:
IOException - in case of I/O errors
HttpMessageNotReadableException - in case of conversion errors
```

⭐️ 정리하자면 HttpMessageConverter.read(...)는 **입력 메시지(두번째 파라미터)를 읽어 주어진 타입(첫번째 파라미터)으로 반환하는 메서드**이다. 두 가지 예외 중에 `HttpMessageNotReadableException`은 **읽은 메시지를 주어진 타입으로 변환할 때 발생**한다.

# [3] 해결 방법

⬇️ **메인 코드: MemberUsernameRequest**
```java
@Getter
@NoArgsConstructor //추가
public class MemberUsernameRequest {
    @JsonProperty("username")
    @NotNull
    private String username;

    @Builder
    public MemberUsernameRequest(String username) {
        this.username = username;
    }
}
```
내가 작성한 코드에 대입해서 생각해보면, username을 변경할 때 호출하는 API에서 Request Body로 들어오는 값이 컨트롤러에 지정해준 타입 `MemberUsernameRequest`으로 변환되는 과정에 문제가 있었다. 기본 생성자가 없어서 객체 생성이 안되기 때문이었다. lombok을 사용하고 있기 때문에 `@NoArgsContructor` 어노테이션을 추가해서 해결하였다.

# 출처
- [스프링 공식 문서 - HttpMessageNotReadableException](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/http/converter/HttpMessageNotReadableException.html)
- [스프링 공식 문서 - HttpMessageConverter.read](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/http/converter/HttpMessageConverter.html#read(java.lang.Class,org.springframework.http.HttpInputMessage))