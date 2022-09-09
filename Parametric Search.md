<p>
  Parametric Search는 주어진 문제를 결정 문제로 변형하여 Binary Search를 통해 해결하는 것이다.<br/>
  (결정 문제: true 또는 false 형태의 답만이 나오는 문제)<br/>
  문제가 특정 조건을 만족하는 최댓값/최솟값을 구하는 형식이거나 이러한 형태로 변형할 수 있어야 한다.
</p>

### 😀 어떤 조건을 만족하는 `param`의 최솟값(=`answer`)을 찾는 문제
`check(param)`이 연속이므로 `param >= answer`에 대해 `check(param)`은 항상 `true`이다.<br/>
`param`이 오름차순이므로 `check(param)`은 `[false, false, ..., false, true, ..., true, true]`이다.<br/>
```
while(lo + 1 < hi) {
  int mid = (lo + hi) >> 1;
  if(check(mid)) hi = mid;
  else lo = mid;
}
```
while-loop가 종료된 후 `check(param)`에서 `lo`와 `hi`가 가리키는 값이 아래와 같기 때문에 `answer`는 `hi`이다.<br/>
함수로 작성했다면 `hi`가 반환 값이다.<br/>
|false|false|...|false|true|...|true|true|
|---|---|---|:---:|:---:|---|---|---|
||||↑<br/>`lo`|↑<br/>`hi`|

💥 `lo`와 `hi`의 구간을 정의할 때, **`lo` = 구간의 최솟값 - 1, `hi` = 구간의 최댓값**으로 정의해야 한다.<br/>
정답이 `hi`이므로 만약 `lo`를 구간의 최솟값으로 정의하면  
반복문의 조건인 `lo + 1 < hi`에 의해 `hi`는 구간의 최솟값이 될 수 없으므로 정답이 구간의 최솟값인 경우 답을 얻을 수 없다.
<br/><br/>
### 😀 어떤 조건을 만족하는 `param`의 최댓값(=`answer`)을 찾는 문제
`check(param)`이 연속이므로 `param <= answer`에 대해 `check(param)`은 항상 `true`이다.<br/>
`param`이 오름차순이므로 `check(param)`은 `[true, true, ..., true, false, ..., false, false]`이다.<br/>
```
while(lo + 1 < hi) {
  int mid = (lo + hi) >> 1;
  if(check(mid)) lo = mid;
  else hi = mid;
}
```
while-loop가 종료된 후 `check(param)`에서 `lo`와 `hi`가 가리키는 값이 아래와 같기 때문에 `answer`는 `lo`이다.<br/>
함수로 작성했다면 `lo`가 반환 값이다.<br/>
|true|true|...|true|false|...|false|false|
|---|---|---|:---:|:---:|---|---|---|
||||↑<br/>`lo`|↑<br/>`hi`|

💥 `lo`와 `hi`의 구간을 정의할 때, **`lo` = 구간의 최솟값, `hi` = 구간의 최댓값 + 1**로 정의해야 한다.<br/>
정답이 `lo`이므로 만약 `hi`를 구간의 최댓값으로 정의하면  
반복문의 조건인 `lo + 1 < hi`에 의해 `lo`는 구간의 최댓값이 될 수 없으므로 정답이 구간의 최댓값인 경우 답을 얻을 수 없다.
<br/><br/>
### 💫 시간복잡도
`while(lo + 1 < hi)`인 동안 `mid = (lo + hi) >> 1`를 이용해 [`lo`, `hi`]를 [`lo`, `mid`] 또는 [`mid`, `hi`]로 줄여나간다.  
한 번의 loop에서 구간의 길이는 절반으로 줄어들기 때문에 최초 구간의 길이를 N이라 하면 while문의 실행 횟수는 O(logN)번이다.  
while문에서 실행되는 `check(mid)`의 시간복잡도를 O(T)라고 하면, Parametric Search의 최종 시간복잡도는 O(T * logN)이다.
