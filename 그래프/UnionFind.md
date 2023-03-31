## Union Find

## Weighted Union Find

size 배열을 만들게 되면 메모리를 더 사용하게 되므로 parent 배열만 사용하는 방법이다.

parent[i]가 음수이면 절댓값이 i번째의 size를 의미하고, 양수이면 i번째의 부모 노드를 의미한다.  
초기 parent 배열은 -1로 초기화되어 있다. (i는 대개 1부터 시작)

즉 parent[i]에는 i가 루트 노드라면 -size, 루트 노드가 아니라면 부모 노드 번호가 저장된다.  
i가 루트 노드라면 parent[i] 값이 음수이고, 아니라면 양수(부모 노드 번호)이다.

```C++
// 부모 노드 번호 찾기
int find(int x) {
  if (parent[x] < 0)
    return x;
  else
    return parent[x] = find(parent[x]);
}

// union (c++에서는 union이 키워드)
void unite(int x, int y) {
  x = find(x); y = find(y);
  if (x == y) return;
  
  if (abs(parent[x]) < abs(parent[y]))
    swap(x, y);
  parent[x] += parent[y];
  parent[y] = x;
}
```
