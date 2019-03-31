---
layout: post
title: <그림으로 공부하는 오라클구조> Chapter4. SQL문 분석과 공유 풀
category: Book_Review
categories: Book_Review
author: bbubbush
comments: true
published : false
---
이번 시간에는 SQL문이 오라클 내부에서 어떻게 동작하는지에 대해 설명하려합니다. 갑자기 말투가 친절해졌다고 생각된다면 그것은 기분탓일거에요 ㅎㅎ

이번 챕터에서는 중요한 내용이 많으니 순차적으로 진행하면서 결론을 내리겠습니다.
![필기내용](/assets/img/book_review/01_oracle_architecture/2019-03-31_oracle_01.png){: .center .img}
>그래도 정리한 내용은 앞으로 뺄게요 :)

#####SQL과 다른 프로그래밍 언어의 차이
SQL이 다른 프로그래밍 언어와 다른 점이 무엇이 있을까요? 바로 처리방법을 개발자가 기술하지 않는다는 점입니다. 예를들어 아래와 같은 쿼리가 있습니다.

```
SELECT A
  FROM B
 WHERE C = 1
```
위 쿼리는 'B라는 테이블에서 C가 1인 조건을 만족하는 데이터를 가저오는데, A컬럼의 값만 꺼내와' 라는 의미입니다. 하지만 어떻게 데이터를 가저오는지, 어디서 가저오는지 우리는 알 수 없습니다.

Full scan을 통해 B 테이블을 전부 조회한 후에 가져올수도 있고, Index를 활용하여 데이터를 조회해 올 수도 있습니다.
바로 '어떻게 처리할지'에 대해 고민하는 것은 오라클이 스스로 해줍니다. 우리가 흔히 옵티마이저라고 불리는 기능이 바로 그것입니다.

옵티마이저가 스스로 처리한다고 비유적으로 표현했지만 사실 일련의 알고리즘을 통해 처리방법을 선택합니다. 크게 '규칙기반(Rule base)'와 '비용기반(Cost base)'로 구분됩니다만 오라클 10g부터는 규칙기반을 지원하지 않습니다.

따라서 비용기반 알고리즘에 대해 집중해보겠습니다.

#####비용기반 옵티마이저
간단하게 후려쳐서 설명하자면 '처리시간이나 I/O 횟수가 가장 적은 처리방법이 최고의 성능이다' 입니다. 따라서 처리시간이나 I/O를 수치화하여 가장 적은 방법을 선택합니다.








'어떻게 처리할지'에 대해 고민하는 것이 바로 옵티마이저다.


크게 Rule base, Cost base로 구분되지만 오라클 10g부터는 Cost base로만 동작한다.





적합한 실행비용과 부적합한 실행비용의 차이

선택가능한 실행계획이 많다는 점, 어디까지나 예측에 지나지 않다는 점   이것이 옵티마이저의 비용계산이 갖고 있는 문제

공유풀을 통해 실행계획을 공유하면 분석에 사용되는 CPU자원을 아낄 수 있다.


공유풀은 SGA안에 존재하며 딕셔너리캐시, 라이브러리 캐시 등으로 구성되어 있다.

SQL문을 해시값으로 저장하여 관리. 따라서 소문자로 작성한 쿼리와 대문자로 작성한 쿼리는 해시값이 달라 다르게 관리된다.(SQL표준을 따라야 하는 이유)

매번 중복되는 SQL문을 사용해야할 때는 바인딩 변수를 활용하면 해시값이 일관되어 빠른 실행계획을 비용없이 사용할 수 있다.

파스는 하드, 소프트, 파스를 안하는 경우  크게 세 가지로 분류

