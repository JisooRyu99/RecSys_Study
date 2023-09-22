# Building Content-Based Recommenders

지식 기반 추천은 장르, 타임라인, 기간에 대한 유저의 선호도를 고려했지만 일반적인 추천이 대부분이었다.</br>
ex) 다크나이트, 아이언맨과 같은 영화를 좋아한다고 할 때, 지식 기반 추천은 "액션 영화를 선호"라는 것밖에 알 수 없고 세부사항(슈퍼히어로 영화)을 포착하지 못한다.

이 문제를 해결하기 위해 input으로 더 많은 metadata를 요구하는 것이다. </br>
예를 들어, 하위 장르를 입력하므로써 슈퍼히어로, 로맨틱코미디 등


-> 이 해결책은 좋지 못함.

문제 1. 하위 장르에 대한 데이터를 보유한 데이터가 없다. </br>
문제 2. 보유하고 있더라도 유저가 좋아하는 영화의 metadata에 대한 지식을 보유할 가능성이 지극히 낮다. </br>
무제 3. 유저들이 input을 길게 넣는 것을 좋아하지 않는다. </br>

=> 대신 본인이 **좋아하는/싫어하는** 영화를 알려주고 취향에 맞는 추천을 기대한다.</br>
ex) 넷플릭스 첫 가입시 좋아하는 영화 몇 편을 요청하여 해당 영화와 가장 유사한 결과를 보여주는 것.

## 콘텐츠(내용) 기반 추천시스템이란?
사용자의 평가와 아이템 속성을 사용하여 추천하는 것으로,
사용자의 평점과 구매 행동이 아이템의 콘텐츠 정보와 조합되어 사용된다. (사용자 평점 + 아이템 속성 필요)


#### Plot description-based recommender : 다양한 영화의 설명과 태그라인을 비교하여 가장 유사한 플롯 설명을 가진 추천을 제공 (영화의 줄거리 내용/정보와 비슷한 영화 추천)

#### Metadata-based recommender : 장르, 키워드, 출연진, 감독 등 다양한 특징을 고려하여 가장 유사한 추천을 제공 (세부 속성 정보가 유사한 영화 추천)

</br

## Document vectors

모델은 텍스트 사이의 pairwise similarity를 계산한다. </br>
ex) A, B, C의 세 영화 중 A의 줄거리가 C의 줄거리보다 B의 줄거리와 더 비슷하다는 것을 수학적으로 증명 </br>

-> 텍스트를 벡터로 표현

방법 1. Count Vectorizer </br>
방법 2. TF-IDF Vectorizer </br>

</br>

## CountVectorizer

A: The sun is a star. </br>
B: My love is like a red, red rose. </br>
C: Mary had a little lamb. </br>

위의 문서를 벡터로 변환하는 방법. </br>
1. 어휘의 크기를 계산 - 고유의 단어의 수를 계산 </br>
- the, sun, is, a, star, my, love, like, red, rose, mary, had, little, lamb -> 어휘의 크기 : 14

2. a, the, is, had, my 등과 같은 일반적인 단어들은 불포함한다.

=> V: like, little, lamb, love, mary, red, rose, sun, star </br>
**어휘의 크기는 9개** 이므로 9차원 벡터로 표현 </br>


#### CountVectorizer로 표현
A: (0, 0, 0, 0, 0, 0, 0, 1, 1) </br>
B: (1, 0, 0, 1, 0, 2, 1, 0, 0) </br>
C: (0, 1, 1, 0, 1, 0, 0, 0, 0) </br>

</br>


## TF-IDFVectorizer
모든 단어에 동일한 가중치를 주는 것 대신 각 단어데 다른 가중치를 부여한다.

$$w_{i,j} = tf_{i,j} \times \log(\frac{N}{df_i})$$

- $w_{i,j}$ : 문서 $j$ 에서 단어 $i$ 의 weight
- $df_i$ : $i$ 라는 단어를 포함하는 문서의 개수
- $N$ : 총 문서의 수

문서에서 단어의 weight는 해당 문서에서 더 자주 발생하고 더 적은 수의 문서에 존재하는 경우 더 크다. </br>
($w_{i,j}$ 의 weight는 0과 1사이의 값을 가짐) </br>

</br>
문서의 양이 많을 경우에는 일반적으로 카운트 기반의 벡터화보다 TF-IDF 방식의 벡터화를 사용한다.
TF-IDF를 사용하면 한 쌍의 문서 간 코사인 유사도 점수 계산 속도가 빨라진다.

</br>

## The cosine similarity score

cosine score은 robust하고 계산이 쉽다. (특히, TF-IDF Vectorizer와 함께 사용할 경우)

$$cosine(x,y) = \frac{x \cdot y^T}{\parallel x \parallel \cdot \parallel y \parallel}$$

cosine score는 -1과 1사이의 값을 가지며 cosine score가 높을수록 문서들이 서로 유사하다.

</br>


## Suggestions for improvements

- 키워드, 장르, 캐스트의 수에 대한 실험 : 예제 코드에서는 키워드, 장르 배우를 최대 세 가지로 고려했지만, 특정 수에 대한 실험을 하는 것이 좋음
- 명확히 정의된 하위 장르 : 예제 모델에서는 처음 등장한 세 개의 키워드만 고려. 하위 장르를 정의하고 하위 장르만을 영화에 할당.
- 감독에 대한 비중 높이기
- 제작진의 다른 구성원 고려하기. ex) 작가
- 다른 metadata 실험 : 장르, 키워드뿐만 아니라 제작사, 국가 및 언어 등 추가 (ex. 두편의 영화가 픽사에서 제작된 경우)
- 인기 필터 도입
