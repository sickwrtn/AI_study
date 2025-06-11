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

![](https://latex.codecogs.com/svg.image?H(X)=w_nx_n&plus;...&plus;w_2x_2&plus;w_1x_1&plus;b)

다음과 같은 다항식은 x_n에 대한 다변수함수로 구성된다.

이 함수로 실수계수 다항식으로 표현가능한 모든 함수를 표현 가능하다.

그리고 이 식은 다음과 같이 변환 가능하다.

<img src="https://latex.codecogs.com/svg.image?w_1x_1&plus;w_2x_2&plus;...&plus;w_nx_n&plus;b=\begin{pmatrix}x_1&x_2&...&x_n\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\\\end{pmatrix}&plus;\begin{pmatrix}b\\b\\...\\b\end{pmatrix}" title="w_1x_1+w_2x_2+...+w_nx_n+b=\begin{pmatrix}x_1&x_2&...&x_n\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\\\end{pmatrix}+\begin{pmatrix}b\\b\\...\\b\end{pmatrix}" />

그리고 이걸 X,W,b로 묶는다면

<img src="https://latex.codecogs.com/svg.image?H(X)=WX&plus;b" title="H(X)=WX+b" />

이게 바로 AI의 모델이다.

## 순전파
만약 학습시킬 데이터 T_x,T_y 에 대해 학습한다면 현재 모델에 T_x에 대한 값을 먼저 구해야 한다.

<img src="https://latex.codecogs.com/svg.image?H(T_x)=WT_x&plus;b" title="H(T_x)=WT_x+b" />

<img src="https://latex.codecogs.com/svg.image?H(T_x)=\begin{pmatrix}t_x_1&t_x_2&...&t_x_n\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\end{pmatrix}&plus;\begin{pmatrix}b\\b\\...\\b\end{pmatrix}=\sum_{i=1}^{n}w_it_x_i&plus;b" title="H(T_x)=\begin{pmatrix}t_x_1&t_x_2&...&t_x_n\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\end{pmatrix}+\begin{pmatrix}b\\b\\...\\b\end{pmatrix}=\sum_{i=1}^{n}w_it_x_i+b" />
## 손실함수
손실함수란 예측값과 실제값의 차이를 계산하는 함수라 할수있다.

선형 회귀에서는 평균 제곱 오차(MSE, Mean Squared Error)를 사용한다.

방금전 H(T_x)를 구했으니 평균 제곱 오차는 다음과 같이 구할수있다.

<img src="https://latex.codecogs.com/svg.image?Loss(W,b)=(H(T_x)-T_y)^2" title="Loss(W,b)=(H(T_x)-T_y)^2" />

## 경사하강법과 역전파

이제 손실함수와 순전파에서 나온 값을 토대로 가중치를 수정해야한다.

그리고 가중치를 수정하기위해 사용하는게 경사하강법이다.

![](https://velog.velcdn.com/images/rjtp5670/post/5493bb60-73f3-4701-93a7-0f5feb828fc3/image.png)

경사하강법은 함수의 최소값을 알아내기위한 알고리즘이다. 미분으로 현재 어느 방향이 더 저점으로 가는 방향인지 구하고 정해진 학습률에 따라 하강하는 방법이다.

경사하강법에 따라 우리는 수정될 가중치를 W+ 라고 표현한다면

<img src="https://latex.codecogs.com/svg.image?W_&plus;=W-\alpha\frac{\partial&space;Loss(W,b)}{\partial&space;W}" title="W_+=W-\alpha\frac{\partial Loss(W,b)}{\partial W}" />

여기서 알파가 학습률이다.

