### :blush: 순열 Permutation (nPr)
순서 O, 중복 X  
```
bool chosen[n + 1]; // 각 원소를 순열에 포함했는지의 여부(중복 검사)
int arr[r]; // or vector<int> arr;

// array
void nPr(int depth) {
  if (depth == r) {
    // 순열 처리
    return;
  }
  for (int i=1; i<=n; i++) {
    if (chosen[i]) continue;
    chosen[i] = true;
    arr[depth] = i;
    nPr(depth + 1);
    chosen[i] = false;
  }
}

// vector
void nPr(int depth) {
  if (depth == r) {
    // 순열 처리
    return;
  }
  for (int i=1; i<=n; i++) {
    if(chosen[i]) continue;
    chosen[i] = true;
    arr.push_back(i);
    nPr(depth + 1);
    chosen[i] = false;
    arr.pop_back();
  }
}
```
nPr(0);으로 호출해서 순열을 구할 수 있다.
<br/><br/>
### :blush: 중복 순열(n&Pi;r)
순서 O, 중복 O  
중복 순열을 구하는 것은 순열에서 중복 검사를 제외한 것과 같다.
```
int arr[r];

void nPIr(int depth) {
  if (depth == r) {
    // 중복 순열 처리
    return;
  }
  for (int i=1; i<=n; i++) {
    arr[depth] = i;
    nPIr(depth + 1);
  }
}
```
nPIr(0);으로 호출해서 중복 순열을 구할 수 있다.
<br/><br/>
### :blush: 조합 Combination (nCr)
순서 X, 중복 X  
```
int arr[r];

void nCr(int depth, int next) {
  if (depth == r) {
    // 조합 처리
    return;
  }
  for (int i=next; i<=n; i++) {
    arr[depth] = i;
    nCr(depth + 1, i + 1);
  }
}
```
nCr(0, 1);로 호출해서 조합을 구할 수 있다.
<br/><br/>
### :blush: 중복 조합 (nHr)
순서 X, 중복 O  
중복 조합과 조합의 차이는 반복문의 시작 값이 이전에 선택한 값이냐 이전에 선택한 값 + 1이냐이다.
```
int arr[r];

void nHr(int depth, int next) {
  if (depth == r) {
    // 중복 조합 처리
    return;
  }
  for (int i=next; i<=n; i++) {
    arr[depth] = i;
    nHr(depth + 1, i);
  }
}
```
nHr(0, 1);로 호출해서 중복 조합을 구할 수 있다.
