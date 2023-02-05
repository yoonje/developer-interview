# Spring 

<br> 

<details>
<summary style="font-size:20px">스프링과 스프링 부트</summary>
<div markdown="1"> 

#### 스프링
* 자바의 `오픈 소스 애플리케이션 프레임워크`
* 객체를 관리할 수 있는 컨테이너 제공 
* IOC, DI, AOP를 지원

#### 스프링 부트
* 스프링 기반의 애플리케이션을 간편하게 설정할 수 있는 도구
* 내장 서버: `Embeded Tomcat`이 포함되어 있어 Tomcat을 따로 설치/관리할 필요가 없음
* Starter를 이용한 의존성 자동화

</div>
</details>


<details>
<summary style="font-size:20px">Maven과 Gradle</summary>
<div markdown="1"> 

* 빌드 관리 도구: 라이브러리, 종속성 정보 등을 설정 파일을 통해 자동으로 다운로드해 간편히 관리해주는 도구 

#### Maven
* Java용 프로젝트 관리 도구
* Apache Ant의 단점을 해소하기 위해 사용
* 빌드 중인 프로젝트, 라이브러리 등 종속 관계를 `pom.xml`에 명시 
  * Project Object Model

#### Gradle
* Java, C/C++, Python 등을 지원
* Apache Maven과 Apache Ant의 장점을 합친 빌드 관리 도구 (완전한 오픈 소스)
* `Build.gradle` 사용: JVM 위에서 동작하는 `Groovy` 언어를 사용 (XML보다 간결) 

#### 차이점
* Gradle은 `Incremental Build`를 허용해 `빌드 시간이 단축`
  * 이미 업데이트된 Task는 빌드가 진행되지 않아 시간 단축 가능
  * Maven 보다 빠름
* 빌드 접근 방식 차이: Gradle은 `작업 의존성 그래프`에 기반, Maven은 `고정적이고 선형적인 단계의 모델`에 기반
* Gradle은 `Build Cache` 사용
  * 2개 이상의 빌드가 있을 경우, 하나의 빌드에서 사용된 파일이 다른 빌드에서 사용되면, 빌드 캐시를 이용해 이전 결과물을 다른 빌드에 사용 가능

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
* 애플리케이션 실행 시점에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달
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
* 객체의 생성부터 소멸까지 개발자가 아닌 `컨테이너`가 관리하는 것 

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
* 스프링 컨테이너에는 `BeanFactory`, `ApplicationContext` 인터페이스가 있음
* 자바 객체를 스프링 빈이라고 함 

#### 참고 
* `AppConfig` 클래스 같은 것이 스프링 컨테이너 -> `@Configuration` 사용
* `AppConfig` 내에서 `@Bean`이 붙은 것이 스프링 빈 

</div>
</details>


<details>
<summary style="font-size:20px">ApplicationContext</summary>
<div markdown="1"> 

* 스프링 컨테이너
* `BeanFactory` 인터페이스의 하위 인터페이스
* `BeanFactory`는 스프링 컨테이너의 최상위 인터페이스로 `ApplicationContext`는 `BeanFactory`에 부가 기능을 추가한 것 

</div>
</details> 


<details>
<summary style="font-size:20px">스프링 빈 주입 방법</summary>
<div markdown="1"> 

#### 스프링 빈 주입 방법

* 필드 주입: 필드에 `@Autowired` 어노테이션 사용
* 생성자 주입: 생성자에서 파라미터로 의존성을 주입, 생성자가 1개라면 `@Autowired` 어노테이션이 필수적이지 않음

#### 생성자 주입을 사용하는 것이 좋음
* `순환 참조` 방지 가능
  * 생성자 주입: 생성자로 객체를 생성하는 시점에 생성자의 인자에 사용되는 빈을 찾거나 생성 -> 빈의 생성자를 호출
  * 그 외: 빈을 먼저 생성 -> 어노테이션이 붙은 필드에 해당하는 빈을 찾아서 주입 / Setter의 객체를 호출해 주입 -> 객체가 실제로 사용되기 전까지는 에러가 발생하지 않음
* `final` 키워드로 불변하는 객체를 생성할 수 있음
  * 런타임에 중에 객체가 변하는 것을 막아 불변성을 유지할 수 있어 오류를 사전에 방지할 수 있음

</div>
</details>


<details>
<summary style="font-size:20px">@Bean 과 @Component의 차이</summary>
<div markdown="1"> 

