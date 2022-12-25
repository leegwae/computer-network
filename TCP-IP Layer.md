# TCP/IP Layer

<img src="https://user-images.githubusercontent.com/57662010/209475219-5a968f4c-3c9a-48ad-9a2b-c1e4106e72d4.png" alt="Network Model" style="zoom: 67%;" />

실제 네트워크 구현 모델은 TCP/IP 모델을 따르고 있다. 응용 계층은 프로세스가 동작한다. 전송 계층의 TCP와 UDP는 커널 내부에 구현되어 사용자 프로세스는 시스템 콜의 형태로 제공되는 소켓(Socket) 인터페이스를 사용한다. 네트워크 계층 이하의 계층은 LAN 카드와 LAN 카드 드라이버 루틴으로 구현된다. 갱신된 TCP/IP 모델은 5계층으로, Network Access Layer가 Data Link Layer와 Phsycial Layer로 분리되어있다.

네트워크 응용 프로그램에는 텔넷, FTP, 웹 브라우저 등이 있다. 소켓마다 고유 주소로 포트 번호가 부여되며, 네트워크 응용 프로그램은 일반적으로 하나의 포트 번호에 대응한다. 인터넷 응용 프로그램의 고유 주소는 IP 주소와 포트 번호의 조합으로 구성된다.

TCP/IP 모델에서 ARP/RARP와 ICMP는 IP 계층에서 사용된다. ARP(Address Resolution Protocol)는 IP 주소를 MAC 주소로 변환하는 프로토콜이다. 송신 호스트가 수신 호스트의 MAC 주소를 얻기 위해 사용한다. RARP(Reverse Address Resolution Protocol)는 MAC 주소를 IP 주소로 변환하는 프로토콜이다. IP 주소는 파일에 보관되는데, 파일 시스템이 존재하지 않는 하드웨어의 경우 LAN 카드의 MAC 주소만 알기 때문에 사용한다. ICMP는 전송 오류가 발생하면 복구 작업을 위해 오류 메시지를 전송하는 프로토콜이다.