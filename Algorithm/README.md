# Algorithm
* 추가할 사항: 각 정렬이 언제 사용되는 가, 트리를 순회하는 방법

## Table of Contents
* [빅오 표기법](#빅오-표기법)
* [정렬 알고리즘에서의 stable](#정렬-알고리즘에서의-stable)
* [정렬 알고리즘의 가짓수가 많은 이유](#정렬-알고리즘의-가짓수가-많은-이유)
* [Selection Sort](#selection-sort)
* [Bubble Sort](#bubble-sort)
* [Merge Sort](#merge-sort)
* [Quick Sort](#quick-sort)
* [Insertion Sort](#insertion-sort)
* [Heap Sort](#heap-sort)
* [이분 탐색](#이분-탐색)
* [Fibonacci 공식을 재귀적인 방법과 동적 계획법을 이용했을 때 각각의 차이](#fibonacci-공식을-재귀적인-방법과-동적-계획법을-이용했을-때-각각의-차이)
* [DFS와 BFS](#dfs와-bfs)
* [재귀호출을 이용할 때의 문제점](#재귀호출을-이용할-때의-문제점)

## 빅오 표기법
* 컴퓨터 공학에서 알고리즘의 `시간복잡도`(실행시간)이나, `공간 복잡도`(사용 메모리)에 대한 `최악`의 경우를 표현하는 표기 방법

## 정렬 알고리즘에서의 stable
* 정렬 기준으로 봤을 때, `값이 동일한 Element가 있어도 정렬 전의 순서와 정렬 후의 순서가 동일함을 보장`하는 것

## 정렬 알고리즘의 가짓수가 많은 이유
* `공간 복잡도`에 따라 사용해야할 알고리즘이 다름 -> Merge Sort는 공간 복잡도는 Selection Sort와 Insertion Sort에 비해 큼
* `안정 정렬`이냐 `불안정 정렬`이냐에 따라 사용해야 할 때가 다름

## Selection Sort
* 최선, 평균, 최악: O(n^2) 
* `불안정 정렬 알고리즘`
* 선택 정렬은 가장 작은 값을 가지는 데이터를 찾아서 가장 작은 값을 앞에서부터 채워 나가면서 정렬하는 방식으로 동작
* 1번의 순환마다 맨 앞의 값이 고정
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

## Bubble Sort
* 최선, 평균, 최악: O(n^2)
* `안정 정렬 알고리즘`
* 처음부터 끝까지 현재 자신과 자신의 다음 데이터를 비교해가면서 큰 값을 맨 뒤로 보내는 방식으로 동작
* 1번의 순환마다 맨 뒤의 값이 고정
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

## Merge Sort
* 최선, 평균, 최악: O(NlogN)
* `안정 정렬 알고리즘`
* 배열을 반으로 쪼개 가면서 하나의 원소를 가진 배열로 만든 이후에 쪼개진 각 배열을 정렬하면서 병합하여 최종 정렬된 배열을 완성
```java
mergeSort(0, array.length-1);

public static void mergeSort(int left, int right) {
    if (left < right) {
        int mid = (left+right) / 2;
        mergeSort(left, mid);
        mergeSort(mid+1, right);
        merge(left, mid, right);
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
    
    for (int i = left; i <= right; ++i) array[i] = sorted[i];
}
```

## Quick Sort
* 최선, 평균: O(NlogN) / 최악: O(N^2)
* `불안정 정렬 알고리즘`
* 분할 정복 알고리즘으로 `파티셔닝` 아이디어를 재귀적으로 활용
* `파티셔닝`이란 pivot 원소를 기준으로 왼쪽은 pivot보다 작은 원소들로 모으고 오른쪽은 pivot보다 큰 원소로 모으는 것을 의미하는데 pivot을 기준으로 파티셔닝이 완료되면 pivot을 고정하고 같은 과정을 `재귀호출` 하여 반복하며 정렬
* pivot 선정 방법 (오름차순 정렬)
    - 가장 기본적인 퀵 정렬은 첫 번째 데이터를 pivot 으로 설정
    - pivot을 제외한 왼쪽에서부터 pivot 보다 큰 데이터를 선택, 오른쪽에서부터 pivot 보다 작은 데이터를 선택
    - 위 두 데이터의 위치가 엇갈리는 경우, `pivot`과 두 데이터 중 `작은 데이터`의 위치를 서로 변경 (**작은 데이터가 pivot이 된다**)
    - 이제 pivot을 기준으로 왼쪽은 모두 pivot보다 작고, 오른쪽은 모두 pivot보다 크다. (파티셔닝)
    - 재귀적으로, 왼쪽과 오른쪽 모두 위의 방법을 순서대로 진행
* Quick Sort가 통상적으로 가장 빠른 정렬을 지원하지만 `Worst Case에서 O(n^2)`이므로 Tim Sort나 Heap Sort를 사용하기도 함
* 최악: 정렬된 배열에서 피봇을 최대/최소 값으로 선택
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

## Insertion Sort
* 최선: O(n) / 평균, 최악: O(n^2)
* 2번째 원소부터 시작하여 그 앞의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬
```java
private static void insertionSort() {
    int j;
    for (int i = 1; i < array.length; ++i) {
        int key = array[i]
        for (j=i-1; j>=0 && array[j]> key; --j) {
            array[j+1] = array[j];
        }
        array[j+1] = key;
    }
}
```

## Heap Sort
* 최선, 평균, 최악: O(nlogn) 
* `불안정 정렬 알고리즘`
* 완전 이진 트리를 기본으로 하는 힙에 데이터를 삽입하고 꺼내서 힙을 통해 정렬

## Counting Sort
* 특정한 조건이 부합할 때만 사용할 수 있지만 **매우 빠르게 동작하는** 정렬 알고리즘
    * 계수 정렬은 **데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때** 사용 가능
* 데이터의 갯수가 N, 데이터(양수) 중 최댓값이 K일 때 최악의 경우에도 수행 시간 `O(N+K)` 보장

## 이분 탐색
* 이분 탐색은 `이미 정렬되어 있는 자료구조`에서 특정 값을 탐색할 때 탐색 범위를 반으로 쪼개서 값을 찾아가는 알고리즘
* O(logN)으로 순차 탐색보다 빠르지만 탐색을 위해 정렬을 하면 순차 탐색보다 더 높은 시간복잡도를 갖게 됨

## Fibonacci 공식을 재귀적인 방법과 동적 계획법을 이용했을 때 각각의 차이
* 재귀적인 방법인 경우 재귀 호출 시에 중복되는 연산이 계속 수행
* 동적 계획법의 경우 이전 값을 `메모리제이션`하기 때문에 중복 연산이 수행되지 않음

## DFS와 BFS
* DFS는 `스택이나 재귀호출`로 구현할 수 있는 탐색 방법으로 한 정점으로부터 연결되어 있는 한 정점으로만 나아가는 방식
* BFS는 `큐`를 통해서 구현할 수 있는 탐색 방법으로 한 정점으로부터 연결되어 있는 모든 정점을 나아가며 탐색하는 방식으로 BFS로 구한 경로는` 최단 경로`라는 장점이 존재

## 재귀호출을 이용할 때의 문제점
* 스택의 범위를 초과할 수 있음