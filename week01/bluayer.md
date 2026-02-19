# Chapter 1. 소개 및 개요

1. 요구사항 명확화
2. 머신러닝 작업으로 문제를 구조화
3. 데이터 준비
4. 모델 개발
5. 평가
6. 배포 및 서비스 제공
7. 모니터링 및 인프라

## 요구사항 명확화

일부러 모호한 질문 => 비즈니스 목표, 영향을 줄 수 있는 피처, 데이터, 제약, 시스템 규모, 성능

실제 ML 시스템 설게 과정에서 미리 확인하는 것 (From CS230 Chapter 2)

1. Data : 어떤 데이터를 수집하고, 분포는 어떨 것인가
2. Input
3. Output
4. Architecture
5. Loss

## 머신러닝 작업으로 문제를 구조화

머신러닝이 필요한 작업이 맞는가?

- 머신러닝 목표 정의
- 시스템의 입력 및 출력 지정
- 적합한 머신러닝 유형 선택 : 지도(회귀, 분류), 비지도, 강화학습

## 데이터 준비

### 데이터 엔지니어링

데이터 수집 / 저장소 / ETL / 데이터 유형 (정형, 비정형)

### 피처 엔지니어링

- raw 데이터에서 예상 피처를 선택하고 추출
- 예측한 피처를 모델에서 사용할 수 있는 형식으로 변환

적절한 피처를 선택하는 것이 필수적이며, 주제별 전문 지식이 필요하게 됨

- 누락 데이터 처리 => 삭제 / 대체
- 피처 스케일링 : 정규화(분포를 변경하지 않고, [0, 1] 범위), 표준화, 로그 스케일링(피처 왜곡 완화를 통해 데이터 분포 왜곡을 줄임)
- 이산화(Bucketing)
- 범주형 피처 인코딩 : 정수 인코딩 / one-hot encoding / Embedding 학습(N차원 벡터에 학습. 피쳐가 갖는 고유 값의 수가 너무 많을 때)

## 모델 개발

기준선 설정 -> 간단한 모델로 실험 -> 복잡한 모델로 전환 -> 여러 모델을 조합(앙상블 => 배깅, 부스팅, 스태킹)

참고
1. 전통 머신러닝 알고리즘 :  https://machinelearningmastery.com/a-tour-of-machine-learning-algorithms/
2. Bagging : https://en.wikipedia.org/wiki/Bootstrap_aggregating
3. Boosting : https://aws.amazon.com/what-is/boosting/
4. Stacking : https://machinelearningmastery.com/stacking-ensemble-machine-learning-with-python/

## 모델 훈련

### 데이터 세트 구성

원시 데이터 수집 -> 피처 및 라벨 식별 -> 샘플링 전략 선택 -> 데이터 분할 -> 클래스 불균형 해결(있는 경우)

클래스 불균형 : 훈련 데이터 리샘플링 (소수 클래스 오버 샘플링, 다수 클래스 언더 샘플링) / 손실 함수가 소수 클래스의 데이터 포인트에 더 많은 가중치를 줄 수도. (class-balanced loss, focal loss)

### 손실 함수 선택

일반적으로 기존에 있는 거 사용함

Cross-entropy, MSE, MAE, Huber loss

### 처음부터 훈련하기와 Fine tuning

### 분산 훈련

## 평가

오프라인 평가 : 개발 단계에서 모델의 성능 평가. 얼마나 ground truth에 가까운가.
온라인 평가 : 배포 후 모델이 운영 환경에서 어떻게 수행되는지.
+ 공정성 및 편향성

## 배포 및 서비스 제공

클라우드 vs 온디바이스

모델 압축 : Knowledge distillation / pruning / quantization (https://arxiv.org/pdf/1710.09282)

## 운영 환경에서 테스트

- Shadow deployment : 기존 모델과 병렬로 배포 (유저가 추론을 두번씩 하게 함)
- A/B Test : 기존 모델과 병렬로 배포 (트래픽을 나눠서 일부 유저에게 라우팅). 중요한 점 = 각 모델로 라우팅되는 트래픽은 무작위여야 함.
- Canary release
- Interleaving experiments
- Bandits

## Inference pipeline

Batch inference
Online inference

## 모니터링

데이터 분포 변화(drift)를 어떻게 따라갈 것인가? : 큰 데이터셋 학습 / 정기적 재학습
