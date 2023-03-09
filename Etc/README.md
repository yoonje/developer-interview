# 기타 

<br>


<details>
<summary style="font-size:20px">함수형 프로그래밍</summary>
<div markdown="1">

* 부수 효과가 없는 순수함수로 프로그램을 만드는 것
  * 순수함수: 데이터 값을 변경시키지 않음, 객체의 필드를 설정하지 않음
* 1급 객체와 데이터 불변성 그리고 고차함수, 합성함수, 순수함수와 같은 다양한 함수 개념으로 구성

#### 참고
* 명령형 프로그래밍: 무엇(What)보다는 `어떻게(How)`할 건지를 설명하는 방식
  * 절차지향 프로그래밍: 수행되어야 할 순차적인 처리 과정을 포함하는 방식 (C, C++)
  * 객체지향 프로그래밍: 객체들의 집합으로 프로그램의 상호작용을 표현 (C++, Java, C#)
* 선언형 프로그래밍: 어떻게(How)보다는 `무엇(What)`을 할 건지를 설명하는 방식
  * 함수형 프로그래밍: 순수 함수를 조합해 소프트웨어를 만드는 방식 (클로저, 하스켈, 리스프)

</div>
</details>


<details>
<summary style="font-size:20px">포인터</summary>
<div markdown="1">

  * 메모리 상의 주소를 저장하는 공간

</div>
</details>


<details>
<summary style="font-size:20px">얕은 복사와 깊은 복사</summary>
<div markdown="1">

#### 얕은 복사
* `주소 값`을 복사
* 참조하고 있는 실제 값은 같음 -> 복사한 객체의 값을 변경하면 기존 객체도 변경
* 자바에서 객체는 Heap, 객체의 주소는 Stack에 저장 -> Stack에 Heap의 주소를 참조하는 공간이 1개 더 생성

#### 깊은 복사
* `실제 값`을 새로운 메모리 공간에 복사
* 자바에서 객체는 Heap, 객체의 주소는 Stack에 저장 -> Heap에 객체가 1개 더 생성, Stack에 Heap의 주소를 참조하는 공간 생성

  <details>
  <summary style="font-size:20px">참고: 파이썬</summary>
  <div markdown="1">

    * 단순 객체 복사
    ```python
    # mutable 객체 (변경가능 객체(리스트 등))
    a = [1, 2, 3, 4]
    b = a     # copy
    print(b)    # [1, 2, 3, 4]
    b[2] = 100   # b의 item 변경
    print(b)    # [1, 2, 100, 4]
    print(a)    # [1, 2, 100, 4], a의 item도 수정됨!!
    
    # immutable 객체
    a = 10
    b = a
    print(b)    # 10 출력
    b = "abc"
    print(b)    # abc 출력
    print(a)    # 10 출력
    ```
    
    * 얕은 복사
      * 객체를 복사할 때, 해당 객체만 복사하여 새 객체를 생성한다.
      * 복사된 객체의 인스턴스 변수는 원본 객체의 인스턴스 변수와 같은 메모리 주소를 참조한다.
      * 따라서, 해당 메모리 주소의 값이 변경되면 원본 객체 및 복사 객체의 인스턴스 변수 값은 같이 변경된다.
    ```python
    import copy
    
    # immutable
    a = [1, [1, 2, 3]]
    b = copy.copy(a)    # shallow copy 발생
    print(b)    # [1, [1, 2, 3]] 출력
    b[0] = 100  # 숫자
    print(b)    # [100, [1, 2, 3]] 출력,
    print(a)    # [1, [1, 2, 3]] 출력, shallow copy 가 발생해 복사된 리스트는 별도의 객체이므로 item을 수정하면 복사본만 수정된다. (immutable 객체의 경우
    
    # mutable
    c = copy.copy(a)
    c[1].append(4)    # 리스트의 두번째 item(내부리스트)에 4를 추가 c[1]=[1,2,3,4] : list (mutable)
    print(c)    # [1, [1, 2, 3, 4]] 출력
    print(a)    # [1, [1, 2, 3, 4]] 출력, a가 c와 똑같이 수정된 이유는 리스트의 item 내부의 객체는 동일한 객체이므로 mutable한 리스트를 수정할때는 둘다 값이 변경됨
    ```
      
    * 깊은 복사
      * 복사본의 값이 mutable한 객체일때, 이를 변경했을 시, 원본의 값도 변경되는 현상을 해결
        * 객체를 복사 할 때, 해당 객체와 인스턴스 변수까지 복사하는 방식
        * 전부를 복사하여 새 주소에 담기 때문에 참조를 공유하지 않는다.
    ```python
    import copy
    
    a = [1, [1, 2, 3]]
    b = copy.deepcopy(a)    # deep copy 실행 
    print(b)    # [1, [1, 2, 3]] 출력
    b[0] = 100 # immutable
    b[1].append(4) # mutable
    print(b)    # [100, [1, 2, 3, 4]] 출력
    print(a)    # [1, [1, 2, 3]] 출력
    ```
  </div>
  </details>

</div>
</details>


<details>
<summary style="font-size:20px">TDD (Test Driven Development)</summary>
<div markdown="1">

* 테스트 주도 개발
* `테스트 코드를 작성 한 후 그것을 통과하는 실행 코드를 작성`하는 매우 짧은 Cycle로 개발
* 디버깅이 쉬워지고 코드의 신뢰성이 높아짐
* 작성하는 코드의 길이가 길어지는 단점이 있음

</div>
</details>


<details>
<summary style="font-size:20px">DDD (Domain Driven Design)</summary>
<div markdown="1">

* 도메인 중심 설계 방법, 도메인이 상호작용 하도록 설계하는 것
* 도메인은 각각 분리되어 있어 MSA에 용이한 설계 가능
* 문맥에 따라 객체의 역할이 바뀔 수 있음: 같은 객체가 존재할 수 있음
* 예) 구매 도메인, 판매 도메인

