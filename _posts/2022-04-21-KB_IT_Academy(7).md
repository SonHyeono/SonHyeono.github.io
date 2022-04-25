---
title: "데이터 분석을 위한 딥러닝(DNN)"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---


## 딥러닝

## Tip

- train과 test를 표준화 할 때는 train과 test의 mean과 std로 해야하고. 만약 train의 mean과 std로 할 경우 기준이 동일해야해서 test데이터에도 train의 mean과 std로 적용해야한다.

- input_shape에는 튜플 형태로 들어가야함. ex) input_shape=(x_tr.shape[1], ) 

- Dense에서 예측 값이 회귀이면 activation이 linear( linear는 기본값이여서 생략 가능 )이고 마지막 출력은 1 이다.

- Dense에서 이진분류 경우, 마지막 출력은 1, activation = 'sigmoid'

- Dense에서 다항분류의 경우, activation = 'softmax', 마지막 출력은 다수 

- batch_size를 주지않으면 train 데이터를 한꺼번에 읽음

## 기본 지식

- Artificial Neural Network
    
    - Artificial 인공
    - Neural 신경
    - Network 망

- NN의 근간은 Logistic Regression
- 입력값 * 가중치 + 편향 => 예측값(선형회귀) => Sigmoid() 적용 -> 성공할 확률 -> 가설

- Framework
    - TensorFlow ( 기능이 많으나 사용하기 어렵다 )
    - PyTorch ( 물체감지에 특화, Torch를 python으로 )
    - Keras ( TensorFlow를 쉽게 사용하도록 만듬, 지금은 TensorFlow와 한 몸 )

- TPU : TensorFlow 처리 전용

- GAN : 가짜를 만들어내는 인공지능

- [이미지, 사운드를 손쉽게 학습할 수 있는 사이트](https://teachablemachine.withgoogle.com/)

- Perceptron을 Node라고도 부름.

- Perceptron을 가지고 있는 덩어리를 Layer라고 함.




---

## DNN

- Perceptron(퍼셉트론)
    - 생물학적 뇌의 뉴런을 모방하여 만든 인공신경망의 기본 단위
    - 여러 입력을 값으로 받아 하나의 0 ~ 1을 출력하는 함수
    - 뇌의 신경세포 즉, 뉴런과 같은 역할

- Activation 함수 ( output으로 값을 전달 )
    - Sigmoid 
    - z 값을 0과 1사이의 값으로 바꾸는 함수


- Multi-Layer Perceptron의 필요성
    - 비 선형 문제
    - 대표적 사례 : XOR 문제
    - 고차원 다항식

- Multi-Layer Perceptron
    - Single-Layer Perceptron
        - 하나의 Perceptron 만을 이용
        - Logistic Regression
    - Multi-Layer Perceptron
        - 여러개의 퍼셉트론 이용
        - Hidden-Layer
            - 정확한 상태를 알 수 없다.


- Activation functions
    - sigmoid
    - tanh
    - ReLUs
    - Leaky ReLU : max(0, x)
    - Maxout
    - ELU
    - Activation 함수 선택 방법
        - Sigmoid를 Hidden Layer에 사용하지 말 것
        - Hidden Layer에 ReLU를 우선적으로 적용
        - 개선을 위해 기타 ReLU 계열 함수 시도


- Backpropagation
    - Chain Rule    

- Gradient Decent Optimizer
    - 기울기 미분 계산 및 가중치 업데이트 자동화 도구
    - W = W - learning_rate * gradient
    - learning_rate 또는 gradient에 운동량 반영할 수학식 추가
    - tk.keras.optimizers
        - Optimizer(learning_rate) : Base Class, 직접 사용 불가
            - learning_rate: 0.1 ~ 0.0001
        - SGD : 확률적 경사하강법
        - RMSprop : 일반 운동 모멘텀
        - Adam (실제 많이 사용) : 1차 및 2차 모멘트 적응적 추정 
        - Adadelta : 차원마다 적응적 learning_rate
        - Adagrad : 파라미터 별 learning_rate 최적화
        - Adamax : Max Norm 을 기반으로 한 Adam의 변형
        - Nadam : Nesterov 모멘텀 + Adam

- Keras API - Layer
    - LayerNeural Network의 하나의 Layer를 추상화
    - tk.keras.layers.Dense(units, activation, use_bias, kernel_initializer, bias_initilizer ... )
        - 가장 일반적인 DNN의 완전 연결층(밀집층)
        - units: 출력 노드 개수 ( 필수, 출력 shape, 샘플 축 생략 )
        - input_shape: 첫 번째 층인 경우 사용 ( input_shape는 반드시 튜플 형태, ex) input_shape(X_train.shape[1] , )  )
        - 예) Dense(32, input_shape=(784,)) : 입력 n x 784, 출력: 32


