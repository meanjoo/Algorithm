구간 합 트리

이를 기반으로 응용해서 구간의 최댓값, 최솟값, 곱을 구하는 트리도 만들 수 있다.

탐색 및 갱신 Time Complexity: `O(log n)`

```C++
vector<int> seg;

// 세그먼트 트리 크기 설정
void initSeg(int n) {
  int h = (int)(ceil(log2(n)));
  int sz = 1 << (h + 1);
  seg.resize(sz);
  
  // seg.resize(4 * n);
}

// 최초 세그먼트 트리 만들기 - 경우에 따라 필요하거나 필요하지 않은 함수
int makeSeg(int node, int start, int end) {
  if (start == end)
    return seg[node] = arr[start];
  
  int mid = (start + end) >> 1;
  return seg[node] = makeSeg(node * 2, start, mid) + makeSeg(node * 2 + 1, mid + 1, end);    
}

// 구간 합 구하기
int getSum(int node, int start, int end, int left, int right) {
  if (left > end || right < start)
    return 0;
  if (left <= start && end <= right)
    return seg[node];
  
  int mid = (start + end) >> 1;
  return getSum(node * 2, start, mid, left, right) + getSum(node * 2 + 1, mid + 1, end, left, right);
}

// 특정 값 변경
void update(int node, int start, int end, int idx, int diff) {
  if (idx < start || idx > end)
    return;
  seg[node] += diff;
  if (start == end) {
    // arr[start] += diff; // 만약 기존 배열을 쓰는 경우라면 이 줄이 필요
    return;
  }
  
  int mid = (start + end) >> 1;
  update(node * 2, start, mid, idx, diff);
  update(node * 2 + 1, mid + 1, end, idx, diff);
}
```
