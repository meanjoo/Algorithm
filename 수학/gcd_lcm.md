두 정수 a, b가 있다.  
a와 b의 GCD(Greatest Common Divisor, 최대공약수)는 a와 b의 공통된 약수 중 가장 큰 수이다. gcd(a, b) == 1은 a와 b는 서로소임을 뜻한다.  
a와 b의 LCM(Lowest Common Multiple, 최소공배수)은 a와 b의 공통된 배수 중 가장 작은 수이다.  

a * b = gcd(a, b) * lcm(a, b)이므로 **lcm(a, b) = a * b / gcd(a, b)** 를 만족한다.  
(두 정수의 곱은 두 정수의 최대공약수와 최소공배수의 곱과 같다. [증명](https://github.com/meanjoo/Algorithm/blob/main/%EC%88%98%ED%95%99/gcd_lcm.md#cowboy_hat_face-pf-%EB%91%90-%EC%A0%95%EC%88%98%EC%9D%98-%EA%B3%B1%EC%9D%80-%EB%91%90-%EC%A0%95%EC%88%98%EC%9D%98-%EC%B5%9C%EB%8C%80%EA%B3%B5%EC%95%BD%EC%88%98%EC%99%80-%EC%B5%9C%EC%86%8C%EA%B3%B5%EB%B0%B0%EC%88%98%EC%9D%98-%EA%B3%B1%EA%B3%BC-%EA%B0%99%EB%8B%A4))  

따라서 우리는 최대공약수만 구할 수 있다면 최소공배수를 구할 수 있다.  
gcd(a, b)를 효율적으로 계산하는 방법인 유클리드 알고리즘(Euclid's algorithm)이 있다. 이 알고리즘은 아래의 공식을 기반으로 한다.  

<img src="https://github.com/meanjoo/LinkPicture/blob/main/euclid.JPG" />

두 수를 a, b라 하고, c를 a mod b라고 하자.  
c를 구하고 a에 b를, b에 c를 대입하는 과정을 b가 0이 될 때까지 반복한다.  
b가 0일 때의 a가 gcd(a, b)이다.

구현은 간단하게 가능하다.  
```
int gcd(int a, int b) {
  if (b == 0) return a;
  return gcd(b, a % b);
}
```

```
int lcm(int a, int b) {
  return a * b / gcd(a, b);
}
```

#### :cowboy_hat_face: pf) 두 정수의 곱은 두 정수의 최대공약수와 최소공배수의 곱과 같다.  
<img src="https://github.com/meanjoo/LinkPicture/blob/main/gcdlcmrelation.jpg" />

위 그림에서 세 가지 정보를 알아낼 수 있다.  
① a = gcd(a, b) * a'  
② b = gcd(a, b) * b'  
③ lcm(a, b) = gcd(a, b) * a' * b'  

a * b = gcd(a, b) * a' * gcd(a, b) * b' (①, ②)  
a * b = gcd(a, b) * gcd(a, b) * a' * b'  
a * b = gcd(a, b) * lcm(a, b) (③)  

Q.E.D.
