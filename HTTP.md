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



## HTTP 버전

### HTTP/0.9

초기에는 버전 번호가 없었으나 이후 버전과 구별하기 위해 0.9로 명명되었다. `GET` 메서드만 지원한다. MIME 타입, HTTP 헤더, 버전 번호를 지원하지 않는다.

- 요청은 아래와 같은 형식이다.

```http
GET /mypage.html
```

- 응답은 아래와 같은 형식이다.

```html
<html>
  A very simple HTML page
</html>
```

### HTTP/1.0

버전 번호, 상태 코드, HTTP 헤더를 지원한다. `Content-Type`으로 리소스 타입을 나타낼 수 있다.

- 요청은 아래와 같은 형식이다.

```http
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)
```

- 응답은 아래와 같은 형식이다.

```http
200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

### HTTP/1.0+

`Keep-Alive` 커넥션, 가상 호스팅, 프락시 연결 등을 지원한다.

#### Keep-Alive를 사용한 지속 커넥션

기본적으로 한 번의 HTTP 트랜잭션마다 TCP 연결과 TCP 연결 해제 과정을 거친다. 이 TCP 커넥션 지연을 해소하기 위해 지속 커넥션을 사용할 수 있다. **지속 커넥션(persistent connection)**은 트랜잭션 처리 후에도 연결이 유지되는 TCP 커넥션이다.

`Connection: Keep-Alive`로 설정하고 `Keep-Alive` 헤더에 옵션을 명시한다. `timeout` 파라미터는 커넥션을 유지하는 동안 처리할 수 있는 트랜잭션의 개수이며, `timeout`은 커넥션을 유지할 시간(초)이다.

```http
HTTP/1.1 200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Thu, 11 Aug 2016 15:23:13 GMT
Keep-Alive: timeout=5, max=1000
Last-Modified: Mon, 25 Jul 2016 04:32:39 GMT
Server: Apache

