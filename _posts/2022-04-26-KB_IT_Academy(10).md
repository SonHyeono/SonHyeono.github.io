---
title: "데이터 분석을 위한 딥러닝(RNN)"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---

## 기본 지식 

- from tensorflow.keras.layers import Flatten : 1차원으로 바꿔줌.

```python

회귀
Dense(1) # 마지막
model.compile(optimizer='adam', loss='mse')

# 이항분류(0,1)
Dense(1, activation='sigmoid') # 마지막
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['acc'])

# 다중분류(0,1,...,9)
Dense(10, activation='softmax') # 마지막
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['acc'])

# 다중분류(희소벡터 = one-hot-encoding  반환)
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['acc'])

```

- 반복적인 패턴 
- 과거의 행위가 다음 판단에 영향을 미치는 경우
    - 순서가 있는 데이터
        - 한번의 입력 만으로 출력 예측 불가
        - 이번의 입력과 그 이전의 입력을 모두 기억해야 출력 예측 가능
- 주식 데이터를 예측 할 경우 데이터셋이 시간 순서대로 위치해야함.(df의 시작이 최근 데이터부터면 reverse 해줘야함.)



- Vanila RNN
    - 바닐라가 기본이여서 Vanila라는 이름이 붙혀짐. 즉 기본 RNN


---


## 삼성전자 종가 예측하기

```python
import pandas as pd

# url = 'https://raw.githubusercontent.com/SonHyeono/datasets/main/105560.KS.csv'
# url = 'https://raw.githubusercontent.com/SonHyeono/datasets/main/KB_1.csv'
url = 'https://raw.githubusercontent.com/SonHyeono/datasets/main/005930.KS.csv'

samsung = pd.read_csv(url)
samsung
```





  <div id="df-d744e527-2bbf-497d-9121-e3dadb757d89">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-04</td>
      <td>6000.0</td>
      <td>6110.0</td>
      <td>5660.0</td>
      <td>6110.0</td>
      <td>4675.783691</td>
      <td>74195000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-05</td>
      <td>5800.0</td>
      <td>6060.0</td>
      <td>5520.0</td>
      <td>5580.0</td>
      <td>4270.192383</td>
      <td>74680000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-06</td>
      <td>5750.0</td>
      <td>5780.0</td>
      <td>5580.0</td>
      <td>5620.0</td>
      <td>4300.802246</td>
      <td>54390000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-07</td>
      <td>5560.0</td>
      <td>5670.0</td>
      <td>5360.0</td>
      <td>5540.0</td>
      <td>4239.580566</td>
      <td>40305000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-10</td>
      <td>5600.0</td>
      <td>5770.0</td>
      <td>5580.0</td>
      <td>5770.0</td>
      <td>4415.591797</td>
      <td>46880000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5599</th>
      <td>2022-04-20</td>
      <td>67000.0</td>
      <td>67400.0</td>
      <td>66500.0</td>
      <td>67400.0</td>
      <td>67400.000000</td>
      <td>16693293</td>
    </tr>
    <tr>
      <th>5600</th>
      <td>2022-04-21</td>
      <td>67600.0</td>
      <td>68300.0</td>
      <td>67500.0</td>
      <td>67700.0</td>
      <td>67700.000000</td>
      <td>12847448</td>
    </tr>
    <tr>
      <th>5601</th>
      <td>2022-04-22</td>
      <td>67200.0</td>
      <td>67300.0</td>
      <td>66700.0</td>
      <td>67000.0</td>
      <td>67000.000000</td>
      <td>11791478</td>
    </tr>
    <tr>
      <th>5602</th>
      <td>2022-04-25</td>
      <td>66500.0</td>
      <td>66700.0</td>
      <td>66300.0</td>
      <td>66300.0</td>
      <td>66300.000000</td>
      <td>11016474</td>
    </tr>
    <tr>
      <th>5603</th>
      <td>2022-04-26</td>
      <td>66400.0</td>
      <td>66500.0</td>
      <td>66300.0</td>
      <td>66400.0</td>
      <td>66400.000000</td>
      <td>634911</td>
    </tr>
  </tbody>
