# Web

<br>


<details>
<summary style="font-size:20px">HTTP 특징</summary>
<div markdown="1">

#### Connectionless
* 클라이언트에서 서버에 요청을 보내면 서버는 클라이언트에 응답을 하고 접속을 끊음

#### Stateless
* HTTP 통신은 요청에 응답하고 접속을 끊기 때문에 클라이언트의 상태정보를 저장하지 않음

</div>
</details>


<details>
<summary style="font-size:20px">HTTP 0.9, 1, 1.1, 2, 3의 차이</summary>
<div markdown="1">

#### HTTP 0.9
* HTTP 헤더가 없음, 상태 코드 없음
* `GET`만 가능
* `HTML 파일`만 전송 가능
* 하나의 연결당 1요청 1응답 -> 성능 저하, 서버 부하

#### HTTP 1.0
* HTTP 헤더가 생김, 상태 코드 생김
* `content-type`을 통해 HTML이 아닌 데이터도 전달 가능
* `Short Connection`: 하나의 연결에 1요청 1응답 -> 성능 저하, 서버 부하
  * 매 요청마다 TCP 세션을 설정(3-way)하고 종료(4-way)하는 과정 진행

#### HTTP 1.1
* `Persistent Connection`: 지정한 Timeout 동안 커넥션을 닫지 않음
  * TCP 세션을 설정(3-way) -> N요청/응답 -> 종료(4-way)
  * `connection : keep-alive` 헤더를 응답으로 전송
* `파이프라이닝`
  * 1.0: 1요청 -> 1응답, 2요청 -> 2응답, 3요청 -> 3응답
  * 1.1: 1, 2, 3요청 -> 1, 2, 3응답
  * 하나의 커넥션에서 응답을 기다리지 않고 순차적인 여러 요청을 연속으로 전송, 요청 순서에 맞춰 응답을 받음 -> RTT(Round Trip TIme) 감소
* HOL(Head of Line) Blocking: 파이프라이닝의 문제점 -> 먼저 받은 요청이 Block되면 다음 요청도 처리 불가
* 헤더의 중복: 파이프라이닝에서 전송되는 요청들의 헤더/쿠키는 많은 부분이 중복 -> 자원 낭비

#### HTTP 2.0
* 메시지 전송 방식 변화
  * 바이너리 프레이밍 계층 사용: 데이터는 `바이너리`로 인코딩해서 전송, 데이터를 `프레임` 단위로 나눔
    * 전송속도 향상, 오류 발생 가능성 하락
* `멀티플렉싱`을 통해 HOL(Head of Line) Blocking 해결 -> 레이턴시 감소
  * 하나의 커넥션에서 여러 스트림 교환 가능
  * 순서를 상관하지 않고 전송, 순서는 스트림 우선순위로 수신측에서 재조합
* `HTTP 헤더 압축`: 헤더 크기 감축 (Huffman Coding) -> 오버헤드 감소
* Server Push: 클라이언트가 요청 하지 않은 JavaScript, CSS, Font, 이미지 파일 등과 같이 필요하게 될 특정 파일들을 서버에서 HTTP 응답에 함께 전송

#### HTTP 3 (QUIC) 
* `UDP 기반` 으로 변화
 * TCP는 신뢰성을 확보하지만 지연을 줄이기 힘듦
 * UDP는 공간이 많아 TCP의 지연을 줄이면서 TCP만큼 신뢰성을 보장하도록 개발
* `HTTPS` 필수

#### 참고
* HTTP 2.0
  * 스트림 > 메시지 > 프레임
    * 프레임: 통신의 최소 단위
      * 헤더 프레임: HTTP 헤더 저장, Data 프레임: HTTP 응답 저장
    * 메시지: 다수의 프레임, 요청/응답의 단위
    * 스트림: 양방향 통신을 통해 전달되는 한 개 이상의 메시지
* HTTP 3.0
  * 전송 속도 향상: 첫 연결 설정에서 필요한 정보와 함께 데이터 전송 -> 연결 성공시 설정을 캐싱하여 다음 연결 때 바로 성립 가능
  * Connection UUID: 고유한 식별자로 서버와 연결 -> 커넥션 재수립 필요X
  * 독립 스트림 -> 향상된 멀티플렉싱
  * 헤더 압축(QPACK)
  
