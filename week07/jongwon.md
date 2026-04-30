```toc
```

[Leveraging Geolocation Data for Machine Learning: Essential Techniques \| Towards Data Science](https://towardsdatascience.com/leveraging-geolocation-data-for-machine-learning-essential-techniques-192ce3a969bc/)


[Search & Discovery at Eventbrite: More Challenging Than Netflix and Amazon](https://medium.com/%40eventbrite/john-berryman-on-building-a-marketplace-search-recommendation-at-eventbrite-460f37f2a069)
-  Event는 영화나 다른 거와 달리 수명이 짧다
- 그래서 협업 필터링을 쓰기 어렵다. 이벤트 시작 시점에는 상호작용 데이터가 없고, 이벤트가 끝날 즈음에가 되어서야 충분한 데이터가 쌓인다
- 그래서 협업 필터링과 콘텐츠 기반 추천, 검색 결합으로 해결
- 사용자의 기존 이벤트 상호 작용을 바탕으로 사용자-이벤트 모델을 구축
- 하지만 데이터가 없는 경우에는 이벤트 분류, 제목 및 설명의 텍스트 + 이벤트 태깅 기반으로 분류
- 두 시스템을 따로 나누진 않고 협업 필터링 + 콘텐츠 기반 추천을 하나의 시스테믕로 통합

[Next-Gen Restaurant Recommendation with Generative Modeling and Real-Time Features](https://www.uber.com/hu/en/blog/next-gen-restaurant-recommendation/)
- 통계 기반 피처에서 사용자 행동 시퀀스로 전환
- 클릭, 주문 등을 포함한 사용자의 행동 로그를 수집하고, 이를 트랜스포머 아키텍처에 넣어 사용자의 실시간 의도를 파악해 추천할 수 있도록
- Pointwise에서 Listwise로 전환

[네이버 당신 취향의 맛집을 추천해드립니다 장소 개인화 추천시스템의 비밀.pdf](https://deview.kr/data/deview/session/attach/1600_T1_%EC%A0%84%EC%98%81%ED%99%98_%EB%8B%B9%EC%8B%A0%20%EC%B7%A8%ED%96%A5%EC%9D%98%20%EB%A7%9B%EC%A7%91%EC%9D%84%20%EC%B6%94%EC%B2%9C%ED%95%B4%EB%93%9C%EB%A6%BD%EB%8B%88%EB%8B%A4_%EC%9E%A5%EC%86%8C%20%EA%B0%9C%EC%9D%B8%ED%99%94%20%EC%B6%94%EC%B2%9C%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%9D%98%20%EB%B9%84%EB%B0%80.pdf)
- 지역 특성 + 장소 특성 + 유저 특성 결합
- 유저의 취향은 협업 필터링 활용
	- 유저의 어뷰징 데이터가 문제가 되었음
	- 유저의 클릭 데이터를 적극 활용하지 않고 가중치를 낮춤
	- -> 사용자의 취향이 잘 반영되지 않음
		- 많은 유저가 클릭한 맛집만 추천
		- 정확도가 낮음
		- 음악, 영상에 비해 상호작용 데이터가 적음
	- 유저들의 선호 데이터로 비슷한 장소들 찾아서 활용 -> A 식당으로 비슷한 식당 B 찾기
- 장소 추천
	- 유저마다 맛집 관심도가 다르다
	- 그에 맞게 그룹 만들어서 따로 추천
- 빈도
	- 자주 가는 곳과 가끔 가는 곳 원하는 맛집이 다르다
	- 유저의 장소 방문 비율로 판단해서 다로 추천

[Event-based Social Networks: Linking the Online and Offline Social Worlds](https://humming80.github.io/papers/ebsn.pdf)
[A Collective Bayesian Poisson Factorization Model for Cold-start Local Event Recommendation](https://weizhangltt.github.io/paper/zhang-kdd2015.pdf)
- 이벤트 추천은
	- 수명이 짧고, cold start 강하고
	- 지역성 강하고
	- 시간 패턴이 있고
	- 온라인 관심 (북마크)랑 오프라인 행동(실제 참여)는 다르다
- 따라서 이벤트는 온라인, 오프라인 만남이 함께 존재하는 새로운 SNS
	- -> EBSN(Event-Based Social network)
- 온라인 관계는 관심사 기반. 오프라인 관계는 행동 기반
	- 온라인 -> 관심사 비슷하다
	- 오프라인 -> 실제로 모임에서 만났다
	- 서로 양의 상관관계를 지님
- 일종의 추천 시스템이 커뮤니티처럼 움직입
	- A가 좋아요를 누르면 A의 친구, A와 같은 커뮤니티 사람 쭉쭉 이어지면서 추천
- 그렇다면 아무도 좋아요, 참여를 아직 안 했다면?
	- 이벤트 내용, 오거나이저, 장소, 시간, 유저의 소셜 관계 등을 기반으로 추천

[A Meta-Learning Perspective on Cold-Start Recommendations for Items](https://proceedings.neurips.cc/paper_files/paper/2017/file/51e6d6e679953c6311757004d8cbbba9-Paper.pdf)

[\[2404.00579\] A Review of Modern Recommender Systems Using Generative Models (Gen-RecSys)](https://arxiv.org/abs/2404.00579)
