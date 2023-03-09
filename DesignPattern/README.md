# Design Pattern

<br>

<details>
<summary style="font-size:20px">디자인 패턴</summary>
<div markdown="1">

* 소프트웨어 코드 작성 시에 생기는 `공통적인 문제를 해결하는데 도움이 되는 코드 패턴`
* 디자인 패턴은 객체 지향의 특성 중 상속, 인터페이스, 객체를 속성으로 사용하는 것을 이용해 구현 

</div>
</details>

<details>
<summary style="font-size:20px">디자인 패턴 종류</summary>
<div markdown="1">

* 생성 패턴: 객체 생성에 관련된 패턴
* 구조 패턴: 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
* 행위 패턴: 클래스나 객체들이 서로 상호작용하는 방법이나 책임 분배 방법을 정의하는 패턴

</div>
</details>


<details>
<summary style="font-size:20px">싱글톤 패턴</summary>
<div markdown="1">

* 오직 인스턴스를 하나만 만들어서 재사용하는 패턴(생성 패턴)
* 한번의 객체 생성으로 `재사용`이 가능하기 때문에 메모리 낭비를 방지하고 객체가 `전역성`을 띄기 때문에 공유가 용이

</div>
</details>


<details>
<summary style="font-size:20px">팩토리 메서드 패턴</summary>
<div markdown="1">

* 하위 클래스에서 객체를 생성 반환에 사용되는 메서드인 팩터리 메서드를 오버라이딩해서 객체를 반환하게 하는 패턴(생성 패턴)
* 팩토리 패턴은 클래스의 `인스턴스를 만드는 것을 서브 클래스에서 결정하는 패턴`으로 팩토리 메서드 패턴과 추상 팩토리 패턴으로 구체화되나 주로 팩토리 메서드 패턴를 사용
</div>
</details>

<details>
<summary style="font-size:20px">프록시 패턴</summary>
<div markdown="1">

* 대신해서 그 역할 수행하는 프록시를 통해서 메서드의 반환 값을 수정하는 게 아니라 별도 로직을 수행하는 패턴(구조 패턴)
</div>
</details>

<details>
<summary style="font-size:20px">데코레이터 패턴</summary>
<div markdown="1">

* 원본에 장식을 더하는 데커레이터를 통해서 객체의 결합을 통해 반환 값에 장식을 덧붙이는 패턴(구조 패턴)
* 장식자의 역할은 원본에 장식을 더하는 것
</div>
</details>

<details>
<summary style="font-size:20px">어댑터 패턴</summary>
<div markdown="1">

* 객체를 속성으로 참조해서 만드는 패턴으로 호출 당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 변환기를 통해 호출하는 패턴(구조 패턴)
* 어댑터(변환기)의 역할은 서로 다른 두 인터페이스 사이에 통신이 가능하게 하는 것
</div>
</details>

<details>
<summary style="font-size:20px">템플릿 메서드 패턴</summary>
<div markdown="1">

* 상위 클래스의 템플릿 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴(행위 패턴)
* 상속을 이용해서 동일한 코드를 제외하고 코드를 추가
</div>
</details>

<details>
<summary style="font-size:20px">전략 패턴</summary>
<div markdown="1">

* 클라이언트가 전략을 생성해 전략을 실행한 컨텍스트에 주입하는 패턴(행위 패턴)
* 객체 주입을 통해서 동일한 코드를 제외하고 코드를 추가
</div>
</details>

<details>
<summary style="font-size:20px">옵서버 패턴</summary>
<div markdown="1">

* 한 객체의 상태 변화를 관찰하다가 변화가 있을 때마다 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴으로 일대다 객체 의존 관계를 구성하는 패턴(행위 패턴)
</div>
</details>


<details>
<summary style="font-size:20px">MVC 패턴</summary>
<div markdown="1">

* Model, View, Controller라고 하는 컴포넌트로 분리하여 `비지니스 처리 로직`과 사용자 `인터페이스 요소`를 분리시켜 서로 영향없이 개발하기 수월

</div>
</details>
