---
layout: post
title: Find_Last_Point Algorism
category: Algolism
author: bbubbush
---

### 문제
>직사각형을 만드는 데 필요한 4개의 점 중 3개의 좌표가 주어질 때, 나머지 한 점의 좌표를 구하려고 합니다. 점 3개의 좌표가 들어있는 배열 v가 매개변수로 주어질 때, 직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 return 하도록 solution 함수를 완성해주세요. 단, 직사각형의 각 변은 x축, y축에 평행하며, 반드시 직사각형을 만들 수 있는 경우만 입력으로 주어집니다.

    def solution(v):
        answer = [0,0]
        for i in v:
            answer[0] ^= i[0]
            answer[1] ^= i[1]
        return answer

x1, x2, y1, y2의 좌표가 각 2개씩 총 8개가 있어야 완성된 직사각형의 좌표를 만들 수 있음을 이용해 입력되지 않은 한쌍을 구하는 문제

이 풀이는  A ^ A = 0, A ^ 0 = A  을 이용하여 해결









<!-- <ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul> -->