</div>
</details>


<details>
<summary style="font-size:20px">HTTP 상태코드</summary>
<div markdown="1">

* 1XX: 정보 응답으로 서버는 요청을 받았고 클라이언트는 작업을 계속 진행하라는 의미
* 2xx: 요청과 응답에 성공
* 3xx: 리다이렉션 응답으로 추가 작업이 필요하다는 의미(클라이언트를 새로운 URL로 이동)
  * 301(Moved Permanently): 요청한 자원의 URL이 변경됨, 새로운 URL이 응답에 있을 수도 있음
  * 302(Found): 요청한 자원의 URL이 일시적으로 변경됨, 새롭게 변경된 URL이 나중에 만들어질 수도 있어 클라이언트는 동일한 URI로 요청해야 함
* 4xx: 클라이언트 에러 응답
  * 401(Unauthorized): 클라이언트는 요청에 대한 응답을 받기위해 인증이 필요
  * 403(Forbidden): 클라이언트는 자원에 접근할 권리가 없음, 401과 다르게 서버가 클라이언트가 누구인지 알 고 있음
* 5xx: 서버 에러 응답

</div>
</details>


<details>
<summary style="font-size:20px">HTTP와 HTTPS의 차이</summary>
<div markdown="1">

#### HTTP
* 웹 브라우저와 웹 서버가 통신하기 위한 프로토콜
* 평문 통신으로 `도청` 가능
  * 암호화하지 않음
* 통신 상대를 확인하지 않아 `위장` 가능
  * 송신자를 확인할 수 없음
* 완전성을 증명하지 않아 `변조` 가능
  * 완전성: 송신 내용과 수신 내용이 같은 것

#### HTTPS (HTTP Secure)
* HTTP에 SSL/TLS 기반의 Secure Socket을 활용한 프로토콜
* 웹 브라우저와 웹 서버가 각각 키를 가지며 `그 키를 통해 암호화/복호화하여 HTTP통신`을 하기 때문에 클라이언트와 서버만이 데이터를 열람 가능

</div>
</details>


<details>
<summary style="font-size:20px">대칭키 암호화</summary>
<div markdown="1">

#### 정의 
* 하나의 키로 암/복호화를 모두 하는 방식

#### 장단점
* 암호화 연산 속도가 빠르기 때문에 효율적인 암호 시스템을 구축할 수 있음
* 키 전달 및 관리에 어려움: 데이터를 보낼 때, 암호키도 함께 전송하는데 암호키 자체는 암호화가 되지 않은 평문으로 분실하거나 타인에게 노출되면 보안에 매우 취약

</div>
</details>


<details>
<summary style="font-size:20px">비대칭키(공개키) 암호화</summary>
<div markdown="1">

#### 정의 
* 암/복호화를 하는 키를 분리한 방식
* 대칭키 암호화 방식의 키 전달의 취약점을 해결하기 위해 나온 방법
* 비공개키(개인키)는 자신만이 소유하여 사용, 공개키는 타인에게 공개

#### 장단점
* 대칭키 암호화 방식의 키 전달 문제를 해결
* 암/복호화를 위해 복잡한 연산을 수행해 속도가 느림

</div>
</details>


<details>
<summary style="font-size:20px">HTTPS 통신 과정 (SSL/TLS Handshaking)</summary>
<div markdown="1">

* 대칭키와 비대칭키를 조합해서 사용

#### 과정
* Client Hello: 웹 브라우저가 웹 서버에 접속, 사용 가능한 암호화 알고리즘(`Ciper Suite`) 목록 전달
* Server Hello: 사용할 암호화 알고리즘(`Ciper Suite`) 선택 및 전달
* Certificate: 웹 서버는 `인증서`를 웹 브라우저에게 전송
  * 인증서: 인증기관의 `개인키`로 암호화된 `사이트의 정보`와 웹 서버의 `공개키`가 있음
