# Java

<br>

<details>
<summary style="font-size:20px">Java 특징</summary>
<div markdown="1">

* 미국의 Sun마이크로시스템이 개발
* `객체 지향` 프로그래밍 언어, `컴파일` 언어
* JVM만 있으면 OS와 상관없이 동작 가능(운영체제에 독립적)
* 고성능(High Performance): 바이트 코드로 변환되어 실행
* 멀티 스레딩 지원

</div>
</details>


<details>
<summary style="font-size:20px">JVM(Java Virtual Machine)</summary>
<div markdown="1">

* `자바 프로그램을 실행`하는 역할
  * 컴파일러를 통해 바이트 코드로 변환된 파일을 JVM에 로딩하여 실행
* Garbage Collection 수행 (메모리 관리)
* `Class Loader`: JVM 내(Runtime Data Area)로 Class 파일을 로드하고 링크
* `Excution Engine`: 메모리(Runtime Data Area)에 적재된 클래스들을 기계어로 변경해 실행
  * 인터프리터: 바이트 코드를 한줄씩 읽어 기계어로 변환
  * JIT 컴파일러: 반복되는 코드를 기계어로 변환해 캐싱 (-> 캐싱한 것을 바로 실행해 속도 향상)
* `Garbage Collecter`: 힙 메모리에서 참조되지 않는 객체를 제거
* `Runtime Data Area`: 자바 프로그램을 실행할 때, OS로부터 할당받는 `메모리`

</div>
</details>


<details>
<summary style="font-size:20px">Java 프로그램 실행 과정</summary>
<div markdown="1">

* JVM은 OS로부터 메모리(Runtime Data Area)를 할당받음
* `컴파일러(javac)`가 `소스코드(.java)`를 읽어들여 `바이트 코드(.class)`로 변환
* `Class Loader`를 통해 Class 파일을 `JVM 내의 Runtime Data Area에 로딩`
* 로딩된 Class 파일을 `Excution Engine을 사용해 해석 및 실행`

</div>
</details>


<details>
<summary style="font-size:20px">JVM 메모리(Runtime Data Area) 구조</summary>
<div markdown="1">

#### JVM 구조

  * 크게 `메소드 영역, JVM 스택, JVM 힙`으로 나뉘며 JVM 힙은 `Young Generation, Old Generation`으로 나뉘고 Young Generation은 `Eden, Survivor0, Survivor1`으로 나뉨

#### Method Area
* 모든 스레드가 공유
* Class Loader가 적재한 `클래스/인터페이스에 대한 정보(바이트 코드)`를 저장
  * 이 영역에 등록된 클래스만 Heap에 생성 가능
* 타입 정보(클래스 or 인터페이스, 접근 제어자 등), 메소드(생성자 포함, 이름, 리턴 타입, 접근 제어자 등), 필드(데이터 타입, 접근 제어자), Static(클래스) 변수
* Runtime Comstant Pool: 클래스와 인터페이스/메소드/필드에 대한 모든 레퍼런스 저장
  * JVM은 이를 이용해 실제 메모리 주소를 찾아 참조

#### JVM 힙
* 모든 스레드가 공유
* `런타임`에 `동적`으로 할당하여 사용하는 영역
* new 연산자로 생성된 객체 저장
* `GC`의 대상: 힙 영역의 객체는 스택의 변수나 다른 객체에서 참조, 참조가 없으면 GC 대상

#### JVM 스택
* 스레드마다 존재, 스레드가 시작될 때 할당, LIFO
* 지역변수, 매개변수, 연산 중 발생하는 임시 데이터 저장
* 참고
  * `기본 타입` 변수: 스택에 `값` 저장
  * `참조 타입` 변수: 힙이나 메소드 영역 객체의 `주소` 저장

#### Native Method Stack
* 스레드마다 존재
* 자바가 아닌 언어로 작성된 네이티브 코드를 위한 스택

#### PC 레지스터
* 스레드마다 존재
* 현재 수행 중인 JVM 명령어의 주소를 가짐

</div>
</details>


<details>
<summary style="font-size:20px">변수의 종류와 메모리 구조</summary>
<div markdown="1">

