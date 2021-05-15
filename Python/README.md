# Python

## Table of Content
- [Generator와 사용 시의 장점](#generator와-사용-시의-장점)
- [Decorator와 사용 시의 장점](#decorator와-사용-시의-장점)
- [Python Garbage Collection 동작 방식](#python-garbage-collection-동작-방식)
- [GIL과 GIL을 보완하는 방법](#gil과-gil을-보완하는-방법)
- [Duck Typing](#duck-typing)

## Generator와 사용 시의 장점
* `Iterator를 생성해주는 루틴`으로 `yield` 키워드를 통해서 만드는데, Generator는 한번에 모든 데이터를 메모리에 적재할 필요가 없어서 메모리 효율이 높고 계산 결과가 필요할 때 수행되므로 수행 시간을 꼭 필요한 시간까지 늦츨 수 있음

## Decorator와 사용 시의 장점
* 기존의 코드에 여러 가지 기능을 추가하는 파이썬 구문으로 데코레이터를 함수나 클래스로 정의하고 수행하고자 하는 함수에 `@` 키워드를 통해서 삽입하여 실행시켜 생산성을 극대화할 수 있음

## Python Garbage Collection 동작 방식
* 각각의 객체마다 `reference count`를 갖고 있고 몇 곳에서 객체를 참조하는지를 나타내는데 인터프리터가 계속 이를 확인하다가 이 count가 0이 되는 경우 그 객체를 삭제

## GIL과 GIL을 보완하는 방법
* 파이썬은 하나의 스레드만이 인터프리터의 제어권을 가질 수 있는 개념인 GIL(Global Interpreter Lock)은 멀티 코어 환경에서도 어느 시점에서나 1개의 스레드만 실행될 수 있기 때문에 `threading`이 아닌 `multiprocessing` 모듈을 통해 스레드 단위가 아닌 프로세스 별로 인터프리터 락을 잡아 보완해야함

## Duck Typing
* 동적 타입을 가지는 프로그래밍 언어에서 많이 사용되는 개념으로, 객체의 실제 타입보다는 객체의 변수와 메소드가 그 객체의 적합성을 결정하는 것을 의미
