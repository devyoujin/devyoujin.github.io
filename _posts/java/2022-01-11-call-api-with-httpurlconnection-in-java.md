---
title: "[Java] HttpURLConnection으로 외부 API 호출하기(GET, POST 요청)"
categories:
  - Java
tags:
  - Java
  - Web
  - API
  - How-To
---

> Java 라이브러리 `HttpURLConnection`을 이용하여 외부 API를 호출하고 테스트 서버를 통해 테스트해본다.

<a href="https://github.com/dev-ujin/java-lab/tree/main/api-call" class="btn btn--github"><i class="fab fa-github"></i> 소스코드</a>

# [0] 선수 작업
- JSON으로 데이터를 처리할 것이기 때문에 **json- simple 라이브러리를 import**하는 작업이 필요하다.
[IntelliJ에 라이브러리 추가하기]({{ site.url }}{{ site.baseurl }}/intellij/import-library-into-intellij)를 참고할 수 있다.

- 우선 **클래스 구조**는 이렇게 작성했다. 꼭 클래스를 만들거나 함수 안에서 실행해야하는 것은 절대 아니다. 생성자나 Getter, Setter는 여기서는 생략한다. 전체 소스코드는 상단에 소스코드 버튼을 누르면 확인할 수 있다.

🔽 ApiCaller.java
```java
public class ApiCaller {
    private String baseUrl;
    private int responseCode;

    public JSONObject sendGetRequest() {
    }

    public void sendPostRequest() {
    }
```

# [1] GET 요청 보내기
🔽 ApiCaller.java > sendGetRequest()
{% highlight java linenos %}
public JSONObject sendGetRequest() {
    JSONObject data = new JSONObject();
    try {
      URL url = new URL(baseUrl);

      HttpURLConnection conn = (HttpURLConnection) url.openConnection();
      conn.setRequestMethod("GET"); //Http Method 지정(default가 GET이라 생략가능)
      conn.connect();

      //InputStream으로 데이터를 읽고, JSONParser를 이용해 JSONObject로 파싱
      InputStreamReader inputStreamReader = new InputStreamReader(conn.getInputStream());
      JSONParser jsonParser = new JSONParser();
      data = (JSONObject) jsonParser.parse(inputStreamReader);

      responseCode = conn.getResponseCode(); //응답코드 담기
    } catch (IOException | ParseException e) {
        e.printStackTrace();
    }
    return data;
}
{% endhighlight %}

# [2] POST 요청 보내기
🔽 ApiCaller.java > sendPostRequest()
{% highlight java linenos %}
public void sendPostRequest(String content) {
    try {
      URL url = new URL(baseUrl); //URL 객체 생성

      HttpURLConnection conn = (HttpURLConnection) url.openConnection();
      conn.setRequestMethod("POST"); //Http Method 지정
      conn.setRequestProperty("Content-Type", "application/json"); //JSON 형태로 데이터 전송
      conn.setDoOutput(true); //OutputStream을 통해 데이터를 전송할지 여부
      conn.connect();

      //OutputStream을 통해 데이터를 전달
      OutputStreamWriter outputStreamWriter = new OutputStreamWriter(conn.getOutputStream());
      outputStreamWriter.write(content);
      outputStreamWriter.flush();

      responseCode = conn.getResponseCode(); //응답코드 담기
    } catch(IOException e) {
        e.printStackTrace();
    }
}
{% endhighlight %}
- (라인 8) `setDoOutput(true)`로 설정하면 request body에 해당하는 내용을 OutputStream을 통해 전달하겠다는 의미이다.

# [3] 테스트하기
[Webhook.site](https://webhook.site/) 테스트 서버를 통해 `HttpURLConnection`이 올바르게 동작하는지 간단히 테스트해본다.

Webhook.site는 사용자마다 **고유 API 서버**를 제공해준다. 회원가입 없이 500개까지 요청을 보낼 수 있어서 간단히 연결 테스트를 하기에 적합할 것 같다. **무료버전에서는 POST로 데이터를 전송했을 때 그 데이터를 서버에서 받는 기능은 사용할 수 없다.**

## 응답 데이터 설정
오른쪽 상단에 `Edit` 버튼을 누르면 응답으로 내려줄 데이터를 설정할 수 있다.
- Default status code: 200
- Content Type: application/json
- Timeout before response: 5
- Response body: 
{
  "Description": "This is api test.",
  "Language": "Java",
}

## 테스트 실행
Webhook.site 에서 받은 unique url을 이용하여 테스트를 실행한다.

🔽 Main.java
```java
public class Main {
    public static void main(String[] args) {
        ApiCaller apiCaller = new ApiCaller("https://webhook.site/123456a7-b116-4cd9-951e-0fg2h7di4j56");

        System.out.println("//===== GET REQUEST =====//");
        JSONObject data = apiCaller.sendGetRequest();
        System.out.println("The Data from Server: " + data);
        System.out.println("Response Code : " + apiCaller.getResponseCode());

        System.out.println("//===== POST REQUEST =====//");
        apiCaller.sendPostRequest("Mood: Nerdy");
        System.out.println("Response Code : " + apiCaller.getResponseCode());
    }
}
```

## 테스트 결과
```terminal
//===== GET REQUEST =====//
The Data from Server: {"Description":"This is api test.","Language":"Java"}
Response Code : 200
//===== POST REQUEST =====//
Response Code : 200
```

# 참고
- `HttpURLConnection`에 설정할 수 있는 함수들을 잘 설명해둔 사이트: <https://www.codejava.net/java-se/networking/how-to-use-java-urlconnection-and-httpurlconnection>
- <https://stackoverflow.com/questions/5725430/http-test-server-accepting-get-post-requests>