* 인스턴스 변수: 객체에서 사용되는 변수 -> 힙 영역
* 클래스 변수: static 변수 -> 메소드 영역
* 지역 변수: 메소드 내에서 선언되어 메소드 안에서만 사용할 수 있는 변수 -> 스택 영역

```java
public class Test{
  private int iv; // 인스턴스 변수
  public static int cv; // 클래스 변수
  public void print(){
  	int lv; // 지역 변수
  }
}
```

</div>
</details>


<details>
<summary style="font-size:20px">Java에서 Garbage Collection이 필요한 이유</summary>
<div markdown="1">

* Garbage: 더 이상 사용되지 않는 메모리, 객체를 가리키는 레퍼런스가 없는 것 
* 자바는 메모리를 명시적으로 해제하지 않기 때문에 GC를 통해서 필요없는 객체를 지움
* 더이상 사용하지 않는 `동적 할당된 메모리 블럭(Heap)`을 찾아 다시 사용 가능한 자원으로 회수

</div>
</details>


<details>
<summary style="font-size:20px">Garbage Collection 동작 방식</summary>
<div markdown="1">

#### GC

* 새롭게 생성된 객체는 `Heap`의 `Young Generation의 Eden 영역`에 저장
* `Eden 영역이 다 차면 Minor GC`가 발생하여 참조 횟수에 따라 증가하는 `age bit`를 보고 불필요한 객체를 삭제하고 생존한 객체는 `S0`으로 이동
* Minor GC가 발생할 때마다 Young 영역의 객체들은 삭제와 이동을 함 (Eden -> S0 / S0 -> S1 / S0 <- S1)
* S1이 가득 차면 필요한 객체는 `OLD 영역으로 이동(Promition)`하고 `OLD 영역이 가득차면 Major GC`를 통해서 값을 삭제

#### 참고
* age bit: 각 객체가 Minor GC에서 살아남은 횟수를 기록, Minor GC가 발생할 때마다 하나씩 증가, age bit 값이 MaxTenuringThreshold 라는 설정 값을 초과하면 Old Generation으로 객체가 이동
* STOP THE WORLD: GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춤, GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작
  * GC가 실행될 때마다 `STOP THE WORLD`가 발생하여 프로그램이 중지

#### 참고: Heap
##### Young Generation
* 자바의 객체가 생성되자마자 저장, 생성된지 오래되지 않은 객체가 저장
* 시간이 지나 우선순위가 낮아지면(Young에서 오랫동안 사용되면) Old Generation으로 이동
* `Minor GC` 발생
* `Eden`, `Survivor0`, `Survivor1`로 구성

##### Old Generation
* Young Generation에서 옮겨진 객체를 저장
* 객체가 사라질 때, `Major GC` 발생

##### (Non-Heap)  Permanent Generation
* Java7버전까지는 Heap에 존재, 8부터는 Native Method Stack에 Meta Space로 변경
* Class Loader에 의해 Load된 클래스의 메타 데이터 저장

</div>
</details>


<details>
<summary style="font-size:20px">추상 클래스와 인터페이스</summary>
<div markdown="1">

#### 추상 클래스
* 반드시 `구현(오버라이딩)`해야하는 추상 메소드를 1개 이상 갖고 있는 클래스
* 실체 클래스의 공통적인 변수와 메소드를 추출해 선언한 클래스
* 추상 메소드와 클래스 모두에 `abstract` 키워드를 붙여서 표기, 추상 클래스의 상속에는 `extends` 키워드 사용
* 추상 클래스와 실체 클래스는 `상속관계` -> 실체 클래스는 추상 클래스의 추상 메소드를 상속받아 `오버라이딩` 해야 함
* 사용 이유
  * 필드와 메소드 통일: 유지보수성 향상 및 통일성 유지 (A객체를 B객체로 변경할 경우 -> 필드/메서드가 동일하면 객체만 변경하면 됨)
  * 규격에 맞는 실체 클래스 구현: 추상클래스의 추상 메소드는 반드시 오버라이딩되어야 함
  * 일반적인 추상화 및 상속에 더 초점, `상속 받아서 기능을 확장`시키는데 목적