(body)
```

### HTTP/1.1

HTTP의 첫번째 표준이다. 지속 커넥션과 파이프라이닝을 지원한다.

#### 지속 커넥션

HTTP/1.1은 기본적으로 **지속 커넥션**을 사용한다. HTTP/1.1 애플리케이션은`Connection:close` 헤더를 명시하여 커넥션을 끊을 수 있다.

#### 파이프라이닝

지속 커넥션은 요청에 대한 응답을 받아야지만 다음 데이터를 요청할 수 있다. **파이프라이닝(pipelining)**에서는 요청에 대한 응답을 기다리지 않고 요청을 보내어 latency를 낮추었다. 한편 서버는 응답을 순서대로 전송한다.

#### HTTP/1.1의 문제

TCP는 신뢰성 있는 데이터를 보장하므로 데이터를 순서에 맞게 보내야한다. 따라서 앞 선 요청에 대한 처리가 끝날 때까지 뒤에 오는 요청의 처리가 대기하는 **HOL(Head Of Line) Blocking** 문제가 발생한다. 또한 지속 커넥션에서 요청의 헤더가 중복되는 경우가 많아 대역폭이 낭비되는 문제가 있었다.

### HTTP/2.0

HTTP/2.0은 SPDY 프로토콜을 사용하여 **회전 지연(latency)**을 줄이고자 하였다. 그러나 TCP를 사용하므로 HOL Blocking 문제를 완전히 해결하지는 못한다.

#### 프레임

<img src="https://web-dev.imgix.net/image/C47gYyWYVMMhDmtYSLOWazuyePF2/2a2cw0nAXe9Mi5txM4Mw.svg" alt="HTTP/2 바이너리 프레이밍 레이어" width="60%;" />

바이너리 프레임 계층에서 하나의 HTTP 메시지는 헤더 프레임과 데이터 프레임으로 분할되고 각각 바이너리 인코딩된다.

#### 스트림과 멀티플렉싱

<img src="https://web-dev.imgix.net/image/C47gYyWYVMMhDmtYSLOWazuyePF2/4RwALfscCwB7MDa1bGsV.svg" alt="공유 연결 내에서 HTTP/2 요청 및 응답 다중화" width="67%;" />

**스트림(stream)**은 프레임의 시퀀스로 양방향 전송이 가능하며 다른 스트림에 독립적이다, 한 쌍의 HTTP 요청과 응답을 하나의 스트림이 처리한다. TCP 연결에 여러 개의 스트림을 동시에 열 수 있다. 각 스트림은 식별자를 가지며 이를 통해 스트림의 우선순위를 나타낼 수 있다.

#### 헤더 압축

<img src="https://web-dev.imgix.net/image/C47gYyWYVMMhDmtYSLOWazuyePF2/IYfczfC6ZCTxUVboaEZy.svg" alt="HPACK: HTTP/2용 헤더 압축" width="50%;" />

HTTP 메시지의 헤더를 HPACK 알고리즘에 따라 압축한다. 클라이언트와 서버는 HPACK compression context를 유지한다. HPACK compression context는 인덱스를 가진 정적 테이블과 동적 테이블로 구성된다.

1. 정적 테이블은 모든 연결에서 공용으로 사용하는 HTTP 헤더 목록을 제공한다.
2. 동적 테이블은 특정 연결에서 사용한 HTTP 헤더 목록을 제공한다.

정적 테이블과 동적 테이블에 헤더가 있다면 인덱스를, 그렇지 않다면 Huffman 인코딩한 값을 넣는다.

#### server push

서버는 클라이언트가 요청할 자원을 푸시할 수 있다. 가령 클라이언트가 HTML 문서를 요청하면 서버는 CSS, JS를 푸쉬하여 API 요청과 레이턴시를 줄일 수 있다.

### HTTP/3.0

HTTP/3.0dms UDP에 기반한 QUIC 프로토콜을 사용한다. 헤더를 커스터마이징하여 TCP의 지연을 줄이면서 TCP만큼의 신뢰성을 제공한다. TLS를 기본으로 적용한다. TCP+TLS의 경우 3 RTT가 소요되나 QUIC는 보내려는 데이터와 연결 설정에 필요한 데이터를 함께 보내 1 RTT를 소요한다. 한 번 연결을 설정했다면 캐싱을 통해 다음 연결부터는 0 RTT를 소요한다. 하나의 UDP 커넥션에 독립적인 QUIC stream을 사용하여 향상된 멀티플렉싱을 지원한다. 클라이언트는 Connection ID를 저장하여 클라이언트의 IP가 변경되어도 서버와 커넥션을 유지할 수 있다.



## HTTP로 통신하기

### WebSocket

HTTP는 단방향 통신으로 서버는 클라이언트의 요청에 대한 응답만 보낼 수 있으며 연결 설정과 해제를 반복해야한다. 이는 실시간으로 두 호스트가 데이터를 주고받는 서비스-채팅에는 적합하지 않다. HTML5의 WebSocket은 한 번 수립된 TCP 연결로 클라이언트와 서버가 자유롭게 데이터를 송수신할 수 있다. 클라이언트는 연결 설정에서 HTTP를 사용하여 서버가 WebSocket을 지원하는지 확인한다.

```http
GET /chat HTTP/1.1
Host: example.com:8000
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Sec-WebSocket-Version: 13
```

서버는 위 요청에 대하여 다음과 같이 수락할 수 있다.

```http
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
```

WebSocket API를 사용하거나 Node.js를 기반으로 WebSocket API를 제공하는 Socket.IO를 사용할 수 있다.

### 폴링

폴링(polling)은 클라이언트가 일정한 주기로 서버에게 HTTP 요청을 보낸다. 폴링의 주기가 짧으면 서버에 부하가 갈 수 있으며 주기가 길면 실시간성이 떨어진다.

### 롱 폴링

롤 폴링(long polling)은 클라이언트의 요청에 즉시 응답을 보내지 않고 대기하다가 이벤트가 발생하면(데이터에 변경이 생기면) 데이터를 전송한다. 클라이언트는 응답을 받으면 다시 요청한다. 클라이언트의 수가 많거나 이벤트의 발생이 잦다면 서버에 부하가 심해진다.

### SSE

HTML5의 SSE(server-sent events)는 단방향 연결을 지원하여 서버가 클라이언트에게 이벤트를 전송할 수 있다. 서버의 이벤트를 클라이언트에게 알릴 때 WebSocket보다 가볍게 사용할 수 있다. HTTP를 통해 전송된다.



## 참고

- [GeeksforGeeks - HTTP Full Form](https://www.geeksforgeeks.org/http-full-form/)
- [위키백과 - HTTP](https://ko.wikipedia.org/wiki/HTTP)
- [MDN - HTTP](https://developer.mozilla.org/ko/docs/Web/HTTP)
- [MDN - HTTP 개요](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
- [MDN - HTTP의 진화](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)
- [MDN - HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [MDN - Keep-Alive](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Keep-Alive)
- [web.dev - Introduction to HTTP/2](https://web.dev/performance-http2/)
- [MDN - Using server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)



## 스터디

1. HTTP의 특징에 대해서 말해보세요

   HTTP의 특징은 비연결성과 무상태성이다.

   1. HTTP의 무상태성이 무엇인가요?

      각각의 HTTP 요청은 독립적으로, 서버는 이전 요청에 대한 어떠한 상태도 유지하지 않는다.

      1. 왜 HTTP는 무상태성을 채택했을까요?

         서버가 상태를 유지하지 않아도 되므로 확장하기 좋다.

         1. 그렇다면 로그인 유지처럼 인증 상태를 유지해야하는 경우는 어떻게 하나요? / 로드밸런싱에서 인증 상태는 어떻게 처리하라 수 있나요?



### TCP/IP 소켓과 WebSocket의 차이는 무엇인가

소켓(socket)은 운영체제 내부에 구현된 인터페이스로 응용 프로그램에게 TCP 통신 기능을 제공한다. 종단점으로서 포트(port)라고 하기도 한다. WebSocket은 하나의 TCP 커넥션으로 실시간 양방향 통신을 제공하는 전송 계층 프로토콜이다.



- TCP는 어떤 단점이 있는가?

  연결 설정으로 인한 지연, 신뢰성 있는 데이터 보장을 위한 지연(데이터 오류 발생시 복구), 이런 기능을 제공하기 위해 헤더가 무거움

  - TCP 위에서 동작하는 HTTP는 어떻게 TCP 성능 문제를 해결하고자 하는가?

    `HTTP/1.*`은 지속 커넥션을 제공하여 커넥션을 재활용하였고 파이프라이닝을 제공하여 latency를 낮추고자 하였다. `HTTP/2.*`는 멀티플렉싱을 지원하여 하나의 커넥션으로 여러 개의 응답을 동시에 받을 수 있도록 하였다. 헤더의 중복을 검사하여 헤더를 압축한다. server push를 지원한다. `HTTP/3.*`은 연결 과정을 축소하고 UDP를 사용하여 빠르게 통신한다.



