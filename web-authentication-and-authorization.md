# Web Authentication

## 인증과 인가란 무엇인가

**인증(Authentication)**은 사용자가 제출한 정보로 사용자가 누구인지 확인하는 절차이다. 일반적으로 사용자는 로그인을 하여 인증 상태를 획득하는데, HTTP는 상태를 유지하지 않으므로 매번 로그인을 거치치 않으려면 어딘가에 인증 상태를 유지해야한다. 

**인가(Authorization)**은 인증된 사용자나 애플리케이션이 서버가 제공하는 특정 자원이나 기능에 대한 접근 권한을 부여받는 것이다. 인증을 통해 인증 상태를 획득한 클라이언트는 서버에게 자원이나 기능을 요청할 때마다 이 인증 상태를 동봉하여 접근 권한을 증명할 수 있다.



## 쿠키 사용하기

**쿠키(cookie)**는 브라우저에 저장되는 키-값 형식의 문자열 데이터이다. 최대 4킬로바이트까지 저장 가능하다. 쿠키의 라이프사이클은 다음과 같다.

1. 클라이언트가 쿠키 생성을 요청한다.
2. 서버는 쿠키를 만들어 HTTP 응답의 `Set-Cookie` 헤더에 실어보낸다. 이때 쿠키 옵션을 설정해줄 수 있다.
   1. path, domain: 쿠키가 붙어갈 유효 범위를 지정한다.
   2. expires, max-age: 쿠키의 만료 기간을 지정한다.
   3. httpOnly: 자바스크립트 접근을 막는다.
   4. Secure: 쿠키를 HTTPS로 암호화한다.
3. 클라이언트는 쿠키를 받아 저장한다.
4. 이후 클라이언트는 동일한 서버에게 요청을 보낼 때 쿠키를 **HTTP 요청의 `Cookie` 헤더**에 실어보낸다.
5. 쿠키에 설정된 유효 기간이 지나면 쿠키는 자동으로 소멸된다.

쿠키는 클라이언트에 저장되어 언제나 위변조될 위험이 있다.

### 쿠키의 문제

- 쿠키는 클라이언트에 저장되므로 언제나 변조될 위험이 있다.
- 4KB 이상의 데이터는 저장할 수 없다.
- CSRF(Cross Site Request Forgery)에 취약하다. 사용자가 쿠키를 발급받은 상태에서 태그의 URL로 쿠키가 삽입된 공격 요청을 서버에게 보낼 수 있다.



## 세션 사용하기

**세션(session)**은 사용자가 브라우저를 통해 웹 서버에 접속한 상태이다. 웹 서버는 세션마다 세션 id를 생성하여 메모리나 DB에 저장한다. 쿠키를 통해 세션 id를 클라이언트에게 전송하는 경우, 세션 쿠키(session cookie)를 사용한다고 한다. 사용자는 로그아웃 요청을 통해 쿠키의 만료를 요청할 수 있다.

서버와 클라이언트 모두 세션 정보를 유지한다. 보안면에서는 클라이언트에만 저장하는 것보다 나을 수 있지만 쿠키를 사용하면 쿠키의 문제가 그대로 발생한다. 또한 서버가 여러 대인 경우 인증 상태를 공유하기 위해 별도의 세션 스토리지를 둘 수 있는데, 인증 요청이 하나의 세션 스토리지에 의존하면 부하가 생길 수 있다.



## 웹 스토리지 사용하기

HTML5의 웹 스토리지(로컬 스토리지, 세션 스토리지)를 사용하여 클라이언트에서 데이터를 키-값 형태로 저장한다. 자바스크립트 객체로 저장할 수 있다. 로컬 스토리지는 same origin의 탭, 창 전체에서 공유되며 세션 스토리지는 same origin의 탭, ifram에서 공유된다. 세션 스토리지는 창이 닫히기 전까지 최대 5MB의 데이터를 저장한다(새로 고침해도 남아있다). 로컬 스토리지는 유효 기간 없이 데이터를 저장한다.

### 웹 스토리지의 문제

- 자바스크립트로 접근 가능하여 XSS(Cross Site Scripting) 공격에 취약하다. 사용자가 공격 스크립트를 삽입한 사이트에 접속하여 삽입된 코드를 실행할 수 있으며, 스토리지에 저장한 값이 탈취당할 수 있다.



## 토큰 사용하기

서버의 부하를 줄이고 HTTP의 무상태성을 유지하기 위해 토큰 방식을 사용할 수 있다. 토큰(token)은 사용자의 인증 정보를 담은 문자열이다. Bearer 포맷의 문자열을 담은 Bearer 토큰이나 JWT 토큰을 사용한다. JWT(Json web token)은 JSON 형식의 문자열로, 헤더와 페이로드를 각각 base64 인코딩한 문자열과 서명이 `.`로 구분되어있다. 서명은 인코딩한 두 문자열과 비밀키를 SHA-256으로 암호화하여 만든다.

토큰은 클라이언트에 저장되어 탈취당할 수 있으므로 중요한 정보는 넣지 않는다.

1. 클라이언트가 서버에게 토큰 발급을 요청한다.
2. 서버가 클라이언트에게 토큰을 페이로드에 담아 발급한다.
3. 앞으로 클라이언트는 요청에 토큰을 `Authorization` 헤더에 담아 서버에 보낸다.
4. 서버는 비밀키로 토큰의 유효성을 검사하고 유효하지 않으면 버린다. 토큰이 유효하다면 디코딩하여 사용자의 정보를 확인한다.

클라이언트는 토큰을 쿠키, 웹 스토리지, 메모리에 저장할 수 있다. 토큰이 만료되거나 메모리에 저장했는데 페이지를 새로고침하여 날라갈 경우 발급받은 리프레쉬 토큰으로 액세스 토큰을 재발급받을 수 있다.



## OAuth2.0

OAuth 2.0(Open Authorization 2.0)은 인증에 사용하는 표준 프로토콜이다. 사용자, 클라이언트, 리소스 서버, 인증 서버가 OAuth 2.0을 이루는 구성원이다. 클라이언트는 사용자를 대신하여 인증 서버에게 액세스 토큰을 발급받아 리소스 서버에게 자원을 요청할 수 있다.

1. 클라이언트를 redirect url을 인증 서버에 등록하여 client id, client secret을 발급받는다.
2. 사용자가 제3서비스로 로그인을 요청한다. 클라이언트는 client id로 로그인 페이지를 요청한다.
3. 사용자가 로그인 페이지를 통해 로그인한다. 인증 서버는 authorization code를 생성하고 redirect url로 이동한다.
4. 클라이언트는 redirect url에서 authorization code를 파싱하고 client id, client secret, authorization code를 사용하여 인증 서버에게 액세스 토큰을 요청한다.
5. 인증 서버는 클라이언트에게 액세스 토큰을 보낸다.
6. 클라이언트는 앞으로 리소스 서버에게 Authorization 헤더에 액세스 토큰을 담아 자원을 요청한다.