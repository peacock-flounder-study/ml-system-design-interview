# 7장 이벤트 추천 시스템
- https://secundo.tistory.com/124

- pointwise LTR
	- 항목과 쿼리를 모델에 주면 연관성 점수를 준다.
	- 한 항목의 점수는 다른 항목과 독립적으로 예측된다.
- pairwise LTR
	- 항목 두개를 가져와서 어떤 항목이 쿼리와 더 관련성이 높은지 예측한다.
	- RankNet, LambdaRank, LambdaMART
- litewise LTR
	- 쿼리가 주어졌을때 전체 항목 목록에서 최적의 순서를 예측한다.
	- SoftRank, ListNet, AdaRank

- 배치 피쳐와 스트리밍 피쳐 비교
- 피쳐 연산 효율성
- 감쇠계수 사용
- 임베딩 학습을 사용
- 사용자의 속성으로 피쳐를 만들면 생길 수 있는 편견

- 의사결정트리의 민감도를 낮추기 위해서 사용되는 기법
	- 배깅
		- 랜덤 포레스트
		- 과대적합(높은 분산)의 영향을 줄인다.
		- 의사 결정 트리를 병렬로 학습할 수 있으므로 학습 시간이 많이 늘어나지 않는다.
		- 의사 결정 트리는 입력을 병렬로 처리할 수 있으므로 추론 시에 대기시간이 많이 추가되지 않는다.
	- 부스팅
		- 편향과 분산을 줄여준다.
		- 훈련 및 추론 속도가 느리다.
	- https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-11-%EC%95%99%EC%83%81%EB%B8%94-%ED%95%99%EC%8A%B5-Ensemble-Learning-%EB%B0%B0%EA%B9%85Bagging%EA%B3%BC-%EB%B6%80%EC%8A%A4%ED%8C%85Boosting
- GBDT:
	- 간편한 데이터 준비
	- 편차를 줄임
	- 편향성을 줄임
	- 반복횟수, 트리 깊이, 정규화 매개 변수 등 조정할 하이퍼파라미터가 많다.
	- GBDT는 이미지, 동영상, 오디오 등과 같은 비정형 데이터에서는 잘 동작하지 않는다.
	- 스트리밍 데이터를 통한 지속적인 학습에는 적합하지 않다.

좀 찾아봤는데, listwise 를 연구하는게 대부분인거 같다.
- 근데 대부분은 llm 기반인듯... 안비싼가?
	- https://arxiv.org/html/2406.14848v2
- 좀 찾아봤는데 재밌어서 공유
https://github.com/kakao/recoteam
- https://github.com/kakao/recoteam/tree/master/programming_assignments/jukebox