```java
public abstract class AbstractClass {
  public void function() {};
  public abstract void abstractFunction();
}
```

#### 인터페이스
* 어떤 메소드를 제공하는지 알려주는 명세(Specification)
* 추상 클래스의 일종으로 default 메소드와 static 메소드를 제외하면 `추상 메소드와 상수만` 가짐
* 상속 관계가 없는 클래스에서 공통되는 로직을 구현하여 사용
* `interface` 키워드를 통해 선언, `implements`로 일반 클래스에서 인터페이스를 구현
* 사용 이유
  * 동일한 목적 하에 동일한 기능을 보장하는 것 -> 메서드를 구현하게 하는 것에 초점
  * 다형성 극대화 -> 코드의 수정은 감소, 유지보수성 증가

```java
public interface Interface {
  public int max = 10; // 상수, 무조건 인터페이스에서 제공하는 값을 사용
  public abstract void abstractFunction(); // 추상 메소드: 일반 클래스에서 오버리이딩 필수
  default void function(){} // default 메소드: 인터페이스에서 제공하는 것을 사용하거나 일반 클래스에서 따로 구현하여 사용할 수 있음
  // 추가 요건으로 메소드를 추가할 때, default를 사용하면 유지보수성을 높일 수 있음
  // 추상 메소드를 추가하면 일반 클래스에서 이를 구현하지 않으면 모두 에러가 발생하기 때문
  static void function2(){} // 정적 메소드: 무조건 인터페이스에서 제공하는 것을 사용
}
```

#### 공통점
* 두 가지 개념 모두 독립적으로 객체 생성 불가, 상속을 목적으로 사용
* 추상 메소드는 오버라이딩이 필요

#### 차이점
* 추상 클래스는 다중 상속 불가능, 인터페이스는 다중 상속 가능
* 추상 클래스는 상속을 통해 기능을 확장하는 것이 목적
* 인터페이스는 추상 클래스와 달리 구현을 강제함으로써 `구현 객체의 같은 동작`을 보장하여 인터페이스를 이용하여 `표준화를 확립할 수 있으므로 서로 관계가 없는 객체들이 상호 작용을 가능하게 함`
 
#### 참고
* https://wildeveloperetrain.tistory.com/112

</div>
</details>

<details>
<summary style="font-size:20px">Collection Framework</summary>
<div markdown="1">

#### JAVA Collection
* 데이터를 효율적으로 관리할 수 있는 자료구조와 알고리즘을 구조화하여 클래스로 구현한 것
* `List, Set, Map 인터페이스`가 존재
  * Collection Interface -> List, Set
  * Map Interface

#### List
* 순서가 있는 데이터 집합, 데이터의 중복 허용
* `ArrayList`(`Vector`를 개선), `Vector`, `Stack`, `LinkedList`
* Stack과 Queue: Stack은 직접 new 키워드로 사용할 수 있으며, Queue는 LinkedList에 new 키워드를 적용하여 사용

#### Set
* 데이터의 중복을 허용하지 않음
* `Hash Set`: value에 대해서 중복된 값을 저장하지 않음

#### Map
* 키와 값의 쌍으로 이루어진 데이터 집합
* 키는 중복을 허용하지 않고 값의 중복은 허용
* `Hash Map`: 해시테이블처럼 `key-value`의 구조로 이루어져 있으며 key를 기준으로 중복된 값을 저장하지 않으며 순서를 보장하지 않음 

</div>
</details>


<details>
<summary style="font-size:20px">Vector와 ArrayList 차이</summary>
<div markdown="1">

* Vector: Thread-Safe
* ArrayList: Thread-SafeX

</div>
</details>


<details>
<summary style="font-size:20px">Hash Map과 Hash Table의 차이</summary>
<div markdown="1">

* Hash Map: 메소드 동기화X, Thread Safe 아님, 성능 빠름
* Hash Table: 메소드 동기화 지원, Thread Safe, 성능 느림

</div>
</details>