* Server Key Exchange: 파라미터를 서버의 개인키로 암호화해서 전송, Ciper Suite의 알고리즘이 DH인 경우에만 수행
* Server Hello Done: 웹 서버가 전송
* Client Key Exchange
  * 웹 브라우저는 이미 가지고 있는 인증기관의 `공개키`로 웹 서버에서 받은 인증서를 `복호화` 해서 확인
  * 웹 브라우저는 실제 데이터의 암호화에 사용될 `대칭키`를 생성, 인증서에서 꺼낸 웹 서버의 `공개키`로 `암호화` 해서 웹 서버로 전송
  * 웹 서버는 자신의 `개인키`로 웹 브라우저가 보내온 `대칭키`를 `복호화` 해서 얻음 (비대칭키 암호화)
  * DH) 파라미터를 공개키로 암호화해서 전송
* ChangeCipherSpec + Finish: 통신 준비 완료, 클라이언트가 전송
* ChangeCipherSpec + Finish: 통신 준비 완료, 서버가 전송
* 웹 브라우저가 전송했던 `대칭키`로 데이터를 암호화해서 주고 받음
  * 서버와 클라이언트는 일련의 과정을 거쳐 대칭키로 `Session Key`를 만들어 사용
  * `Pre Master Secret`(대칭키) -> `Master Secret` -> `Session Key` (클라이언트와 서버 각자가 진행)

#### 참고 1
##### 인증기관 (Certification Authority, CA)
* 인증기관으로부터 공인인증서를 발급받아 서버에 설치해야 HTTPS 통신 가능
* 웹 서비스 제공자는 자신의 공개키와 개인키를 생성, `공개키를 인증기관에 보냄`
* 인증기관은 공개키, 유효기간 등 정보를 포함하여 `인증기관의 개인키로 전자서명한 인증서를 발급`
* 웹 서버는 인증서와 개인키를 가지게 되어 HTTPS 통신을 할 수 있게 됨
* 클라이언트에는 여러 인증기관의 공개키와 인증서가 이미 설치되어 있음
* 웹 서버와 통신 시, 인증기관의 `개인키`로 서명된 인증서를 클라이언트가 받으면 인증기관의 `공개키`로 복호화 가능

#### 참고 2
* SSL을 사용하면 `https://` 를 사용하여 웹서버에 접근 가능
* 대칭키: 실제 데이터 암호화 방식
* 공개키: 대칭키를 공유하기 위해 사용

</div>
</details>


<details>
<summary style="font-size:20px">HSTS (HTTP Strict Transport Security)</summary>
<div markdown="1">

#### 정의
* 강제적으로 `HTTPS Protocol`로만 접속하게 하는 기능
* 브라우저는 HTTPS를 사용해야 하는 웹 사이트의 목록(`HSTS List`)을 만들고 이것을 사용
* 일정시간 (max-age, HSTS 리스트에 존속하는 시간) 동안 HSTS 응답을 한 웹사이트에 대해서 https 접속을 강제화

#### 사용 목적
* SSL Stripping 공격(중간자 공격)을 방지하기 위해 사용
  * 사용자가 HTTPS를 지원하는 사이트에 HTTP로 접속 했을 때, 중간자 공격에 의해 HTTP 통신을 하게 되어 공격자에게 정보가 노출되는 것을 방지
  * HSTS를 사용하면 HTTP 요청에 HSTS 헤더가 발견될 경우, 즉시 중단

</div>
</details>


<details>
<summary style="font-size:20px">쿠키와 세션</summary>
<div markdown="1">

* HTTP 통신에서 Connectionless, Stateless 보완

#### 쿠키
* `클라이언트의 로컬(브라우저)`에 저장되는 `키와 값`이 들어있는 `작은` 텍스트 파일
* 보안에 나쁨: 파일로 저장해 탈취와 변조 가능, 응답/요청 시에 스니핑 위험이 있음
* 브라우저를 종료해도 파일로 남음
* 파일에서 읽어 속도 빠름

