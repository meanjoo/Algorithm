Lower Bound는 배열에서 x 이상의 수가 처음으로 나오는 위치를 반환하는 알고리즘이고,  
Upper Bound는 배열에서 x를 초과하는 수가 처음으로 나오는 위치를 반환하는 알고리즘이다.  

Lower Bound, Upper Bound 알고리즘은 **오름차순으로 정렬된 배열**일 때 사용할 수 있다.

### :blush: Lower Bound(하한)
오름차순으로 정렬된 배열에서 Lower Bound의 반환 값은 특정 값 x 이상의 수가 처음으로 나오는 위치이다.  
배열의 모든 수가 x보다 작다면 배열의 마지막 다음 위치를 반환한다.  
값이 x 이상인 인덱스의 최솟값을 찾는 문제로 변형하여 생각할 수 있다. → Parametric Search
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
값이 x를 초과하는 인덱스의 최솟값을 찾는 문제로 변형하여 생각할 수 있다. → Parametric Search
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
