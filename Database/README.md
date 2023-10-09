# Database

<br>

<details>
<summary style="font-size:20px">DBMS</summary>
<div markdown="1">

* 데이터베이스 관리 시스템(DataBase Management System)
* 데이터베이스의 데이터에 접근하여 사용할 수 있도록 해주는 SW
* 정의, 조작, 제어 기능 수행

|기능|설명|
|:--:|--|
|정의|DB 구조 정의(테이블, 속성)|
|조작|DB 연산 처리(수정, 삭제, 검색)|
|제어|데이터 무결성 및 일관성 유지, 접근 권한 부여, 동시성 제어|

</div>
</details>


<details>
<summary style="font-size:20px">DB를 사용하는 이유</summary>
<div markdown="1">

* `파일 시스템의 문제를 해결`하기 위해 사용
* 확장성이 좋음: 파일 시스템은 OS 종속적
* 중복 최소화, 보안성, 계속적 변화에 대한 적응: 파일 시스템은 데이터 중복, 비일관성, 검색 등의 문제 존재
* DB는 `원자적 갱신`, `동시성 제어`, `데이터 보호`, `백업 및 회복` 등의 여러 데이터 관리 기능을 통해 데이터를 편하게 관리할 수 있음
* 일반적으로 서버는 Scale-Out 구조로 설계되고 DB는 Scale-Up 구조로 설계되기 때문에 DB의 부담을 줄이고 애플리케이션에서 최대한 많은 처리를 하는 것이 권장

</div>
</details>


<details>
<summary style="font-size:20px">관계형 데이터베이스(SQL)와 비관계형 데이터베이스(NoSQL)의 차이</summary>
<div markdown="1">

#### 관계형 데이터베이스
* 엄격한 스키마 아래 행과 열로 구성된 `테이블`들의 관계로 데이터 저장
* SQL을 사용해서 `속성(열)에 맞는 자료형`으로 데이터를 삽입
* ACID
* 데이터 무결성 보장, 데이터를 중복 없이 저장
* 기존의 스키마 수정 어려움, 빅데이터 처리에 비효율적
* 데이터가 자주 변경되거나 명확한 스키마가 있는 경우 사용
* `Oracle`, `MySQL`

#### 비관계형 데이터베이스
* 스키마가 없거나 느슨한 스키마로 데이터 저장 (`key-value`, `Document` 등)
* 데이터 질의 API 다양함
* Eventual Consistency
* 유연하고 확장성 좋음
* 데이터를 자주 변경하지 않고 정확한 데이터 구조를 알 수 없는 경우 사용
* 키-값: `Redis`, 문서형(JSON, XML): `MongoDB`

</div>
</details>


<details>
<summary style="font-size:20px">NoSQL(Not Only SQL)</summary>
<div markdown="1">

* 관계형 데이터베이스가 아닌 다른 형태
로 데이터를 저장하는 기술
* 특징
  * 반정형(명확한 스키마 없음, 일정 수준의 자유도 허용, NoSQL/JSON 형태의 데이터)/비정형(스키마 없음, 비디오/오디오 등의 멀티미디어 데이터) 데이터에 적합
  * ACID 대신 Eventual Consistency: Consistency를 조금 타협하고 꼭 실제 최신은 아닐 수 있지만 `업데이트가 되기 전까지는` 가지고 있는 최신의 데이터를 반환함을 의미 -> 분산형의 특성상 일관성 유지가 어려움
  * 대용량/분산형 데이터 저장에 유리
  * 특정 도메인의 문제 해결에 좋음: Key-value, Graph 등 자료 형태가 다양해 특정 분야에서 고성능(소셜 네트워크: 인간 관계는 그래프)
  * 데이터를 질의하는 API가 다양
  * 분산형 컴퓨터에 최적화, 확장성 좋음: 머신의 수를 늘리는 `수평적 확장`
  * NoSQL은 SQL보다 제품 지원이 어려움
  * 인력 운영 비용이 더 비쌈: 표준화 부족, 질의 언어 다양
