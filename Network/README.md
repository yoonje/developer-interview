# Network 

<br> 

<details>
<summary style="font-size:20px">TCP와 UDP의 차이</summary>
<div markdown="1"> 

#### TCP
* `신뢰성을 보장하는 연결형 프로토콜`
* `흐름제어, 혼잡제어`를 제공
* 웹 HTTP 통신, 이메일, 파일 전송에서 사용 

#### UDP
* `신뢰성을 보장하지 않는 비연결형 프로토콜`
* 흐름제어, 혼잡제어를 제공하지 않음
* 속도 빠르고 연속성이 중요한 서비스(스트리밍)에서 사용
* UDP 자체는 신뢰성을 보장하지 않지만 추가적인 정의를 통해 보장 가능 (HTTP/3에서 QUIC 프로토콜) 

</div>
</details> 

<details>
<summary style="font-size:20px">TCP 흐름제어</summary>
<div markdown="1"> 

* `수신자와 송신자`의 메시지 처리속도 차이를 해결하기 위한 방법
* 수신자와 송신자 세그먼트 간의 TCP Header에 `remain window data`를 통해 남은 버퍼를 알고 흐름을 파악할 수 있음 

#### 종류
##### Stop and Wait
* 전송한 패킷의 ACK을 수신하면 다음 패킷 전송 

##### Sliding Window
* 수신측에서 설정한 윈도우 크기만큼의 패킷을 ACK의 확인 없이 전송, 데이터의 흐름을 동적으로 조절
* `Go Back N`: Cumulative ACK(마지막으로 수신 성공한 패킷의 ACK을 계속 전송), 문제가 된 패킷부터 모두 재전송
* `Selective Repeat`: Individual ACK(수신 성공한 패킷의 개별 ACK 전송), 문제가 된 패킷만 재전송 

</div>
</details> 

<details>
<summary style="font-size:20px">TCP 혼잡제어</summary>
<div markdown="1"> 

* `송신자와 네트워크(라우터)`의 데이터 처리 속도 차이를 해결하기 위한 방법
* 패킷 Loss 시의 확인되는 `Timeout이나 3개의 Duplicate ACK`을 통해서 파악 가능 

#### 종류
* [참고] CWND: Congestion Window, ACK을 확인하지 않고도 보낼 수 있는 데이터 양 (Window Size)
* Slow Start: CWND가 1부터 지수적(2배)으로 증가
* Congestion Avoidance(혼잡 회피): CWND가 1씩 증가
* Fast Recovery(빠른 회복): CWND를 1/2배로 감소하고 선형적 증가 

##### TCP Tahoe
* Slow Start -> ssthresh 도달 -> Congestion Avoidance -> 3개의 duplicate ACK, Timeout 발생 -> Slow Start부터 반복 

##### TCP Reno
* Slow Start -> ssthresh 도달 -> Congestion Avoidance까지는 동일
* Congestion Avoidance 상황에서 3개의 duplicate ACK 발생 -> Fast Recovery
  * TCP Tahoe는 Slow Start로 진입
* Congestion Avoidance 상황에서 Timeout 발생 -> Slow Start 

</div>
</details>

<details>
<summary style="font-size:20px">TCP 3-way Handshake 란</summary>
<div markdown="1"> 

* 서버와 클라이언트가 TCP `연결을 성립할 때` 사용
* Client -> Server: 연결을 요청하는 `SYN(n) 전송`
* Server -> Client: 요청을 수락하는 ` ACK(n+1) 전송` + 연결을 요청하는 `SYN(m) 전송`
* Client -> Server: 요청을 수락하는 `ACK(m+1) 전송` 

#### 필요성
* TCP는 양방향 프로토콜이므로 클라이언트와 서버가 각각 서로에게 패킷을 전송할 수 있다는 것을 확인해야 됨 

#### Sequence Number를 난수로 이용하는 이유
* 연결을 맺을 때 사용하는 포트(port)는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용됨
* 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용할 가능성이 존재함
* 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데, 난수가 아닌 순차적인 number가 전송된다면 이전의 연결로부터 오는 패킷으로 인식할 위험이 있음 

</div>
</details>

<details>
<summary style="font-size:20px">TCP 3-way Handshake 진행 시 서버의 포트가 닫혀있다면 어떻게 되는가 (추가 예정)</summary>
<div markdown="1"> 
 

</div>
</details>

<details>
<summary style="font-size:20px">TCP 4-way Handshake란</summary>
<div markdown="1"> 

* 서버와 클라이언트가 TCP `연결을 종료할 때` 사용
* Client -> Server : 연결을 종료하는 `FIN(n) 전송`
* Server -> Client : 요청을 수락하는 `ACK(n+1) 전송`
* Server -> Client : 연결을 종료하는 `FIN(m) 전송`
* Client -> Server : 요청을 수락하는 `ACK(m+1) 전송` 

#### 타임아웃은 언제, 왜 일어나는가
* 서버의 지연된 패킷을 수신하기 위해 클라이언트에 `Timeout` 존재 (클라이언트가 서버의 FIN을 수신한 이후) 

#### 필요성
* 클라이언트가 일방적으로 끊으면 서버는 `연결은 되어 있으나 요청이 없는 상태`로 오해할 수 있음
* 클라이언트는 데이터 전송을 끝냈다고 하더라도 서버는 전송할 것이 남아있을 수 있음 

</div>
</details>

<details>
<summary style="font-size:20px">TCP 4-way Handshake에서 타임아웃은 언제, 왜 일어나는가</summary>
<div markdown="1"> 

* 클라이언트가 서버의 FIN을 수신한 이후에 발생
* 서버의 지연된 패킷을 수신하기 위해 클라이언트에 `Timeout` 존재

