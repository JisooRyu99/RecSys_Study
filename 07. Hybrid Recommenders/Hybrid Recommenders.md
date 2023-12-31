# Hybrid Recommenders

content-based filtering과 collaborative filtering에는 모두 단점들이 존재
- 해결책 : 하이브리드 추천 시스템
    - 한 모델의 단점과 다른 모델의 장점을 극복하기 위해 **다양한 모델을 결합**

### 예시

넷플릭스
- 현재 보고 있는 영화와 유사한 영화를 보여줄 때 : content-based filtering
- 나와 비슷한 user를 찾아 (내가 아직 보지 않은) 좋아하는 영화를 추천 : collaborative filtering


### Hybird model
**콘텐츠 기반 모델이 추천하는 영화의 평점을 예측하는 협업 필터의 예시**
1. 영화 제목과 user를 입력을 받기
2. content-based 모델을 사용하여 가장 유사한 25편의 영화 찾기
3. collaborative filtering을 사용하여 user가 (2번)에서 추천받은 25편의 영화의 rating을 예측
4. 예측 rating이 가장 높은 상위 10개 영화 반환


### 하이브리드 추천 시스템 종류
- 앙상블 모형 : 콘텐츠 기반 모형 및 협업 필터링 모형의 평점 출력을 단일 출력으로 결합하여 점수/순위 생성
    - 가중화
    - 스위칭
    - 케스케이드
    - 피처 보강
- 모놀리틱 디자인 : 다양한 데이터 유형을 사용해서 통합 추천 알고리즘 모형을 만듦
    - 피처 결합
- 혼합 시스템 : 다양한 유형의 추천 모델을 결합하기도 하고, 동일한 유형의 추천 모델을 결합하기도 함. (ex. 콘텐츠 기반 모형은 텍스트 분류 모델이기에 분류 정확도를 향상시키기 위한 앙상블 모형을 다양하게 사용)
    - 참고 : Netflix Prize (Kaggle)