</table>
<p>5604 rows × 7 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d744e527-2bbf-497d-9121-e3dadb757d89')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d744e527-2bbf-497d-9121-e3dadb757d89 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d744e527-2bbf-497d-9121-e3dadb757d89');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
samsung.columns
```




    Index(['Date', 'Open', 'High', 'Low', 'Close', 'Adj Close', 'Volume'], dtype='object')




```python
samsung[['Adj Close', 'Close']].plot.line(figsize=(20,5))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f21c7a53ad0>




![output_2_1](https://user-images.githubusercontent.com/26592315/165868394-55c6f8be-b98e-47c4-9514-454d4b1ad2d9.png)
    



```python
import tensorflow as tf
import numpy as np

step_size = 4  # 예측을 위한 입력 column 개수, 예측을 위한 날짜 모으는 수
batch_size = 5  

x= [ [[i/10] for i in range(j, j+step_size)] for j in range(batch_size)]
y = [[ (i+step_size)/10] for i in range(batch_size)]
display("x", x, "y", y)
```


    'x'



    [[[0.0], [0.1], [0.2], [0.3]],
     [[0.1], [0.2], [0.3], [0.4]],
     [[0.2], [0.3], [0.4], [0.5]],
     [[0.3], [0.4], [0.5], [0.6]],
     [[0.4], [0.5], [0.6], [0.7]]]



    'y'



    [[0.4], [0.5], [0.6], [0.7], [0.8]]



```python
element_size = 1
model = tf.keras.Sequential([
    tf.keras.layers.SimpleRNN(10, input_shape=[step_size, element_size]),     # 출력노드 10개  , 출력노드 수 (마음대로)
    tf.keras.layers.Dense(element_size)
])

model.summary()
model.compile(optimizer='adam', loss='mse')

model.fit(x, y, epochs=1000, verbose=0)
pred = model.predict(x)
print(f'prediction: {tf.squeeze(pred)}')
```

    Model: "sequential"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     simple_rnn (SimpleRNN)      (None, 10)                120       
                                                                     
     dense (Dense)               (None, 1)                 11        
                                                                     
    =================================================================
    Total params: 131
    Trainable params: 131
    Non-trainable params: 0
    _________________________________________________________________
    prediction: [0.3860347  0.50731605 0.6146359  0.7069057  0.78443253]
    


```python
df = samsung.drop(['Date','Adj Close'],axis=1)
df
```





  <div id="df-411646dd-8748-4bb4-b388-2ca0adc064be">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6000.0</td>
      <td>6110.0</td>
      <td>5660.0</td>
      <td>6110.0</td>
      <td>74195000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5800.0</td>
      <td>6060.0</td>
      <td>5520.0</td>
      <td>5580.0</td>
      <td>74680000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5750.0</td>
      <td>5780.0</td>
      <td>5580.0</td>
      <td>5620.0</td>
      <td>54390000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5560.0</td>
      <td>5670.0</td>
      <td>5360.0</td>
      <td>5540.0</td>
      <td>40305000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5600.0</td>
      <td>5770.0</td>
      <td>5580.0</td>
      <td>5770.0</td>
      <td>46880000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5599</th>
      <td>67000.0</td>
      <td>67400.0</td>
      <td>66500.0</td>
      <td>67400.0</td>
      <td>16693293</td>
    </tr>
    <tr>
      <th>5600</th>
      <td>67600.0</td>
      <td>68300.0</td>
      <td>67500.0</td>
      <td>67700.0</td>
      <td>12847448</td>
    </tr>
    <tr>
      <th>5601</th>
      <td>67200.0</td>
      <td>67300.0</td>
      <td>66700.0</td>
      <td>67000.0</td>
      <td>11791478</td>
    </tr>
    <tr>
      <th>5602</th>
      <td>66500.0</td>
      <td>66700.0</td>
      <td>66300.0</td>
      <td>66300.0</td>
      <td>11016474</td>
    </tr>
    <tr>
      <th>5603</th>
      <td>66400.0</td>
      <td>66500.0</td>
      <td>66300.0</td>
      <td>66400.0</td>
      <td>634911</td>
    </tr>
  </tbody>
</table>
<p>5604 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-411646dd-8748-4bb4-b388-2ca0adc064be')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-411646dd-8748-4bb4-b388-2ca0adc064be button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-411646dd-8748-4bb4-b388-2ca0adc064be');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
df = df.reindex(columns=['Open','High', 'Low','Volume','Close'])
df
```





  <div id="df-de9445e1-f266-4b12-a7f6-b91ab2ff6229">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6000.0</td>
      <td>6110.0</td>
      <td>5660.0</td>
      <td>74195000</td>
      <td>6110.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5800.0</td>
      <td>6060.0</td>
      <td>5520.0</td>
      <td>74680000</td>
      <td>5580.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5750.0</td>
      <td>5780.0</td>
      <td>5580.0</td>
      <td>54390000</td>
      <td>5620.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5560.0</td>
      <td>5670.0</td>
      <td>5360.0</td>
      <td>40305000</td>
      <td>5540.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5600.0</td>
      <td>5770.0</td>
      <td>5580.0</td>
      <td>46880000</td>
      <td>5770.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5599</th>
      <td>67000.0</td>
      <td>67400.0</td>
      <td>66500.0</td>
      <td>16693293</td>
      <td>67400.0</td>
    </tr>
    <tr>
      <th>5600</th>
      <td>67600.0</td>
      <td>68300.0</td>
      <td>67500.0</td>
      <td>12847448</td>
      <td>67700.0</td>
    </tr>
    <tr>
      <th>5601</th>
      <td>67200.0</td>
      <td>67300.0</td>
      <td>66700.0</td>
      <td>11791478</td>
      <td>67000.0</td>
    </tr>
    <tr>
      <th>5602</th>
      <td>66500.0</td>
      <td>66700.0</td>
      <td>66300.0</td>
      <td>11016474</td>
      <td>66300.0</td>
    </tr>
    <tr>
      <th>5603</th>
      <td>66400.0</td>
      <td>66500.0</td>
      <td>66300.0</td>
      <td>634911</td>
      <td>66400.0</td>
    </tr>
  </tbody>
</table>
<p>5604 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-de9445e1-f266-4b12-a7f6-b91ab2ff6229')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-de9445e1-f266-4b12-a7f6-b91ab2ff6229 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-de9445e1-f266-4b12-a7f6-b91ab2ff6229');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
import numpy as np, pandas as pd, matplotlib.pyplot as plt
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler

tf.random.set_seed(0)
seq_length = 7  #  time stamp를 이야기 함. 추적하고 싶은 날짜 수
data_dim = 5    # columns 수

# display(samsung)
# df = samsung
display(df)
values = df.values
# 만약 데이터의 시작이 최근이면 뒤집어야한다. reverse

scaler = MinMaxScaler()
# 0~1 사이로 정규화를 해서 성능을 좋게함.
values_scaled = scaler.fit_transform(values)
# 전체 데이터를 한번에 변환시킴

X, y = [], []
for i in range(0, len(values) - seq_length):        # 그래야지 전체 길이를 check
  start, end = i, i + seq_length
  X.append(values_scaled[start:end])   # end 미만이여서 0 ~ 6 까지 , [ 리스트 ]
  y.append(values_scaled[end, -1])
X, y = np.array(X), np.array(y)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.3, shuffle=False, random_state=0)
X_train.shape, X_test.shape, y_train.shape, y_test.shape


```



  <div id="df-38fbb560-ca09-4962-b99a-332fe041cb82">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6000.0</td>
      <td>6110.0</td>
      <td>5660.0</td>
      <td>74195000</td>
      <td>6110.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5800.0</td>
      <td>6060.0</td>
      <td>5520.0</td>
      <td>74680000</td>
      <td>5580.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5750.0</td>
      <td>5780.0</td>
      <td>5580.0</td>
      <td>54390000</td>
      <td>5620.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5560.0</td>
      <td>5670.0</td>
      <td>5360.0</td>
      <td>40305000</td>
      <td>5540.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5600.0</td>
      <td>5770.0</td>
      <td>5580.0</td>
      <td>46880000</td>
      <td>5770.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5599</th>
      <td>67000.0</td>
      <td>67400.0</td>
      <td>66500.0</td>
      <td>16693293</td>
      <td>67400.0</td>
    </tr>
    <tr>
      <th>5600</th>
      <td>67600.0</td>
      <td>68300.0</td>
      <td>67500.0</td>
      <td>12847448</td>
      <td>67700.0</td>
    </tr>
    <tr>
      <th>5601</th>
      <td>67200.0</td>
      <td>67300.0</td>
      <td>66700.0</td>
      <td>11791478</td>
      <td>67000.0</td>
    </tr>
    <tr>
      <th>5602</th>
      <td>66500.0</td>
      <td>66700.0</td>
      <td>66300.0</td>
      <td>11016474</td>
      <td>66300.0</td>
    </tr>
    <tr>
      <th>5603</th>
      <td>66400.0</td>
      <td>66500.0</td>
      <td>66300.0</td>
      <td>634911</td>
      <td>66400.0</td>
    </tr>
  </tbody>
