---
layout: post
title: BOJ 10451번 문제 - 순열 사이클
category: Algolism
categories: [Algolism]
author: bbubbush
permalink: /:categories/:year/:month/:day/:title
---
### 문제
[ 순열 사이클 ]  
1부터 N까지 정수 N개로 이루어진 순열을 나타내는 방법은 여러 가지가 있다. 예를 들어, 8개의 수로 이루어진 순열 (3, 2, 7, 8, 1, 4, 5, 6)을 배열을 이용해 표현하면

```
(1  2  3  4  5  6  7  8)
(3  2  7  8  1  4  5  6)
```

와 같다. 또는, 아래와 같이 방향 그래프로 나타낼 수도 있다.
```
(1) -> (3)      (2)     (4)  -> (8)
 ^      |                  \   /
 |      v                   (6)
(5) <- (7)
```

위 방향그래프 처럼, 순열 그래프 (3, 2, 7, 8, 1, 4, 5, 6) 에는 총 3개의 사이클이 있다. 이러한 사이클을 "순열 사이클" 이라고 한다.

N개의 정수로 이루어진 순열이 주어졌을 때, 순열 사이클의 개수를 구하는 프로그램을 작성하시오.

```              
입력 예제)
2                    -> TestCase
8                    -> size
3 2 7 8 1 4 5 6      -> 입력된 순열
10
2 1 3 4 5 6 7 9 10 8

출력 예제)
3
7
```
### 접근방법
DFS문제 중 적당한 정답률을 보이길래 선택해서 풀어보았다.  

예제를 통해 해당 문제를 풀 열쇠를 찾아보자. 

순열의 사이즈는 8, 입력된 순열은 [3, 2, 7, 8, 1, 4, 5, 6]으로 되어있고 결과로는 3개의 순열 사이클이 만들어져서 3이 리턴된다.

아래와 같은 2차원 배열을 만들어 생각하면 한결 쉽게 이해된다.
```
(1 2 3 4 5 6 7 8)
(3 2 7 8 1 4 5 6)
```

첫 번째 순열 사이클을 보자. 위에서 아래로 진행된다고 생각하면 편하다. 1 -> 3으로 우선 이동하고 다시 위의 배열에서 3의 위치를 찾아 아래로 이동한다. 3 -> 7.  

위와 같이 반복하면 1 -> 3 -> 7 -> 5 -> 1 의 순열을 만들 수 있다.  이렇게 한 사이클이 끝나면 다시 왼쪽 맨 위의 값 중, 사용되지 않은 수를 찾아 반복하면 된다.

DFS문제임을 알고 푸는 것이라 생각보다 간단하게 결론이 나왔다.

입력된 숫자 배열로 그래프를 만든다. 인접노드는 해당 인덱스와 입력된 값을 이용하여 세팅하였다. 그 다음 아래와 같은 규칙으로 DFS를 실행했다.

1. 전체 노드를 다 돌면 결과를 반환한다.

2. 노드가 중간에 끊기면 전체 노드 중 탐색하지 않은 노드가 있는지 확인하고, 결과값을 +1 한다.

오랜만에 푸는 백준이라 데이터를 입력받는 부분에서 실수가 많았지만 결과적으로는 깔끔하게 통과하게 되었다.

아래 코드는 Grp클래스 안에 DFS를 구현하였고, main 메서드에서 그래프 생성, 인접노드 설정 등을 하였다.

### 코드
```{.java}
class Grp {
    class Node {
        int data;
        LinkedList<Node> adjacent;
        boolean isChecked;
        Node(int idx) {
            data = idx;
            adjacent = new LinkedList<Node>();
            isChecked = false;
        }
    }

    ArrayList<Node> nodes = new ArrayList<Node>();
    Grp(int size) {
        for (int i = 0; i < size; i++) {
            nodes.add(new Node(i));
        }
    }

    void addAdjacent(int first, int second) {
        Node n1 = nodes.get(first);
        Node n2 = nodes.get(second);

        if (!n1.adjacent.contains(n2)) {
            n1.adjacent.add(n2);
        }
        if (!n2.adjacent.contains(n1)) {
            n2.adjacent.add(n1);
        }
    }
    int cnt = 0;
    int dfs() {
        
        Stack<Node> stack = new Stack<Node>();
        boolean isFinished = false;
        
        while (!isFinished) {
            for (Node temp : nodes) {
                if (!temp.isChecked) {
                    stack.push(temp);
                    temp.isChecked = true;
                    break;
                }
            }
            while (!stack.isEmpty()) {
                Node n = stack.pop();
                for (Node node : n.adjacent) {
                    if (!node.isChecked) {
                        stack.push(node);
                        node.isChecked = true;
                    }
                }
            }
            cnt++;
            for (int i = 0; i < nodes.size(); i++) {
                if (!nodes.get(i).isChecked) {
                    break;
                }
                if (i == nodes.size() - 1) {
                    isFinished = true;
                }
            }
        }
        return cnt;
    }
}

public class Main{
	public static void main(String args[]){
		Scanner sc = new Scanner(System.in);
        int testCase = Integer.parseInt(sc.nextLine());
        ArrayList<Integer> result = new ArrayList<>();
        for (int i = 0; i < testCase; i++) {
            int size = Integer.parseInt(sc.nextLine());
            String text = sc.nextLine();
            String[] cycle = text.split(" ");
            
            Grp g = new Grp(size);
            for (int j = 0; j < cycle.length; j++) {
                int second = Integer.parseInt(cycle[j]);
                g.addAdjacent(j, second - 1);
            }
            result.add(g.dfs());
        }

        for (int data : result) {
            System.out.println(data);
        }
	}
}
```

##### 긴 글 읽어주셔서 T.Y ; )