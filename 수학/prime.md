정수 a가 b로 나누어떨어지는 경우, b를 a의 **인수**(factor) 또는 **약수**(divisor)라고 한다.  
n > 1인 어떤 정수 n에 대해 양의 인수가 1과 n뿐이면 n을 **소수**(prime)라고 한다.  
n > 1인 모든 정수에 대해 아래와 같은 꼴의 유일한 **소인수 분해**(prime factorization)가 존재한다.  
> n = p<sub>1</sub><sup>α1</sup>p<sub>2</sub><sup>α2</sup>...p<sub>k</sub><sup>αk</sup>  
> (p<sub>1</sub>, p<sub>2</sub>, ..., p<sub>k</sub>는 서로 다른 소수이고, α1, α2, ..., αk는 양의 정수이다.)

### :blush: 소수 구하기(에라토스테네스의 체)
소수는 에라토스테네스의 체(Sieve of Eratosthenes)를 통해 효율적으로 구할 수 있다.  
에라토스테네스의 체는 2 이상 n 이하의 정수 x가 소수인지를 효율적으로 판별할 수 있도록 sieve 배열을 만드는 전처리 알고리즘이다.  
x(2 ≤ x ≤ n)가 소수인지를 판별하는 sieve(bool) 배열을 만드는 코드이다.  
sieve의 크기는 n + 1이고, 초기 값은 false이다.  
```
void era() {
  for (int i = 2; i <= n; i++) {
    if (sieve[i]) continue;
    // prime.push_back(i); // 2 이상 n 이하의 소수를 저장하고 있는 배열을 만들 수 있다.
    for(int j = 2 * i; j <= n; j += i)
      sieve[j] = true;
  }
}
```
ex) n = 20일 때의 sieve  
|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|F|F|T|F|T|F|T|T|T|F|T|F|T|T|T|F|T|F|T|

체(sieve)에 걸러지는 것(=true)은 소수가 아니다.

:heavy_check_mark: 시간복잡도: O(n log logn)

### :blush: n의 소수 판정
정수 n이 소수가 아니라면 n을 두 정수의 곱 a * b로 나타낼 수 있고, 이때 a ≤ &radic;n 또는 b ≤ &radic;n이 성립한다.  
즉 n이 소수가 아니라면 2 이상 ⌊&radic;n⌋ 이하의 인수가 반드시 존재한다.  
n을 2 이상 ⌊&radic;n⌋ 이하의 모든 정수로 나누어봤을 때, n이 나누어떨어지는 경우가 없다면 소수이다.
```
bool isPrime(int n) {
  if (n < 2) return false;
  for (int i = 2; i * i <= n; i++) {
    if (n % i == 0)
      return false;
  }
  return true;
}
```

### :blush: n의 소인수 분해(모든 소인수를 벡터에 저장)
① 방법 1 (소인수가 f에 오름차순으로 저장된다.)
```
void pf(int n) {
  for (int i = 2; i * i <= n; i++) {
    while (n % i == 0) {
      f.push_back(i);
      n /= i;
    }
  }
  if (n > 1) // 제곱근까지 나누어떨어지지 않으면 소수이다.
    f.push_back(n);
}
```
② 에라토스테네스의 체를 확장하여 소인수 분해 (f에 저장된 소인수가 오름차순이 아닐 수 있다.)  
에라토스테네스의 체를 이용해서 sieve(int)에 각각의 수 k에 대해 가장 작은 소인수를 저장한다.  
sieve를 이용하여 2 이상 n 이하의 모든 수를 소인수 분해 할 수 있다.  
sieve의 크기는 n + 1이고, 초기 값은 0이다.
```
void era() {
  for (int i = 2; i <= n; i++) {
    if (sieve[i] > 0) continue;
    for (int j = i; j <= n; j += i)
      sieve[j] = min(i, sieve[j]);
  }
}

void pf(int n) {
  while (n > 1) {
    f.push_back(sieve[n]);
    n /= sieve[n];
  }
}
```
ex) n = 20일 때의 sieve  
|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|2|3|2|5|2|7|2|3|2|11|2|13|2|3|2|17|2|19|2|
