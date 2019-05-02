---
layout: post
title: Programmers - 전화번호 목록
category: Algolism
categories: [Algolism]
author: bbubbush

---
### 문제
[ 전화번호 목록 ]

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다. 전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.
```
구조대 : 119
박준영 : 97 674 223
지영석 : 11 9552 4421
```

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.
```
제한 사항
phone_book의 길이는 1 이상 1,000,000 이하입니다.
각 전화번호의 길이는 1 이상 20 이하입니다.
```

```
입력 예제)
phone_book  : ["119", "97674223", "1195524421"]

phone_book  : ["123", "456", "789"]

phone_book  : ["12", "123", "1235", "567", "88"]


출력 예제)
false   (문제 예시)

true    (한 번호가 다른 번호의 접두사인 경우가 없으므로 true)

false   ("12" 번호가 "123", "1235"의 접두사가 됩니다)

```
### 접근방법
해시 문제이기 때문에 HashMap 혹은 HashSet을 써야할 것만 같아 이래저래 고민을 해봤습니다만, 활용방법이 도무지 떠오르지 않았습니다. 그래서 일단 직관적으로 문제를 풀어봤습니다.
접근한 순서는 아래와 같습니다.
1. 입력된 배열의 맨 처음 값을 비교하는 문자열로 선택합니다.
2. 입력된 배열의 두 번째 값을 비교를 당할 문자열을 선택합니다.
3. 만약 비교 문자열이 비교당할 문자열보다 길다면 둘을 반대로 저장합니다.
4. 비교할 문자열을 비교하는 문자열의 길이만큼 잘라 서로 같은지 비교합니다.
5. 비교가 끝나면 순차적으로 비교를 당할 문자열을 변경하고, 해당 작업이 끝나면 비교하는 문자열을 다음 문자열로 변경합니다.
6. 모든 작업이 끝나면 true를 리턴하고 4)의 과정에서 같은 문자열을 발견할 경우 false를 리턴합니다.

처음엔 3)의 조건에서 비교 문자열 길이 > 비교할 문자열 인 경우에 비교할 문자열을 그냥 넘겼습니다. 이런 경우에 비교 문자열이 길고, 비교할 문자열이 짧은 케이스 중에서 발생하는 포함관계를 찾지 못했습니다.

여담으로 다른 분의 풀이중에는 애초에 길이 상관없이 두 경우를 번갈아가며 비교하는 코드도 있었습니다. 코드는 간결하나 두 문자열이 포함관계에 없는 경우 중복된 연산을 두번 반복하기 때문에 비용이 더 높다고 판단되었습니다.

마지막으로 작성한 코드를 보고 오늘의 알고리즘 풀이도 마무리 하겠습니다.
```{.java}
class Solution {
    public boolean solution(String[] phone_book) {
        for (int i = 0; i < phone_book.length; i++) {
            for (int j = i+1; j < phone_book.length; j++) {
                String target = phone_book[i];      // 비교 기준
                String eqStr = phone_book[j];       // 비교당하는 문자열
                // 비교하려는 전화번호보다 짧으면 타겟을 변경
                if (target.length() > eqStr.length()) {
                    target = eqStr;
                    eqStr = phone_book[i];
                }

                // if (eqStr.startsWith(target)) {
                //     return false;
                // }

                // 비교하는 대상에서 필요한 만큼만 잘라서 비교(substring 대신 위와 같이 startsWith 메서드를 쓸 수 있습니다)
                if (target.equals(eqStr.substring(0, target.length()))) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
##### 좋은밤 되세요 : )