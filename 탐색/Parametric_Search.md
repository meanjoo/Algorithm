Parametric Search는 주어진 문제를 결정 문제로 변형하여 Binary Search를 통해 해결하는 것이다.<br/>
(결정 문제: true 또는 false 형태의 답만이 나오는 문제)<br/>
문제가 특정 조건을 만족하는 최댓값/최솟값을 구하는 형식이거나 이러한 형태로 변형할 수 있어야만 Parametric Search를 활용할 수 있다.

Parametric Search의 과정을 간단히 요약하면 아래와 같다.
1. `check(lo) != check(hi)`가 되도록 [`lo`, `hi`]를 정의한다.
2. `lo + 1 < hi`인 동안 `check(lo) == check(mid)`라면 `lo = mid`, 아니라면 즉, `check(hi) == check(mid)`라면 `hi = mid`를 반복한다.
3. `lo + 1 == hi`가 되면 반복문을 탈출하고, `lo`와 `hi`는 true와 false의 경계에 위치하게 된다.

1에서 초기 상태의 `lo`, `hi`가 `check(lo) != check(hi)`이므로 결정 문제의 답이 바뀌는 경계는 [`lo`, `hi`] 내에 있음이 보장된다.  
2에서 `lo + 1 < hi`인 동안 [`lo`, `hi`]를 [`lo`, `mid`] 또는 [`mid`, `hi`]로 줄여나가는데, `check(lo)`와 `check(hi)`는 변하지 않는다.  
`check(lo) == check(mid)`이면 `lo = mid`, `check(hi) == check(mid)`이면 `hi = mid`를 대입하기 때문이다.  
1과 2에 따라 결정 문제의 답이 바뀌는 경계는 [`lo`, `hi`] 내에 있음이 보장된다.  
`lo + 1 < hi`가 반복 조건이므로 `lo`와 `hi` 사이에는 적어도 하나 이상의 값이 반드시 존재하고, `mid`는 항상 `lo` < `mid` < `hi`를 만족한다.  
구간의 길이는 반복마다 절반씩 줄어들며 언젠가 `lo + 1 == hi`를 만족하여 반복문을 탈출하게 된다.  
반복문을 탈출하여 Binary Search가 종료되면 `lo`와 `hi`는 결정 문제의 답이 바뀌는 경계에 위치하게 된다.  

*pf1*) lo < mid < hi의 성립  
hi - lo = t라고 하면 lo + 1 < hi에서 lo + 1 < hi = 1 < hi - lo이므로 t > 1, 즉 t >= 2를 만족하고 t / 2 >= 0을 만족한다.  
이때, mid는 (lo + hi) / 2로 구한다.  
① mid = (lo + hi) / 2 = (2 * lo + t) / 2 = lo + t / 2  
t / 2 >= 0이므로 lo + t / 2는 항상 lo보다 크고, lo + t / 2는 mid이다. 따라서 mid > lo를 만족한다.  
② mid = (lo + hi) / 2 = (2 * hi - t) / 2 = hi - t / 2  
t / 2 >= 0이므로 hi - t / 2는 항상 hi보다 작고, hi - t / 2는 mid이다. 따라서 mid < hi를 만족한다.  
∴ lo < mid < hi

*pf2*) 반복문을 탈출하는, 즉 Binary Search 종료 시 lo + 1 == hi의 성립  
반복문의 조건이 lo + 1 < hi이므로 반복문을 탈출했다면 lo + 1 >= hi를 만족했다는 것이다.  
lo < mid < hi인 mid를 lo 또는 hi에 대입하기 때문에 lo < hi이다.  
이때 두 조건 lo < hi <= lo + 1을 만족하는 hi는 lo + 1이 유일하다.  
따라서 반복문을 탈출했을 때 lo와 hi는 항상 lo + 1 == hi를 만족한다.
<br/><br/>
이제 `lo`, `hi`의 초기 값 정의와 결정 함수 구현 문제를 해결해야 한다.  
`lo`, `hi`의 초기 값 정의는 아래에서 보고, 결정 함수에 대해서 살펴보자. `check(param)`을 결정 함수라고 하자.  
`check(param)` := `param`이 어떤 조건을 만족하면 true를, 아니라면 false를 반환하는 결정 함수  
`param`은 연속이어야 하고, 그와 동시에 `check(param)`의 결과 또한 연속이어야 한다.  
`param`이 구간 [`lo`, `hi`] 사이의 값일 때, `check(param)`은 `[false, false, ..., false, true, ..., true, true]` 또는 `[true, true, ..., true, false, ..., false, false]`여야 한다.  
즉, 값이 바뀌는 부분(false → true 또는 true → false)이 한 번만 존재해야 한다. 이 부분이 2개 이상이면 Binary Search가 아닌 삼분 탐색 등 다른 방법으로 문제를 해결해야 한다.
<br/><br/>
### 😊 어떤 조건을 만족하는 `param`의 최솟값(=`answer`)을 찾는 문제
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

💗 `lo`와 `hi`의 초기 값을 정의할 때, **`lo` = 구간의 최솟값 - 1, `hi` = 구간의 최댓값**으로 정의해야 한다.<br/>
정답이 `hi`이므로 만약 `lo`를 구간의 최솟값으로 정의하면  
반복문의 조건인 `lo + 1 < hi`에 의해 `hi`는 구간의 최솟값이 될 수 없으므로 정답이 구간의 최솟값인 경우 답을 얻을 수 없다.
<br/><br/>
### 😊 어떤 조건을 만족하는 `param`의 최댓값(=`answer`)을 찾는 문제
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

💗 `lo`와 `hi`의 초기 값을 정의할 때, **`lo` = 구간의 최솟값, `hi` = 구간의 최댓값 + 1**로 정의해야 한다.<br/>
정답이 `lo`이므로 만약 `hi`를 구간의 최댓값으로 정의하면  
반복문의 조건인 `lo + 1 < hi`에 의해 `lo`는 구간의 최댓값이 될 수 없으므로 정답이 구간의 최댓값인 경우 답을 얻을 수 없다.
<br/><br/>
### 😬 주의사항
* `lo`, `hi` 초기 값 정의에 주의
* `mid`의 overflow에 주의 (Binary Search의 주의사항을 참고)
* 결정 함수 `check()` 구현에 주의 → 특히 부등호
* 답의 범위가 정수처럼 이산적이거나 허용 오차 범위가 있어야 한다.<br/>Binary Search는 연속적인 범위에서 정답에 한없이 가까워질 수는 있지만 정확한 값은 구할 수 없기 때문이다.
<br/><br/>
### 😎 시간복잡도
Binary Search는 `while(lo + 1 < hi)`인 동안 `mid = (lo + hi) >> 1`를 이용해 [`lo`, `hi`]를 [`lo`, `mid`] 또는 [`mid`, `hi`]로 줄여나간다.  
한 번의 loop에서 구간의 길이는 절반으로 줄어들기 때문에 최초 구간의 길이를 N이라 하면 while문의 실행 횟수는 O(logN)번이다.  
while문에서 실행되는 `check(mid)`의 시간복잡도를 O(T)라고 하면, Parametric Search의 최종 시간복잡도는 O(T * logN)이다.
