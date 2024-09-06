### 자료구조
+ Stack
+ Queue
+ Deque
+ [Segment Tree](https://github.com/meanjoo/Algorithm/blob/main/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/SegmentTree.md)

### 탐색
+ [Binary Search](https://github.com/meanjoo/Algorithm/blob/main/%ED%83%90%EC%83%89/Binary_Search.md)
+ [Parametric Search](https://github.com/meanjoo/Algorithm/blob/main/%ED%83%90%EC%83%89/Parametric_Search.md)
+ [Lower Bound & Upper Bound](https://github.com/meanjoo/Algorithm/blob/main/%ED%83%90%EC%83%89/Lower_Bound_and_Upper_Bound.md)

### 수학
+ [소수](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/prime.md)
+ [(중복)순열과 (중복)조합](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/nr.md)
+ modulo 연산의 사칙연산
+ [GCD & LCM](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/gcd_lcm.md)

### 기하
+ [CCW](https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/CCW.md)
+ 다각형 내부의 점 1688

### 그래프
+ DFS & BFS  
+ [Union Find](https://github.com/meanjoo/Algorithm/blob/main/Graph/UnionFind.md)
+ MST: Minimum Spanning Tree

### 문자열

### Technique
+ [배열 회전](https://github.com/meanjoo/Algorithm/blob/main/Technique/rotateArray.md)
+ [문자열 자르기](https://github.com/meanjoo/Algorithm/blob/main/Technique/splitString.md)

### :grinning:
+ [LIS](https://github.com/meanjoo/Algorithm/blob/main/LIS.md)
+ Topological Sort

---
`auto`는 C++11에서 처음 등장하여 C++11 이후로 사용 가능

```C++
for (auto a : arr) // 인자를 복사. 복사 비용 발생. 원래 값 변경 불가. 읽기만 할 것이라면 좋지 못함.
for (auto& a : arr) // &를 통해 복사가 아닌 reference를 가져오지 않음. 복사 비용 X. 원래 값 변경 가능.
for (const auto& a : arr) // &를 통해 복사가 아닌 reference를 가져오지 않음. 복사 비용 X. 원래 값 변경 불가. 
```

## STL - map
:cherry_blossom: `#include <map>`

`map<string, int> m;`이라고 가정
### 순회

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

### 키 검색
Time Complexity: `O(log n)`

- `find()` 사용

  맵에서 키를 검색하여 키가 존재하면 iterator를 반환하고, 존재하지 않으면 `map.end()`를 반환한다.
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

- `count()` 사용 *얘도 O(log n)인가..?*

  단순히 key가 있는지 조사만 하는 것이라면 `count()`를 쓰는 게 더 간편하다. `count()`는 map에 있는 key의 요소 수를 가져온다. map은 key가 고유하기 때문에 key가 있다면 1, 없으면 0을 반환한다.
  ```c++
  if (m.count("keyword")) {} // key가 있는 경우
  else {} // key가 없는 경우
  ```
  ```c++
  if (m.count("keyword") != 0) {} // key가 있는 경우
  else {} // key가 없는 경우
  ```

## STL - set
:cherry_blossom: `#include <set>`

중복을 허용하지 않으며 원소가 정렬된다. (default: 오름차순)

균형 이진 트리로 구현되어 있기 때문에 탐색 시간이 평균, 최악 모두 `O(log n)`이다.

`set<string> s;`라고 가정

- `s.insert(str);`
  - str을 s에 삽입
- `s.clear();`
  - s 초기화

* 순회

  + 전통적인 for문
    ```C++
    for (auto iter = s.begin(); iter != s.end(); iter++) {
      cout << *iter << ' ';
    }
    cout << endl;
    ```
    
  + range based for statement
    ```C++
    for (const auto& elem : s) {
      cout << elem << ' ';
    }
    cout << endl;
    ```
    
* 원소 검색  
  Time Complexity: `O(log n)`
  
  set에서 원소를 검색하여 원소가 존재하면 iterator를 반환하고, 존재하지 않으면 `set.end()`를 반환한다.
  ```C++
  auto item = s.find("word");
  item != s.end() ? cout << "element exist.\n" : cout << "element does not exist.\n";
  ```
  ```C++
  auto item = s.find("word");
  if (item != s.end()) {
    cout << "element: " << *item << endl;
  }
  ```

## STL - unordered_set
:cherry_blossom: `#include <unordered_set>`

중복을 허용하지 않으며 원소가 정렬되지 않는다.

원소 삽입과 검색 시 해시 함수를 사용한다. (해시 테이블 기반 저장)  
따라서 탐색 시간이 평균 `O(1)`이지만, 최악의 경우 `O(n)`이다.  
해시 충돌이 많이 발생하게 되면 성능이 나빠진다.

문자열 길이마다 unordered set을 가지는 것보다 모든 길이의 문자열에 대한 unordered set을 가지는 것이 시간 차이가 꽤 날 수 있다.
해시 충돌이 많이 발생하게 되면 성능이 나빠지기 때문이다. [문제 참고](https://www.acmicpc.net/problem/11478)

## STL - priority_queue
:cherry_blossom: `#include <queue>`

* 생성
  ```C++
  priority_queue<int> pq; // Max Heap으로 priority_queue<int, vector<int>, less<int>> pq;와 같음.
  
  priority_queue<int, vector<int>, greater<int>> pq; // Min Heap
  ```
  
* 사용자 정의  
  영어 점수(eng)가 높은 학생이 top을 유지하도록 만들기. 단, 영어 점수가 같다면 수학 점수(mat)가 높은 학생이 top이 되도록
  
  ```C++
  struct Student {
    string id, name;
    int mat, eng;
    
    Student(string ID, string NAME, int MAT, int ENG) : id(ID), name(NAME), mat(MAT), eng(ENG) {}
    
    bool operator<(const Student& stu) const {
      if (eng == stu.eng)
        return mat < stu.mat;
      return eng < stu.eng;
    }
  };
  
  priority_queue<Student> pq;
  ```
  ```C++
  struct Student {
    string id, name;
    int mat, eng;
    
    Student(string ID, string NAME, int MAT, int ENG) : id(ID), name(NAME), mat(MAT), eng(ENG) {}
  };
  
  struct comp {
    bool operator()(const Student& stu1, const Student& stu2) {
      if (stu1.eng == stu2.eng)
        return stu1.mat < stu2.mat;
      return stu1.eng < stu2.eng;
    }
  };
  
  priority_queue<Student, vector<Student>, comp> pq;
  ```

## string 관련
:cherry_blossom: `#include <string>`

`string str = "hello world!";`

* 관련 함수

  + `str.find()` - 찾기
  
    문자열에서 원하는 문자 또는 문자열의 위치를 찾는다.  
    return 값: 문자열을 찾았으면 해당 문자열의 시작 위치를 반환, 찾지 못했으면 string::npos를 반환
  
    - `str.find("찾을 문자열")` - str의 처음부터 찾을 문자열을 찾음
    
      ex. `str.find("hello")` -> `0`  
      &nbsp;&nbsp;&nbsp;&nbsp;
      `str.find("world")` -> `6`  
      &nbsp;&nbsp;&nbsp;&nbsp;
      `str.find('l')` -> `2`
      
    - `str.find("찾을 문자열", 검색 시작 위치)` - str[검색 시작 위치]부터 찾을 문자열을 찾음
    
      ex. `str.find('l', 2);` -> `2`  
      &nbsp;&nbsp;&nbsp;&nbsp;
      `str.find('l', 4);` -> `9`

### 문자열 자르기
`str.substr()`
  
문자열의 일부를 반환한다.  
원래 문자열의 [idx, idx + count)까지의 문자열을 반환하며, idx가 원래 문자열의 길이보다 길면 out_of_range 예외를 발생시킨다.  
idx + count가 원래 문자열의 길이보다 길면 원래 문자열의 끝까지를 반환한다.

- `str.substr(자를 시작 인덱스)` - 자를 시작 인덱스부터 문자열의 끝까지 반환
  - `str.substr(4)` -> `o world!`
  - `str.substr(6)` -> `world!`

- `str.substr(자를 시작 인덱스, 개수)` - 자를 시작 인덱스부터 개수만큼 문자열을 반환
  - `str.substr(5, 3)` -> ` wo`
  - `str.substr(0, 5)` -> `hello`
  - `str.substr(1, 100)` -> `ello world!`


* 특정 문자 기준으로 자르기

  ```C++
  int sep = str.find("특정 문자");
  int prev = 0;
  
  while (sep != string::npos) {
    string sub = str.substr(prev, sep - prev);
    v.push_back(sub); // 문자열이 정수인 경우: v.push_back(stoi(sub));
    prev = sep + 1;
    sep = str.find("특정 문자", prev);
  }
  v.push_back(str.substr(prev)); // 문자열이 정수인 경우: v.push_back(stoi(str.substr(prev)));
  ```

### 변환
- int <-> string
  - `stoi(numberString)` : string -> int
  - `to_string(number)` : int -> string

## 배열 복사
:cherry_blossom: `#include <algorithm>`

for-loop 대신 복사할 수 있는 방법

`copy(복사할 메모리의 시작을 가리키는 포인터, 복사할 메모리의 마지막을 가리키는 포인터, 복사 받을 메모리의 시작을 가리키는 포인터);`

```C++
const int SIZE = 50;

int arr1[100], arr2[SIZE], arr3[100][100], arr4[SIZE][SIZE];
int copy1[100], copy2[SIZE], copy3[100][100], copy4[SIZE][SIZE];

// 1차원 배열 복사
copy(arr1, arr1 + 100, copy1);
copy(arr2, arr2 + SIZE, copy2);

// 2차원 배열 복사
copy(&arr3[0][0], &arr3[0][0] + (100 * 100), &copy3[0][0]);
copy(&arr4[0][0], &arr4[0][0] + (SIZE * SIZE), &copy4[0][0]);

// 벡터
v1.resize(SIZE); // 1차원
v1.resize(SIZE, vector<int>(SIZE)); // 2차원

copy(v.begin(), v.end(), copyv.begin()); // 복사는 1차원 벡터 2차원 벡터 동일
```