#### @Bean
* 메소드 레벨에서 선언
* 반환되는 객체(인스턴스)를 개발자가 수동으로 등록

#### @Component
* 클래스 레벨에서 선언
* 스프링이 런타임시에 컴포넌트스캔을 하여 자동으로 빈을 등록

</div>
</details>



<details>
<summary style="font-size:20px">스프링 빈 스코프</summary>
<div markdown="1"> 

* 빈이 관리되는 범위

```java
@Scope("singletone")
```

#### Singleton
* Default Scope
  * 이유: 대규모 트래픽을 처리할 수 있도록 하기 위해서, 성능을 위해서
* 스프링 컨테이너의 시작과 종료까지 1개의 객체로 유지됨


#### Prototype
* Bean 객체를 요청할 때마다 새로운 객체 생성
* 프로토타입을 받은 클라이언트가 객체를 관리

#### Web (MVC Wep 앱에서만 사용)
* Request: HTTP 요청별로 객체화, 요청이 끝나면 소멸
* Session: HTTP 세션별로 객체화, 세션이 끝나면 소멸
* Application: Web의 `Servlet Context`와 동일한 생명주기를 가짐
* Websocket: web socket과 동일한 생명주기를 가짐

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
  * DispatcherServlet: Front Controller
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
<summary style="font-size:20px">필터와 인터셉터 차이</summary>
<div markdown="1"> 

* `실행되는 시점`의 차이

#### 필터
* 웹 애플리케이션에 등록 (스프링 Context 외부에 존재)
* 서블릿 필터: `DispatcherServlet` `이전`에 실행 -> 자원의 앞단에서 요청 내용 변경/검증 수행

#### 인터셉터
* 스프링 Context에 등록 
* `DistpatcherServlet`이 `컨트롤러`를 호출하기 전(요청), 후(응답)에 동작 -> Controller에 관한 요청과 응답 처리

</div>
</details>


<details>
<summary style="font-size:20px">Self-invocation 문제</summary>
<div markdown="1"> 

* 스프링 컴포넌트에 있는 AOP 어노테이션은 `스프링 프록시`를 기반으로 동작하기 때문에 내부 호출을 할 때는 프록시가 적용되지 않음


</div>
</details>


<details>
<summary style="font-size:20px">ORM (Object Relational Mapping)</summary>
<div markdown="1"> 

* 관계형 DB를 OOP 언어로 변환하는 기술
* `객체` 클래스를 `RDB 테이블`에 자동으로 연결하는 것 -> SQL 없이 간접적으로 DB 조작 가능 
* 비지니스 로직에 집중할 수 있음, DBMS 종속성 하락
* 프로그램의 복잡성이 커지면 난이도 증가, 잘못될 경우 문제 발생할 가능성 있음 

</div>
</details>


<details>
<summary style="font-size:20px">Java Persistence API 정의</summary>
<div markdown="1"> 

* ORM을 위해 자바에서 제공하는 API
* 자바 ORM 기술에 대한 API 표준 명세
* 자바 애플리케이션에서 `관계형 DB`를 사용하는 방식을 정의한 `인터페이스`
* `EntityManager`를 통해 `CRUD` 처리 

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
<summary style="font-size:20px">JPA 영속성 컨텍스트</summary>
<div markdown="1"> 

* `엔티티를 영구 저장`하는 환경
* 애플리케이션과 데이터베이스 사이에서 객체를 보관하는 가상의 환경
* 영속성 컨텍스트의 생명 주기는 트랜잭션과 동일 

#### 생명주기
* 비영속: 영속성 컨텍스트와 전혀 관계가 없는 상태, 객체를 생성한 상태
* 영속: 엔티티가 영속성 컨텍스트에 의해 관리되는 상태
* 준영속: 영속성 컨텍스트에 저장되었다가 분리된 상태
* 삭제: 엔티티 객체를 영속성 컨텍스트와 DB에서 삭제 

#### 1차 캐시
* 영속성 컨텍스트에서 엔티티를 저장하는 장소
* 같은 엔티티가 있으면 동일한 객체임을 보장 

#### 2차 캐시
* 애플리케이션 범위의 캐시, 공유 캐시
* 애플리케이션이 종료될때까지 캐시 유지
* `동시성`을 극대화 하기 위해 캐시한 객체가 아닌 `복사본`을 반환
* 영속성 컨텍스트가 다르면 동일한 객체임을 보장하지 않음 

