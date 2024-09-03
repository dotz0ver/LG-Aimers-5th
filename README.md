# LG-Aimers-5th
LG Aimers 5기: 제품 이상 여부 판별 프로젝트(Project to determine product defects)

## Overview
최근 기계학습 모델의 발전과 함께 제품의 생산 단계에서 이상 여부를 미리 판단하려는 시도가 증가하고 있습니다. 이번 경진대회에서는 공정 과정의 여러 가지 데이터를 이용해 이상 여부를 판별하는 모델을 구현하고 그 성능을 비교하고자 합니다.

### Period
Phase I: 2024.07.01 ~ 2024.07.26 [Study]

Phase II: 2024.08.01 ~ 2024.08.30 [Hackaton]

### Team
DAPs (Data Analysis Peoples) Leader (4 members total)

### Result
최종 75위 / 740팀 (0.211401점)

---

## Method
### EDA
- 결측치가 있는 공통 열 제거
- 수치형 및 범주형 변수 분리
- 결측치 처리: 수치형 변수는 '중앙값', 범주형 변수는 '가장 빈번한 값'으로 대체

### Background
특정 조합(예: Dam dispenser #2, AJX75334501, 높은 작업 모드)에서 불량 발생 비율이 매우 높다는 점을 발견했습니다. 특히, Dam dispenser #2에서 작업 모드가 높아질 때 불량이 급격히 증가하는 경향이 있어, 이 조합에 대한 공정 개선이 필요하다고 판단했습니다. Dam dispenser #1이 전반적으로 더 높은 불량률을 보이더라도, Dam dispenser #2는 작업 모드가 높아질 때 불량 발생에 더 민감하게 반응하는 것으로 분석되었습니다. 이를 반영해 추가적인 특성 엔지니어링을 수행하여 모델의 예측 성능을 개선했습니다.


### Feature Engineering
- WorkMode_High: WorkMode Collect Result_Fill2 값이 2.0 이상인 경우를 1로 변환하여 새로운 피처 생성
- Model_Equipment_Combined: Model.Suffix_Dam과 Equipment_Dam을 결합하여 새로운 피처 생성
- WorkMode_Binned: WorkMode Collect Result_Fill2 값을 기반으로 Low, Medium, High로 구분
- Combined_Factor: Equipment_Dam, Model.Suffix_Dam, WorkMode_High를 결합한 피처 생성
- 생성된 피처들에 대해 One-Hot Encoding 적용


### Modeling
- 앙상블 모델: Random Forest, Gradient Boosting, K-Nearest Neighbors 모델을 결합한 Voting Classifier를 사용
- SMOTE: 불균형 데이터셋을 보완하기 위해 SMOTE를 사용하여 데이터 균형을 맞춤
- 모델 평가: 검증 데이터셋을 활용하여 F1 Score 및 혼동 행렬을 통해 성능 평가


   

