# 주소창에 URL을 입력하고 엔터를 치면 어떤 일이 발생하는가

>주소창에 `www.example.com`을 입력하고 엔터를 치고 화면에 웹 페이지가 렌더링되기까지 어떤 일이 발생하는지 알아본다.

- [ ] 브라우저 렌더링 과정
- [ ] TCP/IP layer
- [ ] 면접 답변용으로 정리하기



1. 사용자가 주소창에 URL(`www.example.com`)을 입력하고 엔터를 친다.
2. 브라우저가 URL을 프로토콜과 도메인 이름으로 파싱한다.
3. 프로토콜과 도메인 이름이 유효한지 검사한다. 유효하지 않다면 주소창의 텍스트를 브라우저 기본 웹 검색 엔진으로 전달한다.
4. HSTS(HTTP Strict Transport Security) 목록에 도메인이 있는지 검사한다. 있다면 웹 서버에 요청할 때 HTTPS로 요청한다.
5. DNS lookup: 도메인 이름을 IP 주소로 변환한다.
   1. 브라우저 캐시에서 도메인 이름을 조회한다.
   2. 없으면 로컬 호스트 파일에서 도메인 이름을 조회한다.
   3. 없으면 DNS 캐시 테이블에서 도메인 이름을 조회한다.
   4. 없으면 Resolver를 호출하여 주소 변환을 요청한다.
      1. Resolver는 DNS 프로토콜을 사용하여 로컬 DNS 서버에 주소 변환을 요청한다.
         1. 로컬 DNS 서버의 IP 주소는 호스트가 네트워크에 접속할 때 ISP가 설정해준다.
         2. 로컬 DNS 서버의 IP 주소를 MAC 주소로 주소로 변환한다.
            1. ARP 캐시 테이블에서 IP 주소를 조회한다.
            2. 없으면 ARP 프로토콜을 사용하여 ARP 캐시 테이블을 갱신한다.
               1. ARP request: ARP 메시지 브로드캐스팅
               2. ARP reply: ARP 메시지 회신
         3. Resolver는 53번 포트로 DNS 메시지를 전송한다.
            1. 기본적으로 UDP를 사용한다.
            2. DNS 메시지의 크기가 512바이트보다 크면 TCP를 사용한다.
      2. 로컬 DNS 서버는 캐시에서 도메인 이름을 조회한다. 없으면 루트 DNS 서버에 질의한다.
      3. 루트 DNS 서버는 도메인 정보가 없다면 `.com` TLD 서버의 IP 주소를 응답한다.
      4. 로컬 DNS 서버는 `.com` TLD 서버에 질의한다.
      5. `.com` TLD 서버는 도메인 정보가 없다면 `.example.com` 서버의 IP 주소를 응답한다.
      6. `.example.com` DNS 서버는 IP 주소를 응답한다.
      7. 로컬 DNS 서버는 IP 주소를 캐싱하고 Resolver에 IP 주소를 응답한다.
   5. Resolver는 브라우저에게 IP 주소를 전달한다.
6. TCP 3-way handshake: 클라이언트와 서버가 443번 포트로 TCP 연결을 설정한다.
   1. 클라이언트가 서버에게 연결을 요청하는 SYN 패킷을 보낸다.
   2. 서버는 클라이언트에게 연결을 허가하는 ACK, SYN 패킷을 보낸다.
   3. 클라이언트는 서버에게 연결을 허가하는 패킷을 받았다는 ACK 패킷을 보낸다.

7. TLS handshake: 클라이언트와 서버가 세션 키를 분배한다.
   1. Client Hello: TLS 버전, 클라이언트가 생성한 랜덤 데이터, 클라이언트가 지원하는 암호화 방식, 세션 아이디(기존의 세션이 있다면 재활용)을 전송한다.
   2. Server Hello: TLS 버전, 서버가 생성한 랜덤 데이터, 서버가 선택한 암호화 방식을 전송한다.
   3. Server Certificate: 인증서를 전송한다.
   4. Server Hello Done: 서버가 클라이언트에게 메시지를 모두 보내었다.
   5. Client Key Exchange: 클라이언트는 CA의 공개 키로 인증서를 복호화하여 인증서의 유효성을 검증하고 서버의 공개 키를 얻는다. 클라이언트는 서버의 랜덤 데이터와 클라이언트의 랜덤 데이터를 조합하여 pre master secret 값을 만들고 서버의 공개 키로 암호화한다. 서버에게 해당 값을 전송한다. 서버는 자신의 비밀 키로 해당 값을 복호화한다.
   6. Key Generation: 클라이언트와 서버는 pre master secret 값으로 master secret 값을 생성하고 이 값으로 session key를 만든다.
   7. Client Change Cipher Spec & Finished: 앞으로 session key로 암호화하겠다. TLS handshake를 종료한다.
   8. Server Change Cipher Spec & Finished: 앞으로 session key로 암호화하겠다. TLS handshake를 종료한다.

8. TLS 세션을 사용하여 HTTP 통신: 세션 키를 사용하여 HTTP 메시지를 암호화한다.
   1. 클라이언트는 서버에게 `www.example.com`에 해당하는 자원을 요청한다.
   2. 서버는 클라이언트에게 `www.example.com`에 해당하는 자원을 응답한다.

9. TLS 세션 종료: 클라이언트와 서버가 세션 키를 폐기한다.
10. TCP 4-way handshake: 클라이언트와 서버가 TCP 연결을 해제한다.
    1. 클라이언트가 서버에게 연결 해제를 요청하는 FIN 패킷을 보낸다.
    2. 서버는 클라이언트에게 연결 해제를 승인하는 ACK 패킷을 보낸다. 다음 단계 전까지 서버는 클라이언트에게 데이터를 전송할 수 있고 클라이언트는 서버로부터 데이터를 받을 수 있다.
    3. 서버가 클라이언트에게 연결을 해제하는 FIN 패킷을 보낸다.
    4. 클라이언트는 서버에게 연결 해제를 최종적으로 승인하는 ACK 패킷을 보낸다.




## 참고

- [What happens when](https://github.com/alex/what-happens-when)
- [TCP/IP 이론 — DNS 캐시 테이블](https://medium.com/pocs/tcp-ip-%EC%9D%B4%EB%A1%A0-dns-%EC%BA%90%EC%8B%9C-%ED%85%8C%EC%9D%B4%EB%B8%94-6f12c4b44653)

