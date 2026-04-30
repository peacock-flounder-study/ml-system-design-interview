# Chapter 5. 유해 컨텐츠 감지

### 시스템의 입력 및 출력 지정

- Late fusion
- Early fusion

### 적절한 머신 러닝 유형 선택

- Single binary classifier
- 유해등급당 하나의 이진 분류기
- 다중 라벨 분류기
- 다중 작업 분류기

### 피처 엔지니어링

- 텍스트 콘텐츠
- 이미지 또는 동영상
- 게시물에 대한 사용자 반응
- 작성자 피처
- 컨텍스트 정보 (시간, 단말)

## 평가

- PR(precision-recall) 곡선 :  PR-AUC(PR 곡선 아래 면적)이 높을수록 모델이 정확하다
- ROC(Receiver Operating Characteristic) 곡선 : true positive rate와 false positive rate 간의 상충 관계.
