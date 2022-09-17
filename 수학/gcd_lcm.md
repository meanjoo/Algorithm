두 정수 a, b가 있다.  
a와 b의 GCD(Greatest Common Divisor, 최대공약수)는 a와 b의 공통된 약수 중 가장 큰 수이다. gcd(a, b) == 1은 a와 b는 서로소임을 뜻한다.  
a와 b의 LCM(Lowest Common Multiple, 최소공배수)은 a와 b의 공통된 배수 중 가장 작은 수이다.  

a * b = gcd(a, b) * lcm(a, b)이므로 **lcm(a, b) = a * b / gcd(a, b)** 를 만족한다.  
(두 정수의 곱은 두 정수의 최대공약수와 최소공배수의 곱과 같다. [증명])  

따라서 우리는 최대공약수만 구할 수 있다면 최소공배수를 구할 수 있다.  
gcd(a, b)를 효율적으로 계산하는 방법인 유클리드 알고리즘(Euclid's algorithm)이 있다.

#### :cowboy_hat_face: pf) 두 정수의 곱은 두 정수의 최대공약수와 최소공배수의 곱과 같다.  
