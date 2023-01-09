# Web Server and WAS

## 정적 페이지와 동적 페이지

- 정적 페이지(static page)는 HTML, CSS, JavaScript로 작성된다. 서버는 클라이언트의 요청에 항상 동일한 페이지를 응답한다. 서버의 파일들을 수정하기 전까지 사용자는 동일한 페이지를 보게 된다.
- 동적 페이지(dynamic page)는 CGI, AJAX, JSP, Servlet 등으로 작성된다. 서버는 프로그램을 실행하여 페이지를 생성하고 해당 페이지를 응답한다. 사용자는 조건에 따라 매번 다른 페이지를 보게 될 수 있다.



## 웹 서버와 애플리케이션 서버

### Web Server

- **웹 서버(Web Server)**는 HTTP 프로토콜을 사용하여 클라이언트의 요청을 처리한다.
  1. 클라이언트의 요청에 정적 파일을 응답한다.
  2. 클라이언트의 요청을 WAS에 전달하고 WAS가 생성한 동적 파일을 클라이언트에게 응답한다.
- 웹 서버는 웹 서버가 실행되는 컴퓨터를 가리키기도 한다.
- 리버스 프록시의 역할을 수행하고 캐시 기능을 제공한다.
- 예) Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등

### WAS

- WAS(Web Application Server)는 HTTP 프로토콜을 사용하여 웹 애플리케이션을 실행하고 그 결과를 웹 서버에게 응답한다.
- 데이터베이스에 접속하거나 비지니스 로직을 수행하여 동적 페이지를 생성한다.
- WAS는 보통 Web Server의 기능을 자체적으로 내장한다.
- 예) Apache Tomcat, WebSphere, JBoss, JEUS



## 참고

- [geeksforgeeks - Difference between Static and Dynamic Web Pages](https://www.geeksforgeeks.org/difference-between-static-and-dynamic-web-pages/)
- [geeksforgeeks - Difference Between Web server and Application server](https://www.geeksforgeeks.org/difference-between-web-server-and-application-server/?ref=rp)
- [[Web] Web Server와 WAS의 차이와 웹 서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)



## 스터디

### Web Server와 WAS를 분리하면 어떤 장점이 있는가?

웹 서버가 정적 파일의 서빙을, WAS가 DB 조회나 비지니스 로직을 담당하도록 하여 서버 부하를 방지할 수 있다. 여러 대의 WAS를 Web Server에 연결하여 로드밸런싱을 적용할 수 있다.