#### 세션
* 일정 시간동안 `같은 브라우저`에서 들어오는 요구를 하나의 상태로 보고 그 상태를 객체로 `서버`에 `제한 없는` 파일로 저장하는 기술
* 보안에 좋음: `sessionid`를 통해 데이터를 구분하여 처리하여 보안이 좋음
* 브라우저 종료 시, 세션 삭제
* 요청마다 서버에서 처리해 느림

#### 쿠키의 동작 과정
* 클라이언트가 서버에 요청
* 서버는 `HTTP 응답 헤더`에 `set-cookie` 헤더를 추가하여 응답 -> 클라이언트는 쿠키 저장
* 이후, 클라이언트는 전달받은 `쿠키`를 자동으로 요청헤더에 추가하여 요청(브라우저가 자동으로 추가)
* 서버에서 쿠키를 참고하여 로직 수행

#### 세션의 동작 과정
* 클라이언트가 서버에 요청
* 서버는 `세션`에 클라이언트에 대한 데이터를 저장하고 `HTTP 응답 헤더`에 `sessionid`를 추가하여 응답
* 클라이언트는 이후 서버에 요청할 때 전달받은 `세션 쿠키`를 자동으로 요청헤더에 추가하여 요청
* 서버에서 `sessionid`를 참고하여 로직 수행

</div>
</details>


<details>
<summary style="font-size:20px">캐시</summary>
<div markdown="1">

* 리소스들의 임시 저장소
* 이미지나 css, js파일 등을` 브라우저나 서버 앞 단에 저장`해놓고 사용하는 것
* 같은 자원을 로드(load)해야할 때, 해당 자원을 다시 불러오지 않고 캐시되어 있는 자원을 사용
  * `서버를 거치지 않아 속도 향상`
* 캐시에 있는 것을 재사용하기 때문에 경우에 따라 변경된 자원을 참조할 수 없는 경우가 생김

</div>
</details>


<details>
<summary style="font-size:20px">웹 캐시</summary>
<div markdown="1">

#### 웹 캐시

* 대부분의 브라우저에서는 `HTTP 헤더`에 캐시 구현이 포함되어 있어서 웹 캐시를 구현
* 응답 헤더의 Last-Modified, Etag, Expires, Cache-Control 항목 등과 같은 여러 부분의 여러 개의 태그를 통해서 캐싱

#### Cache-Control: HTTP 헤더를 통해 캐싱 정책을 정의
* `no-cache`: 캐시가 유효한지 매번 서버에 재검증 요청
* `no-store`: 캐싱하지 않음

#### Last-Modified, If-Modified-Since
* 브라우저는 최초 응답 시 받은 `Last-Modified` 값을 `If-Modified-Since` 헤더에 포함 시켜 페이지를 요청
* 서버는 요청 파일의 수정 시간을 `If-Modified-Since`값과 비교하여 동일하다면 `304 Not Modified`로 응답하고 다르다면` 200 OK`
* 브라우저는 응답 코드가 304인 경우 `캐시`에서 페이지를 로드하고 200이라면 새로 다운받은 후, `Last-Modified` 값을 갱신

#### Etag, If-None-Match
* 브라우저는 최초 응답 시 받은 `Etag` 값을 `If-None-Match` 헤더에 포함 시켜 페이지를 요청
* 서버는 요청 파일의 `Etag` 값을 `If-None-Match` 값과 비교하여 동일하다면 `304 Not Modified`로 응답하고 다르다면 `200 OK`와 함께 새로운 `Etag` 값을 응답 헤더에 전송
* 브라우저는 응답 코드가 304인 경우 `캐시`에서 페이지를 로드하고 200이라면 새로 다운받은 후, `Etag` 값을 갱신

#### Expires
* 브라우저는 최초 응답 시 받은 `Expires` 시간을 비교하여 기간 내라면 서버를 거치지 않고 바로 캐시에서 페이지를 로드

</div>
</details>


<details>
<summary style="font-size:20px">웹 서버와 웹 애플리케이션 서버의 차이점</summary>
<div markdown="1">

#### 웹 서버
* Http 프로토콜을 기반으로, 클라이언트의 요청을 처리하는 서버
* html이나 css 같은` 정적 컨텐츠`를 내려주거나 부하분산을 위한 프록시 역할을 주로 함
* `정적 컨텐츠`만 처리하는 고성능 서버