</table>
<p>5604 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-38fbb560-ca09-4962-b99a-332fe041cb82')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-38fbb560-ca09-4962-b99a-332fe041cb82 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-38fbb560-ca09-4962-b99a-332fe041cb82');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>






    ((3917, 7, 5), (1680, 7, 5), (3917,), (1680,))




```python
model = tf.keras.models.Sequential()
model.add(tf.keras.layers.LSTM(50, input_shape=(seq_length, data_dim), return_sequences=False))
model.add(tf.keras.layers.Dropout(0.3))
model.add(tf.keras.layers.Dense(1))

model.compile(loss='mse', optimizer='adam', metrics=['mae'])
model.summary()
```

    Model: "sequential_2"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     lstm_1 (LSTM)               (None, 50)                11200     
                                                                     
     dropout_1 (Dropout)         (None, 50)                0         
                                                                     
     dense_2 (Dense)             (None, 1)                 51        
                                                                     
    =================================================================
    Total params: 11,251
    Trainable params: 11,251
    Non-trainable params: 0
    _________________________________________________________________
    


```python
print(X_train.shape, y_train.shape)
history = model.fit(X_train, y_train,
                    epochs=200, batch_size=20,
                    validation_split=0.2, verbose=0)
```

    (3917, 7, 5) (3917,)
    


