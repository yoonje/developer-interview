# Spring

<br>

<details>
<summary style="font-size:20px">스프링과 스프링 부트</summary>
<div markdown="1">

#### 스프링
* 자바의 `오픈 소스 애플리케이션 프레임워크`
* 객체를 관리할 수 있는 컨테이너 제공

#### 스프링 부트
* 스프링 기반의 애플리케이션을 간편하게 설정할 수 있는 도구
* * 내장 서버: `Embeded Tomcat`이 포함되어 있음

</div>
</details>


<details>
<summary style="font-size:20px">스프링의 버전별 차이 (추가 예정)</summary>
<div markdown="1">

</div>
</details>


<details>
<summary style="font-size:20px">DI</summary>
<div markdown="1">

* Dependency Injection, 의존 관계 주입
* 객체 간의 의존 관계를 미리 설정해 두면 스프링 컨테이너가 의존관계를 자동으로 연결
* 의존하는 객체를 직접 생성하거나 검색해서 가져올 필요가 없어 `결합도`가 낮아짐

#### 참고
* 객체들의 `의존성(결합도)을 줄이기 위해` 사용되는 스프링의 IOC 컨테이너의 구체적인 구현 방식
* 개발 코드에서 객체를 생성하는 것이 아니라, 데이터 주입만 담당하는 별도의 공간에서 객체를 생성하고 데이터간의 의존성을 주입해 개발 코드에서 가져다 씀
*애플리케이션 실행 시점에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달
* 재사용성 향상, 팩토리 패턴과 유사 
* 방법 3가지: 생성자에 `@Autowired` 추가, 필드 주입, setter 주입(setter에 `@Autowired` 추가)

</div>
</details>


<details>
<summary style="font-size:20px">IoC</summary>
<div markdown="1">

* Inversion of Control, 제어의 역전
* 제어권이 사용자에게 있지 않고 프레임워크에 있는 것
* 메소드나 객체의 호출을 개발자가 결정하는 것이 아니라, `외부에서 결정`
* 객체의 생성부터 소멸까지 개발자가 아닌 컨테이너가 관리하는 것

</div>
</details>


<details>
<summary style="font-size:20px">AOP</summary>
<div markdown="1">

* Aspect Oriented Programming, 관점 지향 프로그래밍
* `공통 관심 사항(Cross-Cutting Concern)`과 핵심 관심 사항(Core Concern)을 분리하는 것
* 특정 로직(로그, 성능테스트 등)을 모든 메소드에 적용하고 싶을 때, 모든 메소드에 일일이 로직을 추가하는 것이 아니라, 로직을 만들어서 모든 메소드에 적용
* 비지니스 로직의 앞/뒤에 공통 관심 사항을 수행해 `중복 코드를 줄이는 것`

</div>
</details>


<details>
<summary style="font-size:20px">스프링 컨테이너와 스프링 빈</summary>
<div markdown="1">

* 자바 객체의 생명 주기(생성 ~ 소멸)를 관리하는 컨테이너
* 스프링 컨테이너에는 `BeanFactory`, `ApplicationContext` 클래스가 있음
* 자바 객체를 스프링 빈이라고 함

#### 참고 
* `AppConfig` 클래스 같은 것이 스프링 컨테이너 -> `@Configuration` 사용
* `AppConfig` 내에서 `@Bean`이 붙은 것이 스프링 빈

</div>
</details>


<details>
<summary style="font-size:20px">스프링 MVC</summary>
<div markdown="1">

* Model: 비지니스 로직를 처리, DB와 상호작용하는 모듈
* View: Client에게 보여지는 화면을 반환하는 모듈
* Controller: 모델과 뷰 사이의 정보 교환, Client 요청이 들어왔을 때, 어떤 로직을 실행할 것인지 제어하는 모듈

</div>
</details>


<details>
<summary style="font-size:20px">스프링 MVC 과정</summary>
<div markdown="1">

