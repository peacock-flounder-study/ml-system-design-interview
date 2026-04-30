# 6장 동영상 추천 시스템

- 협업 필터링: collaborative filtering
	- Memory Based Approach
		- User-based Filtering
		- Item-based Filtering
	- Model Based Approach
		- Matrix Factorization
	- 장점: 도메인 지식이 필요하지 않다. 사용자의 새로운 관심 분야를 쉽게 발견할 수 있다. 효율적이다.
	- 단점: 콜드 스타트 문제, 특이한 관심사를 처리할 수 없다.
- Contents-Based Filtering
- 모델 개발
	- 행렬 인수분해 matrix factorization
		- 장점 학습 속도, 서빙속도
		- 사용자와 동영상 상호작용에만 의존한다. 사용자의 다른 정보들을 사용하지 않는다.
		- 신규 사용자를 처리하기는 어렵다.
	- Two tower neural network
		- 두개의 인코더 타워로 구성한다.
		- https://www.kaggle.com/code/kanruwang/tensorflow-recommender-two-tower-multitask