||layer내 마지막 Dense의 activation(활성화 함수)|compile() 함수내 파라미터 loss (손실 함수)|
|---|---|---|
|회귀|linear(기본이기에 생략)|mse  / 마지막 Dense의 출력값은 1|
|이진분류|sigmoid|binary_crossentropy /  마지막 Dense의 출력값은 1|
|다중분류|softmax|[sparse_]categorical_crossentropy / 마지막 Dense의 출력값은 분류 종류 개수|

- categorical_crossentropy -> 종속 변수는 one-hot-encoding 형태로 반환
    - 답이 0 0 0 => 2로 해석
- sparse_categorical_crossentopy -> 종속 변수는 숫자형태로 반환
    - 답 2로 반환


- 첫번째 Dense()내 input_shape 값은 X의 칼럼갯수를 지정한다.

- layer내 모든 Dense의 activation은 relu를 지정한다

---


- Keras API - Model, Sequential
    - tf.keras.Sequential(layers)
        - tf.keras.Model을 상속
        - layers : 순서를 갖는 Layer stack 생성
        - add(layer): 계층 추가
        - compile(optimizer, loss, metrics, ...) : 훈련을 위한 모델 설정
            - optimizer : tf.keras.optimizers에 있는 객체 또는 이름(str)   (필수 파라미터)
            - loss : tf.keras.losses내의 객체 또는 이름(str)    (필수 파라미터)
            - metrics : 훈련과 테스트 과정에서 평가할 항목       (옵션 파라미터)
        - summary() : Network의 층과 파라미터 갯수 출력
        - history = fit(x,y, batch_size, epochs, verbose, callbacks, validation_split, validation_data ... ) : 모델 학습
            - history: 학습 동안의 loss 등의 매트릭 기록
                - history: dictionary, 기록 항목 별
        - evaluate(x, y ...) : 테스트 결과 반환
        - predict(x, ...) : 예측 결과
        - save(filepath, ...) : 모델 파일 저장
        - trainable_variables: 학습할 변수 목록

    - tf.models.load_model(filepath): 모델 복원

    
- Vanishing Gradient
    - sigmoid 함수를 사용하면 input값들이(x1, x2, x3, ..., xn) layer을 거치면서 0에 수렴
    - 0에 수렴하는 값들이 다른 layer의 input 값으로 입력된다.
    - 입력된 값들은 layer를 거치면서 0에 수렴
    - x1, x2, x3, ... , xn의 값은 최종으로 출력 되는 값에 영향이 없다
    - cost가 줄어들지 않는다.
    

- 이진분류
    - IMDB 데이터셋을 이용한 이진분류 실습
    
    - imdb.load_data(~)
        - path='imdb.npz' 
        - num_word=None: 정수, 고려한 가장 빈번한 단어, 드문 단어는 oov_char로 대체
        - 


- Callback

    - 매 batch 때 마다 호출할 함수 전달
        - model.fit(callbacks=[cb])
    - tf.keras.callbacks.Callback
        - callback 생성을 위한 base class, 상속해서 구현
        - on_train_batch_begin(): 훈련 배치 시작
        - on_train_batch_end() : 훈련 배치 끝
        - on_test_batch_begin(): 테스트 배치 시작
        - on_test_batch_end: 테스트 배치 끝

    - 미리 구현된 Callback 클래스들
        - tf.keras.callbacks
            - EarlyStopping
            - TensorBoard
            - ModelCheckpoint
    
- 다항 분류
    - 여러 클래스를 분류하는 방법
        - 각 클래스별 Weight 계산 필요
        - 이진 분류기를 여러 번 쓰는 것
        - 하나의 행렬로 계산
        - 이진 분류기를 여러 번 쓰는 방법에 비해 행렬 연산을 하는 것이 효과적
    - 범주형 데이터를 숫자로 표현할 방법 필요
        - One-Hot Encoding
    - 출력 층 활성화 함수 - Softmax
        - 여러 클래스에 대한 각각의 H(x)를 확률로 변형 필요
        - Sigmoid 대신 Softmax 함수 사용