* 종류
  * Column-based: 열 별로 연속적으로 저장, 기존 SQL은 테이블에 행 단위로 순차적으로 저장 -> 레코드의 특정 부분만 수정할 때, 필요한 열의 데이터만 로드하면 되서 IO 작업 감소, 한 열에 들어가는 데이터 형식에 일관성이 있어 DB 내의 한 블록은 동일한 유형의 데이터를 보유 -> 데이터의 유형에 맞는 압축 인코딩 가능, 디스크 공간 절약 및 성능 향상 가능
  * Document-oriented: JSON 객체로 문서(레코드)를 구성, 다양항 구조로 테이블 구성 가능, `MongoDB`
  * Key-Value: 연관 배열을 데이터 모델로 이용, Key는 한 Collection에 한 번만 등장 가능
  * Graph

</div>
</details>


<details>
<summary style="font-size:20px">테이블</summary>
<div markdown="1">

#### 테이블
* 행과 열로 이루어진 데이터의 집합

#### 행
* 테이블을 구성하는 데이터 셋으로 `튜플`이나 `레코드`라고 불림
* 한 객체에 대한 정보를 가짐

#### 열
* 테이블을 구성하는 데이터 셋으로 `속성`이라고 불림

#### 도메인
* 데이터베이스 필드에 채워질 수 있는 `값들의 집합`

</div>
</details>


<details>
<summary style="font-size:20px">뷰</summary>
<div markdown="1">

* 하나 이상의 테이블에서 유도된, 메모리에 물리적으로 존재하지 않는 `가상 테이블`
* 특정 사용자로부터 특정 속성을 `숨기는` 기능으로 뷰를 정의하여 그 뷰를 테이블처럼 사용
* 인덱스를 가질 수 없고, 뷰의 정의를 변경할 수 없음
* 테이블의 기본키를 포함하여 정의 시, 삽입/삭제/갱신 가능

</div>
</details>


<details>
<summary style="font-size:20px">조인</summary>
<div markdown="1">

* 두 개 이상의 테이블을 `연결하여 데이터를 검색`하는 방법
* 적어도 하나의 칼럼을 서로 공유하고 있어야 함

</div>
</details>


<details>
<summary style="font-size:20px">스키마와 테이블의 차이</summary>
<div markdown="1">

#### 스키마
* 데이터베이스의 데이터 구조에 대한 공식적인 설명 -> 테이블, 열, 데이터 유형, 인덱스 등의 정의를 포함

#### 테이블
* `행과 열로 구성된 데이터 집합`

</div>
</details>


<details>
<summary style="font-size:20px">키</summary>
<div markdown="1">

<img src="https://user-images.githubusercontent.com/38900338/139516864-ce72fa77-10dc-465c-9e6d-959db391f61d.png" width="300px">

#### 정의
* 검색, 정렬 시 튜플을 구분하는 기준이 되는 속성 (Attribute)
* 무조건 레지스터에 한번에 들어갈 수 있는 INT, LONG, DATETIME 속성을 사용하는 것이 권장
* 용어
  * 유일성: 키로 튜플을 유일하게 식별할 수 있음
  * 최소성: 튜플을 구분하는데 꼭 필요한 속성들로만 구성

#### 슈퍼 키
* 유일성을 만족, 최소성은 만족하지 않는 속성들의 집합

#### 후보 키
* `유일성`과 `최소성`을 만족하는 속성들의 집합
* 기본 키로 사용할 수 있는 속성들
* 모든 테이블은 하나 이상의 후보 키를 가짐

#### 기본 키
* 후보 키 중에서 선택한 Main Key (주 키)
* `유일성`과 `최소성` 만족
* 중복 값과 NULL 값 불가 (`개체 무결성`)
* 데이터 저장 시에 기본 키(PK)가 유사한 레코드들끼리 묶어서 저장

#### 대체 키 (보조 키)
* 후보 키가 두개 이상일 때, 기본 키를 제외한 나머지 후보 키
 
