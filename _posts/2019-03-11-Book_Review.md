---
layout: post
title: <그림으로 공부하는 오라클구조> Chapter4. SQL문 분석과 공유 풀
category: Book_Review
categories: Book_Review
author: bbubbush
comments: true
published : false
---

##### SQL문과 일반적인 프로그래밍 언어의 차이
SQL은 처리방법에 대해 기술하지 않는다는게 일반적인 프로그래밍 언어와의 큰 차이라고 할 수 있다. 아래 간단한 쿼리가 있다.
```
SELECT A
  FROM B
 WHERE C = 1
```
B라는 테이블에서 C가 1이라는 조건을 만족하는 데이터의 A컬럼의 값을 꺼내 오라는 의미는 알겠다. 그럼 어떻게 처리하는지에 대해서도 알겠는가? 난 잘 모르겠다.
풀 스캔을 통해 데이터를 전부 조회할지, 인덱스를 활용하여 데이터를 조회할지 개발자는 그저 결과만 받을 뿐이다.

'어떻게 처리할지'에 대해 고민하는 것이 바로 옵티마이저다.


크게 Rule base, Cost base로 구분되지만 오라클 10g부터는 Cost base로만 동작한다.