1. 클라이언트가 서버에 요청을 보내면 `DispatcherServlet`에 요청이 전달<br>
  *  DispatcherServlet: Front Controller
2. `DispatcherServlet`은 요청된 `URL`을 `HandlerMapping`에게 전달, ` HandlerMapping`은 호출해야 할 `Controller` 객체를 리턴<br>
3. DispatcherServlet이 `HandlerAdapter` 객체에게 요청을 위임하고 `HandlerAdapter`는 `컨트롤러의 메소드를 실행(호출)`하여 `ModelAndView` 객체로 반환<br>
4. DispatcherServlet은 `ViewResolver`를 이용해 `View` 객체를 얻음<br>
  * `ModelAndView` 객체의 View이름으로 객체를 찾음, 없다면 생성하여 반환
5. DispatcherServlet은 ViewResolver가 리턴한 View객체를 이용해 사용자에게 화면 표시(응답 결과 표시)

#### 참고
*`HandlerMapping`, `HandlerAdapter`, `ViewResolver`: Spring Bean
* HandlerMapping: `@Controller`로 선언되었거나 `HttpRequestHandler` 인터페이스를 구현한 클래스를 찾음
* ModelAndView: 응답할 View 이름과 View에 전달할 데이터

</div>
</details>


<details>
<summary style="font-size:20px">MVC 1과 MVC 2의 차이</summary>
<div markdown="1">

#### MVC 1
* `JSP` 페이지에서 View, Controller 역할 담당 (로직 처리)
* 구조 단순
* JSP 내에서 html과 자바 코드가 함께 사용되어 복잡하고 유지보수가 어려움
#### MVC 2
* Model, View, Controller로 모듈화됨
* JSP는 Client에게 보여지는 `View`만 담당 (로직 처리 없음)
* 구조가 복잡하나 유지보수가 용이함

#### 참고
* Spring MVC는 `MVC2`로 설계되어 있음

</div>
</details>


<details>
<summary style="font-size:20px">Servlet</summary>
<div markdown="1">

* 클라이언트의 요청을 처리해 결과 반환, 웹 페이지를 동적으로 생성하기 위한 서버측 프로그램
* Spring MVC에서 `Controller` 역할 수행

</div>
</details>


<details>
<summary style="font-size:20px">DispatcherServlet</summary>
<div markdown="1">

* 서버로 들어오는 요청을 처리하는 `Front Controller`
* 웹 요청의 진입점, 요청을 처리하여 결과를 응답

#### 디스패처 서블릿으로 인한 web.xml 역할 축소
* 기존에는 모든 서블릿에 대해 URL 매핑을 활용하기 위해 web.xml에 등록이 필수
* 디스패처 서블릿이 요청을 처리하면서 작업이 편리

</div>
</details>


<details>
<summary style="font-size:20px">필터와 인터셉터 차이 (추가 예정)</summary>
<div markdown="1">

* 실행되는 시점의 차이
* 필터: 웹 애플리케이션에 등록
* 인터셉터: 스프링 Context에 등록

Filter 서블릿필터는 DispatcherServlet 이전에 실행이 되는데 자원의 앞단에서 요청 내용을 변경하거나 여러가지 검증을 수행합니다. Intercepter 필터는 스프링의 컨텍스트 외부에 존재하여 요청에 대한 작업 전/후로 가로채 동작한다.

인터셉터 DistpatcherServlet이 컨트롤러를 호출하기 전, 후로 끼어들기 때문에 스프링 컨텍스트내부에서 Controller에 관한 요청과 응답에 대해 처리합니다.

</div>
</details>


<details>
<summary style="font-size:20px">DAO (Data Access Object)</summary>
<div markdown="1">

* `DB 접근`에 사용하는 객체
* DB에 접근하는 로직과 비지니스 로직을 분리하기 위해 사용

</div>
</details>