#### 복합 키
* 두개 이상의 컬럼을 묶어서 하나의 기본 키로 지정하는 것
* 기본 키는 하나의 테이블에 하나만 존재할 수 있으며 기본 키는 하나 이상의 컬럼으로 구성

#### 외래 키
* 한 테이블의 키 중에서 다른 테이블의 튜플을 식별할 수 있는 키
* 참조되는 릴레이션의 `기본 키`와 대응되어 릴레이션 간에 `참조 관계`를 표현하는 키
* 사용 이유: 테이블을 연결, 중복 방지, 무결성 유지
  * 예시: 물건 구매시 같은 사람이 여러 물건을 구매하면 사람에 대한 데이터가 중복 -> 사람과 물건 구매로 테이블을 분리해 중복 제거
 

</div>
</details>


<details>
<summary style="font-size:20px">무결성 제약조건</summary>
<div markdown="1">

* 무결성: 데이터의 정확성, 일관성
  * 데이터에 중복/누락이 없음
* 개체 무결성: 주키는 null, 중복 값을 가질 수 없음
* 참조 무결성: 외래키는 null이거나 참조 릴레이션의 기본키 값과 동일해야 함

</div>
</details>

<details>
<summary style="font-size:20px">관계</summary>
<div markdown="1">

#### 관계
* 테이블 간의 상호작용을 기반으로 설정되는 여러 테이블 간의 논리적 연결
* 주로 외래키(foreign key)를 통해 위 관계를 명시

#### 1:1 관계
* 하나의 레코드가 다른 테이블의 레코드 한 개와 연결된 경우
* 다른 테이블의 레코드 한 개에만 연결돼야 하므로 자주 사용되진 않음

#### 1:N 관계
* 하나의 레코드가 다른 테이블의 서로 다른 여러 개의 레코드와 연결된 경우
* 가장 많이 사용되는 관계

#### N:M 관계
* 관계를 가진 양쪽 테이블에서 1:N 관계를 가진 경우
* 1:N, 1:M 이라는 관계를 갖는 테이블 두개로 니눠서 설정
 
