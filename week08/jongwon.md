
[LinkedIn Challenges and practical lessons from building a deep-learning-based ads CTR prediction model](https://www.linkedin.com/blog/engineering/machine-learning/challenges-and-practical-lessons-from-building-a-deep-learning-b)
- 과거에는 GLMix 모델로 CTR 예측했음
- 최적화된 프레임워크에 풍부한 피처 엔지니어링으로 좋은 베이스라인이었음
- 이를 최근에 딥러닝 기반으로 교체했고, +8.5% CTR 향상을 가져옴

![](files/Pasted%20image%2020260505213327.png)

- two tower가 아니라 three tower 아키텍처
	- deep tower
		- 회원 정보, 광고주 정보, 활동, 컨텍스트 등을 받음
		- 임베딩 후 fully connected layer에 넣음
		- 회원, 광고, 컨텍스트 특성 전반에 걸친 feature interaction 확보하는 게 목적
		- 회원 및 광고를 각각 임베딩 후 이를 모델에 넣는 것도 가능하고 이게 효율적이지만 이는 특징 간 상호작용을 놓치므로 효과적이지 않았음
		- 따라서 그냥 특성 전체를 모델에 넣는 방법을 택함
		- we did some post-ramping analysis and found that the interaction between context features and other features is critical to the relevance lift we saw during A/B tests.
	- wide tower
		- 광고 ID, 광고주 ID 등 희소 ID 피처를 받음
		- 광고 성과는 시간 및 날짜에 따라 다르고, 새로운 광고와 광고주가 유입되므로 지속적으로 재학습 함
		- 입력 피처가 가벼워 재학습이 빠름
	- shallow tower
		- 관련성을 목표로하는 다른 도메인과 달리 광고 도메인은 수익화 가치도 고려함
		- 이를 ECPI(Expected Cost Per Click)이라고 함
		- 이는 랭킹에만 쓰이는 게 아니라 광고주 과금에도 쓰임
		- 따라서 랭킹 순서뿐만 아니라 도출되는 ECPI, pCTR 등도 중요함
		- 기존 딥러닝 모델은 pCTR 분포가 다르게 생겼고 이로 인해 광고주에게 과도한 과금으로 이어질 수 있음
		- 따라서 deep tower와 거의 동일한 입력을 받는 shallow tower를 만들었음
		- 왜 이게 효과적이라는지는 이해를 못했는데.. 결과적으로 과대 예측이 40 -> 10% 감소함
		- The shallow and deep tower architecture can be thought of as a special [residual block](https://www.google.com/url?q=https://en.wikipedia.org/wiki/Residual_neural_network&sa=D&source=editors&ust=1660920377909223&usg=AOvVaw11Y_nfI7VfNZtucB853QbG) that combines a linear model and a deep model. Instead of optimizing for desired underlying mapping directly, the deep tower is now optimizing for the residual between the desired mapping and the linear model mapping.
		- 이러한 과대 예측은 실제 오프라인 데이터와 온라인 데이터 간 편향에 의해 생김
		- 그래서 나머지 10% 과대 예측은 prod 트래픽을 % 단위로 흘리며 딥러닝 모델을 돌리고, 이 결과를 바탕으로 캘리브레이션 모델을 학습하고, 트래픽 %를 늘리고 다시 학습하고 하는 등의 방법을 택함
		- 더 많은 데이터를 학습할수록 과대 예측이 0에 수렴되는 걸 확인함


![](files/Pasted%20image%2020260505223851.png)

[Practical Lessons from Predicting Clicks on Ads at Facebook \| Facebook AI Research](https://ai.meta.com/research/publications/practical-lessons-from-predicting-clicks-on-ads-at-facebook/)
- Meta의 2014년 논문
- GBDT로 feature 교차하고, 이를 바탕으로 로지스틱 회귀

- 2016~2018
	- [Wide & Deep Learning for Recommender Systems](https://arxiv.org/abs/1606.07792)
	- FM, FFM, DeepFM, DCN 등
	- 모델이 피처 교차를 학습할 수 있도록 여러 모델 만들던 시기


![](files/Pasted%20image%2020260505225636.png)
- [Deep Interest Network for Click-Through Rate Prediction](https://arxiv.org/abs/1706.06978)
	- 광고 모델을 선별할 때 고객의 모든 피처 및 행동 기록을 고려하는 게 아니라 고려하고 있는 광고랑 관련된 행동에 가중치
		- 수영복 광고라면 사용자의 모든 구매 기록이 아니라 수영복 관련 구매 기록에 가중치를 둔다거나 등등
	- 온라인 A/B 테스트 상에서 최대 10% CTR, 3.8% RPM 향상을 가져옴
	- 현재는 주요 트래픽 처리 중
- 그 외에도 사요요자의 행동을 세션 단위로 나누고 세션 내부 관심, 세션 간 관심 변화를 학습하거나
- Transformer로 사용자의 행동 시퀀스를 분석하거나 등등도 있음

[Sequence learning: A paradigm shift for personalized ads recommendations - Engineering at Meta](https://engineering.fb.com/2024/11/19/data-infrastructure/sequence-learning-personalized-ads-recommendations/)
- 2024년 Meta
- 수동으로 피처 엔지니어링을 하는 건 한계가 있다. 
	- 어떤 피처들이 있었냐
		- N일 동한 사람이 클릭한 광고 배열
		- M일 동안 방문한 Facebook 페이지와 방문 횟수 
	- 이에는 이런 한계가 있었음
		- 순차 정보가 사라짐
		- 특정 피처를 설계하고 만드니 이벤트 내 자세한 정보들은 사라짐
		- 인간 직관에 의존해 한계가 있음
		- 사람이 하나하나 만드니 중복되는 것들이 많아져 리소스 낭비가 커지고 관리가 어려워짐
![](files/Pasted%20image%2020260505230344.png)
- 그래서 모델이 알아서 이를 학습하도록 함
	- 이벤트 속성으로부터 임베딩 만들고
	- 이를 선형 압축해 단일 이벤트 속성 기반 임베딩으로 요약함
	- 대신, 시간 정보를 넣기 위해 타임스탬프도 같이 인코딩함
	- 이를 시퀀스 모델에 넣음. 이는 attention 기반
	- 세부적인 내용 및 최적화는.. 잘 모르겠음
	- kv cache 최적화, 멀티 모달 강화를 하려고 한다네요
- 일부 세그먼트에서 전환을 2~4% 증가

[Meta Adaptive Ranking Model: Bending the Inference Scaling Curve to Serve LLM-Scale Models for Ads - Engineering at Meta](https://engineering.fb.com/2026/03/31/ml-applications/meta-adaptive-ranking-model-bending-the-inference-scaling-curve-to-serve-llm-scale-models-for-ads/)
![](files/Pasted%20image%2020260505230740.png)
- 사용자 컨텍스트, 의도를 바탕으로 모델을 동적으로 라우팅해 효율적 처리를 보장
- 지연시간 O(100ms), MFU 35%, 모델 파라미터 O(1T) 등
- 잘은 모르겠으나 참고가 될까 싶어서 가져는 와봤습니다. 여러 커널 최적화, 메모리 최적화, 로딩 속도 개선, 임베딩 공유 등등.. 을 했다네요
- 광고 전환 3% 증가, 광고 클릭률 5% 증가

[번개장터의 디지털 광고 시스템2: 예측](https://medium.com/bunjang-tech-blog/%EB%B2%88%EA%B0%9C%EC%9E%A5%ED%84%B0%EC%9D%98-%EB%94%94%EC%A7%80%ED%84%B8-%EA%B4%91%EA%B3%A0-%EC%8B%9C%EC%8A%A4%ED%85%9C2-%EC%98%88%EC%B8%A1-ff28d62360ee)
![](files/Pasted%20image%2020260505231924.png)
- 신기해서 가져왔어요
- 2020년 기준
- LightGBM을 쓰고
	- GBDT 알고리즘
	- 학습 및 추론 비용이 적어서 썼다는데 추론은 그럴 수 있는데 한번 학습 후에는 비용이 클텐데 뭐지 싶긴 하네요
- 노출 및 클릭 로그를 활용하고 있고
- 이후에는 ROI, ROAS 측정 및 예측을 하고 싶다네요

[토스 Next ML Challenge - 광고 클릭 예측(PCTR) ML 경진대회 출제 후기](https://toss.tech/article/toss-next-ml-challenge)


아래는 찾은 건데 못 읽어본 글
- Pinterest
	- [Evolution of Ads Conversion Optimization Models at Pinterest](https://medium.com/pinterest-engineering/evolution-of-ads-conversion-optimization-models-at-pinterest-84b244043d51)
	- [GPU-Serving Two-Tower Models for Lightweight Ads Engagement Prediction](https://medium.com/pinterest-engineering/gpu-serving-two-tower-models-for-lightweight-ads-engagement-prediction-5a0ffb442f3b)
- X
	- [Addressing Delayed Feedback for Continuous Training with Neural Networks in CTR prediction](https://arxiv.org/pdf/1907.06558)
- 