#### 웹 애플리케이션 서버
* 보통 웹서버 뒤에서 DB 조회 및 다양한 로직 처리 요구 시, `동적 컨텐츠`를 처리하는 서버
* tomcat, netty

</div>
</details>


<details>
<summary style="font-size:20px">URI, URL, URN</summary>
<div markdown="1">

#### URI(Uniform Resource Identifier)
* 자원을 고유하게 `식별`하고 `위치`를 지정하는 통합 자원 식별자
* URL, URN 두 가지 형태 존재
* 인터넷 프로토콜을 명시함
* 예시: http://www.naver.com

#### URL(Uniform Resource Location)
* 특정 서버의 한 리소스에 대한 구체적인 `위치`
* 자원의 위치와 접근 방법을 분명히 알려줌
* 예시: http://test.com/test/test.pdf 는 test.com서버에서 test폴더안의 test.pdf 파일을 요청

#### URN(Uniform Resource Name)
* 자원의 위치와 독립적인 `이름`
* URL이 변경되면 기존의 객체를 찾을 수 없다는 URL의 한계를 극복하기 위해 사용
* 예시: urn:2.19.222

</div>
</details>


<details>
<summary style="font-size:20px">REST (Representational State Transfer)</summary>
<div markdown="1">

#### REST

* 자원을 `이름(표현)`으로 구분하여 자원의 `상태(정보)`를 주고 받는 것
* `HTTP URI`를 통해 자원을 구분하고 `HTTP Method(POST, GET, PUT, DELETE)`를 통해 해당 자원에 대한 `CRUD` 연산을 적용

#### REST가 필요한 이유
* 다양한 클라이언트(다양한 브라우저, AOS, IOS)의 등장으로 멀티 플랫폼에 대한 지원
* 클라이언트와 서버 간의 역할 분리, 분산 애플리케이션 구현에 적합

#### REST 구성 요소
* 자원(Resource): URI
* 행위(Verb): HTTP Method
* 표현(Representation): JSON, XML

</div>
</details>


<details>
<summary style="font-size:20px">REST API 설계원칙 및 특징</summary>
<div markdown="1">

* `REST API`는 `REST 기반의 규칙들을 지켜서 설계된 API`

#### 설계 원칙
* 자원에 대한 정보는 `명사`로 표현하고 자원에 대한 행위는 `HTTP 메소드`로 표현
  * URI에 `HTTP 메소드`, `동사`를 포함하지 않음
* `/(슬래시)`를 `계층`관계를 나타내는데 사용하되 마지막 문자에 `/`를 포함하지 않음
* `소문자`와 `-(하이픈)`를 사용
  * 대소문자에 따라 다른 자원으로 인식될 수 있음
  * 밑줄(_)은 사용하지 않음
* 브라우저는 form-data 형식의 submit 으로 보내고 서버에서는 json 형태로 보내는 식의 분리보다는 둘 다 form-data 형식으로 보내든 하나로 통일

#### REST 특징
* 일관성
  * 동일 API로 일관된 처리
* 서버-클라이언트 구조
  * 클라이언트는 서버 내부 작업을 몰라도 됨
  * 각각 독립적으로 개발 가능
* Stateless (무상태)
  * HTTP는 Stateless해 서버가 클라이언트의 상태를 저장하지 않음
  * 요청에는 필요한 모든 정보가 포함되어야 함
* Cacheable (캐시 처리 가능)
  * HTTP 프로토콜의 기존 인프라를 활용해 캐싱 가능
  * 응답에 캐시 가능한지 불가능한지 명시 필요
* Self-Descriptive Message
  * API의 메시지만 보고도 이해 가능하도록 설계
* HATEOAS
</div>
</details>

<details>
<summary style="font-size:20px">REST (API) 장단점</summary>
<div markdown="1">

#### 장점
* HTTP를 사용하므로 웹 인프라를 그대로 이용 가능 (별도의 인프라 필요 없음)
* HTTP 표준 프로토콜을 따르는 모든 플랫폼에서 사용 가능
* MSA에 적합하여 재사용에서 이점이 존재

