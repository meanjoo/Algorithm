<p>
  Parametric Search는 주어진 문제를 결정 문제로 변형하여 Binary Search를 통해 해결하는 것이다.<br/>
  (결정 문제: true 또는 false 형태의 답만이 나오는 문제)<br/>
  문제가 특정 조건을 만족하는 최댓값/최솟값을 구하는 형식이거나 이러한 형태로 변형할 수 있어야 한다.
</p>

#### * 어떤 조건을 만족하는 param의 최솟값(=answer)을 찾는 문제
`check(param)`이 연속이므로 `param >= answer`에 대해 `check(param)`은 항상 `true`이다.<br/>
`param`이 오름차순이므로 `check(param)`은 `[false, false, ..., false, true, ..., true, true]`이다.<br/>

```
while(lo + 1 < hi) {
  int mid = (lo + hi) >> 1;
  if(check(mid)) hi = mid;
  else lo = mid;
}
```
while-loop가 종료된 후 check(param)에서 `lo`와 `hi`가 가리키는 곳이 아래와 같기 때문에 `answer`는 `hi`이다.<br/>
함수로 작성했다면 `hi`가 반환 값이다.<br/>
|false|false|...|<span style="color:red">false</span>|true|...|true|true|
|---|---|---|:---:|:---:|---|---|---|
||||↑<br/>`lo`|↑<br/>`hi`|
