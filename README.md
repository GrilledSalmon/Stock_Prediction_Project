# Stock_Prediction_Project
특정 종목의 미래 수익률이 코스피를 능가할 것인지 머신러닝을 이용해 예측해보는 프로젝트입니다.

- 프로젝트 기간 : 21.11.08~11.11

### 1. 주제 : 어떤 주식을 사야 미래에 오를까?
### 2. 목표 : 내가 고른 주식의 데이터를 넣었을 때, 해당 주식이 미래에 코스피 지수보다 더 오를지, 덜 오를지 '분류'하는 모델 만들기
- 모델 종류 : 이진 분류
- Target
    - 0 : 고른 종목(데이터)이 6개월 뒤 KOSPI보다 낮은 수익률을 보였다.
    - 1 : 고른 종목이 6개월 뒤 KOSPI보다 높은 수익률을 보였다.
    
    
### 3. 데이터
- 분석 종목 : 2003년 기준 시가총액 상위 400위 기업(데이터 누수를 피하기 위해 현재 기준으로 하지 않음)
- 종류  
    1) 시가총액 데이터 : 한국거래소  
    2) 주가 변동 데이터 : 2003년 ~ 현재, `FinanceDataReader` 라이브러리 사용  
    3) 종목에 따른 연도별 PER, PBR, 배당수익률 데이터 : 한국거래소
    
### 4. Feature
- 미래의 주가에 영향을 끼칠 것이라 예상되는 것들로 선정
- 종류  
    1) 12개월 간 수익률 : 최근 12개월 간 수익률이 얼마나 났는가 (float)  
    2) KOSPI대비 12개월 간 수익률 : 최근 12개월 간 KOSPI 대비 수익률이 얼마나 났는가 (float)  
    3) 12개월 간 KOSPI 이김 : 최근 12개월 간 KOSPI 대비 수익률이 높았는가 (binary)  
    4) PER_inv : 해당 종목, 해당 시점의 PER의 역수 (float)  
    5) PBR_inv : 해당 종목, 해당 시점의 PBR의 역수 (float)  
    6) 배당수익률 : 주주에게 배분된 배당금과 주주가 갖고 있는 주식 가치의 비 (float)
   
    
 (* PER, PBR은 시가총액과 당기순이익, 자본의 비이며 낮을 수록 저평가된 기업으로 여겨짐)
 
 
 ### 5. 가설
 - Feature와 Target 사이에는 시간에 독립적인 관계가 있다.
 - 따라서 시간에 관계 없이 종목의 feature, target 데이터만 있으면 모델을 학습시키고, 결과를 예측할 수 있다.
 
 ### 6. 결론
- 1년동안 많이 오른 종목은 이후 6개월간 덜 오르는 경향이 있다.
- KOSPI를 이긴 종목이은 이후 6개월간 오르는 경향이 있다.
- PBR, PER가 낮을 수록 이후 6개월간 오르는 경향이 있다. 특히 PBR이 더 큰 영향 끼친다.

#### *지난 1년간의 수익률, PER, PBR, 배당수익률을 바탕으로  6개월 뒤 KOSPI보다 오를 주식을 어느 정도 찾을 수 있다.*

### 7. 한계점
- 추가적인 Feature Engineering을 통해 모델 성능을 향상시킬 여지가 많으나, 시간이 부족해 하지 못했다.
- 데이터 누수를 피하기 위해 2003년의 시가총액 상위 기업들만 대상으로 분석을 진행해 신규 회사들을 학습, 예측하지 못했다.
- 모델의 성능을 dramatic하게 올리진 못했으며, threshold 조정에 따른 precision score의 편차가 커서 일반화하기 어렵다.
 
