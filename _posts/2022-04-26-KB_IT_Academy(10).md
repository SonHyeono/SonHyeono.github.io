---
title: "데이터 분석을 위한 딥러닝(RNN)"
categories:
  - KB 국민은행 IT 아카데미
feature_text: |
  The History of the KB 국민은행 IT 아카데미 IT's Your Life
---

## 기본 지식

- 반복적인 패턴 
- 과거의 행위가 다음 판단에 영향을 미치는 경우
    - 순서가 잇는 데이터
        - 한번의 입력 만으로 출력 예측 불가
        - 이번의 입력과 그 이전의 입력을 모두 기억해야 출력 예측 가능
- 주식 데이터를 예측 할 경우 데이터셋이 시간 순서대로 위치해야함.(df의 시작이 최근 데이터부터면 reverse 해줘야함.)



- Vanila RNN
    - 바닐라가 기본이여서 Vanila라는 이름이 붙혀짐. 즉 기본 RNN