</div>
</details>


<details>
<summary style="font-size:20px">JPA Fetch 종류</summary>
<div markdown="1"> 

* 즉시 로딩: 엔티티를 조회할 때, 연관된 엔티티도 `함께` DB를 조회
* 지연 로딩: 엔티티를 조회할 때, 연관된 엔티티는 조회하지 않고 `프록시 객체`로 넣어두었다가 엔티티가 실제로 `사용`될 때 조회 

#### 프록시
* 실제 엔티티 대신에 사용되는 객체, 원본 엔티티를 `상속`받은 객체 

</div>
</details>


<details>
<summary style="font-size:20px">JPA N+1 문제</summary>
<div markdown="1"> 

* 조회 시, 1개의 쿼리를 생각하고 설계했으나 예상하지 못했던 쿼리 N개 더 발생하는 문제
* `연관 관계`에 의해 다른 객체가 함께 조회되어 N+1 문제가 발생함 

#### 원인
* 즉시 로딩 시에, 전체 데이터를 조회하고 Eager가 감지되어 N개의 쿼리가 추가로 발생
* 지연 로딩 시에, 전체 데이터를 조회한 후, 연관된 객체가 사용될 때 N개 쿼리가 발생 

#### 해결 방법
* Fetch Join 사용: 연관된 엔티티나 컬렉션을 한 번에 함께 조회하는 역할
* @EntityGraph 사용
* @BatchSize 사용:` where 절의 in 조건`으로 미리 지정된 사이즈 만큼만 조회하여 1개 쿼리로 처리 가능
* @Fetch 사용: `where 절의 in 조건`으로 조회해 1개 쿼리로 처리 가능 (BatchSize 무한대와 동일) 

</div>
</details>



<details>
<summary style="font-size:20px">JPA에서 Entity Id에 Long을 사용해야 되는 이유</summary>
<div markdown="1"> 

* Wrapper Type인 Long을 사용해야 Null을 사용할 수 있음
* 하이버네이트 공식 문서에도 Nullable한 값을 사용하라고 권장 

</div>
</details>


<details>
<summary style="font-size:20px">JPA에서 스프링에서 다대다 관계가 좋지 않은 이유</summary>
<div markdown="1"> 

* 다대다의 경우, 정규화를 통해 `중간 테이블`을 생성해야 함
  * 중간 테이블로 `일대다` + `다대일` 형태로 변형해야 함
* JPA에서 `@ManyToMany` 연관 관계를 사용할 경우, 하이버네이트가 중간 테이블을 알아서 만들어서 처리
  * 관계 설정에 필수적으로 필요한 정보만 담기고 비지니스 로직에 필요한 정보는 담기지 않음
  * 실무에서는 사용하지 않는 것을 권장
* 다대다 관계를 사용하고 싶은 경우라면 중간 테이블에 대한 클래스를 직접 만들어서 `@OneToMany`, `@ManyToOne`의 조합을 만들어 사용해야 함

#### 정리
* 중간 테이블에는 매핑정보만 들어가고 추가 데이터를 넣는 것이 불가능
* 중간 테이블이 숨겨져 있기 때문에 쿼리가 예상하지 못하는 형태로 발생 가능
* 실무 비즈니스는 복잡해서 ManyToMany로 풀 수있는게 거의 없음

</div>
</details>


<details>
<summary style="font-size:20px">Hibernate</summary>
<div markdown="1"> 

* `JPA의 구현체`, 인터페이스를 직접 구현한 `라이브러리`
* SQL문을 직접 작성하지 않고 `메소드 호출`만으로 쿼리 수행이 가능해 생산성 향상
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
<summary style="font-size:20px">Spring Data JPA</summary>
<div markdown="1"> 

* JPA를 편리하게 사용할 수 있도록 스프링에서 제공하는 프로젝트
* CRUD 처리를 위한 공통 `인터페이스` 제공 

</div>
</details>


<details>
<summary style="font-size:20px">Mybatis</summary>
<div markdown="1"> 

#### 정의
* 자바의 관계형 데이터베이스 프로그래밍을 쉽게 할 수 있도록 도와주는 개발 프레임워크
* JDBC를 통해 DB에 접근하는 작업을 캡슐화, SQL 쿼리 매핑
#### 사용 이유
* 프로그램의 SQL 쿼리를 한 파일로 구성하여 코드와 SQL을 분리할 수 있어 사용 

</div>
</details>