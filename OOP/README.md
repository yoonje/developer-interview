# OOP(Object-Oriented Programming)

<br>

<details>
<summary style="font-size:20px">C, C++, JAVA, Python</summary>
<div markdown="1">

* C
  * 컴파일 언어이자 절차지향 언어
* C++: 컴파일 언어이자 객체지향 언어
  * C의 상위 호환으로 객체를 활용하는 기능이 있음
  * 각 OS에 맞는 기계어로 변환해 실행(속도 빠름)
  * 메모리를 직접 관리할 수 있음
* JAVA
  * 컴파일 언어이자 객체지향 언어
  * 기본 단위가 Class로 완전한 OOP 언어
  * 가상머신에서 실행하여 OS와 독립적이며 가비지 콜렉션을 지원
* Python
  * 인터프리터 언어
  * 코드를 한줄씩 번역해 실행
  * 객체를 활용하는 기능이 있음

</div>
</details>


<details>
<summary style="font-size:20px">객체지향 프로그래밍과 장점</summary>
<div markdown="1">

* 프로그래밍에서 필요한 데이터를 `추상화`시켜 상태와 행위를 가진 `객체`를 만들고 그 객체들 간의 유기적인 `상호작용`을 통해 로직을 구성하는 프로그래밍 방식
* `추상화`가 쉽고 `상속`을 통해 코드 `재산성성`을 높일 수 있으며 객체 단위로 코드가 나눠져 있기 때문에 `디버깅과 유지보수`에 용이

</div>
</details>

<details>
<summary style="font-size:20px">객체지향 프로그래밍의 특징</summary>
<div markdown="1">

* `추상화`: 복잡한 시스템에서 핵심적인 것을 간추리는 것을 의미
  * 하위클래스들에 존재하는 공통적인 메소드를 `인터페이스`로 정의
* `캡슐화`: 객체의 속성과 기능을 하나로 묶고 일부를 외부에 감추어 `은닉`하는 것을 의미
  * `private`으로 멤버 변수 선언, 해당 변수에 접근하는 별도의 함수 정의
* `상속`: 상위 클래스의 특성을 하위 클래스가 이어 받아서 재사용 또는 확장하는 것을 의미
  * 코드 재사용
* `다형성`: 하나의 메서드나 클래스가 다양한 방법으로 동작하는 것을 의미
  * 상위 클래스: 추상 클래스, 함수: 추상 함수
  * 하위 클래스: 상위 클래스의 함수를 자신의 목적에 맞게 서로 다른 방법으로 구현

</div>
</details>

<details>
<summary style="font-size:20px">객체</summary>
<div markdown="1">

#### 객체
* 데이터(변수)와 데이터의 동작(함수, 절차, 기능)을 모두 포함한 개념

#### 객체의 종류
- VO(Value Object): 불변 객체, 동일하게 생성된 VO는 항상 동일한 상태여야하며 인스턴스화된 VO는 항상 유효한 값을 리턴해야함
- DTO(Data Transfer Object): 데이터 전송 객체, 상태를 보호하지 않으며 모든 속성을 노출하는 객체
- Entity: 유일한 식별자가 있는 객체로 보통 데이터 베이스에 저장
- DAO(Data Access Object, Repository): 데이터 베이스에 접근할 때 사용하는 추상 객체
- BO(Business Object, Service): 비지니스 로직이 들어있는 객체
  
</div>
</details>

<details>
<summary style="font-size:20px">관계</summary>
<div markdown="1">

#### 관계
* 클래스 간의 속성, 지역 객체, 메소드 인자, 상속, 인터페이스 등의 형태로 맺는 관계를 의미

#### 관계의 종류
- 연관 관계: 한 클래스가 다른 클래스에서 제공하는 기능을 사용하는 상황에서 계속 그 관계가 유지되는 관계
- 일반화 관계: 객체지향 개념에서 상속 관계와 같은 의미, is a kind of
- 집합 관계: 클래스들 사이의 전체 또는 부분 같은 관계
- 의존 관계: 한 클래스가 다른 클래스에서 제공하는 기능을 사용하는 상황에서 실행하는 동안만 그 관계가 유지되는 관계
- 실체화 관계: 객체지향 개념에서 인터페이스와 이를 실현한 클래스들의 관계, can do this
</div>
</details>

<details>
<summary style="font-size:20px">디미터 법칙</summary>
<div markdown="1">

* 디미터 법칙: 최소 지식의 법칙, 모듈은 자신이 조작하는 객체의 속사정을 몰라야한다는 원칙으로 여러 개의 .(도트)를 사용하지 말라는 법칙으로 불림

</div>
</details>

<details>
<summary style="font-size:20px">CQRS</summary>
<div markdown="1">

* CQRS(Command and Query Responsibility Segregtaion): 하나의 메소드는 명령이나 쿼리여야하며 두 가지 기능을 모두 가져서는 안된다는 이론으로 명령은 객체의 상태를 변경할 수 있지만 값을 반환하지 않고 쿼리는 값을 반환하지만 객체를 변경하지 않음

</div>
</details>

<details>
<summary style="font-size:20px">TDA 원칙</summary>
<div markdown="1">

* TDA 원칙(Tell Dont Ask): 물어보지 말고 그냥 시켜라, 객체와 객체가 협력하는 경우 다른 객체의 정보를 요구하지 말고 그냥 행위하도록 시키라는 의미
* 객체의 상태를 조회하는 메서드를 없애고 상태에 대한 판단 자체를 하는 메서드를 만드는 것은 권장하는 원칙

