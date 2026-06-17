# AutoEncoder와 SVR 기반 수위 데이터 분석 프로젝트

> 두 지역(여수, 통영)의 시계열 데이터를 활용하여  
> AutoEncoder와 SVR 모델의 성능을 비교 분석한 프로젝트

---

## 프로젝트 소개

본 프로젝트는 폭우 및 기후 변화로 인해 발생하는 수위 이상 상황을 보다 효율적으로 분석하고 예측하기 위해  
AutoEncoder와 SVR(Support Vector Regression) 모델을 활용한 데이터 분석을 수행한다.

여수와 통영 두 지역 데이터를 기반으로  
모델별 성능을 비교 분석한다.

---

## 지역 선정 이유

여수와 통영은 해안 지역으로 강수량 변동이 크고  
폭우 발생 가능성이 높은 지역이다.

특히 여수는 비교적 높은 강수량 특성을 가지므로  
이상 탐지 및 수위 예측 모델을 검증하기에 적합한 데이터 환경을 제공한다.

---

## 문제 정의

- 기존 수위 감지 시스템의 실시간성 및 정확도 한계  
- 다양한 기상 변수로 인한 데이터 복잡성 증가  
- 단일 모델로는 데이터 구조 및 예측을 동시에 만족하기 어려움  

---

## 연구 목표

- AutoEncoder 기반 이상 탐지 성능 분석  
- SVR 기반 수위 예측 성능 분석  
- 지역별 데이터 특성 차이 분석  

---

## 모델 설명

### AutoEncoder

- 입력 데이터 압축 및 패턴 학습  
- 정상 패턴 기반 anomaly detection 수행  

#### 특징
- 비선형 패턴 학습 가능  
- 이상 탐지에 강점  

---

### SVR (Support Vector Regression)

- 회귀 기반 예측 모델  
- 미래 강수량(수위) 예측  

#### 특징
- 안정적인 예측 성능  
- 작은 데이터에서도 강건  

---

## Baseline 모델

본 프로젝트에서는 LSTM 기반 강수량 예측 모델을 baseline으로 사용하였다.

https://github.com/Suchetha21/Rainfall-Prediction-LSTM

---

## 데이터셋

### 데이터 출처

기상청 기상자료개방포털 (ASOS 데이터)

https://data.kma.go.kr/data/grnd/selectAsosRltmList.do?pgmNo=36&tabNo=1  

---

### 데이터 특징

본 데이터셋은 약 6.48MB 규모로,  
총 132,464개의 시계열 데이터와 8개의 기상 변수를 포함한다.

---

## 데이터 전처리

- 결측치 제거  
- 표준화 (StandardScaler)  
- 30분 단위 리샘플링  
- Sliding Window 적용  

---

## 사용 기술

### Language
- Python  

### Libraries
- TensorFlow / Keras (AutoEncoder)  
- scikit-learn (SVR)  
- Pandas  
- NumPy  
- Matplotlib  

### Data Processing
- StandardScaler  
- Time Series Resampling  
- Sliding Window  

---

## 환경 설정

pip install pandas numpy matplotlib scikit-learn tensorflow openpyxl

---

## 실행 방법

다음 두 모델을 각각 실행하여 결과를 확인할 수 있다.

### AutoEncoder

python autoencoder.py

출력:
- Reconstruction 그래프  
- Scatter Plot  
- 이상 탐지 결과  

---

### SVR

python svr.py

출력:
- 시계열 예측 그래프  
- Scatter Plot  

---

### 실행 흐름

1. Excel 데이터 로드 및 병합  
2. datetime 기준 정렬  
3. 30분 단위 리샘플링  
4. 결측치 처리 및 정규화  
5. Sliding Window 적용  
6. 모델 학습  
7. 결과 시각화 및 성능 평가  

---

# 실험 결과

---

## 여수 (Yeosu)

### AutoEncoder
- MSE: 0.009759

#### 결과

[Yeosu AutoEncoder]

<img width="324" height="184" alt="yeosu_ae" src="https://github.com/user-attachments/assets/3e1d3691-eb97-48a8-9786-18ec4449d78d" />

#### 분석
- 정상 구간에서 높은 재현 정확도  
- 폭우 구간에서 reconstruction error 증가  

이상 탐지 성능이 우수함.

---

### SVR
- MSE: 0.010719

#### 결과

[Yeosu SVR]

<img width="334" height="182" alt="yeosu_svr" src="https://github.com/user-attachments/assets/af257c88-54e3-4de4-b19e-a8c32d4ba756" />

#### 분석

- 전반적으로 Actual과 Predicted가 거의 일치  
- 폭우 구간에서도 정확하게 추종  
- 급격한 상승 패턴도 안정적으로 예측  

높은 예측 정확도를 보인다.

---

## 통영 (Tongyeong)

### AutoEncoder
- MSE: 약 0

#### 결과

[Tongyeong AutoEncoder]

<img width="308" height="169" alt="tongyeong_ae" src="https://github.com/user-attachments/assets/d972abb1-04d5-4ed8-864f-2f8a27de7156" />

#### 분석
- 전체적으로 매우 높은 재구성 성능  
- 반복 패턴을 안정적으로 학습  

재현 성능이 매우 우수함.

---

### SVR
- MSE: 0.010541

#### 결과

[Tongyeong SVR]

<img width="334" height="182" alt="yeosu_svr" src="https://github.com/user-attachments/assets/b9f4afa9-84a3-4f48-824a-0d8e83a5b99a" />



#### 분석

- 전체 흐름은 잘 추종  
- 급격한 변화에서 일부 오차 발생  

전반적으로 안정적인 예측 성능을 보인다.

---

# 모델 및 지역 비교

## 모델 비교

| 모델 | 강점 | 약점 |
|------|------|------|
| AutoEncoder | 이상 탐지 성능 우수 | 직접 예측 어려움 |
| SVR | 수치 예측 정확 | 급격한 변화에 취약 |

---

## 지역 비교

| 지역 | 특징 |
|------|------|
| 여수 | 급격한 변화 많음 |
| 통영 | 안정적인 패턴 |

---

## 종합 성능 비교

| 지역 | 모델 | MSE | 특징 |
|------|------|------|------|
| 여수 | AutoEncoder | 0.009759 | 이상 탐지 |
| 여수 | SVR | 0.010719 | 높은 정확도 |
| 통영 | AutoEncoder | 약 0 | 높은 재현 |
| 통영 | SVR | 0.010541 | 안정적 예측 |

---

# 최종 결론

AutoEncoder는 정상 패턴 학습을 통해 폭우와 같은 이상 상황을 효과적으로 탐지할 수 있다.

SVR은 일반적인 수위 예측에서 안정적인 성능을 보이며,  
특히 여수 데이터에서 높은 예측 정확도를 확인하였다.

따라서  
이상 탐지에는 AutoEncoder,  
수위 예측에는 SVR이 적합하며,  

두 모델을 결합한 방식이 가장 효율적인 분석 방법으로 판단된다.

또한 데이터 특성과 목적에 따라  
적절한 모델 선택이 필요함을 확인하였다.

---

## 향 후 연구

- AutoEncoder + SVR 결합 모델  
- LSTM 기반 시계열 예측  
- 실시간 홍수 탐지 시스템  