#### 단점
* 명확한 표준이 존재하지 않아 사람마다 다르게 해석하고 사용할 수 있음
* HTTP를 사용하므로 HTTP 통신 모델에 제약적
* 사용 가능한 메소드가 제한적

</div>
</details>


<details>
<summary style="font-size:20px">RESTful</summary>
<div markdown="1">

* `REST 원리를 따르는 시스템`을 나타내기 위해 사용하는 용어
* RESTful한 API를 구현하는 목적은 성능 향상이 아니라 `일관적인 컨벤션`을 통한 API의 이해도 및 호환성을 높이는 것

#### RESTful 하지 못한 경우
* 모든 CRUD 연산을 POST로 처리하는 API
* URI에 Resource, Id 외의 정보가 들어가는 경우

</div>
</details>


<details>
<summary style="font-size:20px">HTTP GET과 POST</summary>
<div markdown="1">

#### GET
* 자원을 `조회`하는 메소드
* `URL의 파라미터`로 전달되어 `길이 제한`이 있어 많은 데이터 전송 불가

#### POST
* 자원을 `생성`하는 메소드
* `HTTP Request Message의 Body`에 담겨 전달되어 길이 제한 없음

#### 공통점
* 서버로 데이터를 전송할 수 있음

</div>
</details>


<details>
<summary style="font-size:20px">HTTP POST와 PUT</summary>
<div markdown="1">

#### POST
* 자원을 `생성`하는 메소드
* 같은 요청을 반복할 경우, 새로운 자원을 계속 생성
* 멱등X

#### PUT
* 자원을 `생성 및 수정`하는 메소드
* 자원의 `식별자`를 이미 알고있는 상태 -> request message와 함께 넘어온 식별자의 자원을 만드는 것
* 같은 요청을 반복할 경우, 처음에는 자원이 없기 때문에 생성되고 그 이후는 생성되지 않음
* 멱등

#### POST 요청 예시

* 아래 요청을 2번 반복할 경우
```
POST /new
{
  "name": "고양이",
  "grade": 1
}
```

* 식별자가 다른 2개의 자원 생성
```
{ "id": 1, "name": "고양이", "grade": 1 }
{ "id": 2, "name": "고양이", "grade": 1 }
```

#### PUT 요청 예시

* 아래 요청을 2번 이상 반복할 경우
* POST와 다르게 요청에 식별자 포함
```
PUT /new/3
{
  "name": "강아지",
  "grade": 2
}
```
* 처음에는 자원이 없기 때문에 생성되고, 그 이후는 생성되지 않음
```
{ "id": 3, "name": "강아지", "grade": 2 }
```

</div>
</details>


<details>
<summary style="font-size:20px">HTTP PATCH와 PUT</summary>
<div markdown="1">

#### PATCH
* 자원의 `일부분을 수정`할 경우

#### PUT
* 자원 `전체를 수정/생성`할 경우
* 요청을 보내지 않은 필드는 `DEFAULT` 값으로 변경되므로 요청 시에 모든 필드를 전송해야 됨

</div>
</details>


<details>
<summary style="font-size:20px">HTTP 멱등성</summary>
<div markdown="1">

* 같은 요청을 반복하는 경우, 모든 요청에 따른 `서버의 상태가 같아야` 함
* 안전한 메소드(GET, 서버의 상태 변경X)는 서버의 상태를 변경시키지 않음
* 멱등한 메소드(PUT, DELETE, GET)는 서버의 상태를 변경시킬 수도 있고 아닐 수도 있음
* POST는 멱등이 아니면서 안전하지도 않음

</div>
</details>


<details>
<summary style="font-size:20px">JWT (JSON Web Token)</summary>
<div markdown="1">

* `Json` 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim 기반의 Web Token
* Header, Payload, Signature로 구성
* 세션은 사용자의 수 만큼 서버 메모리를 차지하기 때문에, 최근에는 세션의 문제를 보완한 토큰 기반의 인증방식을 사용하는 추세

</div>
</details>
