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

w_1에 대한 수정된 가중치가 필요하다면

<img src="https://latex.codecogs.com/svg.image?w_1_&plus;=w_1-\alpha\frac{\partial&space;Loss(W,b)}{\partial&space;w_1}" title="w_1_+=w_1-\alpha\frac{\partial Loss(W,b)}{\partial w_1}" />

로 각 w_n에 대해 가중치 수정을 할수있다.

## 다중회귀

입력값과 출력값이 단순 1~2D 텐서에 머무르지 않고 다차원 텐서를 사용가능하도록 하는것이다.

<img src="https://latex.codecogs.com/svg.image?H(X)=\begin{pmatrix}x_1&x_2_1&...&x_n_1\\x_1_2&...&...&...\\...&...&...&...\\x_1_m&...&...&x_n_m\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\end{pmatrix}&plus;\begin{pmatrix}b\\b\\...\\b\end{pmatrix}" title="H(X)=\begin{pmatrix}x_1&x_2_1&...&x_n_1\\x_1_2&...&...&...\\...&...&...&...\\x_1_m&...&...&x_n_m\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\end{pmatrix}+\begin{pmatrix}b\\b\\...\\b\end{pmatrix}" />

X를 n x m 행렬로 보고 계산을 한다. 그렇다면 H(X)는 다음과 같이 표현 가능하다.

<img src="https://latex.codecogs.com/svg.image?\begin{pmatrix}x_1&x_2_1&...&x_n_1\\x_1_2&...&...&...\\...&...&...&...\\x_1_m&...&...&x_n_m\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\end{pmatrix}&plus;\begin{pmatrix}b\\b\\...\\b\end{pmatrix}=\begin{pmatrix}\sum_{i=1}^{n}w_ix_i_1&plus;b\\\sum_{i=1}^{n}w_ix_i_2&plus;b\\...\\\sum_{i=1}^{n}w_ix_i_m&plus;b\end{pmatrix}" title="\begin{pmatrix}x_1&x_2_1&...&x_n_1\\x_1_2&...&...&...\\...&...&...&...\\x_1_m&...&...&x_n_m\\\end{pmatrix}\begin{pmatrix}w_1\\w_2\\...\\w_n\end{pmatrix}+\begin{pmatrix}b\\b\\...\\b\end{pmatrix}=\begin{pmatrix}\sum_{i=1}^{n}w_ix_i_1+b\\\sum_{i=1}^{n}w_ix_i_2+b\\...\\\sum_{i=1}^{n}w_ix_i_m+b\end{pmatrix}" />

이걸 보면 알수있듯 X가 n x m 행렬이라면 H(X)는 m 행렬이라는 것이다.

그리고 손실함수와 역전파를 해준다면 가중치 수정이 가능하다.

## 인공신경망과 다층 퍼셉트론

선형회귀는 정확히는 인공신경망은 아니다.

인공신경망은 다층 퍼셉트론으로 이루어져야 하는데 여기서 퍼셉트론이란

선형회귀에 활성화 함수를 더해둔 것이라고 할수있다.

다층 퍼셉트론은 이 퍼셉트론을 여러개 연결시킨것이라 할수있다.

### 활성화 함수
활성화 함수인 시그모이드 함수는 순전파중 H(X)를 구하는 과정에서 이 H(X)를 0~1까지의 범위로 제한시킨다.

![](https://blog.kakaocdn.net/dn/sib2q/btsDJkfaBMy/pkKQYrLYXHVDODrXvQNqK0/img.png)

수식으로 쓰자면 

<img src="https://latex.codecogs.com/svg.image?H(x)=\phi(WX&plus;b)" title="H(x)=\phi(WX+b)" />

이렇게 쓸수있다. 여기서 phi가 시그모이드 함수이다.

### 왜 활성화 함수를 쓰는가?

만약 모델을 여러개 연결시켜 가중치를 연결시킨다면 문제가 생긴다.

<img src="https://latex.codecogs.com/svg.image?H(H(x))=W(WX)=W^2X" title="H(H(x))=W(WX)=W^2X" />

분명 모델을 두번 사용했지만 한번사용한것과 별다른 차이점을 두지 못하게 되어버린다.

그렇기 때문에 활성화 함수가 필요한것이다.

<img src="https://latex.codecogs.com/svg.image?H(\phi(H(x)))=W(\phi(WX))" title="H(\phi(H(x)))=W(\phi(WX))" />

이렇게 하면 모델을 연결한 효과를 볼수있다.

### 다층 퍼셉트론

다층 퍼셉트론이란? 

![](https://wikidocs.net/images/page/61010/ann.PNG)

우리가 자주 보는 AI 딥러닝 이미지다. 보다 싶이 은닉층(가중치 행렬)이 한개가 아닌 여러개가 서로 연결되어있는 구조를 지닌다.

그리고 이것이 바로 진짜 인공신경망이자. 딥러닝이다.

우리는 은닉층이 두개인 모델을 만들어보자.

수식으로 쓴다면 다음과 같다.

<img src="https://latex.codecogs.com/svg.image?Neuron(X)=hidden_2\circ\phi\circ&space;hidden_1(X)" title="Neuron(X)=hidden_2\circ\phi\circ hidden_1(X)" />

i번째 은닉층을 수식으로 표현하면 이렇다.

<img src="https://latex.codecogs.com/svg.image?&space;hidden_p(X)=\begin{pmatrix}x_1&...&x_n\\\end{pmatrix}\begin{pmatrix}w^p_1_1&\cdots&w^p_n_1\\\vdots&\ddots&\vdots\\w^p_1_m&\cdots&w^p_n_m\\\end{pmatrix}=\begin{pmatrix}\sum_{i=1}^{m}w^p_1_i\cdot&space;x_i&\cdots&\sum_{i=1}^{m}w^p_n_i\cdot&space;x_i\\\end{pmatrix}" title=" hidden_p(X)=\begin{pmatrix}x_1&...&x_n\\\end{pmatrix}\begin{pmatrix}w^p_1_1&\cdots&w^p_n_1\\\vdots&\ddots&\vdots\\w^p_1_m&\cdots&w^p_n_m\\\end{pmatrix}=\begin{pmatrix}\sum_{i=1}^{m}w^p_1_i\cdot x_i&\cdots&\sum_{i=1}^{m}w^p_n_i\cdot x_i\\\end{pmatrix}" />




