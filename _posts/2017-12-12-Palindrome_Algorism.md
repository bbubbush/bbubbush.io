---
layout: post
title: Palindrome Algorism
category: Algolism
author: bbubbush
permalink: pretty
---


### 재귀를 이용한 형태

    def longest_palindrom(s):  
        if s[::-1] == s:  
            return len(s)  
        else:  
            return max(longest_palindrom(s[:-1]), longest_palindrom(s[1:]))  









<!-- <ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul> -->