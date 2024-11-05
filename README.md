# 2024 생명연구자원 AI활용 경진대회 : 인공지능 활용 부문

## 🏆 프로젝트 개요

### 🧑‍🤝‍🧑 팀원
- **팀장**: 임형수 - **구체적인 모델링 방법 및 코드 효율 개선**
- 서은서 - **데이터 전처리 및 방법론에 맞는 인코딩 기법**
- 최시훈 - **외부데이터 수집 및 모델링**

### 📅 프로젝트 기간
- **2024년 8월 28일 - 2024년 10월 21일**

### 🎯 목표
- **바이오 분야에서의 AI 활용 확대 및 복잡한 바이오 데이터를 효율적으로 분석하고 해석할 수 있는 AI 알고리즘 개발**
- 반려동물 보호자들에게 **정확하고 신속한 피부질환 상담 서비스 제공**
- AI 기술을 통한 **상담 정확도 및 효율성 증대**
- 맞춤형 상담을 통해 **개인화 서비스 제공**

---

## 📊 데이터

### 1. 주요 데이터셋
- **train.csv**
  - **6201개의 행**
  - **ID**: 샘플 별 고유 ID
  - **SUBCLASS**: 암종 (26개 클래스)
  - **암환자 유전체 변이 정보** (4384개의 유전체 관련 컬럼)
  
- **test.csv**
  - **2546개의 행**
  - **ID**: 샘플 별 고유 ID
  - **암환자 유전체 변이 정보** (4384개의 유전체 관련 컬럼, train.csv와 동일)

### 2. 외부 데이터
- **TCGA (The Cancer Genome Atlas) 데이터**
  - 11,000명 이상의 암 환자와 33개 주요 암종에 대한 유전체 변이 정보를 포함.
  - 모델 성능 향상을 위해 주요 데이터셋과 병합하여 사용됨.

---

## 🔄 데이터 전처리 및 주요 과제

### 변이 유형 분류
- **동의변이 (예: R213R)**: 변이가 발생했지만 아미노산이 동일.
- **비동의변이 (예: R213T)**: 변이가 발생하여 아미노산이 변경됨.
- **프레임 시프트 변이 (예: R213Tfs)**: 프레임 시프트 변이로 시퀀스를 방해함.
- **종결변이 (예: R123\*)**: 변이로 인해 종결 코돈이 발생하여 시퀀스가 종료됨.
- **결실변이 (예: R123del)**: 아미노산이 삭제됨.
- **삽입변이 (예: R123ins)**: 아미노산이 추가됨.

### 핵심 전처리 작업
1. **데이터 정규화 (1NF)**: 각 셀에 여러 변이 코드가 포함되어 1NF에 위배. 가장 앞에 있는 변이 코드만 유지.
2. **불균형 데이터**: 대부분의 셀이 변이 없는 "WT" 값으로 채워져 있어, SMOTEENN 기법을 사용해 클래스 불균형 문제 해결.
3. **TCGA 특정 데이터**: 테스트 셋에만 존재하는 많은 고유 값이 있어 인코딩 및 피처 엔지니어링이 복잡해짐.

---

## 💻 모델 학습 및 방법론

### 1. 모델 선택
- **CatBoost**: 범주형 데이터를 효과적으로 처리하고 클래스 불균형 문제를 잘 다룸.

### 2. 데이터 증강
- **SMOTEENN**: SMOTE와 ENN을 결합하여 클래스 불균형을 해결하고 과적합 방지.

### 3. MultiLabelBinarizer
- TCGA 데이터로 인해 늘어난 컬럼 수를 줄이기 위해 사용. 각 레이블을 적합한 벡터 형식으로 변환하여 학습에 활용.

### 4. 하이퍼파라미터 튜닝
- **Optuna**: 모델 성능을 극대화하기 위해 하이퍼파라미터를 최적화.

---

## 📈 주요 성과
- **모델 성능 지표 및 평가 결과를 기반으로 추후 추가 예정**
- **public 9등 private 8등**

---

## 🔍 향후 계획
- **추가적인 데이터 소스와 피처 엔지니어링을 통해 모델 정확도를 더욱 개선할 계획**
- **실시간 상담 기능 구현 및 피드백을 통한 지속적 모델 개선을 모색**

---

## 🧹 참고 자료
- TCGA 데이터: [Genomic Data Commons (GDC)](https://portal.gdc.cancer.gov/)

---
