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

2차원 벡터 2개에 신발끈 공식을 활용하면 이 값의 부호에 따라 다음 벡터의 진행 방향을 알 수 있다.
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/formal.jpg" width="400" height=auto/>
<br/><br/>
### :blush: 평면 위 세 점의 방향 관계
주어진 정보가 2차원 상의 벡터가 아닌 2차원 상의 점인 경우에 대해 알아보자.  
평면 상의 점 A, B, C가 순서대로 어떤 방향을 이루고 있는지는 점 3개를 순서대로 이은 선의 방향과 같다.

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
