# 2024 날씨 빅데이터 콘테스트
- 2024 날씨 빅데이터 콘테스트 과제 2: **기상특성에 따른 안개 발생 진단**
<br>

## 프로젝트 개요
### 분석 배경 및 목적
- 안개로 인한 **교통 시스템 제한** 및 불필요한 **사회적 비용** 문제 인식
- 안개 발생 시의 **기상 요인** 식별 및 머신러닝 기반 **안개 예측** 모델 개발
<br>

### 스킬셋
- `Python`, `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`
- `GitHub`, `Jira`, `Notion`, `Google SpreadSheet`, `Discord`
<br>

## 연구 가설 및 분석 전략
### 가설
- **계절/지역**에 따라 **안개 발생 및 시정 계급**의 분포가 상이할 것이다.
    - 지역 구분 기준: 내륙, 내륙 산간, 동해안, 서해안, 남해안
- **공기 냉각**과 관련하여 아래의 요소들이 안개 발생에 유의미한 영향을 끼칠 것이다.
    - 기온-지면 온도 차
    - 기온의 이슬점 도달 여부
    - 습수
<br>

### 분석 상세
#### 1. EDA
- 월별, 지역별 안개 발생 **동향의 차이**를 식별
- 관측 오류, 기상 이변 등에 의한 **이상치 및 결측치**를 탐지

#### 2. Feature Engineering
- 관측소 변수를 **지역 특성**에 따라 그룹핑하는 방법 고안
- ±3 std를 기준으로 월별, 지역별 **이상치 Capping** 처리
- **결측치**를 월별, 지역별 평균값으로 대체
- **파생 변수** 생성
    - 이슬점 산출, 이슬점 도달 여부, 습수
    - 기온-지면 온도 차
    
#### 3. Modeling
- 이진 분류 모델과 다중 분류 모델을 혼합한 **Ensemble 모델** 개발
    - **각 지역**에 대해 `Random Forest Classifier` 모델 생성
    - 선행 모델은 안개 발생 여부를 예측하는 **이진 분류** 수행
    - 이후, 안개의 시정 계급을 예측하는 **다중 분류** 수행
    - 하이퍼파라미터 튜닝
        - `max_depth`, `max_features` 조정하여 **과적합 방지**
- 평가 지표: CSI Index
    - 최종 Validation CSI Index **0.319** 달성
<br>

## 프로젝트 회고 및 개선 방안
- **데일리 스크럼** 방식의 협업을 경험해 볼 수 있어 매력적이었음.
    - Jira를 통해 **일정을 관리**하고, Discord를 통해 **실시간으로 소통**하였음.
    - Notion을 통해 작업물을 **아카이빙**하고, Jira와 GitHub를 연동하여 과업에 대한 결과물을 **버전 단위로 관리**하였음. 
- 문제를 **체계적으로 정의**하고, 이를 해결해 나가는 과정을 단계별로 경험할 수 있었음.
    - 기상 도메인에 대해 연구한 내용을 바탕으로 **Feature Engineering** 수행하였음.
    - 기상 특성, 지역 특성 등을 고려한 **Model Architecture** 설계하였음.
- 안개의 종류에 따른 **상이한 발생 요인**을 체계적으로 분류해내지 못해 아쉬웠음.
    - 관측소가 마스킹된 상태로 제공되어, 변수 선택에 **지리적 특성**을 반영하기 까다로웠음.
    - 일조량이 아닌 일사량 데이터가 제공되어, **일출 시간**에 따른 안개 감지를 진행하지 못했음.
    - 추후 확장된 기상 데이터와 관측소 지점 데이터를 활용한다면, 더욱 **높은 성능**의 안개 예측 모델 구축이 가능할 것으로 예상됨.
<br>

## References
        “시정계 자료와 기계학습 기법을 이용한 지역 안개예측 모형 개발”, 김대하 (2021).
        “안개분석기술과 예측방법 27호”, 기상청.
        “한반도 연안해역 해무 관측 및 예측 가이드”, 박소희 (2011).
        “인천공항의 안개 유형별 분석 및 예측연구”, 이충태 (2006)