<details>
<summary style="font-size:20px">Hash Map과 Tree Map의 차이</summary>
<div markdown="1">

* Hash Map: 해싱 구현, 랜덤 정렬(순서 유지X), Null 키 가능, 훨씬 빠름
* Tree Map: 레드블랙트리(이진탐색트리)로 구현, key로 자동 정렬, Null 키 불가능

</div>
</details>


<details>
<summary style="font-size:20px">Hash Set과 Tree Set의 차이</summary>
<div markdown="1">

* Hash Set: 해싱으로 구현, 삽입된 요소는 랜덤 정렬, Null 저장 가능, 성능 빠름, 값 비교에 equals 사용
* Tree Set: 레드블랙트리(이진탐색트리) 구현, 정렬 순서 유지(자동 정렬), Null 저장 불가, 성능 느림, 값 비교에 comparedTo 사용

</div>
</details>


<details>
<summary style="font-size:20px">Generic</summary>
<div markdown="1">

* `컴파일 과정에서 타입을 체크`하는 기능
* 클래스 내부에서 사용할 데이터 `타입`을 외부에서 지정하는 기법
* 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에서 사용
* 사용 이유
  * 잘못된 타입이 사용될 문제를 컴파일 과정에서 제거 가능
  * 코드 재사용성 증가

</div>
</details>


<details>
<summary style="font-size:20px">Annotation</summary>
<div markdown="1">

* 어노테이션이란 본래 주석이란 뜻이지만, 자바에서는 인터페이스를 기반으로 한 문법
* `코드에 달아 클래스에 특별한 의미를 부여하거나 기능을 주입함`

</div>
</details>


<details>
<summary style="font-size:20px">Access Modifier(접근 제한자)</summary>
<div markdown="1">

* public: 모든 클래스에서 접근할 수 있다는 것을 의미(패키지가 달라도 허용)
* protected: `같은 패키지`에서 접근 허용, `다른 패키지의 상속`받은 클래스에서 접근 허용, 다른 패키지의 다른 클래스에서 접근 불가
* default: `같은 패키지` 내에서만 접근 허용
* private: 동일 패키지라도 접근 불가, `같은 클래스` 내에서만 접근 허용
* 사용 이유
  * 정보은닉(민감 정보 유출 안하기), 외부에서 알 필요 없는 값은 노출X
  * 응집도 높이고 결합도 낮추기

</div>
</details>


<details>
<summary style="font-size:20px">final 키워드</summary>
<div markdown="1">

* final 키워드는 `상수`로 정의하는 키워드
* final class: 다른 클래스에서 상속하지 못함
* final method: 다른 메소드에서 오버라이딩하지 못함 (오버로딩 가능)
* final variable: 변하지 않는 상수값이 되어 새로 할당할 수 없는 변수가 됨
* 생성자: final이 될 수 없음

</div>
</details>


<details>
<summary style="font-size:20px">non-static과 static 멤버의 차이</summary>
<div markdown="1">

#### non-static
* 객체마다 멤버가 존재
* 객체 생성 시에 멤버 생성
  * 객체가 생성될 때 멤버 생성, 객체가 사라질 때 멤버가 사라짐
* 같은 클래스의 객체 사이에서 공유되지 않음

#### static
* 객체를 많이 생성해도 해당 변수는 한개만 존재(객체와 무관한 키워드), 클래스당 1개 존재
* 클래스를 로딩할 때, 멤버 생성, 처음 설정된 메모리 공간이 변하지 않음을 의미 
  * 객체가 생성되기 전에 사용 가능, 객체가 사라져도 멤버 사라지지 않음 -> 프로그램 종료 시 사라짐
* 동일한 클래스의 모든 객체들에 의해 공유

</div>
</details>


<details>
<summary style="font-size:20px">Wrapper Class</summary>
<div markdown="1">

* 기본 타입 데이터를 객체로 포장해주는 클래스
* 기본 타입 데이터를 객체로 만들어야 할 경우 사용
* Byte, Integer, Long, Double, Boolean, Character 등

#### Boxing
* 기본 타입 -> 래퍼 클래스

