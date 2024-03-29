# Network Basics

**네트워크(network)**는 물리적인 전송 매체를 통해 연결되어 데이터를 교환하는 **시스템(system)**의 모임이다. 이 네트워크를 구성하는 시스템을 일반적으로 **노드(node)**라고 하는데, 특히 컴퓨팅 기능이 있는 시스템은 **호스트(host)**라고 한다. 호스트는 다른 말로도 **종단(end system)**이라고도 한다.

한편 호스트는 서버와 클라이언트로 그 역할을 나누어볼 수 있다. **클라이언트(client)**는 서버에게 서비스를 요청하고 응답을 받아 서비스를 이용한다. **서버(server)**는 클라이언트의 요청을 대기하고 요청을 받아 서비스를 제공한다.

**프로토콜(protocol)**은 송신자와 수신자 간에 데이터를 전달하고 전달받는 절차나 데이터 양식 따위를 정의한 것이다. 이때 송수진자 간에 전달되는 데이터를 일반적으로 **패킷(packet)**이라고 한다. 패킷은 제어 정보와 사용자 데이터로 이루어지며, 사용자 데이터는 본문(body) 또는 **페이로드(payload)**라고도 한다.



## 기초 용어

### 네트워크 기초 용어

#### 네트워크

**네트워크(Network)**는 전송 매체를 통해 연결되어 데이터를 교환하는 시스템(System)의 모임이다. 즉, 물리적으로 호스트 시스템과 전송 매체로 구분된다.

#### 시스템

**시스템(System)**은 내부 규칙에 따라 능동적으로 동작하는 대상을 가리킨다.

#### 전송 매체

**전송 매체(Transmission Media)**는 시스템이 데이터를 교환하기 위해 사용하는 물리적인 전송 수단이다.

#### 인터페이스

**인터페이스(Interface)**는 시스템과 전송 매체의 연결 지점에 대한 규격이다.

#### 프로토콜

**프로토콜(Protocol)**은 시스템이 데이터를 교환할 때 따르는 표준화된 통신 규칙이다.

####  인터페이스와 프로토콜의 차이

인터페이스는 시스템을 연동하기 위한 특정 접촉 지점(Access Point)를 가리킨다. 프로토콜은 데이터를 주고받을 때 그 데이터의 형식이나 발생하는 절차적 순서를 가리킨다.

#### 표준화

**표준화(Standardization)**는 시스템이 상호 연동하여 동작하기 위해 연동 형식을 통일하는 것을 뜻한다.

#### 인터넷

**인터넷(Internet)**는 전 세계의 모든 네트워크가 연결되어 동작하는 통합 네트워크이다. 인터넷으로 연결된 시스템, 인터페이스, 전송 매체, 프로토콜은 종류가 매우 다양하나 데이터 전달 기능은 **IP(Internet Protocol)**만을 사용한다.



### 시스템 기초 용어

#### 시스템의 구분

네트워크를 구성하는 시스템은 수행하는 기능에 따라 다음과 같이 부를 수 있다.

- **노드(Node)**: 일반적으로 인터넷에 연결된 시스템을 의미한다. 데이터를 주고받는 시스템을 통칭한다.
- **호스트(Host)**: 일반적으로 컴퓨팅 기능이 있는 시스템을 의미한다. 일반 사용자는 호스트 내의 응용 프로그램을 실행하여 네트워크에 접속한다.

한편, 호스트는 클라이언트와 서버로 나눌 수 있다.

#### 클라이언트와 서버

호스트는 이용하는 서비스의 종류에 따라, 혹은 특정 서비스를 기준으로 상대적인 관점에서 클라이언트와 서버로 나눌 수 있다.

- **클라이언트(Client)**: 서버에 서비스를 요청하고, 서비스를 이용하는 시스템이다.
- **서버(Server)**: 클라이언트의 요청을 대기하고, 클라이언트의 요청에 따라 서비스를 제공하는 시스템이다.



## 네트워크의 구분

네트워크는 호스트 간의 거리를 기준으로 구분할 수 있다.

- **LAN(Local Area Network)**는 하나의 건물 같은 소규모 지역에서 물리적으로 연결된 호스트로 구성된 네트워크이다. 
- **MAN(Metropolitan Area Network)**는 여러 대의 건물이나 하나의 도시 정도의 규모를 대상으로 하는 네트워크이다.
- **WAN(Wide Area Network)**는 국가 이상의 넓은 지역을 대상으로 하는 네트워크이다. 호스트 사이의 거리가 가장 멀다.



## 네트워크의 기능

컴퓨터 네트워크는 그 기능을 연관된 그룹으로 묶어 계층 모델로 설명할 수 있다.

### 계층 모델

서로 다른 시스템 간의 연결을 위해 표준된 연결 방식이 필요하다. 국제 표준화 기구인 **ISO(International Standard Organization)**는 **OSI(Open System Interconnectioin)** 7계층 모델로 네트워크 시스템이 갖춰야할 기능을 정의한다.

