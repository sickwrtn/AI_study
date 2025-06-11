# AI란?
AI는 하나의 함수다. 입력값을 넣으면 출력이 나오는 함수로 볼수있다.
다만 입력값과 출력값이 텐서(행령)인점이 특이점이라 볼수있다.
## 선형 회귀 (simple linear regression)
선형회귀란? 수많은 점을 그래프 위에 그린다고 치자 그리고 그 점들이 특정한 '규칙'에 의해 찍히고 있다면
규칙을 근사하는 선을 그을수있을것이다.
![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Normdist_regression.png/330px-Normdist_regression.png)
그리고 그 선을 예측함수 라고 하고 H(X) 라고 쓴다. 그럼 이 H(x)는 어떻게 구할까?
### 예측함수
그래프 위에서 특정 규칙에 의해 찍히고 있는 점들 이 점들을 지나는 선을 구하기 위해서는 다항식이 필요하다.
[](https://latex.codecogs.com/svg.image?H(x)=w_nx_n&plus;...&plus;w_2x_2&plus;w_1x_1&plus;b)
다음과 같은 다항식은 x_n에 대한 다변수함수로 구성된다.
