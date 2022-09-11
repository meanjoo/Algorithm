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

* 반시계 방향 회전 ⇔ z 성분이 양수
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/ccw.jpg" width="400" height=auto/>

* 시계 방향 회전 ⇔ z 성분이 음수
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/cw.jpg" width="430" height=auto/>

* 일직선(평행) ⇔ z 성분이 0
<img src="https://github.com/meanjoo/Algorithm/blob/main/%EA%B8%B0%ED%95%98/parallel.jpg" width="430" height=auto/>
