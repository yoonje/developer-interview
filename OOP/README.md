# OOP(Object-Oriented Programming)

<br>

<details>
<summary style="font-size:20px">자바, C++, C, Python</summary>
<div markdown="1">

* 자바: 컴파일 언어(코드 전체를 한번에 번역), 객체지향 언어, 기본 단위가 Class, 거의 완전한 OOP, 가상머신에서 실행하여 OS와 독립적, 가비지 콜렉션 지원
* C++: 컴파일 언어, 객체지향 언어, C의 상위 호환으로 절차지향이 섞임, 각 OS에 맞는 기계어로 변환해 실행(속도 빠름), 메모리를 직접 관리할 수 있음
* C: 컴파일 언어, 절차지향 언어
* Python: 인터프리터 언어(코드를 한줄씩 번역해 실행), 객체지향 언어, C언어를 기반으로 한 언어로 머신러닝, 빅데이터 등의 분야에서 많이 사용

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

* `추상화`: 사물의 불필요한 부분을 제거하고 공통된 특징만 추출하여 이해하기 쉽게 만드는 작업
  * 하위클래스들에 존재하는 공통적인 메소드를 `인터페이스`로 정의
* `캡슐화`: 속성과 기능을 멤버 변수와 멤버 함수로 만들어 클래스라는 캡슐에 넣음
  * 목적: 소스 코드의 수정없는 재활용
  * 외부 사용자는 클래스의 세부 구현에 대해 알 필요X
  * `정보 은닉`: 접근지정자 `private`으로 멤버 변수 선언, 해당 변수에 접근하는 별도의 함수 정의
* `상속`: 부모 클래스의 기능을 모두 또는 일부 수정하여 자식 클래스가 사용하는 것
  * 코드 재사용
* `다형성`: 같은 메서드가 각각의 객체에서 서로 다른 방법으로 응답, `상속`에서 효과를 발휘, 하나의 변수명/함수명 등이 상황에 따라서 다르게 동작하는 것
  * 부모 클래스: 추상 클래스, 함수: 추상 함수
  * 자식 클래스: draw 함수를 자신의 목적에 맞게, 서로 다른 방법으로 구현 / ex) 삼각형, 사각형 그리기

</div>
</details>


<details>
<summary style="font-size:20px">객체지향과 절차지향</summary>
<div markdown="1">

* 객체지향: 객체별 개별 코딩, 클래스를 이용해 기능별로 구성 가능, 실행 속도 느림, Java -> 상태 보관
* 절차지향: 해야 할 작업을 순서대로 코딩, 함수 단위로 구성, 실행 속도 빠름, C

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
<summary style="font-size:20px">디미터 법칙</summary>
<div markdown="1">

* 디미터 법칙: 최소 지식의 법칙, 모듈은 자신이 조작하는 객체의 속사정을 몰라야한다는 원칙

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

</div>
</details>

<details>
<summary style="font-size:20px"> Call by Value vs Call by Reference</summary>
<div markdown="1">

* `값을 복사`를 하여 처리하는지 `직접 참조`하는지의 차이
* Call by Value: 인자로 받은 값을 복사하여 처리
* Call by Reference: 인자로 받은 값의 주소를 참조하여 직접 값에 영향을 줌

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
  * 의존성(다른 객체나 함수를 사용하는 것)
  * 변하지 않는 객체에 의존한다.
  * 상위 클래스, 인터페이스, 추상 클래스일수록 변하지 않을 가능성이 높기에 하위 클래스나 구체(concrete) 클래스가 아닌 상위 클래스, 인터페이스, 추상 클래스에 의존한다.

</div>
</details>

<details>
<summary style="font-size:20px">의존성 주입</summary>
<div markdown="1">

#### 의존성 주입
* 의존성에 필요한 값을 외부에서 파라미터로 받아 넣어주는 것

#### 객체 생성 시의 의존성 주입의 방법
* 수정자 주입: Setter를 통해서 필드에 의존성을 주입하는 것
* 생성자 주입: 생성자를 호츨 할 때 의존성을 주입하는 것
* 필드 주입: DI 프레임워크가 필수적으로 필요한 방법으로 필드에 맞는 프레임워크에 의해 의존성을 주입하는 것

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
<summary style="font-size:20px">Immutable</summary>
<div markdown="1">

* 생성 후 변경 불가한 객체로 변경을 하려면 복사 이후 변경해야함

</div>
</details>

<details>
<summary style="font-size:20px">순환 참조</summary>
<div markdown="1">

* 순환 참조: 각각의 객체가 서로를 참조하고 있는 상태로 객체를 Serializable을 불가능하게 만들고 JPA의 mappedby에서 신경을 추가로 써야함

</div>
</details>

<details>
<summary style="font-size:20px">디자인 패턴</summary>
<div markdown="1">

* 소프트웨어 코드 작성 시에 생기는 `공통적인 문제를 해결하는데 도움이 되는 코드 패턴`

</div>
</details>


<details>
<summary style="font-size:20px">싱글톤 패턴</summary>
<div markdown="1">

* 전체 프로그램에서 `단 1개의 객체`를 생생하고 공유하는 코드 패턴
* 한번의 객체 생성으로 `재사용`이 가능하기 때문에 메모리 낭비를 방지하고 객체가 `전역성`을 띄기 때문에 공유가 용이

</div>
</details>


<details>
<summary style="font-size:20px">MVC 패턴</summary>
<div markdown="1">

* Model, View, Controller라고 하는 컴포넌트로 분리하여 `비지니스 처리 로직`과 사용자 `인터페이스 요소`를 분리시켜 서로 영향없이 개발하기 수월

</div>
</details>


<details>
<summary style="font-size:20px">팩토리 패턴</summary>
<div markdown="1">

* 팩토리 패턴은 클래스의 `인스턴스를 만드는 것을 서브클래스에서 결정하는 패턴`으로 팩토리 메서드 패턴과 추상 팩토리 패턴으로 구체화됨
* 팩토리 메서드 패턴: 객체를 생성하기 위한 인터페이스를 정의하는데, 어떤 클래스의 인스턴스를 만들지는 `서브클래스`에서 결정
* 추상 팩토리 패턴: 인터페이스를 이용하여 서로 연관된, 또는 의존하는 객체를 구상 클래스를 지정하지 않고도 생성

</div>
</details>

<details>
<summary style="font-size:20px">퍼사드 패턴</summary>
<div markdown="1">

* 
</div>
</details>


