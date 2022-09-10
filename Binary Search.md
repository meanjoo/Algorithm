Binary Search는 **정렬된 배열**에서 특정 원소의 존재 여부를 파악하는 문제를 O(logn) 시간에 해결하는 알고리즘이다.

n개의 원소로 구성되어 있는 정렬된 배열이 있을 때, 이 배열에 목푯값 x가 존재하는지를 판별한다고 하자.  

### 😊 방법
이 방법은 Binary Search를 구현할 때 가장 많이 쓰이는 방법이고, 사전에서 단어를 찾는 방법과 비슷하다.  
배열의 특정 부분을 살펴보며 탐색이 진행되고, 처음 탐색을 시작할 때는 배열 전체를 놓고 시작한다.  
단계별로 알고리즘을 진행해 나가면서 탐색 범위를 절반으로 줄여나간다.  
단계마다 현재 살펴보고 있는 부분 배열의 중앙 원소를 검사한다.  
만약 중앙 원소가 목푯값과 같다면 탐색을 종료하고, 다르다면 중앙 원소의 값에 따라 부분 배열의 왼쪽 절반 또는 오른쪽 절반을 선택해서 재귀적으로 탐색을 계속한다.  
단계마다 부분 배열의 크기를 절반씩 줄여나가기 때문에 시간 복잡도는 O(logn)이다.  
```
int bs(int x) {
  int left = 0, right = n - 1;
  while (left <= right) {
    int mid = (left + right) >> 1;
    if(arr[mid] == x) {
      return mid; // arr[mid]에서 x를 찾음
    }
    if(arr[mid] < x)
      left = mid + 1;
    else
      right = mid - 1;
  }
  return -1; // 배열에 목푯값 x가 존재하지 않을 때
}
```
### 😬 주의사항
방법 1의 코드에서 `mid`를 `(left + right) / 2`라고 정의하는데 이 문장에는 위험이 존재한다.  
`left + right`가 int의 최대 값인 2<sup>31</sup>-1을 초과하게 되면 overflow가 발생하여 잘못된 값이 `mid`에 대입된다.  
`left + right`의 결과 값이 overflow가 발생하지 않음이 보장되면 `int mid = (left + right) >> 1;`라고 쓰는 것이 간단하고 편하다.    
하지만 만약 `left + right`의 결과 값이 overflow가 발생할 가능성이 존재하면 이를 해결해줘야 한다. 해결 방법은 두 가지가 있다.  
① 메모리를 더 쓰긴 하지만 간단하게 `left`, `right`, `mid`의 자료형을 int보다 더 큰 자료형인 long long으로 설정한다.  
(하지만 left + right가 long long도 초과한다면 ②로 해결해야 한다.)  
② `int mid = left + ((right - left) / 2);`로 정의한다. 또는 `int mid = right - ((right - left) / 2);`  
right - left를 함으로써 overflow를 피하고 이 값을 2로 나누면 양끝인 left, right에서부터 left와 right의 중간 원소까지의 offset이 된다.  
left + offset 또는 right - offset은 [left, right]에서 중간 원소의 위치이다.