OSI 7 계층에 대해서는 [다음](https://github.com/leegwae/computer-network/blob/main/osi-7-layer-model.md)을 참고한다.

### 인터네트워킹

**인터네트워킹(Internetworking)**은 네트워크와 네트워크의 연결을 의미한다. 예를 들어 여러 독립적인 LAN을 WAN을 통해 연결하는 것이다.

#### 네트워크의 연결

네트워크 `A`, 네트워크 `B`를 연결하는 인터네트워킹 시스템 `Z`은 양쪽 네트워크 모두에게 물리적이고 논리적인 인터페이스를 지원한다. 양쪽 네트워크의 프로토콜이 일치하는데 필요한 변환 작업 역시 수행한다.

### 게이트웨이

**게이트웨이(Gateway)**는 인터네트워킹 기능(네트워크 간의 연결)을 수행하는 시스템을 의미한다. 리피터, 브리지, 라우터로 구분할 수 있다.

- **리피터(Repeater)**: 물리 계층의 기능을 지원하여, 한쪽에서 입력된 신호를 물리적으로 증폭하여 다른 쪽으로 넘긴다.
- **브리지(Bridge)**: 물리 계층에서 발생한 오류를 해결한다. 리피터의 기능에 데이터 링크 계층의 기능이 추가된 것이다.
- **라우터(Router)**: 물리, 데이터 링크, 네트워크 계층의 기능을 지원한다. 경로 선택 기능을 제공하기 위해 네트워크와 호스트에 대한 정보를 보관한다.



## 네트워크 주소의 표현

### 주소와 이름

네트워크 시스템은 내부적인 주소와 일반 사용자를 위한 이름을 부여받는다. 이 주소와 이름은 일대일 관계를 가진다.

- **주소(address)**는 네트워크 시스템을 구별하기 위한 식별자(identifier)로, 숫자로 되어있다.
- **이름(name)**은 일반 사용자가 시스템에 접근할 때 사용하기 쉽도록 기호로 되어있다.

#### IP 주소

**IP 주소(IP Address)**는 네트워크 계층의 기능을 수행하는 IP 프로토콜이 호스트를 구별하기 위해 사용하는 주소 체계이다. 호스트는 인터넷에 연결되기 위해 반드시 IP 주소를 할당받아야한다.

- IPv4(Internet Protocol Version 4): 32비트의 이진수로 주소를 표현한다.
  - 일반적으로 8비트씩 끊어 십진수로 표현하며, `.`로 구분한다.
  - 주소 공간의 크기가 32비트로 제한되어 확장성에 문제가 있다.
- IPv6: IPv4의 문제점을 해결하기 위하여 128비트의 이진수로 주소를 표현한다.

#### 호스트 이름

호스트 이름은 일반 사용자가 호스트를 지칭할 때 사용한다. DNS는 호스트 이름을 다음과 같이 네 계층 구조로 나눈다.

```
<호스트>.<단체 이름>.<단체 종류>.<국가 도메인>
```

예) `google.co.kr` 에서 `google`은 단체 이름, `co`는 일반 회사(company)를 가리키는 단체 종류, `kr`은 한국(korea)를 가리키는 국가 도메인

### 주소 정보의 관리

- 호스트 이름을 **도메인 이름(domain name)**이라고 한다. 
- 네트워크 계층은 IP 주소를 사용하므로, 도메인 이름을 IP 주소로 변환할 수 있어야 한다.
- 변환 방법에는 두 가지가 있다.
  - 호스트 파일 사용하기
  - DNS 사용하기

#### 호스트 파일

- 특정 파일로 호스트의 이름과 IP 주소를 매핑을 기록한다. 예) UNIX의 `/etc/hosts`
- 호스트 파일은 시스템 관리자가 관리하여 수작업으로 갱신한다.

#### DNS 시스템

- **DNS(Domain Name System)**는 주소와 이름을 자동으로 관리하는 분산 데이터베이스 시스템이다.
- **네임 서버(Name Server)**: 주소와 이름을 관리하는 호스트이다. 클라이언트는 네임 서버에 요청하여 IP 주소를 얻는다.
- DNS는 전체 호스트의 정보를 계층 구조를 가진 여러 대의 네임 서버에 분산하여 관리한다.

#### 기타 주소

- MAC(Medium Access Protocol) 주소: 계층 2의 MAC 계층에서 사용한다.
- 포트 주소(port address): 전송 계층에서 사용한다. 호스트에서 실행되는 프로세스를 구분한다. 포트 번호 또는 소켓 주소라고도 부른다.
- 메일 주소: 응용 계층의 메일 시스템에서 사용한다. 사용자를 구분한다. `사용자이름@호스트이름`으로 표기한다.



## 연결형 서비스와 비연결형 서비스

송신자 호스트와 수신자 호스트는 패킷을 전송하기 전 서로 연결을 설정하거나 그러지 않을 수 있다.

