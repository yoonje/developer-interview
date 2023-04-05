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

* 생성 패턴: 객체 `생성`에 관련된 패턴
  * 팩토리 메서드 패턴(Factory Method Pattern): 어떤 클래스의 인스턴스를 만들지는 서브 클래스에서 결정하는 패턴
  * 싱글턴 패턴(Singleton Pattern): 오직 인스턴스를 하나만 만들어서 재사용하는 패턴
  * 빌더 패턴(Builder Pattern): 생성(construction)과 표기(representation)를 분리해 복잡한 객체를 생성하는 패턴
* 구조 패턴: `클래스나 객체를 조합해 더 큰 구조를 만드는 패턴`
  * 데코레이터 패턴(Decorator Pattern): 원본에 장식을 더하는 데커레이터를 통해서 객체의 결합을 통해 반환 값에 장식을 덧붙이는 패턴
  * 프록시 패턴(Proxy Pattern): 대신해서 그 역할 수행하는 프록시를 통해서 메서드의 반환 값을 수정하는 게 아니라 별도 로직을 수행하는 패턴
  * 어댑터 패턴(Adapter Pattern): 객체를 속성으로 참조해서 만드는 패턴으로 호출 당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 변환기를 통해 호출하는 패턴
* 행위 패턴: 클래스나 객체들이 서로 `상호 작용하는 방법이나 책임 분배 방법을 정의하는 패턴`
  * 옵서버 패턴(Observer Pattern): 한 객체의 상태 변화를 관찰하다가 변화가 있을 때마다 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴으로 일대다 객체 의존 관계를 구성하는 패턴
  * 템플릿 메서드 패턴(Template Method Pattern): 상위 클래스의 템플릿 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴
  * 전략 패턴(Strategy Pattern): 클라이언트가 전략을 생성해 전략을 실행한 컨텍스트에 주입하는 패턴

</div>
</details>


<details>
<summary style="font-size:20px">싱글톤 패턴</summary>
<div markdown="1">

* 오직 인스턴스를 하나만 만들어서 재사용하는 패턴(생성 패턴)
* 한번의 객체 생성으로 `재사용`이 가능하기 때문에 메모리 낭비를 방지하고 객체가 `전역성`을 띄기 때문에 공유가 용이
* 예시
```java
public class Singleton {

    static Singleton singletonObject;

    private Singleton() {};

    public static Singleton getInstance() {
        if (singleObject == null) {
            singletonObject = new Singleton();
        }
        return singletonObject;
    }
}
```
</div>
</details>


<details>
<summary style="font-size:20px">팩토리 메서드 패턴</summary>
<div markdown="1">

* 하위 클래스에서 객체를 생성 반환에 사용되는 메서드인 팩터리 메서드를 오버라이딩해서 객체를 반환하게 하는 패턴(생성 패턴)
* 팩토리 패턴은 클래스의 `인스턴스를 만드는 것을 서브 클래스에서 결정하는 패턴`으로 팩토리 메서드 패턴과 추상 팩토리 패턴으로 구체화되나 주로 팩토리 메서드 패턴를 사용
* 예시
```java
abstract class Coffee {

    // 팩터리 메서드
	public abstract int getPrice();

	@Override
	public String toString() {
		return "Hi this coffee is " + this.getPrice();
	}
}
```
```java
class CoffeeFactory {
	public static Coffee getCoffee(String type, int price) {
		if ("Latte".equalsIgnoreCase(type))
			return new Latte(price);
		else if ("Americano".equalsIgnoreCase(type))
			return new Americano(price);
		else {
			return new DefaultCoffee();
		}
	}
}
```
```java
class Americano extends Coffee {
	private int price;

	public Americano(int price) {
		this.price = price;
	}

	@Override
	public int getPrice() {
		return this.price;
	}
}
```
```java
class Latte extends Coffee {
	private int price;

	public Latte(int price) {
		this.price = price;
	}

	@Override
	public int getPrice() {
		return this.price;
	}
}
```
```java
public class TestApplication {
	public static void main(String[] args) {
		Coffee latte = CoffeeFactory.getCoffee("Latte", 4000);
		Coffee americano = CoffeeFactory.getCoffee("Americano", 3000);
		System.out.println("Factory latte ::" + latte);
		System.out.println("Factory americano ::" + americano);
	}
}
```
</div>
</details>

<details>
<summary style="font-size:20px">빌더 패턴</summary>
<div markdown="1">

