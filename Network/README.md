# Network 

<br>

<details>
<summary style="font-size:20px">OSI 7계층와 TCP/IP 4계층</summary>
<div markdown="1">

![image](https://user-images.githubusercontent.com/38535571/230088639-3eeec45b-5ad5-48e6-8217-0e076cde69b0.png)

#### OSI 7계층
* 네트워크의 통신 과정을 7단계로 나눠 표준화한 것
* ISO(국제표준기구)에서 만듦 

#### OSI Application(7, Message or Data)
* 사용자에게 `실제 애플리케이션 서비스를 제공`하는 계층
* HTTP, FTP, DNS
#### OSI Presentation(6, Message or Data)
* 애플리케이션의 `데이터 형태와 구조를 변환(번역, 암호화, 압축)`시키는 계층
* 코드 간의 번역을 담당 -> 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어줌
#### OSI Session(5, Message or Data)
* 양 끝단의 응용 프로세스가 `통신을 관리하기 위한 방법`을 제공
  * 동시 송수신 방식(duplex)- 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신 등
* 애플리케이션 간의 `TCP/IP 세션을 구축하고 관리하며 종료`시키는 계층
* Socket
#### OSI Transport(4, Segment)
* 통신 `양단 간의 신뢰성 있는 통신`을 보장하는 계층
* TCP, UDP
#### OSI Network(3, Packet)
* 목적지까지의 경로를 선택하고 `경로에 따라 패킷을 전달(라우팅)`해주는 계층
* IP / 라우터
#### OSI Link(2, Frame)
* 인접한 `피어 간의 신뢰성 있는 통신`을 보장하는 계층
* ARP, MAC / 브릿지, 스위치
#### OSI Physical(1, Bit)
* 전기적, 기계적, 기능적인 특성을 이용해서 `통신 케이블로 데이터를 전송`
* 리피터, 케이블, 허브, NIC

#### TCP/IP 4계층
* 네트워크 통신 과정을 4계층으로 나눠 표현한 것
* TCP/IP 4계층에서 에플리케이션 계층을 3개로 쪼개고 인터넷 계층을 네트워크 계층이라고 부르면서 링크 계층을 데이터 링크 계층과 물리 계층으로 나누면 OSI 7계층이 됨

#### TCP/IP Application(4, Message)
* 응용 프로그램이 사용되는 프로토콜 계층
* HTTP, FTP, DNS
#### TCP/IP Transport(3, Segment)
* 송신자와 수신자를 연결하는 통신 서비스를 제공하며 애플리케이션과 인터넷 계층 사이의 데이터가 전달될 때 중계하는 역할을 하는 계층
* TCP, UDP
#### TCP/IP Internet(2, Packet)
* 장치로부터 받은 네트워크 패킷을 IP 주소로 지정된 목적지로 전송하기 위해 사용되는 계층
* IP
#### TCP/IP Link(1,Frame/Bit)
* 전선, 광섬유, 무선 등 실질적으로 데이터를 전달하며 장치 간에 신호를 주고 받는 규칙을 정하는 계층

</div>
</details>


<details>
<summary style="font-size:20px">PDU</summary>
<div markdown="1">

#### PDU
![image](https://user-images.githubusercontent.com/38535571/230087342-ff3182cc-c6e1-485b-aeb2-71fd91e492cc.png)
* 네트워크 어떠한 계층에서 다른 계층으로 데이터가 전달될 때 한 덩이리의 단위를 PDU(Protocal Data Unit)이라고 함
* PDU는 메타 정보를 갖고 있는 `헤더`와 데이터를 의미하는 `페이로드`로 구성되며 계층마다 부르는 명칭이 다름

#### 캡슐화와 비캡슐화
![image](https://user-images.githubusercontent.com/38535571/230087480-27c5292e-8066-4dae-aaf4-a21dd47ca4f9.png)
* 캡슐화 과정은 상위 계층의 헤더와 데이터를 하위 계층의 데이터 부분에 포함시키고 해당 계층의 헤더를 삽입하는 과정
* 비캡슐화 과정은 하위 계층에서 상위 계층으로 가며 각 계층의 헤더 부분을 제거하는 과정
* 송신자의 애플리케이션 계층에서부터 각 계층에서 캡슐화를 통해 데이터가 생성되고 수신자의 링크 계층에서부터 각 계층에서 비캡슐화를 통해 데이터가 전달

</div>
</details>

<details>
<summary style="font-size:20px">TCP와 UDP</summary>
<div markdown="1"> 

#### TCP
* `신뢰성을 보장하는 연결형 프로토콜`
* `흐름제어, 혼잡제어`를 제공
* 웹 HTTP 통신, 이메일, 파일 전송에서 사용 

#### UDP
* `신뢰성을 보장하지 않는 비연결형 프로토콜`
* 흐름제어, 혼잡제어를 제공하지 않음
* 속도가 중요한 서비스(스트리밍)에서 사용
* UDP 자체는 신뢰성을 보장하지 않지만 추가적인 정의를 통해 보장 가능 (HTTP/3에서 QUIC 프로토콜) 

</div>
</details> 

<details>
<summary style="font-size:20px">TCP 흐름제어</summary>
<div markdown="1"> 

#### TCP 흐름제어
* `수신자와 송신자`의 메시지 처리속도 차이를 해결하기 위한 방법
* 수신자는 윈도우 크기를 자신의 응답 헤더에 담아서 송신 측에게 전해주게 되고, 송신자는 상대방에게 데이터를 보낼 때 이 윈도우 크기를 확인

#### 종류
##### Stop and Wait
![image](https://user-images.githubusercontent.com/38535571/230088843-64d1d387-0105-42a6-be71-5313a904db4d.png)
* 전송한 패킷의 ACK을 수신하면 다음 패킷 전송 

##### Sliding Window - Go Back N
![image](https://user-images.githubusercontent.com/38535571/230088958-430d6c0c-ccd1-44a1-b06a-e9e3f7191572.png)

* 수신 측에서 설정한 윈도우 크기만큼의 패킷을 ACK의 확인 없이 전송, 데이터의 흐름을 동적으로 조절하는데 Cumulative ACK(마지막으로 수신 성공한 패킷의 ACK을 계속 전송)을 받고 문제가 된 패킷부터는 모두 재전송

##### Sliding Window - Selective Repeat
* 수신 측에서 설정한 윈도우 크기만큼의 패킷을 ACK의 확인 없이 전송, 데이터의 흐름을 동적으로 조절하는데 Selective ACK(수신 성공한 패킷의 개별 ACK 전송)을 받고 문제가 된 패킷만 재전송 

</div>
</details> 

<details>
<summary style="font-size:20px">TCP 오류제어</summary>
<div markdown="1"> 

#### TCP 오류제어
* TCP 오류 제어는 수신자와 송신자의 패킷 오류 처리를 하는 방법
* 수신자가 송신자에게 명시적으로 NACK(부정응답)을 보내거나 송신자에게 ACK(긍정응답)가 오지 않거나 중복된 ACK가 계속 해서 오면 오류가 발생했다고 판단

#### 종류

##### Stop and Wait ARQ
![image](https://user-images.githubusercontent.com/38535571/230089063-3f38e92f-18c8-4fe0-960f-574930b1b7c2.png)
* 송신 측에서 1개의 프레임을 송신하고, 수신측에서 수신된 프레임의 에러 유무에 따라 ACK 혹은 NAK를 보내는 방식

##### Go Back N ARQ과 SR(Selective-Reject) ARQ
![image](https://user-images.githubusercontent.com/38535571/230089122-4e131f97-3c44-4a69-bf3d-76feb0c46f7d.png)

* Go Back N ARQ: 전송된 프레임이 손상되거나 분실된 경우 그리고 ACK 패킷의 손실로 인한 타임아웃이 발생한 경우에 확인된 마지막 프레임 이후로 모든 프레임을 재전송하는 방식
* SR(Selective-Reject) ARQ: 손실된 프레임만 재전송하여 Go Back N ARQ의 확인된 마지막 프레임 이후의 모든 프레임을 재전송하는 단점을 보완한 기법

</div>
</details>

<details>
<summary style="font-size:20px">TCP 혼잡제어</summary>
<div markdown="1"> 

#### TCP 혼잡제어
* `송신자와 네트워크(라우터)`의 데이터 처리 속도 차이를 해결하기 위한 방법
* 패킷 손실 시 파악되는 타임 아웃이나 중복된 ACK을 통해서 혼잡을 파악
* ACK을 확인하지 않고도 보낼 수 있는 데이터 양인 CWND(Congestion Window)를 기반으로 동작

#### 종류

##### Additive Increase/Multicative Decrease
![image](https://user-images.githubusercontent.com/38535571/230089448-878526f9-afab-4fb3-a575-96af91da0c6e.png)
* CWND를 기본 값에서 시작하여 1씩 증가시키는 방법

##### Slow Start
![image](https://user-images.githubusercontent.com/38535571/230089559-d3a441a1-9710-4762-b077-1e25420113be.png)
* CWND가 1부터 지수적(2배)으로 증가시키는 방법
##### Congestion Avoidance(혼잡 회피)
* CWND가 임계치에 도달하면 1씩 증가키는 방법

##### Fast Recovery(빠른 회복)
* 혼잡 상황에서 사용되는 기법으로 CWND를 1/2배로 감소하고 선형적 증가시키는 방법
##### Fast Retransmit(빠른 재전송)
* 중복 ACK를 3개 받으면 재전송을 하는 방법

</div>
</details>

<details>
<summary style="font-size:20px">TCP 3-Way Handshake</summary>
<div markdown="1"> 

#### TCP 3-Way Handshake
![image](https://user-images.githubusercontent.com/38535571/230090204-4d27034e-9954-4a5a-b14b-105cf1bcafef.png)
* 서버와 클라이언트가 TCP `연결을 맺을 때` 사용

#### TCP 3-Way Handshake 과정
* 클라이언트는 서버로 통신을 시작하겠다는 SYN을 보낸다.
* 서버는 그에 대한 응답으로 SYN+ACK를 보낸다.
* 마지막으로 클라이언트는 서버로부터 받은 패킷에 대한 응답으로 ACK를 보낸다.

#### TCP 3-Way Handshake 상태

* LISTEN: 포트가 열린 상태로 연결 요청 대기 중인 상태
* SYN-SENT: SYN 요청을 한 상태
* SYN-RECEIVED: SYN 요청을 받고 상대방의 응답을 기다리는 중인 상태
* ESTABLISEHD: 연결의 수립이 완료된 상태, 서로 데이터를 교환할 수 있음

#### 필요성
* TCP는 양방향 프로토콜이므로 클라이언트와 서버가 각각 서로에게 패킷을 전송할 수 있다는 것을 확인해야 됨 

#### Sequence Number를 난수로 이용하는 이유
* 연결을 맺을 때 사용하는 포트(port)는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용됨
* 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용할 가능성이 존재함
* 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데, 난수가 아닌 순차적인 number가 전송된다면 이전의 연결로부터 오는 패킷으로 인식할 위험이 있음 

</div>
</details>

<details>
<summary style="font-size:20px">TCP 4-Way Handshake</summary>
<div markdown="1"> 

#### TCP 4-Way Handshake
![image](https://user-images.githubusercontent.com/38535571/230090283-f712544c-4d3d-43c8-b751-3ce893704e20.png)
* 서버와 클라이언트가 TCP `연결을 종료할 때` 사용

#### TCP 4-Way Handshake 과정
* 클라이언트는 응답을 주고 연결을 끊기 위해 FIN패킷을 보낸다.
* 서버는 클라이언트에서 보낸 패킷에 대한 응답으로 ACK 패킷을 보낸다.
* 서버는 자신의 통신이 모두 끝나면 사용한 소켓을 정리하며 통신을 완전히 끝내도 된다는 의미로 FIN 패킷을 보낸다.
* 클라이언트는 서버 패킷에 대한 응답으로 ACK패킷을 보낸다.

#### TCP 4-Way Handshake 상태
* CLOSE-WAIT	상대방의 FIN(종료 요청)을 받은 상태 (상대방 FIN에 대한 ACK를 보내고 애플리케이션에 종료를 알림)
* FIN-WAIT-1	자신이 보낸 FIN에 대한 ACK를 기다리거나 상대방의 FIN을 기다리는 상태
* LAST-ACK	CLOSE-WAIT 상태를 처리 후 자신의 FIN요청을 보낸 후 FIN에 대한 ACK를 기다리는 상태
* FIN-WAIT-2	자신이 보낸 FIN에 대한 ACK를 받았고 상대방의 FIN을 기다리는 상태
* TIME-WAIT	모든 FIN에 대한 ACK를 받고 연결 종료가 완료된 상태 (새 연결과 겹치지 않도록 일정 시간 동안 기다린 후 CLOSED로 전이)
* CLOSE	연결 수립을 시작하기 전의 기본 상태 (연결 없음)

#### 필요성
* 클라이언트가 일방적으로 끊으면 서버는 `연결은 되어 있으나 요청이 없는 상태`로 오해할 수 있음
* 클라이언트는 데이터 전송을 끝냈다고 하더라도 서버는 전송할 것이 남아있을 수 있음 

</div>
</details>

<details>
<summary style="font-size:20px">IP 주소 체계</summary>
<div markdown="1"> 

#### IPv4
* 현재 일반적으로 사용되는 주소 체계
* 32비트를 8비트로 단위로 점을 찍어 표기하는 방식
* 123.45.67.88 같은 방식으로 표기됨

#### IPv6
* IPv4의 주소의 개수가 부족 문제를 해결하기 위해 생긴 주소 체계
* 64비트를 16비트 단위로 점을 찍어 표기하는 방식
* 2001:db8::ff00:42:8329 같은 방식으로 표기됨


#### IPv4 IPv6 헤더
![image](https://user-images.githubusercontent.com/38535571/230091358-80da4098-409a-4315-afa2-0b7fd03b7513.png)

#### IPv4 IPv6 패킷
![image](https://user-images.githubusercontent.com/38535571/230091472-20cb9246-77ef-47e2-9401-597a7e51d130.png)
![image](https://user-images.githubusercontent.com/38535571/230091539-a2455449-b874-466c-8b37-9fe6d5af24b8.png)

</div>
</details>

<details>
<summary style="font-size:20px">클래스 기반 할당 방식</summary>
<div markdown="1"> 

#### 클래스 기반 할당 방식
![image](https://user-images.githubusercontent.com/38535571/230091833-02061247-24a4-4a54-bce3-d8dbf125f81b.png)
* 클래스를 구분하여 대역을 설정하여 앞에 있는 부분을 네트워크 주소, 그 뒷 부분을 주소인의 호스트 주소로 IP를 활용하는 방법
* A 클래스의 12.0.0.0 네트워크를 부여받았다면 12.255.255.255.255는 브로드 캐스트용 주소가 되며 12.0.0.1 ~ 12.255.255.255.254의 호스트 주소로 사용 가능
* 116.0.0.0 네트워크를 부여받았다면 A 클래스이며 116.0.0.1 ~ 12.255.255.255.254의 호스트 주소로 사용 가능

#### 클래스 A
* 앞에 첫번째 바이트를 네트워크 주소로 나머지 3개의 바이트를 호스트 주소로 사용
* 구분 비트가 0 -> 00000000.00000000.00000000.00000000 ~ 01111111.11111111.11111111.11111111
* 대역 0.0.0.0 ~ 127.255.255.255 사용

#### 클래스 B
* 앞에서부터 두번째 바이트까지를 네트워크 주소로 나머지 2개의 바이트를 호스트 주소로 사용
* 구분 비트가 10 -> 10000000.00000000.00000000.00000000 ~ 10111111.11111111.11111111.11111111
* 대역 128.0.0.0 ~ 191.255.255.255 사용

#### 클래스 C
* 앞에서부터 세번째 바이트까지를 네트워크 주소로 나머지 1개의 바이트를 호스트 주소로 사용
* 구분 비트가 110 -> 11000000.00000000.00000000.00000000 ~ 11011111.11111111.11111111.11111111
* 대역 192.0.0.0 ~ 223.255.255.255 사용

</div>
</details>

<details>
<summary style="font-size:20px">CIDR (Classless Inter-Domain Routing) 방식</summary>
<div markdown="1"> 
 
![image](https://user-images.githubusercontent.com/38535571/230092405-0fa92be9-3fc4-43a0-a6b3-30e51d0441b1.png)

 * 클래스 없는 도메인 간 라우팅 기법
* 최신의 IP 주소 할당 방법으로 정적이였던 클래스 방식에 비해 IP 주소의 영역을 여러 네트워크 영역으로 나눌 수 있기 때문에 기존방식에 비해 유연 
* 서브넷으로 최대 호스트 수를 유추할 수 있음
* 예를 들면 10.0.2.23/xx 같은 형식
  * xx 자리수까지는 고정 IP
* 서브넷의 사용 가능 IP 수: 2^(32-xx) - 2
  * 첫번째: 네트워크 주소, 마지막: 브로드캐스팅 주소
* 네트워크가 143.7.65.203/22 이면 앞에 22비트는 네트워크 주소를 나타내고 나머지 10비트는 호스트 주소를 나타내고 143.7.64.0 ~ 143.7.67.255의 호스트 주소를 사용
</div>
</details>

<details>
<summary style="font-size:20px">NAT (Network Address Translation)</summary>
<div markdown="1">

![image](https://user-images.githubusercontent.com/38535571/230092496-4cd47fc8-ea85-4f8e-b47b-82f74572f901.png)

#### 정의
* IP 패킷의 TCP/UDP 포트 숫자와 소스 및 목적지의 IP 주소 등을 `재기록`하면서 `라우터`를 통해 통신하는 기술
* 외부에 공개된 `공인(Public) IP`와 내부에서 사용하는 `사설(Private) IP`를 `맵핑`하여 원활히 통신할 수 있게 하는 기술
* IPv4 주소 체계로 많은 주소를 표기하지 못했는데 이를 해결해준 기술
* 사설 IP를 통하기 때문에 내부망 IP들이 노출되지 않으므로 보안적 강점이 있음
* 외부에서 사설 IP를 알 방법이 없어 내부 네트워크와 호스트를 보호 가능 

#### 동작 과정
##### 요청 패킷 전송하기
* 패킷 헤더 = `소스 IP: 사설 IP`, `목적 IP: 목적지 IP`
* 게이트 웨이에서 `소스 IP: 게이트웨이의 공인 IP`로 변경, `목적 IP: 목적지 IP` 변경 없음
* NAT 테이블에 맵핑 내역을 저장

##### 응답 패킷받기
* 패킷 헤더 = `소스 IP: 목적지 IP`, `목적 IP: 게이트웨이의 공인 IP`
* 게이트 웨이에서 `소스 IP: 목적지 IP` 변경 없음, `목적 IP: 사설 IP`로 변경 (재기록)
* NAT 테이블을 참조하여 수정 

</div>
</details>

<details>
<summary style="font-size:20px">CDN (Contents Delivery Network)</summary>
<div markdown="1"> 

#### CDN
* `지리적, 물리적으로 떨어져 있는` 사용자에게 웹 페이지 콘텐츠 `로드 지연을 최소화`하는 촘촘히 `분산된 서버`로 이루어진 플랫폼 기술
* 각 지역에 캐시 서버(PoP, Points of Presence)를 분산 배치해서 가까운 사용자의 요청에 원본 서버가 아닌 캐시 서버가 콘텐츠를 전달 

#### CDN 사용 시의 이점
* 지리적으로 가까운 캐시 서버가 응답하여 빠른 응답 가능
* Origin 서버에 문제가 생겨도 다른 서버로 대체가 가능해 안전성 증가
* 트래픽 집중 방지 가능 

#### CDN 처리 과정
* 클라이언트는 HTML, 이미지, CSS, JavaScript 파일 등 필요한 콘텐츠를 요청
* `콘텐츠에 대한 각 요청이 발생하면 최적으로 배치된 CDN 서버에 엔드유저가 매핑`
* CDN 서버는 요청된 파일의 `캐싱`된(사전 저장된) 버전으로 응답 

</div>
</details>

<details>
<summary style="font-size:20px">DNS (Domin Name System)</summary>
<div markdown="1"> 

![image](https://user-images.githubusercontent.com/38535571/230093255-b1d91c83-b6e0-4410-96c7-05d9c03c085d.png)

#### 도메인
* 네트워크 상에서 컴퓨터를 식별하는 호스트명

#### DNS
* 컴퓨터를 식별하는 호스트명인 도메인을 실제 서버와 연결 시켜주는 시스템

</div>
</details>

<details>
<summary style="font-size:20px">GSLB (Global Server Load Balancing)</summary>
<div markdown="1"> 

![image](https://user-images.githubusercontent.com/38535571/230092667-f2fbf5e6-bc34-44e4-97a2-0ea5ddd37376.png)

* 전통적인 DNS 서비스를 발전시킨 형태로 헬스 체크와 지리적 정보를 사용하는 시스템
* DNS 기반의 로드 밸런싱으로 IP가 아닌 도메인을 갖음
* DNS와 VIP를 통해서 구성을 한 경우 한 IDC에 서버들이 몰려 있으면 DR 상황에서 문제가 생길 수 있기 때문에 서버의 위치를 고려할 수 있는 GSLB를 사용
* VIP와 GLSB를 함께 사용 할 수도 있고 VIP 없이 GSLB만 서버에 묶어서 구성할 수도 있음
* 일반적인 DNS 방식과 달리 헬스 체크를 통해서 서버가 죽은 경우 해당 서버로 요청이 가지 않도록 할 수 있음
* 일반적인 DNS 방식과 달리 L4/L7의 스위치가 추가로 필요

</div>
</details>


<details>
<summary style="font-size:20px">로드 밸런싱</summary>
<div markdown="1">
 
![image](https://user-images.githubusercontent.com/38535571/230092566-e9686218-692f-43ce-8d0a-65171baacace.png)

#### 로드 밸런싱
* 로드 밸런서를 클라이언트와 서버 사이에 두고, 부하가 집중되지 않도록 여러 서버에 분산하는 방식
* Scale out 시에 사용
* Server Load Balancing이라고도 불림

#### 로드 밸런서
* 로드 밸런싱 작업을 담당하는 장비

#### 로드 밸런서의 역할
* NAT(Network Address Translation): 사설IP - 공인IP 전환
* Tunneling: 데이터를 캡슐화하여 연결된 노드만 캡슐을 해제할 수 있게 만듦
* DSR(동적 소스 라우팅): 요청에 대한 응답을 할 때 로드밸런서가 아닌 클라이언트의 IP로 응답

#### L4 로드 밸런싱
* IP와 PORT 기반의 로드 밸런싱
* 보통 L4 스위치 장비로 로드밸런싱하며 가격이 비쌈
* VIP를 통한 로드 밸런싱은 L4 로드밸런싱

#### L7 로드 밸런싱
* URI, Payload, Http Header, Cookie 등 기반의 로드 밸런싱
* 보통 L7 스위치 장비로 로드밸런싱하며 가격이 비쌈
* nginx나 apache를 통한 로드 밸런싱은 L7 로드밸런싱

#### VIP(Virtual IP)
* 여러 개의 실제 서버를 대표하는 가상의 IP로 DNS와 VIP를 연결하여 다수의 서버에 연결할 때 사용
* VIP는 IP 기반의 `로드 밸런싱`하는 역할을 겸할 수 있음

</div>
</details>

<details>
<summary style="font-size:20px">FQDN</summary>
<div markdown="1"> 

* Fully Qualified Domain Name의 약자로 전체 `주소 도메인 네임`
* 도메인 하위에 서브 도메인을 구성할 수 있는데 FQDN은 서브도메인까지 포함한 Full Domain

</div>
</details>

<details>
<summary style="font-size:20px">ACL</summary>
<div markdown="1"> 

* Access Control List의 약자로 네트워크 망에 접근을 허가하는 IP 리스트와 포트

</div>
</details>

<details>
<summary style="font-size:20px">Proxy 서버</summary>
<div markdown="1"> 

#### 프록시

* 다른 서버와 통신하기 전에 반드시 거치도록 되어 있는 서버로 `클라이언트가 프록시를 통해서 다른 네트워크 서비스에 간접적으로 접속하게하는 서버 프로그램` 함
* Access Control, Cache, 보안 등의 기능을 할 수 있음
* 포워드 프록시라고 부르기도 함

#### 리버스 프록시
* 한 대 이상의 서버로부터 자원을 추출하여 클라이언트에 전달하는 프록시 서버
* 부하 분산이 가능
* 주로 웹 서버를 통해 리버스 프록시 서버를 구축

</div>
</details>

<details>
<summary style="font-size:20px">CORS</summary>
<div markdown="1"> 

* 교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제

</div>
</details>

<details>
<summary style="font-size:20px">웹 브라우저에 URL을 입력했을 때의 수행 과정</summary>
<div markdown="1">

* 사용자의 PC는 `DHCP 서버`에서 사용자 `자신의 IP 주소`, `가장 가까운 라우터의 IP 주소`, `가장 가까운 DNS서버의 IP 주소`를 받음
* `DNS` 서버로 쿼리를 전송해 URL의 `IP 주소`를 응답받음
  * `ARP`를 이용하여 가장 가까운 라우터의 IP 주소로 MAC 주소를 얻어 요청 전송
* TCP Socket을 통해 웹 서버와 `3-Way Hand Shaking`을 하여 연결
* `HTTP Request`가 TCP Socket을 통해 보내지고, 응답으로 웹페이지의 정보가 사용자의 PC에 전달

#### 참고
* DHCP: IP 주소 및 TCP/IP 설정을 클라이언트에 자동으로 제공하는 프로토콜
* DNS: IP 주소와 도메인의 매핑 정보를 관리하는 프로토콜
* ARP: IP 주소를 물리 주소로 변환하는 프로토콜
* IP 주소: 컴퓨터 마다 부여된 고유의 주소, 변할 수 있음
* MAC 주소: NIC 카드 마다 부여된 네트워크 장비 고유의 주소, 변하지 않음

</div>
</details>
