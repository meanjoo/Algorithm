CCW는 Counter Clockwise의 약자로, 평면 위에 놓여진 세 점의 방향 관계를 알아낼 수 있는 알고리즘이다.  
CCW는 외적(cross product, vector product)을 이용하므로 외적에 대해 알아야 한다.

### :blush: 외적(cross product, vector product)
두 벡터 a, b가 있을 때 외적 **a** × **b**의 결과는 벡터 a와 b에 모두 수직이 되는 벡터이다.  
벡터의 외적은 3차원에서만 정의되는데, 2차원 벡터의 z 성분을 0이라고 두면 2차원 벡터에 대한 외적을 구할 수 있다.  
외적을 통해 2차원 벡터에 관한 방향 정보를 알 수 있다.

<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/crossproduct.jpg" width="800" height=auto/>

2차원 벡터의 외적에서 z 성분인 ***x<sub>1</sub>y<sub>2</sub> - y<sub>1</sub>x<sub>2</sub>*** 의 부호에 따라 **a** 뒤에 **b**를 놓았을 때 어느 방향(시계 or 반시계)으로 회전하는지 알 수 있다.  

오른손의 엄지를 제외한 네 손가락을 시작 벡터(**a**) 방향으로 두고, 이 손가락들을 다른 벡터(**b**)쪽을 향하게 감았을 때  
엄지의 방향이 외적 방향이다.  
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/explanation.jpg" width="700" height=auto/>

* 반시계 방향 회전 ⇔ z 성분이 양수
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/ccw.jpg" width="400" height=auto/>

* 시계 방향 회전 ⇔ z 성분이 음수
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/cw.jpg" width="430" height=auto/>

* 일직선(평행) ⇔ z 성분이 0  
외적의 크기는 |a×b| = |a||b|sin&theta;이다. &theta;=0이거나 &theta;=&pi;일 때 sin&theta;=0이므로 외적이 0이다.
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/parallel.jpg" width="430" height=auto/>

즉 2차원 벡터 2개를 2×2 행렬식을 구하는 것과 비슷한 방식으로 계산하면 이 값의 부호에 따라 다음 벡터의 진행 방향을 알 수 있다.
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/formal.jpg" width="400" height=auto/>
<br/><br/>
### :blush: 평면 위 세 점의 방향 관계
주어진 정보가 2차원 상의 벡터가 아닌 2차원 상의 점인 경우에 대해 알아보자.  
평면 상의 점 A, B, C가 순서대로 어떤 방향을 이루고 있는지는 점 3개를 순서대로 이은 두 선분의 방향과 같고, 결국 2차원 벡터의 경우와 같다.  
(∵ 벡터는 점 A에서 점 B로 향하는 방향과 크기가 주어진 선분)

2차원 벡터를 통해 평면 상의 세 점 A(x<sub>1</sub>, y<sub>1</sub>), B(x<sub>2</sub>, y<sub>2</sub>), C(x<sub>3</sub>, y<sub>3</sub>)가 어떤 방향을 이루고 있는지 구하는 방법은 두 가지가 있다.  
① 점 A를 시점으로 하는 점 A에 대한 점 B의 위치벡터 **AB**와 점 A에 대한 점 C의 위치벡터 **AC**의 외적  
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/cp1.jpg" width="600" height=auto/>

② 벡터 **AB**와 벡터 **BC**의 외적  
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/cp2.jpg" width="600" height=auto/>

①과 ②의 외적은 다음과 같다.  
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/cp_result1.jpg" width="600" height=auto/>

①과 ②의 z 성분을 각각 풀어서 써보면 결국 둘은 같은 값을 나타내고 있음을 알 수 있다.  
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/cp_result2.jpg" width="700" height=auto/>

:heavy_check_mark: 위처럼 어렵게 빼는 성분의 순서를 기억해서 계산하지 않고, 신발끈 공식을 이용하면 쉽게 계산할 수 있다.  
단, 이때 공식에 작성하는 점의 순서를 주의해야 한다. ***어떤 방향으로 놓여있는지 알아낼 세 점의 순서대로 작성***해야 한다.  
마찬가지로 구해진 값의 부호에 따라 세 점의 방향 관계를 알 수 있다. (양수: 반시계, 음수: 시계, 0: 일직선/평행)  
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/formal2.jpg" width="900" height=auto/>
```
typedef struct point {
  int x, y;
}Point;

int CCW(Point p1, Point p2, Point p3) {
  int result = p1.x * p2.y + p2.x * p3.y + p3.x * p1.y - p2.x * p1.y - p3.x * p2.y - p1.x * p3.y;
  if (result > 0)		// ccw
    return 1;
  else if (result < 0)	// cw
    return -1;
  else	// parallel
    return 0;
}
```
코드를 작성할 때 고려해야 할 부분은 Point와 (특히) result의 자료형이다.  
신발끈 공식에서 점들이 곱해지므로 overflow가 발생할 가능성이 있는지 생각해봐야 한다. (int로 커버가능한지, 안 되면 long long)