* 생성(construction)과 표기(representation)를 분리해 복잡한 객체를 생성하는 패턴(생성 패턴)
* 복잡한 객체의 생성의 경우에 유용
* 예시
```java
public class Industry {

	private String id;
	private String code;
	private String name;
	private Area area;

	public String getCode() {
		return code;
	}

	public void setCode(String code) {
		this.code = code;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public Area getArea() {
		return area;
	}

	public void setArea(Area area) {
		if (area.isValid()) {
			this.area = area;
		} else {
			throw new IllegalArgumentException(grade);
		}
	}

	public static final class Builder {
		private String id;
		private String code;
		private String name;
		private Area area;

		public Builder() {
		}

		public static Builder industry() {
			return new Builder();
		}

		public Builder id(String id) {
			this.id = id;
			return this;
		}

		public Builder code(String code) {
			this.code = code;
			return this;
		}

		public Builder name(String name) {
			this.name = name;
			return this;
		}

		public Builder area(Area area) {
			this.area = area;
			return this;
		}

		public Industry build() {
			Industry industry = new Industry();
			industry.setId(id);
			industry.setCode(code);
			industry.setName(name);
			industry.setArea(area);
			return industry;
		}
	}
}
```
</div>
</details>

<details>
<summary style="font-size:20px">프록시 패턴</summary>
<div markdown="1">

* 대신해서 그 역할 수행하는 프록시를 통해서 메서드의 반환 값을 수정하는 게 아니라 별도 로직을 수행하는 패턴(구조 패턴)
* 예시
```java
public interface IService {
    String runSomething();
}
```
```java
public class ServiceA implements IService {
    public String runSomething() {
        return "서비스";
    }
}
```
```java
public class Proxy implements IService {
    IService service;

    public String runSomething() {
        System.out.println("호출에 대한 흐름 제어가 목적, 반환 값은 그대로");
        service = new ServiceA();
        return service.runSomething();
    }
}
```
```java
public class ClientWithProxy {
    // 프록시를 이용한 호출
    IService proxy = new Proxy();
    System.out.println(proxy.runSomething());
}
```
</div>
</details>

<details>
<summary style="font-size:20px">데코레이터 패턴</summary>
<div markdown="1">

* 원본에 장식을 더하는 데커레이터를 통해서 객체의 결합을 통해 반환 값에 장식을 덧붙이는 패턴(구조 패턴)
* 장식자의 역할은 원본에 장식을 더하는 것
* 예시
```java
public interface IService {
    String runSomething();
}
```
```java
public class ServiceA implements IService {
    public String runSomething() {
        return "서비스";
    }
}
```
```java
public class Decorator implements IService {

    IService serivce;

    public String runSomething() {
        System.out.println("호출에 대한 장식이 주목적, 반환 값에 장식을 더함");
        service = new ServiceA();
        return "정말" + service.runSomething();
    }
}
```
```java
public class ClientWithDecorator {

    public statis void mian(String[] args) {
        // 데코레이터를 이용한 호출
        IService decorator = new Decorator();
        System.out.println(decorator.runSometing());
    }
}
```

</div>
</details>

<details>
<summary style="font-size:20px">어댑터 패턴</summary>
<div markdown="1">

* 객체를 속성으로 참조해서 만드는 패턴으로 호출 당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 변환기를 통해 호출하는 패턴(구조 패턴)
* 어댑터(변환기)의 역할은 서로 다른 두 인터페이스 사이에 통신이 가능하게 하는 것
* 예시
```java
public class AdapterServiceA {

    ServiceA sa1 = new ServiceA();

    void run() {
        sa1.runA();
    }
}
```
```java
public class AdapterServiceB {

    ServiceB sb1 = new ServiceB();

    void run() {
        sb1.runB();
    }
}
```
```java
public class ClientWithAdapter {

    public static void main(String[] args){
    
        AdapterServiceA asa1 = new AdapterServiceA();
        AdapterServiceB asb1 = new AdapterServiceB();

        // 어댑터에 의해 래핑되어 동일한 메서드 명 사용
        asa1.run();
        asb1.run();
    }
}
```
</div>
</details>

<details>
<summary style="font-size:20px">템플릿 메서드 패턴</summary>
<div markdown="1">

