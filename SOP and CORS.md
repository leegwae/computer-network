# SOP and CORS

## URL

<img src="https://user-images.githubusercontent.com/57662010/211197277-083bc783-b79f-4239-99d0-a00c39ab09b7.png" alt="url"/>

**URL(Uniform Resource Locator)**은 웹 상에서 하나의 자원을 고유하게 가리키는 주소이다.

1. scheme: 자원에 접근할 때 사용해야하는 프로토콜
2. domain name: 서버의 이름
3. port
4. path: 서버 내에서 자원의 위치
5. parameter: 쿼리 스트링
6. anchor

```javascript
location.origin;
```



## Origin

웹 컨텐츠의 **Origin**은 컨텐츠에 접근할 때 사용하는 URL의 scheme(사용하는 프로토콜), hostname(도메인 이름), port로 구성된다. 두 컨텐츠의 Origin이 같다면 same-origin이라고 하며, 그렇지 않다면 cross-origin이라고 한다.



## SOP

**SOP(Same-origin policy)**는 도큐먼트나 스크립트가 cross-origin 컨텐츠와 상호작용하지 못하도록 제한하는 보안 정책이다. 브라우저는 SOP에 의거해 cross-origin 요청을 막아 잠재적인 공격 격로를 줄인다. 서버 사이드 렌더링을 사용하던 초기에는 다른 origin으로 요청을 보내는 것을 악의적인 공격(CSRF, XSS)으로 간주하는 것이 자연스러웠기 때문이다. 그러나 웹이 발전하면서 브라우저단에서 cross-origin으로 요청을 보내고자 하는 요구가 늘어났고, CORS를 사용해 cross-origin 접근을 허용할 수 있게 되었다.



## CORS

**CORS(Cross-Origin Resource Sharing)**은 HTTP 헤더를 사용하여 cross-origin 접근을 허용하거나 막는 메커니즘이다. CORS를 사용하는 요청은 세 가지가 있다.

### Simple Requests

Simple Request로 간주되는 요청은 다음과 같다.

- `GET`, `HEAD`, `POST` 중 하나의 메서드를 사용
- `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` 헤더만 사용
  - `Content-Type`의 값은 `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain`만 허용

브라우저는 모든 cross-origin 요청에 `Origin` 헤더를 붙여보낸다. `Origin` 요청을 받은 서버가 `Access-Control-Allow-Origin` 헤더에 허가하는 origin을 담아 보낸다. 브라우저는 `Origin` 헤더의 값이 `Access-Control-Allow-Origin` 헤더의 값에 포함되면 스크립트에 응답을 전달하고 그러지 않다면 응답을 파기한다.

사용자 인증을 위한 `Cookie`, `Authorization` 헤더를 사용할 수 없고, `Content-Type`에 `application/json`을 사용할 수 없으므로 사용되는 경우가 드물다.

### Requests with credentials

브라우저는 기본적으로 `XMLHttpRequest`나 Fetch API를 사용하면 `Cookie`와 `Authorization` 헤더를 붙여보내지 않는다. fetch API의 `credentials` 옵션으로 붙여보내도록 할 수 있다.

```js
fetch(url, { credentials: 'include' })
```

이때 서버는 다음과 같은 헤더를 포함하여 응답해야한다.

1. `Access-Control-Allow-Credentials: true`
2. `Access-Control-Allow-Origin`: URL (`*`을 사용할 수 없음) 

### Preflighted requests

요청을 보내기 전, 브라우저는 다음 헤더와 함께 `OPTIONS` 메서드로 요청을 보내어 서버가 CORS 정책을 위반하지 않는지 확인한다.

1. `Access-Control-Request-Method`: 실제 요청의 메서드
2. `Access-Control-Request-Headers`: 실제 요청의 추가 헤더

```
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-PINGOTHER, Content-Type
```

서버는 다음과 같은 헤더를 포함하여 응답한다.

1. `Access-Control-Allow-Origin`: cross-origin 접근을 허용하는 origin 
2. `Access-Control-Allow-Methods`: 해당 자원에 대해 지원 중인 메서드 (`*`을 사용할 수 없음) 
3. `Access-Control-Allow-Headers`: 해당 자원에 대해 지원 중인 헤더 (`*`을 사용할 수 없음) 
4. `Access-Control-Max-Age`: preflighted request에 대한 응답을 캐시할 수 있는 시간 (`*`을 사용할 수 없음) 

```
Access-Control-Allow-Origin: http://foo.example
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
Access-Control-Max-Age: 86400
```

안전하지 않은 메서드의 경우 서버의 부작용을 야기할 수 있기 때문에 preflighted request로 CORS를 위반하지 않는지 확인하여 서버를 보호한다.



### CORS 위반 해결하기

1. `Access-Control-Allow-Origin`에 `*`나 URL 명시하기
2. 프록시 서버 사용하기
   1. 프론트 개발환경이라면 webpack-dev-server의 `proxy` 옵션을 사용할 수 있다.
   2. 웹 서버(NGNIX 등)을 사용한다.



## 참고

- [MDN - What is a URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL)
- [web.dev - Understanding "same-site" and "same-origin"](https://web.dev/i18n/en/same-site-same-origin/#site)
- [MDN - Origin](https://developer.mozilla.org/en-US/docs/Glossary/Origin)
- [MDN - Same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- [MDN - Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)