**연결 서비스**는 연결이 설정되는 시점에 전달 경로가 선택된다. 따라서 패킷이 모두 동일한 경로를 통해 전달되어 패킷의 전달 순서가 보장된다. 또한 패킷이 제대로 도착했는지를 확인한다. 

**비연결 서비스**는 매 전송마다 전달 경로를 선택한다. 따라서 패킷이 서로 다른 경로를 통해 전달되어 패킷의 전달 순서가 보장되지 않는다. 또한 패킷이 제대로 도착했는지를 확인하지 않는다. 그래서 연결 서비스보다 데이터의 신뢰성이 떨어진다.



## 교환 방식

종단 호스트들이 전송하는 패킷은 네트워크 전송 경로에서 교환 시스템을 거친다. 교환 시스템은 패킷을 목적지까지 중개하는 **교환(switching) 기능**을 제공한다. 교환 기능은 연결형 서비스를 제공하는 회선 교환 방식과 비연결형 서비스를 제공하는 패킷 교환 방식으로 구분된다.



### 회선 교환 방식

**회선 교환(Circuit Switching) 방식**은 송수신 호스트가 패킷을 전달하기 전 연결을 설정한다. 송수신자는 고정 대역폭을 할당받아 독점하여 고정 크기의 안정적인 데이터 전송률을 지원한다.

대용량의 데이터나 연속된 데이터를 전송하기에 좋다. 주로 전화망에 사용한다.

그러나 연결을 설정하는 오버헤드가 있다. 송수신자는 할당받은 대역폭을 독점하므로 데이터를 전송하지 않는 경우에도 다른 호스트가 사용할 수 없다는 점에서 비효율적이다.



### 패킷 교환 방식

패킷 교환 방식(Packet Switching) 방식에서 송수신 호스트는 데이터를 패킷 단위로 나누어 전송한다. 대역을 독점하지 않아 가변 크기의 데이터 전송률을 지원한다. 대역폭을 독점하지 않으므로 전송 선로를 효율적으로 사용할 수 있다. 주로 컴퓨터 네트워크망에 사용한다.

패킷 교환 방식은 가상 회선 방식과 데이터그램 방식으로 나뉜다. **가상 회선 패킷 교환 방식**은 연결형 서비스를 지원한다. 모든 패킷은 일정한 경로를 통하여 전송된다. **데이터그램 패킷 교환 방식**에서는 비연결형 서비스를 지원한다. 패킷이 각각의 경로를 통하여 전송된다. 이때의 패킷을 데이터그램이라고 한다.



## 인터넷과 웹

**인터넷(Internet)**은 컴퓨터로 이루어진 네트워크다. **웹(WWW, W3, Web; World Wide Web)**은 인터넷에 연결된 호스트가 데이터를 주고받을 수 있는 공간이다. 웹에서 호스트는 HTTP(HyperText Transfer Protocol)를 사용하여 하이퍼텍스트(hypertext) 형식의 데이터를 주고받을 수 있다(현재는 이미지, 비디오, 음성 등 거의 모든 형식의 데이터를 주고받을 수 있어 하이퍼미디어라고 한다). 웹 서비스는 클라이언트와 서버 모델을 사용한다.

일반적으로 웹 서버의 TCP 포트 번호는 80번이다. 웹 브라우저는 80번으로 TCP 연결한다.



## 스터디

### 네트워크, 인터넷, 웹에 대해 설명해주세요

네트워크(network)은 전송 매체를 통해 연결되어 데이터를 교환하는 시스템의 모임이다. 인터넷(Internet)은 컴퓨터로 이루어진 네트워크이다. 웹(Web)은 인터넷에 연결된 호스트가 데이터를 주고 받을 수 있는 공간이다.

### 게이트웨이란 무엇인가

게이트웨이는 네트워크 간의 연결을 수행하는 시스템을 말한다. 리피터, 브리지, 라우터가 있다.

### 패킷 교환 방식은 무엇인가요? 주로 어디에 사용하는가?

송수신 호스트가 데이터를 패킷 단위로 나누어 전송하는 교환 기능이다. 주로 컴퓨터 네트워크 환경에서 사용된다.

#### 회선 교환 방식에 비교하여 패킷 교환 방식의 장점은?

대역을 독점하지 않아서 전송 선로를 효율적으로 사용할 수 있다.

#### 연결형 서비스를 지원하는 가상 회선 패킷 교환 방식과 비연결형 서비스를 지원하는 데이터그램 패킷 교환 방식이 무엇이고 차이는 무엇인가?

가상 회선 패킷 교환 방식이 연결형 서비스를 지원하고 데이터그램 패킷 교환 방식이 비연결형 서비스를 지원한다. 가상 회선의 경우 데이터를 전송하기 전 송수신 호스트가 연결을 설정한다. 패킷이 전송될 때마다 같은 경로로 전달되어 전달 순서가 보장된다. 데이터그램의 경우 연결을 설정하지 않아 데이터그램이 서로 다른 경로로 전달될 수 있다.