```java
Integer num = new Integer(17);
```

#### Unboxing
* 래퍼 클래스 -> 기본 타입

```java
int n = num.intValue();
```

</div>
</details>


<details>
<summary style="font-size:20px">기본(원시)형과 참조형의 차이점</summary>
<div markdown="1">

* 기본형: boolean, char, byte, short, int, long, float, double
* 참조형: 기본형 8가지를 제외한 나머지 타입, Integer, Long, Double, Boolean 등
* 참조형은 null을 입력할 수 있지만 기본형은 null 불가능

```java
int i = null; //불가능
Integer ii = null; //가능
```

* 참조형은 제너릭 타입에서 사용 가능하지만 기본형은 불가능
  * 제너릭(Generic): 클래스에서 사용할 타입을 클래스 외부에서 설정, 타입을 파라미터화해서 컴파일시 구체적인 타입이 결정

```java
List<int> i; //불가능
List<Integer> ii; //가능
```

* 참조형은 할당연산자 사용 시에 값의 주소가 전달되고 기본형은 값 자체가 전달 -> 기본형은 `스택`에 값이 존재, 참조형은 값은 `힙`에 존재하고 `스택`에 참조 값이 존재해 언박싱 필요
* 참조형은 기본형보다 차지하는 메모리가 크고 접근 속도가 느림

</div>
</details>


<details>
<summary style="font-size:20px">Integer와 int</summary>
<div markdown="1">

#### Integer
* Wrapper Class로 Unboxing을 해야 산술 연산이 가능하고 null을 처리할 수 있음
* int를 클래스로 감싼 형태

#### int
* 기본 자료형으로 산술 연산이 가능하고 null 처리는 불가능

</div>
</details>


<details>
<summary style="font-size:20px">int와 short</summary>
<div markdown="1">

#### int
* 4바이트

#### short
* 2바이트

</div>
</details>


<details>
<summary style="font-size:20px">String, StringBuilder, StringBuffer</summary>
<div markdown="1">

#### String, StringBuilder, StringBuffer 특성

* String: `불변성`, StringBuilder/StringBuffer: `가변성`

#### String
* 값을 변화시킬 때, Heap에 새로운 메모리를 사용, 스택에서 참조되는 메모리 주소 변경
  * 기존 Heap 메모리는 GC의 대상이 됨
* 값이 바뀌지 않는 문자열에 사용하는 것이 좋음
* 단순 읽기에서 성능 좋음
* Thread-Safe: 동기화 지원

#### StringBuilder
* 같은 객체에서 값을 바꿀수 있음
* Thread-Safe 아님: 동기화 지원하지 않음
* StringBuffer보다 빠름

#### StringBuffer
* 같은 객체에서 값을 바꿀수 있음
* Thread-Safe: 동기화 지원

</div>
</details>


<details>
<summary style="font-size:20px">==와 equals()의 차이</summary>
<div markdown="1">

* == 연산자는 참조형을 비교할 때 `레퍼런스(주소)를 비교`하고 eqals()는 참조형을 비교할 때 `값을 비교`

```java
String a = "string"; // 리터럴 선언: String Constant Pool (힙)
String b = "string";
String c = new String("string"); // new 선언: 힙

System.out.println(a == b); // true // 주소 비교인데 같은 객체를 가리킴
System.out.println(a == c); // false

System.out.println(a.equals(b)); // true
System.out.println(a.equals(c)); // true
```

</div>
</details>


<details>
<summary style="font-size:20px">람다 표현식</summary>
<div markdown="1">

* `익명 함수`(Anonymous Function)의 한 종류
* 함수를 따로 만들지 않고 코드 한 줄에 함수를 써서 그것을 호출
* 자바8부터 지원, 코드가 간결하고 가독성이 높음
* 재사용이 불가능하고 디버깅이 어려움
* 예시: Optional, Stream

</div>
</details>


<details>
<summary style="font-size:20px">Thread 생성방법</summary>
<div markdown="1">

* `Thread 클래스 상속`
* `Runnable 인터페이스 구현`

</div>
</details>


<details>
<summary style="font-size:20px">Synchronized</summary>
<div markdown="1">

