---
layout: post
title: Secret Miro Algorism
category: Algolism
author: bbubbush
permalink: pretty
---


### 그냥 비교하여 푼 방법

    def miro(n, arr1, arr2):
      temp1, temp2 = [], []
      answer = ['' for i in range(n)]
      for i in arr1:
          temp = len(bin(i)[2:]) < n and ('0' * (n-len(bin(i)[2:]))) + bin(i)[2:] or bin(i)[2:]
          temp1.append(temp)
      for i in arr2:
          temp = len(bin(i)[2:]) < n and ('0' * (n-len(bin(i)[2:]))) + bin(i)[2:] or bin(i)[2:]
          temp2.append(temp)

      for i in range(n):
          for j in range(n):
              if temp1[i][j] == '0' and temp2[i][j]  == '0':
                  answer[i] += ' '
              else:
                  answer[i] += '#'

      return answer









<!-- <ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul> -->