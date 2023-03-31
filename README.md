### 자료구조
Stack  
Queue  
Deque  
Segment Tree  

### 탐색
[Binary Search](https://github.com/meanjoo/Algorithm/blob/main/%ED%83%90%EC%83%89/Binary_Search.md)  
[Parametric Search](https://github.com/meanjoo/Algorithm/blob/main/%ED%83%90%EC%83%89/Parametric_Search.md)  
[Lower Bound & Upper Bound](https://github.com/meanjoo/Algorithm/blob/main/%ED%83%90%EC%83%89/Lower_Bound_and_Upper_Bound.md)  

### 수학
[소수](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/prime.md)  
[(중복)순열과 (중복)조합](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/nr.md)  
modulo 연산의 사칙연산  
[GCD & LCM](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/gcd_lcm.md)  

### 기하
[CCW](https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/CCW.md)  

### 그래프
DFS & BFS  
Union Find  

### 문자열

### :grinning:
[LIS](https://github.com/meanjoo/Algorithm/blob/main/LIS.md)  
Topological Sort

---
`auto`는 C++11에서 처음 등장하여 C++11 이후로 사용 가능

```C++
for (auto a : arr) // 인자를 복사. 복사 비용 발생. 원래 값 변경 불가. 읽기만 할 것이라면 좋지 못함.
for (auto& a : arr) // &를 통해 복사가 아닌 reference를 가져오지 않음. 복사 비용 X. 원래 값 변경 가능.
for (const auto& a : arr) // &를 통해 복사가 아닌 reference를 가져오지 않음. 복사 비용 X. 원래 값 변경 불가. 
```

### STL - map
`map<string, int> m;`이라고 가정

* 순회

  + while-loop 및 전통적인 for문
    ```C++ 
    auto iter = m.begin(); // type of m is map<string, int>::iterator
    while (iter != m.end()) {
      cout << "key: " << iter->first << ' ' << ", value: " << iter->second << endl;
      iter++;
    }
    ```
    ```C++
    for (auto iter = m.begin(); iter != m.end(); iter++) {
      cout << "key: " << iter->first << ' ' << ", value: " << iter->second << endl;
    }
    ```
  
  + range based for statement
  
    C++11에 range based for statement(범위 기반 for문)가 추가되었다. 이를 이용해서 보다 간단하게 map을 순회할 수 있다.
    ```C++
    for (const auto& item : m) {
      cout << "key: " << item.first << ' ' << ", value: " << item.second << endl;
    }
    ```
    
  + range based for statement 2
  
    이 방법은 C++17 이후에서 지원된다.
    ```C++
    for (const auto& [key, value] : m) {
      cout << "key: " << key << ' ' << ", value: " << value << endl;
    }
    ```

* 키 값 찾기  
  Time Complexity: `O(log n)`
  ```C++
  auto item = m.find("keyword");
  item != m.end() ? cout << "key exist.\n" : cout << "key does not exist.\n";
  ```
  ```C++
  auto item = m.find("keyword");
  if (item != m.end()) {
    cout << "key: " << item->first << ' ' << ", value: " << item->second << endl;
  }
  ```