* 공유 자원에 두개 이상의 쓰레드가 동시에 접근하지 못하도록 `Lock`
* 자바에서는 메소드 앞에 `synchronized`를 붙여 동기화
* 객체에도 사용 가능

</div>
</details>


<details>
<summary style="font-size:20px">ThreadLocal</summary>
<div markdown="1">

* 오직 한 쓰레드에 의해 읽고 쓰여질 수 있는 변수를 생성
* 다른 쓰레드가 같은 ThreadLocal을 호출해도 서로 다른 값을 가짐

</div>
</details>


<details>
<summary style="font-size:20px">Casting</summary>
<div markdown="1">

#### 업캐스팅
* 자식 클래스의 객체가 부모 클래스의 객체로 캐스팅

```java
SuperClass super = new ChildClass();
super.childFunction(); // 자식 클래스의 함수 실행
```

* 부모 클래스의 함수를 오버라이딩한 자식 클래스의 함수 실행 가능
* 부모 클래스의 static 메소드 실행 가능
* 자식 클래스에만 있는 멤버는 실행 불가(컴파일 에러)

#### 다운캐스팅
* 부모 클래스의 객체가 자식 클래스로 캐스팅 -> 업캐스팅되어 고유의 특성을 잃은 자식 클래스의 객체를 복구시키는 것

```java
SuperClass super = new ChildClass();
ChildClass child = (ChildClass)super;
child.superFunction(); //가능
```

</div>
</details>


<details>
<summary style="font-size:20px">Promotion과 Casting</summary>
<div markdown="1">

#### Promotion: 묵시적 형변환
* 작은 타입이 큰 타입으로 변환

```java
int a = 10; float b;
b = a;

SuperClass super = new SubClass();
```

#### Casting: 명시적 형변환
* 큰 타입을 작은 타입으로 변환

```java
int a; float b = 1.1;
a = (int)b;

SuperClass super;
SubClass sub = (SubClass)super;
```

</div>
</details>


<details>
<summary style="font-size:20px">reflection</summary>
<div markdown="1">

* 런타임에 클래스를 사용해야 할 때 필요
* 동적으로 객체를 생성하고 메서드를 호출하는 방법
* Class, Constructor, Method, Field : 객체 생성, 메서드 호출, 변수 값 변경 등 가능

</div>
</details>

<details>
<summary style="font-size:20px">Error와 Exception</summary>
<div markdown="1">

#### Error
* `런타임`에서 실행 시 발생되며 모두 예측 불가능한 Unchecked Error
* 핸들링 불가능

#### Exception
* Checked Exception: 실행하기 전에 예측 가능 -> SQLException, FileNotFoundException 
* Unchecked Exception: 실행하고 난 후에 알 수 있음 -> ArrayIndexOutOfBoundException, NullPointerException(Null인 객체에 접근하면 발생)
* 핸들링 가능, 예외 처리 가능(try ~ catch)

</div>
</details>


<details>
<summary style="font-size:20px">Java7에서 Java8로 올라오면서 달라진 점</summary>
<div markdown="1">

* 람다 표현식 추가: 함수형 프로그래밍
* Permanent Generation: Java7버전까지는 Heap에 존재, 8부터는 Native Method Stack에 Meta Space로 변경
* 인터페이스에 default 메소드, static 메소드 추가
* stream API: 데이터의 추상화
* java.time 패키지: Joda-Time을 이용한 새로운 날짜와 시간 API

</div>
</details>

<details>
<summary style="font-size:20px"> Call by Value vs Call by Reference</summary>
<div markdown="1">

* `값을 복사`를 하여 처리하는지 `직접 참조`하는지의 차이
* Call by Value: 인자로 받은 값을 복사하여 처리
* Call by Reference: 인자로 받은 값의 주소를 참조하여 직접 값에 영향을 줌
* JAVA에서는 모든 전달 방식이 Call by value로 Call by reference는 해당 객체의 주소값을 직접 넘기는 게 아닌 객체를 보는 또 다른 주소값을 만들어서 넘김

</div>
</details>
