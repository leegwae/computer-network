# HTTP

**HTTP(HyperText Transfer Protocol)**는 웹 상에서 클라이언트와 서버가 자원을 주고 받을 때 사용하는 통신 규약이다. 기본 포트는 80이다. 클라이언트는 서버에게 HTTP 요청을 하고, 서버는 이 요청에 대하여 클라이언트에게 HTTP 응답을 한다.



## HTTP의 특징

### 비연결성

서버는 클라이언트에게 응답을 보낸 후 연결을 끊는데 이것을 HTTP의 `비연결성(connectionless)`라고 한다. 서버는 클라이언트와의 연결을 계속 유지하지 않으므로 리소스를 낭비하지 않는다는 장점이 있다. 그러나 매 요청마다 연결을 설정하고 해제해야한다는 단점이 있다.

### 무상태성

각각의 HTTP 요청은 독립적으로, 서버는 이전 요청에 대한 어떠한 상태도 유지하지 않는데 이것을 HTTP의 `무상태성(stateless)`라고 한다. HTTP에서 상태를 유지하기 위해서는 쿠키(cookie)나 세션(session) 혹은 HTML5의 모던 스토리지(로컬 스토리지, 세션 스토리지)를 사용한다.



## HTTP 메세지

![image](https://user-images.githubusercontent.com/57662010/197606544-8b8633ba-acd6-4fc9-ae98-cbc6529616e8.png)

클라이언트의 요청과 서버의 응답은 **HTTP 메시지**의 형태로 이루어진다. 즉, 클라이언트와 서버는 HTTP 메시지를 주고받는다. 클라이언트가 서버에게 보내는 HTTP 메시지를 **HTTP 요청(HTTP request)**, 서버가 클라이언트에게 보내는 HTTP 메시지를 **HTTP 응답(HTTP response)**라고 한다. HTTP 메시지는 크게 헤드(head)와 본문(body)로 구성된다. 헤드와 본문은 빈 줄 한 개로 구분되며, 헤드는 시작 줄과 헤더들로 다시 나눌 수 있다.

### HTTP 요청 헤드

![image](https://user-images.githubusercontent.com/57662010/197606355-e8ec3392-1cc9-458b-b819-9a2caac773ef.png)

- 시작 줄은 요청문(Request Line)으로 HTTP 메서드, URI, HTTP 버전을 명시한다. (여기서는 순서대로 `POST`, `/`, `HTTP/1.1`이다.)
  - HTTP 메서드는 서버가 무엇을 해야할지를 나타낸다.
  - URI는 리소스를 식별한다.

- 헤더들에는 요청에 대한 부가적인 정보를 나타내는 HTTP 헤더를 나열한다.

### HTTP 응답 헤드

![img](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages/http_response_headers3.png)

- 시작 줄은 응답문(Response Line)으로 HTTP 버전, HTTP 상태 코드, HTTP 상태 텍스트를 명시한다. (여기서는 순서대로 `HTTP/1.1`, `200`, `OK`이다.)
  - HTTP 상태 코드는 HTTP 요청이 성공했는지 나타낸다.
  - HTTP 상태 텍스트는 HTTP 상태 코드에 대응하는 텍스트이다.

- 헤더들에는 응답에 대한 부가적인 정보를 나타내는 HTTP 헤더를 나열한다.



## HTTP 요청 메서드

HTTP 요청 메시지는 **HTTP 메서드(HTTP 요청 메서드, HTTP request method)**를 명시하여 서버가 무엇을 해야할지 알린다. 9가지가 있다.

### GET

HTTP `GET` 메서드는 리소스를 요청할 때 사용한다. 본문, 페이로드를 담지 않는 것이 적절하다.

### DELETE

HTTP `DELETE` 메서드는 리소스의 삭제를 요청할 때 사용한다.

### POST

HTTP `POST` 메서드는 서버에 데이터를 제출하기 위해 사용한다. (새로운 자원의 생성을 요청할 때 사용한다.)

### PUT

HTTP `PUT` 메서드는 리소스의 교체를 요청할 때 사용한다.

### PATCH

HTTP `PATCH` 메서드는 리소스의 수정을 요청할 때 사용한다.

### CONNECT

HTTP `CONNECT` 메서드는 요청 자원에 대해 양방향 연결을 시작한다. HTTP 터널을 열기 위해 사용될 수 있다.

### HEAD

HTTP `HEAD` 메서드는 `GET` 메서드로 리소스를 요청했을 때 돌아오는 응답의 헤더를 확인하기 위해 사용한다.

### OPTIONS

HTTP `OPTIONS` 메서드는 명시한 자원에 대해 서버가 어떤 통신 옵션을 지원하는지 알기 위해 사용한다.

- 어떤 메서드로 요청할 수 있는지
- 크로스 오리진 요청을 허용하는지

### TRACE

HTTP `TRACE` 메서드는 리소스로 가는 경로를 따라 message loop-back 테스트를 수행하여 디버깅을 제공한다.

### 안전한 메서드

HTTP 메서드를 수행해도 서버의 상태가 바뀌지 않으면 메서드가 안전하다.

### 멱등성

메서드가 멱등성을 가진다면 메서드를 한 번 실행한 결과와 메서드를 여러 번 실행한 결과가 같다. 모든 안전한 메서드는 멱등하다.

### GET과 POST의 차이

GET은 서버에 리소스를 요청할 때 사용하고 POST는 서버에 리소스를 생성할 때 사용한다. GET은 안전한 메서드로 멱등하나 POST는 멱등하지 않다. 또한 GET은 서버에 데이터를 전달하기 위해 URL을 사용하여 본문을 사용하는 POST 보다 보안이 약하다. GET은 캐시를 사용할 수 있고 POST는 그렇지 않다.

### POST와 PUT의 차이

POST는 요청할 때마다 새로운 자원이 생기지만 PUT은 여러 번 요청해도 그 결과가 바뀌지 않는다. 즉 POST는 멱등하지 않으나 PUT은 멱등하다.

### PUT과 PATCH의 차이

PUT은 특정 리소스의 전체를 수정하고 PATCH는 리소스의 일부를 수정한다.



## HTTP 응답 상태 코드

HTTP 응답 메시지는 **HTTP 응답 상태 코드(HTTP response status codes)**를 명시하여 HTTP 요청이 성공적으로 완료되었는지 클라이언트에게 알린다. 5개의 클래스로 나눈다.

1. Informational responses(`100` – `199`)
2. Successful responses(`200` – `299`)
3. Redirection messages(`300` – `399`)
4. Client error responses (`400` – `499`)
5. Server error responses(`500` – `599`)

### 주요 상태 코드

- `200 OK`: 요청이 성공적으로 수행되었다.
- `202 Accepted`: 요청이 수락되었지만 수행이 완료되지 않았다.
- `400 Bad Request`: 요청 메시지에 오류가 있어 요청을 처리할 수 없거나 처리하지 않을 것이다.
- `401 Unauthorized`: 요청한 자원에 접근할 수 있는 권한이 증명되지 않았다.
- `403 Forbidden`: 요청이 거부되었다.
- `404 Not Found`: 요청한 자원이 찾을 수 없다.
- `500 Internal Server Error`: 서버에 오류가 발생하여 요청을 처리할 수 없다.
- `501 Not Implemented`: 서버가 요청을 수행하기 위해 필요한 기능을 지원하지 않는다.



## HTTP 캐시(TODO)

트래픽을 줄이기 위해 캐싱을 적용할 수 있다.

[웹 서비스 캐시 똑똑하게 다루기](https://toss.tech/article/smart-web-service-cache)

[web.dev - Prevent unnecessary network requests with the HTTP Cache](https://web.dev/i18n/ko/http-cache/)

[MDN - HTTP Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)

[CDN과 캐시 설정으로 정적파일을 빠르게](https://velog.io/@heka1024/CDN%EA%B3%BC-%EC%BA%90%EC%8B%9C-%EC%84%A4%EC%A0%95%EC%9C%BC%EB%A1%9C-%EC%A0%95%EC%A0%81%ED%8C%8C%EC%9D%BC%EC%9D%84-%EB%B9%A0%EB%A5%B4%EA%B2%8C)



## HTTP 동작 과정

1. 사용자가 주소창에 도메인(예: `https://www.google.co.kr/`)을 입력한다.
2. DNS로 도메인을 IP 주소로 변환한다.
3. 클라이언트와 서버가 TCP 연결한다. (TCP 3-way handshaking)
4. 클라이언트가 해당 주소에 대한 리소스(HTML 문서)를 요청한다.
5. 서버는 리소스(HTML 문서)를 응답한다.
6. 클라이언트와 서버가 TCP 연결을 종료한다. (TCP 4-way handshaking)
7. 클라이언트가 HTML 문서를 렌더링한다.



## 참고

- [GeeksforGeeks - HTTP Full Form](https://www.geeksforgeeks.org/http-full-form/)
- [위키백과 - HTTP](https://ko.wikipedia.org/wiki/HTTP)
- [MDN - HTTP](https://developer.mozilla.org/ko/docs/Web/HTTP)
- [MDN - HTTP 개요](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
- [MDN - HTTP의 진화](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)
- [MDN - HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)



## 스터디

1. HTTP의 특징에 대해서 말해보세요

   HTTP의 특징은 비연결성과 무상태성이다.

   1. HTTP의 무상태성이 무엇인가요?

      각각의 HTTP 요청은 독립적으로, 서버는 이전 요청에 대한 어떠한 상태도 유지하지 않는다.

      1. 왜 HTTP는 무상태성을 채택했을까요?

         서버가 상태를 유지하지 않아도 되므로 확장하기 좋다.

         1. 그렇다면 로그인 유지처럼 인증 상태를 유지해야하는 경우는 어떻게 하나요? / 로드밸런싱에서 인증 상태는 어떻게 처리하라 수 있나요?