</div>
</details>


<details>
<summary style="font-size:20px">Overriding과 Overloading</summary>
<div markdown="1">

* 오버라이딩: 부모 클래스에 존재하는 메서드를 자식 클래스에서 재정의하는 것
```java
SuperClass super = new SubClass();
super.function(); // SubClass의 함수 실행
```

* 오버로딩: 같은 이름의 메소드를 여러 개 정의, 매개변수의 타입이나 개수가 달라야 함

</div>
</details>


<details>
<summary style="font-size:20px">객체지향 설계의 5원칙</summary>
<div markdown="1">

* `SRP(Single Responsibility Principle)`: 단일 책임 원칙, 클래스는 단 하나의 책임을 가져야 하며 클래스를 변경하는 이유는 단 하나의 이유이어야 한다.
* `OCP(Open-Closed Principle)`: 개방-폐쇄 원칙, 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다.
  * 추상화(인터페이스)
* `LSP(Liskov Substitution Principle)`: 리스코프 치환 원칙, 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다.
  * 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있다는 원칙이다
  * 자식 클래스가 부모 클래스의 기존 메소드의 의미를 해치지는 않는다.
  * 보통 상속보단 컴포지션을 사용해라.
* `ISP(Interface Segregation Principle)`: 인터페이스 분리 원칙, 인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 한다.
  * 인터페이스는 public으로 선언된 메서드이다.
  * 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 원칙
  * 일반적인 한 개의 인터페이스보다 구체적인 여러가지의 인터페이스를 구현하는 원칙
* `DIP(Dependency Inversion Principle)`: 의존 역전 원칙, 고수준 모듈은 저수준 모듈의 구현에 의존해서는 안된다.
  * 변하지 않는 객체에 의존한다.
  * 상위 클래스, 인터페이스, 추상 클래스일수록 변하지 않을 가능성이 높기에 하위 클래스나 구체(concrete) 클래스가 아닌 상위 클래스, 인터페이스, 추상 클래스에 의존한다.

</div>
</details>

<details>
<summary style="font-size:20px">의존성 주입</summary>
<div markdown="1">

#### 의존
* 기능 구현을 위해 다른 구성 요소를 사용하는 것
* 객체 생성, 메서드 호출, 데이터 사용
#### 의존성 주입
* 의존성에 필요한 값을 외부에서 파라미터로 받아 넣어주는 것

#### 의존성 주입의 방법
* 수정자 주입: Setter를 통해서 필드에 의존성을 주입하는 것
* 생성자 주입: 생성자를 호츨 할 때 의존성을 주입하는 것
* 필드 주입: DI 프레임워크가 필수적으로 필요한 방법으로 필드에 맞는 프레임워크에 의해 의존성을 주입하는 것

#### 조립기
* 객체 생성 및 의존 주입을 처리해주는 모듈
* 스프링 프레임워크에서 ApplicationContext가 이 역할을 수행

#### 의존성 주입 장점
* 의존 대상이 바뀌면 조립기 설정만 변경하면 가능
* 의존하는 객체 없이 대역 객체를 사용해서 테스트가 가능

</div>
</details>


<details>
<summary style="font-size:20px">클래스와 인스턴스의 차이</summary>
<div markdown="1">

* 클래스는 객체를 만들기 위한 템플릿, 객체는 클래스라는 템플릿을 토대로 `메모리에 할당한 실체`
* 클래스: `객체를 만드는 틀`, 객체의 속성과 기능(행위)을 정의
* 객체: `클래스라는 틀에서 생겨난 실체`, 속성(멤버 변수)과 기능(메소드, 함수)의 집합

</div>
</details>

<details>
<summary style="font-size:20px">상속과 인터페이스의 차이</summary>
<div markdown="1">

* 상속
  * 상속은 확장해서 사용할 수 있다는 의미
  * 상위 클래스에서 구현된 메서드는 모든 하위 클래스의 객체에서 사용 가능
  * 올바른 상속의 설계는 is a kind of 관계(하위 클래스 is a kind of 상위 클래스)를 만족해야함
* 인터페이스
  * 행위에 대한 기능을 강제한다는 의미
  * 올바른 인터페이스의 설계는 be able to 관계를 만족해야함

</div>
</details>

<details>
<summary style="font-size:20px">결합도와 응집도의 차이</summary>
<div markdown="1">

* 결합도
  * 클래스(모듈) 간의 상호 의존 정도
  * 결합도가 낮으면 모듈 간의 상호 의존성이 줄어들어 객체의 재사용이나 수정 및 유지보수가 용이
* 응집도
  * 클래스(모듈) 내부에 존재하는 구성 요소들의 기능적 관령성
  * 응집도가 높은 모듈은 하나의 책임에 집중하고 독립성이 높아져 재사용이나 기능의 수정 및 유지보수가 용이

</div>
</details>


<details>
<summary style="font-size:20px">Immutable</summary>
<div markdown="1">

* 생성 후 변경 불가한 객체로 변경을 하려면 복사 이후 변경해야함

</div>
</details>

<details>
<summary style="font-size:20px">순환 참조</summary>
<div markdown="1">

* 순환 참조: 각각의 객체가 서로를 참조하고 있는 상태
* 객체의 Serializable을 불가능하게 만들고 JPA의 mappedby에서 신경을 추가로 써야함

</div>
</details>