```python
print(history.history.keys())

mae = history.history['mae']
val_mae = history.history['val_mae']
loss = history.history['loss']
val_loss = history.history['val_loss']

epochs = range(1, len(loss) + 1)

plt.figure(figsize=(15,5))
plt.subplot(1,2,1)
plt.plot(epochs, loss, label='Training loss')
plt.plot(epochs, val_loss, label='Validation loss')
plt.title('Training and validation loss')
plt.legend()

plt.subplot(1,2,2)
plt.plot(epochs, mae, label='Training MAE')
plt.plot(epochs, val_mae, label='Validation MAE')
plt.title('Training and validation MAE')
plt.legend()
```

    dict_keys(['loss', 'mae', 'val_loss', 'val_mae'])
    




    <matplotlib.legend.Legend at 0x7f214a4ed390>




    
![output_10_2](https://user-images.githubusercontent.com/26592315/165868386-6251aaea-019a-4dd3-92b1-6bc8ae109226.png)




```python
trainPredict = model.predict(X_train)

plt.figure(figsize=(20,5))
plt.plot(y_train, label='train real')
plt.plot(trainPredict, label='train predicted')
plt.title('Train data prediction')
plt.legend()
```




    <matplotlib.legend.Legend at 0x7f214a4ab790>




![output_11_1](https://user-images.githubusercontent.com/26592315/165868390-13c1120c-3878-44e6-9ca8-1f9b445ad35a.png)
    
    



```python
testPredict = model.predict(X_test)

plt.figure(figsize=(20,5))
plt.plot(y_test, label='test real')
plt.plot(testPredict, label='test predicted')
plt.title('Test data prediction')
plt.legend()  
```




    <matplotlib.legend.Legend at 0x7f214a292710>




    
![output_12_1](https://user-images.githubusercontent.com/26592315/165868392-920b04dd-51b3-4a19-bf60-9e5b7ab5ed34.png)



