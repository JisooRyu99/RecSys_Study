# The simple recommender
## Metric
사용할 수 있는 평가 지표 중 하나는 영화 평점이 있다. 하지만, 영화 평점은 **인기**를 반영하지 않는 단점을 가지고 있다.
</br>

예를 들어 100명의 User가 평점 9를 매긴 영화 A와 10만명의 User가 평점 8을 매긴 영화 B가 있다고 한다면, <br>
영화 A의 평점(평점 9)이 더 높지만 전체적으로 보았을 때 영화 B를 사람들이 더 선호한다는 것을 알 수 있다.

IMDB의 weight rating 공식을 사용하여 다음과 같이 나타낼 수 있다.
> $$Weighted Rating (WR) = (\frac{v}{v+m} \times R) + (\frac{m}{v+m} \times C)$$

```
v  : 영화 표 수 
m : 영화가 차트에 포함되기 위해 필요한 최소 표 수 (필수)
R : 영화의 평균 평점
C : 데이터셋에 있는 모든 영화의 평균 평점
```

---

## The prerequisties
IMDB weight rating 공식에서 score를 계산하기 위해 필요한 m은 임계치 이상인 영화만 순위에 고려되도록 하기 위해 사용된다. 즉, 변수 m의 값은 반영할 영화를 결정하고, score의 최종 값을 결정한다.
<br>

m의 값은 임의적으로 실험 후 가장 좋은 추천을 해준다고 생각하는 것을 선택하는 것이 좋다. 

<br>

----



# The knowledge-based recommender
## The knowledge-based recommender
지식 기반이란?<br>
내가 원하는 콘텐츠(속성)의 사용을 기바능로 추천 제공 (사용자 사양 + 아이템 속성 + 도메인 지식)


1. 찾고 있는 영화 장르
2. 기간
3. 영화이 타임라인
4. 수집된 정보를 이용하여 가중치가 높은 rating(IMDB 공식, WR)과 위 조건을 만족하는 영화를 유저에게 추천

