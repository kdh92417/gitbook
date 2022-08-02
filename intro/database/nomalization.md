# 정규화



> 정규화는 [이상현상](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#1-%EC%A0%95%EA%B7%9C%ED%99%94%EB%8A%94-%EC%96%B4%EB%96%A4-%EB%B0%B0%EA%B2%BD%EC%97%90%EC%84%9C-%EC%83%9D%EA%B2%A8%EB%82%AC%EB%8A%94%EA%B0%80)이 있는 릴레이션을 분해하여 이상현상을 제거하는 것
>
> 즉, 데이터가 꼬이는 것을 막기 위해 테이블을 잘게 나누는 것

\
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9PZHv%2Fbtq2lAE2xpY%2FHfgOTfyyYlhGDH0bLt4IIk%2Fimg.png)

출처 : liveyourit.tistory.com/213

\


* 릴레이션(Relation) : 데이터들의 표(Table)의 형태로 표현한 것
* 튜플(Tuple) : 릴레이션을 구성하는 각각의 행, 속성의 모임으로 구성된다.(컬럼)
* 속성(Attribute) : 데이터를 구성하는 가장 작은 논리적 단위, 개체의 특성

\


### 제 1정규화

> 모든 속성은 반드시 하나의 값만 가져야 한다.

### 제 2정규화

> 모든 속성은 반드시 모든 기본키에 종속되어야 한다. (기본키 일부에만 종속되면 안된다.)
>
> Ex. 학생 id, 과목 id 가 PK 상태에서 담임 선생님의 튜블이 과목 id의 속성에만 종속될때

### 제 3정규화

> 기본키가 아닌 모든 속성간에는 서로 종속될 수 없다.
>
> 기본키 A와 일반속성 B, C가 있을 때, 일본속성 C가 일본속성 B에 종속되어지는 것

\


## 참고

* [Youtube - 정규화만 잘해도 데이터 전문가는 나의 것!](https://www.youtube.com/watch?v=pMcv0Zhh3J0)
* [기술면접 Github Repo - 정규화에 대해서](https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/Database#%EC%A0%95%EA%B7%9C%ED%99%94%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)
