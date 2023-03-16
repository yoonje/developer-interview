# Algorithm

<br>

<details>
<summary style="font-size:20px">시간 복잡도와 공간 복잡도</summary>
<div markdown="1">

#### 표기법

* 주로 `빅오 표기법`으로 표현

#### 시간 복잡도
* 알고리즘의 `수행 시간`을 분석하는 방법

#### 공간 복잡도
* 알고리즘 수행에 필요한 `메모리 양`을 분석하는 방법

</div>
</details>


<details>
<summary style="font-size:20px">정렬 알고리즘에서의 Stable</summary>
<div markdown="1">

* 정렬 기준으로 봤을 때, `값이 동일한 Element가 있어도 정렬 전의 순서와 정렬 후의 순서가 동일함을 보장`하는 것

</div>
</details>


<details>
<summary style="font-size:20px">정렬 알고리즘의 가짓수가 많은 이유</summary>
<div markdown="1">

* `공간 복잡도`에 따라 사용해야할 알고리즘이 다름 -> Merge Sort의 공간 복잡도는 Selection Sort와 Insertion Sort에 비해 큼
* `안정 정렬`이냐 `불안정 정렬`이냐에 따라 사용해야 할 때가 다름

</div>
</details>


<details>
<summary style="font-size:20px">Selection Sort</summary>
<div markdown="1">

* 최선, 평균, 최악: O(n^2) 
* `불안정 정렬 알고리즘`
* 가장 작은 값을 가지는 데이터를 찾아서 가장 작은 값을 앞에서부터 채워 나가면서 정렬하는 방식으로 동작
* 1번의 순환마다 맨 앞의 값이 고정
* 정렬을 위해 비교하는 횟수는 많으나, 교환 횟수는 적음 -> 역순으로 정렬되어 있는 것과 같이 많은 교환이 필요한 상태에서 효율적으로 사용 가능
 
  <details>
  <summary style="font-size:20px">코드</summary>
  <div markdown="1">

    ```java
    public static void selectionSort() {
        for (int i = 0; i < array.length-1; ++i) {
            for (int j = i+1; j < array.length; ++j) {
                if (array[i] > array[j]) {
                    int tmp = array[i];
                    array[i] = array[j];
                    array[j] = tmp;
                }
            }
        }
    }
    ```

</div>
</details>

</div>
</details>


<details>
<summary style="font-size:20px">Bubble Sort</summary>
<div markdown="1">

* 최선, 평균, 최악: O(n^2)
* `안정 정렬 알고리즘`
* 처음부터 끝까지 인접한 두 데이터를 비교하면서 큰 값을 맨 뒤로 보내는 방식으로 동작
* 1번의 순환마다 맨 뒤의 값이 고정

  <details>
  <summary style="font-size:20px">코드</summary>
  <div markdown="1">
  
    ```java
    public static void bubbleSort() {
        for (int i = array.length - 1; i > 0; --i) {
            for (int j = 0; j < i; ++j) {
                if(array[j] > array[j+1]) {
                    int tmp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = tmp;
                }
            }
        }
    }
    ```
  
  </div>
  </details>

</div>
</details>


<details>
<summary style="font-size:20px">Merge Sort</summary>
<div markdown="1">

* 최선, 평균, 최악 시간 복잡도: O(NlogN)
  * 이유: 배열을 반씩 나눠서 1개 원소로 나누는 것은 `logN`, 합치는 것도 `logN`번 수행, 합치면서 `N`개 원소들을 읽으면서 비교 
* `안정 정렬 알고리즘`, `분할 정복`
* 배열을 반으로 쪼개 가면서 하나의 원소를 가진 배열로 만든 이후에 쪼개진 각 배열을 정렬하면서 병합하여 최종 정렬된 배열을 완성

  <details>
  <summary style="font-size:20px">코드</summary>
  <div markdown="1">

    ```java
    static int[] array = new int[N]; // 원본 배열
    static int[] sorted = new int[N]; // 합치는 과정에서 정렬된 원소를 저장하는 임시 배열
    
    mergeSort(0, array.length-1);
    
    public static void mergeSort(int left, int right) {
        if (left < right) {
            int mid = (left+right) / 2;
            mergeSort(left, mid);
            mergeSort(mid+1, right);
            merge(left, mid, right);
        }
    }

    public static void merge(int left, int mid, int right) {
        int l = left, m = mid+1, k = left;
        while (l <= mid && m <= right) {
            if (array[l] <= array[m]) sorted[k++] = array[l++];
            else sorted[k++] = array[m++];
        }
    
        if (l > mid) {
            for (int i = m; i <= right; ++i) sorted[k++] = array[i];
        } else {
            for (int i = l; i <= mid; ++i) sorted[k++] = array[i];
        }
    
        for (int i = left; i <= right; ++i) array[i] = sorted[i];
    }
    ```

  </div>
  </details>

</div>
</details>


<details>
<summary style="font-size:20px">Quick Sort</summary>
<div markdown="1">

