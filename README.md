![header](https://capsule-render.vercel.app/api?type=rect&color=ff6a00&text=교통상황과%20환경개선을%20위한%20공유자동차%20서비스%20활성화%20방안%20제안&fontSize=26&fontColor=ffffff)
<div align="left">
	<img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=Python&logoColor=white" />
	<img src="https://img.shields.io/badge/Sklearn-F7931E?style=flat&logo=scikit-learn&logoColor=white" />
</div>
&nbsp;

# Members
- **김소휘**  : EDA, 데이터 전처리, 학습모델 탐색 및 실험, 결과분석, 코드시연
- **김송류**  : 데이터셋 탐색, 데이터 전처리, 학습모델 탐색 및 실험, 결과분석, 코드정리
- **김종해**  : 데이터셋 가공, 데이터 전처리, Markov Clustering 구현, 코드정리
- **이주석**  : 데이터셋 탐색, 학습모델 탐색 및 실험, 결과분석, 발표

&nbsp;

# 프로젝트 개요
> 공유경제의 일환인 공유자동차는 한 대의 차량을 여러 사람이 짧은 시간 단위로 나눠 쓰는 이용 형태입니다. 공유자동차의 이용은 꾸준히 증가하고 있으며, 이는 경제뿐만 아니라 교통상황과 환경을 개선하는 효과를 가져오고 있습니다. 공유자동차 서비스의 인프라를 발전시켜 활성화를 촉구한다면 더 쾌적한 도시환경을 구축할 수 있을 것입니다.

&nbsp;

# Repository 구조
```
├─ data
└─ DCC_TeamSpark
	├─ notebook_pre
    ├─ notebook_geo
    ├─ notebook_train
    ├─ notebook_markov
	└─ notebook_appendix
```	

# 데이터셋
1. 기업제공 데이터
 - 공유자동차 예약이력 데이터, 공유자동차 운행이력 데이터
 ![캡처](images\Raw_data.png)
2. 외부 데이터
 - 국토정보플랫폼 - 국토정보맵에서 제공하는, 수도권의 500m 격자 단위 지리정보 데이터
 ![캡처](images\Geo_data.png)
 - 공공데이터포털 - 국토교통부_전국버스정류장위치정보 데이터
 - 1차 가공된 수도권 지하철역 데이터
 ![캡처](images\Trans_data.png)


&nbsp;

# 프로젝트 수행 절차
<h3> 1. EDA  </h3>
<h3> 2. 데이터셋 탐색 및 EDA  </h3>
<h3> 3. 데이터 가공 및 전처리  </h3>
<h3> 4. 학습모델 탐색 및 실험  </h3>
<h3> 5. 결과분석 및 서비스 발전  </h3>

&nbsp;

# 문제정의
<h3> 1. 원본 데이터의 낮은 활용가능성   </h3>  

- EDA 결과, 운행이력 데이터는 일정 속력을 기준으로 기록이 시작, 중지됨을 알 수 있었다.
- 이는 학습에 이용되기 어려운 형태라 판단하였고, 데이터를 가공하여 한 운전자의 운행 이력으로 볼 수 있는 데이터를 생성하였다.
- 데이터의 오차를 줄이기 위해, 수도권 지역을 500m 격자 단위로 나누었고, 출발과 도착의 위도, 경도를 격자 영역 번호로 치환하였다.

<h3> 2. 데이터 라벨의 불균형   </h3>  

- 수도권 격자 영역에 대한 공유자동차 예약 여부(0 or 1)를 집계한 결과 예약 여부가 없는(0) 데이터가 10배 가량 많았다.
- 이러한 데이터 라벨 불균형은 학습에 악영향을 끼칠 것으로 생각되어, 'SMOTEENN' 기법을 활용하여 예약 여부가 있는 데이터를 Sampling 하였다.

&nbsp;

# 데이터 분석 기법
- RandomForest
    - GridSearchCV와 Manual Search 기법을 활용하여 RandomForest 모델에 알맞는 Hyperparameter를 탐색
    - 공유자동차 예약 여부를 예측하는 데 가장 높은 성능을 기록
 ![캡처](images\RandomForest.png)

- Markov Clustering
    - 격자 영역마다 운행의 시작과 끝이 발생한 비율을 활용하여 행렬을 생성
    - 해당 행렬에 Markov Chain을 적용하고, 경향성이 짙은 영역 (=운행비율이 높은 지역)이 두드러지도록 정규화 작업 적용
 ![캡처](images\MarkovClustering.png)

&nbsp;


# 활용방안
- 공유자동차 주차장 입지 선정
    - 학습된 RandomForest 모델을 바탕으로 공유자동차 예약 여부가 존재할 격자 영역을 탐색
    - 해당 영역 중 실제로 예약 이력이 없는 곳을 선정하고, 인근 인프라와 교통상황 등을 고려하여 주차장 입지 제안
- 공유자동차 수요 예측 및 적절한 차량 배치 도출
    - Markov Clustering의 결과 차량 운행이 많은 중심 영역을 산출하고, 이를 통해 공유자동차 수요의 큰 흐름을 분석
    - 분석한 수요를 바탕으로 마케팅 전략 수립, 주차장 입지 선정 등에 활용하여 공유자동차 서비스 활성화

&nbsp;

# 기타
- 주관 : 한국데이터산업진흥원
- 수상 : 우수 프로젝트 발표 입상