</div>
</details>

<details>
<details>
<summary style="font-size:20px">OSI 7계층이란</summary>
<div markdown="1">

* 네트워크의 통신 과정을 7단계로 나눠 표준화한 것
* ISO(국제표준기구)에서 만듦 

### 사용 이유
* 통신 과정을 이해하기 쉬움
* 문제 발생 시 해당 단계의 장비와 SW만 수정하면 됨 -> 해결 용이 

### 각 계층의 역할
* Application - Application(7), Presentation(6), Session(5) 계층으로 분리
#### Application(7, Data)
* 사용자에게 `실제 애플리케이션 서비스를 제공`하는 계층
* HTTP, FTP, DNS
#### Presentation(6, Data)
* 애플리케이션의 `데이터 형태와 구조를 변환(번역, 암호화, 압축)`시키는 계층
* 코드 간의 번역을 담당 -> 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어줌
#### Session(5, Data)
* 양 끝단의 응용 프로세스가 `통신을 관리하기 위한 방법`을 제공
  * 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신 등
* 애플리케이션 간의 `TCP/IP 세션을 구축하고 관리하며 종료`시키는 계층
* API, Socket
#### Transport(4, Segment)
* 통신 `양단 간의 신뢰성 있는 통신`을 보장하는 계층
* TCP, UDP
#### Network(3, Packet or Datagram)
* 목적지까지의 경로를 선택하고 `경로에 따라 패킷을 전달(라우팅)`해주는 계층
* IP / 라우터
#### Link(2, Frame)
* 인접한 `피어 간의 신뢰성 있는 통신`을 보장하는 계층
* MAC / 브릿지, 스위치
#### Physical(1, Bit)
* 전기적, 기계적, 기능적인 특성을 이용해서 `통신 케이블로 데이터를 전송`
* 리피터, 케이블, 허브 

</div>
</details>

<details>
<summary style="font-size:20px">CDN (Contents Delivery Network)</summary>
<div markdown="1"> 

![zz](https://user-images.githubusercontent.com/38900338/135851877-de1980d4-c90f-44c9-89d9-91899775feb6.PNG) 

#### 정의
* `지리적, 물리적으로 떨어져 있는` 사용자에게 웹 페이지 콘텐츠 `로드 지연을 최소화`하는, 촘촘히 `분산된 서버`로 이루어진 플랫폼 기술
* 각 지역에 캐시 서버(PoP, Points of Presence)를 분산 배치해, 가까운 사용자의 요청에 원본 서버가 아닌 캐시 서버가 콘텐츠를 전달 

#### 사용 시의 이점
* 지리적으로 가까운 캐시 서버가 응답하여 빠른 응답 가능
* Origin 서버에 문제가 생겨도 다른 서버로 대체가 가능해 안전성 증가
* 트래픽 집중 방지 가능 

#### 과정
* 웹 브라우저를 실행하는 디바이스인 사용자 에이전트는 HTML, 이미지, CSS, JavaScript 파일을 렌더링하는데 필요한 콘텐츠를 요청
* `콘텐츠에 대한 각 요청이 발생하면 최적으로 배치된 CDN 서버에 엔드유저가 매핑`
* CDN 서버는 요청된 파일의 `캐싱`된(사전 저장된) 버전으로 응답 

</div>
</details>

<details>
<summary style="font-size:20px">로드 밸런싱</summary>
<div markdown="1"> 

* 로드 밸런서를 클라이언트와 서버 사이에 두고, 부하가 집중되지 않도록 여러 서버에 분산하는 방식
* 로드 밸런서는 물리 장비를 이중화해서 구현하거나 nginx(엔진X)와 같은 웹서버를 이용하여 구현 

</div>
</details>

<details>
<summary style="font-size:20px">CIDR (Classless Inter-Domain Routing)</summary>
<div markdown="1"> 

* 클래스 없는 도메인 간 라우팅 기법
* 최신의 IP 주소 할당 방법으로 정적이였던 클래스 방식에 비해 IP 주소의 영역을 여러 네트워크 영역으로 나눌 수 있기 때문에 기존방식에 비해 유연 

</div>
</details>

<details>
<summary style="font-size:20px">NAT (Network Address Translation)</summary>
<div markdown="1"> 

#### 정의
* IP 패킷의 TCP/UDP 포트 숫자와 소스 및 목적지의 IP 주소 등을 `재기록`하면서 `라우터`를 통해 통신하는 기술
* 외부에 공개된 `공인(Public) IP`와 내부에서 사용하는 `사설(Private) IP`를 `맵핑`하여 원활히 통신할 수 있게 하는 기술 

#### 목적
##### 공인 IP 부족 문제 해결
* 한정적인 IP를 다수가 공유해 IP 절약 가능
##### 보안성
* 사설망을 외부로부터 보호할 수 있음
* 외부에서 사설 IP를 알 방법이 없어 내부 네트워크와 호스트를 보호 가능 

#### 동작 원리
#### 외부로 요청 패킷 전송
* 패켓 헤더 = `소스 IP: 사설 IP`, `목적 IP: 목적지 IP`
* 게이트웨이에서 `소스 IP: 게이트웨이의 공인 IP`로 변경, `목적 IP: 목적지 IP` 변경 없음
* NAT 테이블에 맵핑 내역을 저장 (포트도 기록) 

### 응답 패킷 받기
* 패켓 헤더 = `소스 IP: 목적지 IP`, `목적 IP: 게이트웨이의 공인 IP`
* 게이트웨이에서 `소스 IP: 목적지 IP` 변경 없음, `목적 IP: 사설 IP` 로 변경 (재기록)
* NAT 테이블을 참조하여 수정 

</div>
</details>