#### 관계 표기 방법(ERD)
![image](https://github.com/yoonje/developer-interview/assets/38535571/503faa2a-41c2-4a0c-a456-ee693c36cfe1)

</div>
</details>


<details>
<summary style="font-size:20px">트랜잭션 정의</summary>
<div markdown="1">

* 데이터베이스의 상태를 변화시키는 하나의 `원자적인/논리적인 작업 단위`
* 트랜잭션은 Exclusive Lock 을 발생시키에 Lock과 유사한 기능을 하지만 Lock은 동일한 자원을 요청할 경우 한 시점에는 하나의 커넥션만 변경하는데에 반해 트랜잭션은 논리적인 작업의 쿼리의 개수와 관계없이 논리적인 작업 셋 자체가 `100% 적용되거나 아무것도 적용되지 않아야 함을 보장`
* 주의사항
  * 최소한의 코드에 적용하는 것이 좋음
  * DB 커넥션의 수는 제한적 -> 커넥션이 부족해 대기할 수 있음
  * 트랜잭션 범위를 작게 나눠서 적용해야 DB에 오버헤드가 줄음

</div>
</details>


<details>
<summary style="font-size:20px">트랜잭션 ACID</summary>
<div markdown="1">

* 데이터의 유효성을 보장하기 위한 트랜잭션의 특징
* `Atomicity(원자성)`: `모든 작업이 반영되거나 모두 롤백되는 특성`입니다.
* `Consistency(일관성)`: 데이터는 `미리 정의된 규칙에서만 수정이 가능한 특성`을 의미합니다.
  * 도메인, 외래키 관게 유지
* `Isolation(고립성)`: 두 개 이상의 트랜잭션이 동시에 발생할 때, 서로의 연산에 영향을 줄 수 없음
  * Lock으로 보장
* `Durability(영구성)`: 한번 반영(커밋)된 트랜젝션의 내용은 `영원히 적용`되는 특성을 의미합니다.

</div>
</details>


<details>
<summary style="font-size:20px">트랜잭션 격리수준</summary>
<div markdown="1">

#### 트랜잭션 격리수준
* 동시에 여러 트랜잭션이 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경/조회하는 데이터에 대한 접근 권한 수준을 결정하는 것
* 일관성 없는 데이터를 허용하도록 하는 수준
* ACID를 희생하고 동시성을 높이는 방법
  * 레벨이 낮을수록 동시성은 높음, 무결성은 하락

#### 필요성
* 락으로 모든 트랜잭션이 순서대로 처리하도록 하면 DB의 성능이 떨어짐

#### 종류
##### Read Uncommitted (레벨 0)
* Select를 수행할 때 해당 데이터에 Shared Lock이 걸리지 않는 레벨
* Commit되지 않은 데이터를 읽을 수 있음
* 일관성 유지가 거의 불가능
##### Read Committed (레벨 1)
* SELECT를 수행하는 동안 해당 데이터에 Shared Lock이 걸리는 레벨
* 커밋된 내용만 접근 가능
##### Repeatable Read (레벨 2)
* 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 레벨
  * 트랜잭션 범위 내에서 조회한 데이터는 항상 동일
* 트랜잭션에 진입하기 이전에 커밋된 내용만 접근 가능
* 데이터 추가는 허용, 변경/삭제는 허용하지 않음
##### Serializable (레벨 3)
* 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 레벨
  * 트랜잭션 범위 내에서 조회한 데이터는 항상 동일
* 완벽한 읽기 일관성을 제공함
* 데이터의 추가/변경/삭제 불가능

#### 참고: Lock
* 공유락(Shared Lock): `Select`에 의해 설정, 데이터를 다른 트랜잭션이 읽기 허용, 쓰기 불허용
* 베타락(Exclusive Lock): `INSERT`, `UPDATE`, `DELETE`에 의해 설정, 데이터를 다른 트랜잭션이 읽기, 쓰기 모두 불허용
</div>
</details>


<details>
<summary style="font-size:20px">인덱스 정의</summary>
<div markdown="1">

* `추가적인 쓰기와 저장 공간` 사용을 통해 `검색 속도 향상`을 위해 사용하는 자료구조
* 칼럼의 `값`과 해당 레코드가 저장된 `주소`를 `키와 값의 쌍`으로 인덱스 정의

</div>
</details>

<details>
<summary style="font-size:20px">인덱스 장단점</summary>
<div markdown="1">

#### 장점
* 검색 속도 향상

#### 단점
* 데이터의 추가, 삭제, 수정의 경우 인덱스도 변경해야 하여 성능이 오히려 저하될 수 있음 (정렬 상태를 계속 유지해야 함)
* 추가적인 저장 공간 필요 및 성능 저하
* 복합 키나 복합 인덱스의 경우 컬럼 순서가 맞지 않아서 인덱스를 타지 못하거나 칼럼의 값에 따라 인덱스의 위치가 변화될 수 있어 문제를 유발할 수 있음

</div>
</details>

<details>
<summary style="font-size:20px">복합 인덱스 효과적으로 달기</summary>
<div markdown="1">

* 여러 필드를 기반으로 조회할 때 복합 인덱스를 생성
* 생성 순서에 따라 성능이 달라지는데 순서는 `같음`, `정렬`, `부호(> or <)`, `카디널리티` 순으로 생성해야함

</div>
</details>

<details>
<summary style="font-size:20px">인덱스 자료구조: 트리</summary>
<div markdown="1">

#### B 트리

![tree](https://user-images.githubusercontent.com/38900338/105454677-9bf88400-5cc5-11eb-993e-fb6f7b9675a1.png)
* 이진 트리를 확장해서, 더 많은 수의 자식을 가질 수 있게 일반화 시킨 자료구조
* 균형 트리: 루트 ~ 리프의 거리가 일정한 트리
* Branch 노드: Key와 Data 저장

#### B+ 트리

![Bplustree](https://user-images.githubusercontent.com/38900338/105454222-d9104680-5cc4-11eb-96e9-31e46c0bf2aa.png)

* B 트리를 확장해서, 데이터의 빠른 접근을 위한 인덱스 역할만 하는 비단말 노드(not Leaf)를 추가한 자료구조
* Branch 노드: Key만 저장, Leaf 노드: Key와 Data 저장 + Linked List로 연결(부등호를 사용한 순차 검색에 유용)
* B 트리보다 풀 스캔 빠름
* Leaf 노드를 제외하면 데이터를 저장하지 않아 더 많은 Key를 저장할 수 있음 -> 트리의 높이가 낮아져 Cache Hit 향상 가능

</div>
</details>


<details>
<summary style="font-size:20px">인덱스 자료구조: 해시 테이블</summary>
<div markdown="1">

* 칼럼의 값으로 생성된 해시를 기반으로 인덱스 구현
* O(1)로 매우 빠름
* `부등호` 연산 때문에 성능이 떨어짐
* `>=, Between, like, order by` 등은 불가능하지만 `==, in, is null` 등에서의 성능은 좋음

</div>
</details>

<details>
<summary style="font-size:20px">Clustered Index vs Non Clustered Index</summary>
<div markdown="1">

#### Clustered Index
* 인덱스로 지정한 컬럼을 기준으로 데이터를 `물리적으로 정렬`하여 사용하는 인덱스
* 테이블 구조에 영향을 미치는 인덱스
* 한 테이블에 `1개` 생성 가능
* 기본키는 클러스터형 인덱스
* 비클러스터형 인덱스보다 `검색 속도는 빠르지만`, 데이터의 입력/수정/삭제는 느림
* 일반적으로 PK를 Clustered Index라고 부름

#### Non-Clustered Index
* 데이터를 물리적으로 재배열 하지 않고 인덱스 페이지만 정렬하여 사용하는 인덱스
* 한 테이블에 `여러 개` 생성 가능
* 클러스터형 인덱스보다 `검색 속도는 느리지만`, 데이터의 입력/수정/삭제는 빠름
* 일반적으로 생성하는 인덱스는 모두 Non-Clustered Index라고 부름

</div>
</details>


<details>
<summary style="font-size:20px">정규화</summary>
<div markdown="1">

### 정의
* 데이터의 중복을 제거해 데이터 무결성을 유지하는 것
* 속성 간의 종속성으로 인한 `이상현상`을 `테이블을 분해`해 해결하는 것
  * 이상현상 (Anomaly): 테이블 내의 데이터가 중복되어 테이블을 조작할 때 발생하는 데이터 불일치
* 테이블의 속성들이 상호 종속적인 관계를 갖는 특성을 이용하여 테이블을 `무손실 분해` 하는 과정
  * 무손실 분해: 하나의 릴레이션을 분해하고 다시 조인연산을 했을 때 데이터 손실이 없는 것, 분해된 테이블이 표현하는 정보는 분해되기 전의 정보를 모두 포함

### 목적
* 데이터 `중복 최소화`, 불필요한 데이터 최소화
* `무결성` 유지, `이상 현상` 방지
* 테이블의 구성을 논리적/직관적으로 수정

### 종류

#### 제 1 정규화 (1NF)
* 테이블 컬럼이 `원자 값`을 갖도록 분해
* 모든 필드가 원자 값으로만 되어 있어야 함

#### 제 2 정규화 (2NF) 
* 테이블의 모든 컬럼이 `완전 함수 종속`을 만족하도록 분해 
  * 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속
  * 기본키를 구성하는 속성 중 일부에 종속되지 않음
* 테이블에서 기본키가 복합키(키1, 키2)로 묶여있을 때, 두 키 중 하나의 키만으로 다른 컬럼을 결정지을 수 있으면 안됨
  * 기본키의 부분집합이 결정자가 되면 안됨

##### 함수적 종속
* X -> Y: X = 결정자, Y = 종속자 (Y는 X에 함수적 종속, X/Y는 속성의 부분집합)
* X의 값을 알면 Y를 식별할 수 있고, X의 값에 Y의 값이 달라짐

#### 제 3 정규화 (3NF)
* 기본키가 아닌 모든 컬럼이 기본키에 `비이행적 종속(직접 종속)`하도록 분해
* 기본키가 아닌 컬럼이 다른 컬럼을 결정할 수 없음

##### 이행적 함수 종속
* X, Y, Z 속성에 대해 X->Y 이고 Y->Z 이면 X->Z

#### BCNF (Boyce and Codd Normal Form)
* 모든 결정자가 `후보키`가 되도록 분해
* 함수 종속성 X->Y일 때, 모든 결정자 X가 후보키
* 일반 튜플이 후보키를 결정지으면 안됨

</div>
</details>
 
 <details>
<summary style="font-size:20px">반정규화</summary>
<div markdown="1">

### 정의
* 데이터베이스의 성능 향상을 위하여, 데이터 중복을 허용하고 `조인을 줄이는 방법`
 
### 목적
* 정규화에 충실하여 종속성, 활용성은 향상 되었지만 수행 속도가 느려지는 것을 막음
* 조회 속도를 향상시키지만, 데이터 모델의 유연성은 낮아짐
* Join 이 3번이상 발생한다면, 이건 시스템 장애를 일으킬 수 있는 쿼리일 수 있으므로 반정규화를 고려

</div>
</details>


<details>
<summary style="font-size:20px">파티셔닝</summary>
<div markdown="1">

### 정의
* `하나의 DB`에서 데이터를 물리적으로 분할하는 것

### 장단점
* 큰 테이블을 제거하여 관리가 쉬움
* DML 성능 향상: 접근하는 데이터 수 감소, 인덱스 크기 감소
* 조인 비용 증가
* 테이블과 인덱스를 별도로 파티셔닝 할 수 없고 함께 파티셔닝 해야 함

### 분할 방법
#### 수평 분할 (Horizontal Partitioning)
* `하나의 DB`안에 `스키마가 같은` 데이터를 두 개 이상의 테이블에 분할하여 저장
* 예시
  * 주민 테이블 -> a동 테이블, b동 테이블로 분리

#### 수직 분할 (Vertical Partitioning)
* 테이블을 열을 기준으로 분리
* 정규화된 테이블을 분리하는 것

</div>
</details>

<details>
<summary style="font-size:20px">샤딩</summary>
<div markdown="1">

* `여러 DB`에 데이터를 물리적으로 `수평 분할 방식(Horizontal Partitioning)`으로 분산 저장/조회하는 것
* `트래픽 분산` 목적으로 사용: 데이터베이스에 데이터 증가 -> 용량 이슈, CRUD 성능 저하
* 쿼리 성능 향상
* 복잡도 증가, Hotspot이 생기면 샤딩 무의미 해짐
* 두 개 이상의 샤드에서 `JOIN 불가`, 일관성과 복제에서 불리
* 예시
  * 주민 테이블 -> a동 테이블은 A DB, b동 테이블은 B DB에 저장

</div>
</details>

<details>
<summary style="font-size:20px">레플리카</summary>
<div markdown="1">

* `동일한 데이터를 Master/Slave DB로 나누어 저장`하는 것 (이중화)
* 목적
  * 읽기(Slave)와 쓰기(Master) DB를 분리하여 성능을 향상시킴
  * 많은 Slave를 생성해 읽기 성능을 향상시킬 수 있음

</div>
</details>


<details>
<summary style="font-size:20px">클러스터링과 리플리케이션의 차이</summary>
<div markdown="1">

#### 클러스터링
* DB를 `수평` 구조로 다중화
* Fail Over 시스템 구축을 위해 사용
* 동기 방식으로 동기화 -> 항상 일관성 유지, 동기화 시간 소요
* 1개 DB가 고장나도 시스템 계속 운영 가능
* Active - Active, Active - Standby

#### 리플리케이션
* DB를 `수직` 구조인 Master와 Slave로 다중화
* Master는 쓰기, Slave는 읽기만 수행 -> 부하 분산
* 비동기 방식으로 동기화 -> 시간 지연 거의 없음
* Master 오류시 복구 어려움

</div>
</details>


<details>
<summary style="font-size:20px">SQL Injection</summary>
<div markdown="1">

* 해커에 의해 조작된 SQL 쿼리문이 데이터베이스에 그대로 전달되어 비정상적인 명령을 실행시키는 공격 기법
* 입력값 검증
* Prepared Statement 사용: 쿼리에 대한 컴파일을 먼저 수행하고, 입력값을 나중에 넣는 방식
  * 바인딩 변수: 삽입되는 데이터는 문자열로 취급되어 SQL의 역할을 하지못함

</div>
</details>


<details>
<summary style="font-size:20px">힌트(Hint)</summary>
<div markdown="1">

* SQL을 `튜닝`하기 위한 지시 구문, 개발자가 직접 최적의 실행 계획을 제공하는 것

</div>
</details>


<details>
<summary style="font-size:20px">시퀀스</summary>
<div markdown="1">

* `순차적으로 증가하는 숫자를 생성`하는 객체
* `기본 키`와 같은 유일한 숫자를 자동으로 생성하는 것
* 캐시에 있어 속도 빠름, 중복 방지에 사용

</div>
</details>


<details>
<summary style="font-size:20px">트리거</summary>
<div markdown="1">

* DML이 수행되었을 때, 자동으로 실행되게 정의한 프로시저
* DML(INSERT, UPDATE, DELETE)에 의한 데이터 상태관리 자동화
* 데이터 무결성 강화, 업무 처리 자동화

</div>
</details>



<details>
<summary style="font-size:20px">커넥션 풀</summary>
<div markdown="1">

* `미리 일정 수의 Connection을 만들어 pool에 보관 -> 사용자의 요청이 발생하면 연결을 해주고 연결 종료 시 pool에 다시 반환하여 보관하는 것`
* 사용자의 요청에 따라 Connection 을 생성하다 보면 많은 수의 연결이 발생했을 때 서버에 과부하가 걸리게 되므로 이러한 상황을 방지하기 위해 사용
* 커넥션 풀을 사용하면 커넥션을 생성하고 닫는 시간이 소모되지 않기 때문에 그만큼 어플리케이션의 `실행 속도가 빨라짐`
* 한 번에 생성될 수 있는 커넥션 수를 제어하기 때문에 동시 접속자 수가 몰려도 웹 어플리케이션이 쉽게 다운되지 않음

</div>
</details>

<details>
<summary style="font-size:20px">Redis와 MongoDB</summary>
<div markdown="1">

* Redis는 NoSQL 방식을 사용하는 인메모리 데이터베이스로 `Key-Value` 형식으로 데이터를 저장하며 주로 캐쉬로 사용
* MongoDB는 NOSQL 방식을 사용하는 데이터베이스로 JSON같은 구조의 `Document` 형식으로 데이터를 저장하고 문서에 대한 ID를 키로 표현

</div>
</details>

<details>
<summary style="font-size:20px">Redis의 데이터 휘발을 막기 위한 방법</summary>
<div markdown="1">

* `snapshot` 기능을 통해 디스크에 백업하거나 `AOF(Append Only File)` 기능을 통해 `명령 쿼리를 저장`해두고 서버가 셧다운 되면 재실행
* snapshot: 특정 시점의 백업 및 복구에 유리, 빠르게 복구 가능, 서버가 다운되면 스냅샷 사이에 변경된 데이터 유실
* AOF: 모든 write/update 연산 자체를 모두 log 파일로 기록, 서버가 실행되면 순차적으로 연산을 재실행하여 데이터를 복구, write 속도 빠름, 데이터 유실X, 데이터 사용량이 큼, 서버 restart 시 속도 느림

</div>
</details>

<details>
<summary style="font-size:20px">PostgresSQL과 ElasticSearch의 차이점</summary>
<div markdown="1">

* PostgresSQL은 관계형 데이터베이스이고 ElasticSearch는 검색 및 분석엔진
* ES는 데이터 모델을 JSON으로 하고 있어 NoSQL처럼 사용할 수 있음

</div>
</details>