<details>
<summary style="font-size:20px">DTO (Data Transfer Object)</summary>
<div markdown="1">


* 다른 말로 VO(Value Object)
* 계층(컨트롤러, 뷰, 비즈니스 계층 등)간 `데이터 교환(전송)`을 위한 자바 빈
* 로직을 가지지 않음: 속성과 속성에 접근하기 위한 getter, setter가 있고 추가적으로 toString(), equals() 가능

</div>
</details>


<details>
<summary style="font-size:20px">JPA에서 Entity를 설계할 때 주의점</summary>
<div markdown="1">

* `Setter`를 사용하지 않음
* 모든 연관 관계는 `지연로딩(LAZY)`으로 설정
  * 즉시로딩(EAGER)를 사용 할 경우, 어떤 SQL이 나갈지 추적하기 어려움
* 컬렉션은 필드에서 바로 초기화

#### 참고
* `@ManyToOne`과 같은 연관 관계가 있을 경우
* 지연로딩: 연관 테이블은 조회하지 않고, 연관 관계가 실제로 사용되는 시점에 조회
* 즉시로딩: 연관 테이블까지 바로 조회 <br>
  -> 많은 데이터가 조회될 수 있음

</div>
</details>


<details>
<summary style="font-size:20px">ORM (Object Relational Mapping)</summary>
<div markdown="1">

* 관계형 DB를 OOP 언어로 변환하는 기술
* `객체` 클래스를 `RDB 테이블`에 자동으로 연결하는 것 -> SQL 없이 간접적으로 DB 조작 가능 
* 비지니스 로직에 집중할 수 있음, DBMS 종속성 하락
* 프로그램의 복잡성이 커지만 난이도 증가, 잘못될 경우 문제 발생할 가능성 있음

</div>
</details>


<details>
<summary style="font-size:20px">JPA (Java Persistence API)</summary>
<div markdown="1">

* ORM을 위해 자바에서 제공하는 API
* 자바 ORM 기술에 다한 API 표준 명세
* 자바 애플리케이션에서 `관계형 DB`를 사용하는 방식을 정의한 `인터페이스`
* `EntityManager를` 통해 `CRUD` 처리

</div>
</details>


<details>
<summary style="font-size:20px">Hibernate</summary>
<div markdown="1">

* JPA의 구현체, 인터페이스를 직접 구현한 라이브러리
* 생산성, 유지보수, 비종속성

</div>
</details>


<details>
<summary style="font-size:20px">ORM, JPA, Hibernate 장단점</summary>
<div markdown="1">

#### 장점
* 비지니스 로직에 집중 가능, 객체 중심 개발 가능
* 메소드 호출만으로 DB 조작 -> 생산성 향상, 유지보수 쉬움
* DBMS 의존성 하락

#### 단점
* 직접 SQL을 호출하는 것보다는 성능이 떨어짐
* 복잡한 쿼리는 메소드로 처리가 어려움

</div>
</details>


<details>
<summary style="font-size:20px">Mybatis (추가 예정)</summary>
<div markdown="1">

#### 정의
* 자바의 관계형 데이터베이스 프로그래밍을 쉽게 할 수 있도록 도와주는 개발 프레임워크
* JDBC를 통해 DB에 접근하는 작업을 캡슐화, SQL 쿼리 매핑
#### 사용 이유
* 프로그램의 SQL 쿼리를 한 파일로 구성하여 코드와 SQL을 분리할 수 있어 사용

</div>
</details>


<details>
<summary style="font-size:20px">Mybatis, JPA 차이 (추가 예정)</summary>
<div markdown="1">


</div>
</details>


<details>
<summary style="font-size:20px">Spring JDBC (추가 예정)</summary>
<div markdown="1">

* 자바에서 데이터베이스에 접속할 수 있도록 해주는 자바 API
* DB에서 자료를 쿼리하거나 업데이트에 사용

</div>
</details>