* 최선, 평균: O(NlogN) / 최악: O(N^2)
* `불안정 정렬 알고리즘`, `분할 정복 알고리즘`
* `파티셔닝` 아이디어를 재귀적으로 활용
* `파티셔닝`이란 pivot 원소를 기준으로 왼쪽은 pivot보다 작은 원소들로 모으고 오른쪽은 pivot보다 큰 원소로 모으는 것을 의미하는데 pivot을 기준으로 파티셔닝이 완료되면 pivot을 고정하고 같은 과정을 `재귀호출` 하여 반복하며 정렬
* 과정 (오름차순 정렬)
    - 가장 기본적인 퀵 정렬은 첫 번째 데이터를 pivot 으로 설정
    - pivot을 제외하고 왼쪽에서부터 pivot 보다 큰 데이터를 선택, 오른쪽에서부터 pivot 보다 작은 데이터를 선택해 교환
    - 두개의 위치가 겹치거나 엇갈린 경우, `pivot`과 두 데이터 중 `작은 데이터`의 위치를 서로 변경 (**작은 데이터가 pivot이 된다**)
    - 이제 pivot을 기준으로 왼쪽은 모두 pivot보다 작고, 오른쪽은 모두 pivot보다 크다. (파티셔닝)
    - 재귀적으로, 왼쪽과 오른쪽 모두 위의 방법을 순서대로 진행
* Quick Sort가 통상적으로 가장 빠른 정렬을 지원하지만 `Worst Case에서 O(n^2)`이므로 Tim Sort나 Heap Sort를 사용하기도 함
* 최악: 정렬된 배열에서 피봇을 최대/최소 값으로 선택

  <details>
  <summary style="font-size:20px">코드</summary>
  <div markdown="1">

    ```java
    quickSort(0, array.length-1);
    
    private static void quickSort(int low, int high) {
        if (low >= high) return;
        int mid = partition(low, high);
        quickSort(low, mid - 1);
        quickSort(mid, high);
    
    private static int partition(int low, int high) {
        int pivot = array[(low + high) / 2];
        while (low <= high) {
            while (array[low] < pivot) low++;
            while (array[high] > pivot) high--;
            if (low <= high) {
                int tmp = array[low];
                array[low] = array[high];
                array[high] = tmp;
                low++;
                high--;
            }
        }
        return low;
    }
    ```

  </div>
  </details>

</div>
</details>


<details>
<summary style="font-size:20px">Insertion Sort</summary>
<div markdown="1">

* 최선: O(n) / 평균, 최악: O(n^2)
* 2번째 원소부터 시작하여 그 앞의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬

  <details>
  <summary style="font-size:20px">코드</summary>
  <div markdown="1">

    ```java
    private static void insertionSort() {
        int j;
        for (int i = 1; i < array.length; ++i) {
            int key = array[i];
            for (j=i-1; j>=0 && array[j]> key; --j) {
                array[j+1] = array[j];
            }
            array[j+1] = key;
        }
    }
    ```

  </div>
  </details>

</div>
</details>


<details>
<summary style="font-size:20px">Heap Sort</summary>
<div markdown="1">

* 최선, 평균, 최악: O(NlogN)
* `불안정 정렬 알고리즘`
* 완전 이진 트리를 기본으로 하는 힙에 데이터를 삽입하고 꺼내서 힙을 통해 정렬

</div>
</details>


<details>
<summary style="font-size:20px">Counting Sort</summary>
<div markdown="1">

* 데이터의 개수를 Count 해서 정렬하는 것
* 데이터의 갯수가 N, 데이터(양수) 중 최댓값이 K일 때 최악의 경우에도 수행 시간 `O(N+K)` 보장
* 속도가 빠르지만, 수의 범위가 극단적으로 클 경우에는 메모리 낭비가 될 수 있음
  * `데이터의 범위가 제한되어 0 또는 양수 형태로 표현할 수 있을 때` 사용

</div>
</details>


<details>
<summary style="font-size:20px">이분 탐색</summary>
<div markdown="1">

* `이미 정렬되어 있는 자료구조`에서 특정 값을 탐색할 때 탐색 범위를 반으로 쪼개서 값을 찾아가는 알고리즘
* `O(logN)`으로 순차 탐색보다 빠르지만 탐색을 위해 정렬을 하면 순차 탐색보다 더 높은 시간복잡도를 갖게 됨

</div>
</details>


<details>
<summary style="font-size:20px">Fibonacci 공식을 재귀적인 방법과 동적 계획법을 이용했을 때 각각의 차이</summary>
<div markdown="1">

* 재귀적인 방법인 경우 재귀 호출 시에 중복되는 연산이 계속 수행
* 동적 계획법의 경우 이전 값을 `메모리제이션`하기 때문에 중복 연산이 수행되지 않음

</div>
</details>


<details>
<summary style="font-size:20px">DFS와 BFS</summary>
<div markdown="1">

* DFS는 `스택이나 재귀호출`로 구현할 수 있는 탐색 방법으로 한 정점으로부터 연결되어 있는 한 정점으로만 나아가는 방식
* BFS는 `큐`를 통해서 구현할 수 있는 탐색 방법으로 한 정점으로부터 연결되어 있는 모든 정점을 나아가며 탐색하는 방식으로 BFS로 구한 경로는` 최단 경로`라는 장점이 존재

</div>
</details>


<details>
<summary style="font-size:20px">재귀호출을 이용할 때의 문제점</summary>
<div markdown="1">

* 스택의 범위를 초과할 수 있음

</div>
</details>


<details>
<summary style="font-size:20px">트리 순회 방법</summary>
<div markdown="1">

* 전위 순회(Pre-order): root 방문 -> 왼쪽 서브트리 방문 -> 오른쪽 서브트리 방문
* 중위 순회(In-order): 왼쪽 서브트리 방문 -> root 방문 -> 오른쪽 서브트리 방문
* 후위 순회(Post-order): 왼쪽 서브트리 방문 -> 오른쪽 서브트리 방문 -> root 방문

</div>
</details>