</div>
</details>


<details>
<summary style="font-size:20px">크롬 탭은 프로세스인지 스레드인지</summary>
<div markdown="1">

* 크롬은 탭마다 PID를 가지고 있는 Process
* 각 Tab마다 랜더링 정보나 기타 데이터를 따로 관리, 그로 인해 메모리를 많이 잡아먹기도 하지만 하나의 Tab에 오류가 생겼다고 모든 Tab에 영향을 끼치진 않는 장점이 존재

</div>
</details>


<details>
<summary style="font-size:20px">프레임워크와 라이브러리의 차이</summary>
<div markdown="1">

* 실행 흐름을 제어하는 권한이 어디에 있는 가의 차이

#### 프레임워크
* 흐름을 자체적으로 제어
* IoC가 적용되는 것

#### 라이브러리
* 흐름 제어가 필요할 때, 사용자가 필요한 상황에 가져다 쓸 수 있는 것


</div>
</details>



<details>
<summary style="font-size:20px">Git에서 merge와 rebase의 차이</summary>
<div markdown="1">

* git merge를 하면 브랜치의 커밋 로그는 사라지고 `병합하는 커밋 로그가 master에 head에 추가`
* git rebase를 하면 브랜치를 base로 master `커밋을 재정렬하여 브랜치의 커밋 하나 하나가 master에 정리되어 추가`

</div>
</details>


<details>
<summary style="font-size:20px">메시지 큐 (Message Queue)</summary>
<div markdown="1">

* Queue 자료구조를 이용해 데이터(메시지)를 관리하는 시스템
* 비동기 통신으로 메시지를 빠르게 교환
* Producer가 메시지를 큐에 넣으면 Consumer가 메시지를 가져와 처리
* 예) Kafka, Rabbit MQ, AMPQ 

</div>
</details>
