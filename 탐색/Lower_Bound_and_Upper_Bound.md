Lower Bound는 배열에서 x 이상의 수가 처음으로 나오는 위치를 반환하는 알고리즘이고,  
Upper Bound는 배열에서 x를 초과하는 수가 처음으로 나오는 위치를 반환하는 알고리즘이다.  

Lower Bound, Upper Bound 알고리즘은 **오름차순으로 정렬된 배열**일 때 사용할 수 있다.

### :blush: Lower Bound(하한)
오름차순으로 정렬된 배열에서 Lower Bound의 반환 값은 특정 값 x 이상의 수가 처음으로 나오는 위치이다.  
배열의 모든 수가 x보다 작다면 배열의 마지막 다음 위치를 반환한다.  
값이 x 이상인 인덱스의 최솟값을 찾는 문제라고 생각할 수 있다. ⇔ arr[i] >= x인 i의 최솟값 → Parametric Search
```
int Lower_Bound(int x) {
  int lo = -1, hi = n;  // 반환 값은 hi이고, 답이 될 수 있는 범위가 [0, n]이다. n은 배열의 모든 수가 x보다 작을 때 반환되는 값이다.
  while (lo + 1 < hi) {
    int mid = (lo + hi) >> 1;
    if (arr[mid] >= x)
      hi = mid;
    else
      lo = mid;
  }
  return hi;
}
```

### :blush: Upper Bound(상한)
오름차순으로 정렬된 배열에서 Upper Bound의 반환 값은 특정 값 x를 초과하는 수가 처음으로 나오는 위치이다.  
배열의 모든 수가 x보다 작거나 같다면 배열의 마지막 다음 위치를 반환한다.  
값이 x를 초과하는 인덱스의 최솟값을 찾는 문제라고 생각할 수 있다. ⇔ arr[i] > x인 i의 최솟값 → Parametric Search
```
int Upper_Bound(int x) {
  int lo = -1, hi = n; // 반환 값은 hi이고, 답이 될 수 있는 범위가 [0, n]이다. n은 배열의 모든 수가 x보다 작거나 같을 때 반환되는 값이다.
  while (lo + 1 < hi) {
    int mid = (lo + hi) >> 1;
    if (arr[mid] > x)
      hi = mid;
    else
      lo = mid;
  }
  return hi;
}
```

### :sunglasses: 시간복잡도
O(logn)

### :hand_over_mouth: Lower Bound와 Upper Bound의 성질
lower bound와 upper bound를 이용하면 배열 내 x의 개수를 구할 수 있다. (배열에 x가 없어도 되고, 이때의 결과 값은 0이다.)  
* 직접 구현한 함수  
`Upper_Bound(x) - Lower_Bound(x)`  
* C++ STL  
`upper_bound(v.begin(), v.end(), x) - lower_bound(v.begin(), v.end(), x)`  

우리는 배열이 정렬되어 있을 때 배열 내 x의 개수를 O(logn)에 구할 수 있다.

### :wink: in C++
C++의 \<algorithm\> 헤더에서는 lower_bound와 upper_bound 함수를 제공한다. *(배열이 오름차순으로 정렬되어 있어야 함)*  
lower_bound) vector → `lower_bound(v.begin(), v.end(), x)` / array → `lower_bound(arr, arr + n, x)`  
upper_bound) vector → `upper_bound(v.begin(), v.end(), x)` / array → `upper_bound(arr, arr + n, x)`  
직접 구현한 함수 Lower_Bound()와 Upper_Bound()는 반환 값이 인덱스인 반면,  
C++의 STL에서 제공하는 함수 lower_bound()와 upper_bound()는 반환 값이 iterator이다.  
즉 조건을 만족하는 인덱스가 있는 경우 해당 인덱스를 가리키는 iterator를,  
조건을 만족하는 인덱스가 없는 경우 마지막 다음 칸을 가리키는 iterator(vector의 경우 v.end())를 반환한다.  
따라서 iterator가 아닌 몇 번째 인덱스인지 알고 싶으면 반환 값에서 첫 번째 iterator를 빼주면 된다.  
vector → `lower_bound(v.begin(), v.end(), x) - v.begin()` / array → `lower_bound(arr, arr + n, x) - arr`  
(해당 인덱스 자체의 값을 알고 싶으면 `*lower_bound(v.begin(), v.end(), x)`로 쓰면 된다.)  
※ Reference  
[lower_bound](https://cplusplus.com/reference/algorithm/lower_bound/), 
[upper_bound](https://cplusplus.com/reference/algorithm/upper_bound/)  

set에서 lower_bound나 upper_bound를 쓰려면 바로 `s.lower_bound(x)` 또는 `s.upper_bound(x)`를 쓰면 된다.  
set의 lower_bound와 upper_bound는 \<set\>에서 제공하고 있다.  
※ Reference  
[set::lower_bound](https://cplusplus.com/reference/set/set/lower_bound/), 
[set::upper_bound](https://cplusplus.com/reference/set/set/upper_bound/) 
