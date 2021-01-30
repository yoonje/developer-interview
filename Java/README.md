### Java
* JVM과 Java 프로그램 실행 과정
  * JVM은 Java Virtual Machine의 약자로 자바 프로그램을 실행하는 역할을 하고 프로그램이 시작되면 컴파일러를 통해 바이트 코드로 변환하고 변환된 파일을 JVM에 로딩하여 실행
  * `Java Source code (.java)` -> 컴파일(파일 저장 시, 자동 생성) -> `Java Application (.class)` -> 실행 -> `JVM` -> 실행 -> `컴퓨터`
* JVM 메모리 구조
  * 크게 `메소드 영역, JVM 스택, JVM 힙`으로 나뉘며 JVM 힙은 `Young Generation, Old Generation, Permanent Generation`으로 나뉘고 Young Generation은 `Eden, Survivor0, Survivor1`으로 나뉨
* Java에서 Garbage Collection이 필요한 이유에 대해서 설명
  * 자바는 메모리를 명시적으로 해제하지 않기 때문에 GC를 통해서 필요없는 객체를 지우는 작업을 수행
  * 더이상 사용하지 않는 동적 할당된 메모리 블럭(Heap)을 찾아 다시 사용 가능한 자원으로 회수
  * 장점: 유효하지 않는 포인터 접근, 이중 해제, 메모리 누수의 버그를 줄임
  * 단점: 오버헤드, 비용, 프로그램 예측 불가, 실시간 시스템에는 적합X
* Java Garbage Collection 동작 방식
  * 새롭게 생성된 객체는 `Young의 Eden 영역`으로 들어가게 되고 `Eden 영역이 다 차면 Minor GC`가 발생하여 참조 횟수에 따라 증가하는 `age bit`를 보고 불필요한 객체를 삭제하고 생존한 객체는 S0으로 이동
  * Minor GC가 발생할 때마다 각각 Young 영역의 객체들은 삭제와 이동을 하게되는데 (Eden -> S0 / S0 -> S1)
  * S1이 가득 차면 필요한 객체는 `OLD 영역`으로 이동하고 `OLD 영역이 가득차면 Major GC`를 통해서 값을 삭제
  * GC가 실행될 때마다 `STOP THE WORLD`가 발생하여 프로그램이 중지
* Overriding과 Overloading
  * `오버라이딩은 부모 클래스에 존재하는 메서드를 하위 클래스에서 재정의하는 것`이고 `오버로딩은 같은 메서드 이름을 갖게 하지만 시그니처가 다르게 정의하는 것`
* 추상 클래스와 인터페이스
  * 추상 클래스는 반드시 구현(오버라이딩)해야하는 추상 메소드를 1개 이상 갖고 있는 클래스로 추상 메소드에도 abstract 키워드를 붙여주고 추상 클래스에도 abstract 키워드를 붙여서 표기
  * 인터페이스는 추상 메소드만 갖고 있는 개념으로 class 대신 interface 키워드를 붙이고 메소드에도 abstract 키워드를 붙이지 않고 표기
  * 두 가지 개념 모두 독립 생성이 불가능하고 상속을 목적으로 사용하는데 추상 클래스는 1번만 상속받을 수 있지만 인터페이스는 여러번 상속 가능
  * 인터페이스는 추상 클래스와 달리 구현을 강제함으로써 구현 객체의 같은 동작을 보장하여 인터페이스를 이용하여 `표준화를 확립할 수 있으므로 서로 관계가 없는 객체들이 상호 작용을 가능하게 함`
* Collection
  * List: 대표적인 구현체로는 `ArrayList`가 존재한다. 이는 기존에 있었던 `Vector`를 개선한 것이다.
  * Map: 대표적인 구현체로 `HashMap`이 존재한다. 해시테이블처럼 `key-value`의 구조로 이루어져 있으며 key를 기준으로 중복된 값을 저장하지 않으며 순서를 보장하지 않는다. 
  * Set: 대표적인 구현체로 `HashSet`이 존재한다. `value에 대해서 중복된 값을 저장하지 않는다.`
  * Stack과 Queue: Stack은 직접 new 키워드로 사용할 수 있으며, Queue는 LinkedList에 new 키워드를 적용하여 사용
* Annotation
  * 어노테이션이란 본래 주석이란 뜻이지만, 자바에서는 인터페이스를 기반으로 한 문법으로 주석과 다른 점은 주석처럼 `코드에 달아 클래스에 특별한 의미를 부여하거나 기능을 주입함`
* Generic
  * 제네릭은 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에서 사용하는 것으로, `컴파일 과정에서 타입체크를 해주는 기능`
* Access Modifier
  * public: 어떤 클래스든 접근할 수 있다는 것을 의미
  * protected: 자기 자신, 같은 패키지, 서로 다른 패키지다 하더라도 상속받은 자식 클래스에서만 접근할수 있다는 것을 의미
  * private(default): 자기 자신의 스코프에서만 접근할 수 있다는 것을 의미
* final 키워드
  * final 키워드는 상수로 정의하는 키워드
  * final class: 다른 클래스에서 상속하지 못한다.
  * final method: 다른 메소드에서 오버라이딩하지 못한다.
  * final variable: 변하지 않는 상수값이 되어 새로 할당할 수 없는 변수가 된다.
* Wrapper class
  * 
* Synchronized
  * 
* ThreadLocal
  * 
* String, StringBuilder, StringBuffer
  * 
* ==와 equals()의 차이
  * == 연산자는 참조형을 비교할 때 `레퍼런스를 비교`하고 eqals()는 참조형을 비교할 때 `값을 비교`
* equals() 메소드 동작 원리
  * 
* 기본(원시)형과 참조형의 차이점
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
* Integer vs int
  * 
* int와 short
  *
* Java String
  * 
* non-static과 static 멤버의 차이
  * 
* 변수의 종류와 메모리 구조
  * 
* reflection
  * 
* Java Thread
  *  
* Casting(업케스팅, 다운케스팅)
  * 
* 고유 락
  * 
* Promotion & Casting
  * 
* Error & Exception
  * 
* Java7에서 Java8로 올라오면서 달라진 점
  * 