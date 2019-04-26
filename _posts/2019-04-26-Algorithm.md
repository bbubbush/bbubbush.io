---
layout: post
title: Programmers - 완주하지못한 선수
category: Algolism
categories: [Algolism]
author: bbubbush

---
### 문제
[ 완주하지못한 선수 ]

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.


```
입력 예제)
participant : [leo, kiki, eden]
completion  : [eden, kiki]

participant : [marina, josipa, nikola, vinko, filipa]
completion  : [josipa, filipa, marina, nikola]

participant : [mislav, stanko, mislav, ana]
completion  : [stanko, ana, mislav]

출력 예제)
leo

vinko

mislav  (동명이인이 참가하여 한 사람만 완주함)

```
### 접근방법
문제에서 단 한명의 선수만 완주하지 못한다고 명시했습니다. 따라서 간단하게 완주자 명단에 없는 한 명을 찾으면 됩니다.

혹시 배열로 데이터가 입력되니깐 배열에서 찾아 바로 제거해야겠다는 생각을 한다면 시간초과로 인해 이 문제를 풀 수 없을 것입니다.

배열에서 데이터를 찾는 속도는 O(n) (n은 배열의 크기) 이기 때문에 완주자를 일일이 찾게 된다면 O(n^2)의 시간이 걸리게 됩니다. (한 명의 완주자를 찾는데 O(n), 이를 완주자 명단만큼 반복하기 때문)

그래서 해시를 사용해서 풀었습니다. 해시는 탐색 시 O(1)의 속도가 걸리기 때문에 배열에 비해 월등히 빠릅니다.
풀이 순서는 아래와 같습니다.

1. 참가자 명단을 HashMap에 이름을 key로, 등장횟수를 value로 입력한다.

2. 참가자 명단을 입력한 HashMap에서 완주자 명단의 이름을 key로 찾아 해당 값을 -1 해준다.

3. HashMap을 돌면서 value가 0 보다 큰 데이터를 찾아 key를 return한다.

마지막으로 코드를 보겠습니다.
```{.java}
import java.util.HashMap;
import java.util.Optional;

class Solution {
    public String solution(String[] participant, String[] completion) {
        HashMap<String, Integer> players = new HashMap<>();
        // 참가자 명단에 있는 선수들을 HashMap에 담아 이름의 등장횟수 세기
        for(String player : participant) {
            int countName = Optional.ofNullable(players.get(player)).orElse(0);
            players.put(player, ++countName);
        }
        // HashMap에서 완주자 명단의 이름을 찾아 value를 -1 하기
        for(String player : completion) {
            int countName = Optional.ofNullable(players.get(player)).orElse(0);
            players.put(player, --countName);
        }
        // HashMap을 돌면서 value가 0 보다 큰 데이터 찾기
        for (String key: players.keySet()) {
            if (players.get(key) > 0) {
                return key;
            }
        }
        return "";
    }
}
```
##### 오랜만에 포스팅이라 매끄럽지 않은 글은 양해 부탁드릴게요 ; )