* 상위 클래스의 템플릿 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴(행위 패턴)
* 상속을 이용해서 동일한 코드를 제외하고 코드를 추가
* 예시
```java
public abstract class Animal {
    // 템플릿 메서드
    public void playWithOwner() {
        System.out.println("귀염둥이 이리온...");
        play();
        runSomething();
        System.out.println("잘했어");
    }

    // 추상 메서드 (오버라이딩 강제)
    abstract void play();

    // 훅 메서드 (오버라이딩 선택)
    void runSomething() {
        System.out.println("꼬리 살랑 살랑~");
    }    
}
```
```java
public class Dog extends Animal {

    @Override
    void play () {
        System.out.println("멍멍");
    }

    @Override
    void runSomething() {
        System.out.println("멍멍 꼬리 살랑 살랑~");
    }
}
```
```java
public class Cat extends Animal {

    @Override
    void play () {
        System.out.println("야옹야옹");
    }

    @Override
    void runSomething() {
        System.out.println("야옹야옹 꼬리 살랑 살랑~");
    }
}
```

</div>
</details>

<details>
<summary style="font-size:20px">전략 패턴</summary>
<div markdown="1">

* 클라이언트가 전략을 생성해 전략을 실행한 컨텍스트에 주입하는 패턴(행위 패턴)
* 객체 주입을 통해서 동일한 코드를 제외하고 코드를 추가
* 전략 패턴 각 구성 요소
  * 전략 메서드를 가진 전략 객체
  * 전략 객체를 사용하는 컨텍스트
  * 전략 객체를 생성해 컨텍스트에 주입하는 클라이언트
* 예시
```java
public interface Strategy {
    public abstract void runStrategy();
}
```
```java
// 전략 객체
public class StrategyGun implements Strategy {
    @Override
    public void runStrategy() {
        System.out.println("탕탕");
    }
}
```
```java
// 전략 객체
public class StrategySword implements Strategy {
    @Override
    public void runStrategy() {
        System.out.println("챙챙");  
    }
}
```
```java
// 컨텍스트
public class Solider {
    void runContext(Strategy strategy) {
        System.out.println("전투 시작");
        strategy.runStrategy();
        System.out.println("전투 종료");
    }
}
```
```java
// 클라이언트
public class Client {
    public static void main(String[] args) {
        Strategy strategy = null;
        Solider solider = new Solider();

        // 총을 통한 전투
        strategy = new StrategyGun();
        solider.runContext(strategy);

        // 검을 통한 전투
        strategy = new StrategySword();
        solider.runContext(strategy);
    }
}
```

</div>
</details>

<details>
<summary style="font-size:20px">옵서버 패턴</summary>
<div markdown="1">

* 한 객체의 상태 변화를 관찰하다가 변화가 있을 때마다 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴으로 일대다 객체 의존 관계를 구성하는 패턴(행위 패턴)
* 예시
```java
interface Subject {
    public void register(Observer obj);
    public void unregister(Observer obj);
    public void notifyObservers();
    public Object getUpdate(Observer obj);
}
```
```java
interface Observer {
    public void update(); 
}
```
```java
class Topic implements Subject {
    private List<Observer> observers;
    private String message; 

    public Topic() {
        this.observers = new ArrayList<>();
        this.message = "";
    }

    @Override
    public void register(Observer obj) {
        if (!observers.contains(obj)) observers.add(obj); 
    }

    @Override
    public void unregister(Observer obj) {
        observers.remove(obj); 
    }

    @Override
    public void notifyObservers() {   
        this.observers.forEach(Observer::update); 
    }

    @Override
    public Object getUpdate(Observer obj) {
        return this.message;
    } 
    
    public void postMessage(String msg) {
        System.out.println("Message sended to Topic: " + msg);
        this.message = msg; 
        notifyObservers();
    }
}
```
```java
class TopicSubscriber implements Observer {
    private String name;
    private Subject topic;

    public TopicSubscriber(String name, Subject topic) {
        this.name = name;
        this.topic = topic;
    }

    @Override
    public void update() {
        String msg = (String) topic.getUpdate(this); 
        System.out.println(name + ":: got message >> " + msg); 
    } 
}
```
```java
public class TestApplication { 
    public static void main(String[] args) {
    
        Topic topic = new Topic(); 
        Observer a = new TopicSubscriber("a", topic);
        Observer b = new TopicSubscriber("b", topic);
        Observer c = new TopicSubscriber("c", topic);
        
        topic.register(a); // 옵저버 등록
        topic.register(b); // 옵저버 등록
        topic.register(c); // 옵저버 등록
   
        topic.postMessage("amumu is op champion!!"); // 상태 변화 노티
    }
}
```
</div>
</details>


<details>
<summary style="font-size:20px">MVC 패턴</summary>
<div markdown="1">

* Model, View, Controller라고 하는 컴포넌트로 분리하여 `비지니스 처리 로직`과 사용자 `인터페이스 요소`를 분리시켜 서로 영향없이 개발하기 수월

</div>
</details>
