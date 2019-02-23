---
layout: post
title: <그림으로 공부하는 오라클구조> Chapter1. I/O와 디스크
category: Book_Review
author: bbubbush
---

일주일에 한번씩 작성하기로 했는데 지난주에 못써서 이번주에 두장을 포스팅하게 되었다 : (   

우선 개별적으로 1장을 읽으며 정리한 내용을 토대로 결론을 내리자면 다음과 같다.  

# 디스크는 느리다!

![필기내용](/assets/img/book_review/01_oracle_architecture/2019-02-22_oracle_01.jpg){: .center}
> 개발자 답게 개발스러운 필기다 : )

흔히 SSD(흔히 스스디라고 표현하는 저장장치)를 한번이라도 사용한 사람은 HDD(a.k.a 하드디스크)를 쓰기 힘들다고 한다. 왜냐하면 느리기 때문이다. 

데이터베이스를 설명하다가 왜 뜬금없이 HDD가 느리다고 디스하는지 궁금할 것이다. HDD가 느리다고 생각하는건 사람만 그런 것이 아니라 데이터베이스 입장에서도 마찬가지이기 때문이다.  

그나마 우리는 SSD와 HDD를 비교하지만 데이터베이스는 메모리(물리적으로는 RAM을 말한다.)와 HDD를 비교하기 때문에 더더욱 HDD의 속도에 불만을 갖고 사용하기 싫어한다.  

아래 그림을 보자
![HDD의 동작원리](/assets/img/book_review/01_oracle_architecture/2019-02-22_oracle_02.jpg){: .center}
> 개발자 답게 개발스러운 필기다 : )