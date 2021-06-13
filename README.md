# MACHINE LEARNING PROJECT
### w/ SOCAR DATA
#### 2021. 03. 29. -  2021. 04. 27.

</br>

<img src="https://user-images.githubusercontent.com/73205057/118067958-7d390d00-b3dc-11eb-8382-3d1118d3b3fb.png" width="350">
</br>

모빌리티 서비스 브랜드 인지도 1위\
'카셰어링'하면 가장 먼저 떠오르는 브랜드\
운전면허 보유자 5명 중 1명은 쏘카 회원\
대한민국 최초의 모빌리티 유니콘
   
</br>

## 프로젝트 목표 

> 🚙.&ensp; 쏘카의 실제 데이터를 분석하여  
> &emsp;&ensp; 보험사기를 탐지하는 최적의 모델 구축

</br>

## 구조
<img src="https://user-images.githubusercontent.com/73205057/121798273-4a469b00-cc60-11eb-8186-8eb0ff275a28.png" width="600">

</br>

## 데이터 소개
- 본 프로젝트에서 사용한 데이터는 SOCAR에서 제공받았다.
- 총 16,000개의 데이터로, 타깃 컬럼인 [fraud_YN]를 포함 총 25개의 컬럼으로 구성되어 있다.
- 본 데이터는 train set와 test set이 정해져 있다.
- ☝🏻 **타깃 컬럼을 제외한 컬럼은 SOCAR 측의 요청대로 비공개 처리한다.**

</br>

## 데이터 탐색
- 16000 rows x 25 columns
- fraud_N 의 개수가 15,959개인 반면 fraud_N의 개수는 단 41개로, 극심하게 불균형한 데이터이다.
- test set을 제외하면, fraud_N는 12,845개, fraud_Y는 34개..이다.

### 1. 불균형 데이터
fraud인 데이터와 fraud가 아닌 데이터의 컬럼 간에 불균형 존재
</br>

<img src="https://user-images.githubusercontent.com/73205057/118069719-9d1e0000-b3df-11eb-8768-2f3dae42d1d0.png" width="600">
<img src="https://user-images.githubusercontent.com/73205057/118069790-c63e9080-b3df-11eb-8606-9147bda31d61.png" width="600">

### 2. x16 비율
<img width="600" alt="스크린샷 2021-05-13 오전 11 39 51" src="https://user-images.githubusercontent.com/73205057/118069924-fdad3d00-b3df-11eb-81ce-a428f72d6235.png">

### 3. x13 비율
<img src="https://user-images.githubusercontent.com/73205057/118069825-d48cac80-b3df-11eb-9fec-4c8430ef1e6c.png" width="600">

### 4. x14 & x19
<img src="https://user-images.githubusercontent.com/73205057/118069940-030a8780-b3e0-11eb-94a4-64c94ad68f8c.png" width="600">

### 5. null 값이 너무 많다..
<img src="https://user-images.githubusercontent.com/73205057/118069953-07cf3b80-b3e0-11eb-9b09-03a378db0055.png" width="450">

</br>

## 데이터 전처리
  
### 1. Encoding

#### 1-1 re-labeling

: 라벨과 내용의 순서가 이어지지 않는 컬럼 8개에 대해 순서 정리

#### 1-2 OneHotEncoding

: 기존에 라벨링 되어있는 컬럼 중에 순서가 없는 컬럼 6개에 대해 원핫인코딩 진행

### 2. Outlier Removal

: 결측치를 채우기 전에 이상치부터 제거

<img src="https://user-images.githubusercontent.com/73205057/118073132-33552480-b3e6-11eb-8558-b9a6dd9a8781.png" width="600">
<img src="https://user-images.githubusercontent.com/73205057/118073147-39e39c00-b3e6-11eb-9c76-7582708d515c.png" width="400">

### 3. 결측치 처리
#### 3-1 kMeans
<img src="https://user-images.githubusercontent.com/73205057/118073303-8a5af980-b3e6-11eb-9539-43cfd3d37417.png" width="600">

#### 3-2 nanmedian
<img src="https://user-images.githubusercontent.com/73205057/118073350-9f378d00-b3e6-11eb-9fde-807c7bcc474d.png" width="600">

### 4. Scaling
<img src="https://user-images.githubusercontent.com/73205057/118073360-a3fc4100-b3e6-11eb-83d2-51504541240f.png" width="600">

### 5. Resampling

: SOCAR data는 Imbalanced data!!

⇒ resampling 적용

- Oversampling: Duplicating samples from the minority class
- Undersampling: Deleting samples from the majority class

</br>

## 모델평가
### Baseline
- 15기 score
    - LightGBM
    - Accuracy: 0.964114/ Precision: 0.043478/ Recall: 0.714286
    
### 평가 기준
![12](https://user-images.githubusercontent.com/73205057/118074082-37824180-b3e8-11eb-8d69-8c28ad9a569c.png)

### 😀 여러 조합으로 평가를 해보았다.
<img src="https://user-images.githubusercontent.com/73205057/118074089-39e49b80-b3e8-11eb-9ecd-a94cce46f503.png" width="400">

### 모델 4-2
<img src="https://user-images.githubusercontent.com/73205057/118074097-3d782280-b3e8-11eb-97a0-da0a3f76bb54.png" width="700">

### 모델 5-2
: fraud를 잡기 위함이 목적이라면 이 모델이 적합해 보인다.
<img src="https://user-images.githubusercontent.com/73205057/118074107-40731300-b3e8-11eb-9579-5b34f3a238bd.png" width="700">

</br>

## 마무리
- 어떤 스코어를 기준으로 모델을 평가하면 좋을지 끝까지 고민했다..
- null 값이 너무 많아서 해당 부분을 다루는 데 어려움이 있었다.
- 더 많은 데이터가 있었으면 스코어를 더 낼 수 있지 않았을까..
- EDA를 통해 알게 된 내용을 활용하지 못해 아쉽다.

</br>

## 팀원/ 역할
- 이경무/ EDA, 데이터 전처리, 모델링, 발표 자료 작성, 🐥
- 장혜임/ EDA, 데이터 전처리, 결측치 처리, 모델링, 발표 자료 작성, README
- 정민주/ EDA, 발표
