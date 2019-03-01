---
layout: post
title: 자료구조 - Depth First Search(DFS)
category: Algolism
author: bbubbush
---

알고리즘 공부를 하면서 Queue, Stack, List, Hash, DFS, BFS, DP 와 같은 용어를 참 많이 들었다.  
개념상으로는 이해할 지 몰라도 직접 구현해 본적은 없어 마침, 이직 준비를 하는 김에 확실히 개념 정리를 하기로 했다.

DFS는 Depth First Search의 약어로 흔히 '깊이 우선 탐색'이라고 한다. 아래 하나의 Graph를 통해 예를 들어 보겠다.

```
         (0)
        /   \
      (1)   (2)
     /   \
   (3)   (4)
```

위와 같은 Graph가 있을 때 수직으로 탐색을 먼저 하는 방법이다. (1)번 Node를 기준으로 탐색을 시작한다면   

0 - 1 - 3 - 4 - 2  순으로 탐색한다. 말 그대로 탐색의 갈림길이 발생 했을때 깊이를 우선으로 탐색하는 방법이다.

여기까지가 개념적인 부분이다.

> 그럼 직접 구현해보자! ~~사실 이 부분이 어렵고 알고리즘 문제에 응용하기가 힘들다~~

구현에 있어 기본 개념은 아래와 같다.
1. DFS를 구현하려면 세 가지 준비물이 필요하다.
  - 전체 Node의 개수
  - Node간의 연결관계(간선)
  - 하나의 Stack
2. 맨 처음 탐색을 시작할 Node를 Stack에 담는다.(여기까지가 초기화)
3. Stack에서 Node를 하나 꺼내 해당 Node의 인접 Node를 모두 Stack에 넣는다. 단, 이미 스택에서 한번 들어간 값은 중복해서 넣지 않는다.(여기서부터는 반복적으로 실행)
4. Stack에서 꺼낸  Node는 할 일을 다 했으므로 출력결과에 담는다.
5. 2~4번을 반복적으로 실행한다.
6. 출력결과를 실행한다.

아래는 자바로 구현한 DFS이다. 유튜버 '엔지니어 대한민국'님의 도움을 받았다.
```{.java}
import java.util.LinkedList;
import java.util.Stack;

class Graph {
    // Node 클래스를 만든다. inner class로 만든 이유는 Graph에 사용되는 하나의 부품의 역할에 충실하기 위함으로 추측된다. 
    // (Graph는 Node와 Edge로 구성되기 때문)
    class Node {
        int data;   // Node의 번호
        LinkedList<Node> adjacent; // 인접한 Node
        boolean marked; // Node가 스택에 들어갔었는지를 확인

        // 초기화
        Node (int data) {
            this.data = data;
            this.marked = false;
            adjacent = new LinkedList<Node>();
        }
    }

    // Graph에 사용되는 전체 Node의 집합
    Node[] nodes;
    Graph(int size) {
        nodes = new Node[size];
        for (int i = 0; i < size; i++) {
            nodes[i] = new Node(i); // 넘버링된 Node객체를 넣어준다
        }
    }

    // Node간의 관계를 기록
    void addEdge (int i1, int i2) {
        Node n1 = nodes[i1];
        Node n2 = nodes[i2];

        // 중복된 저장을 막기 위해 중복체크
        if (!n1.adjacent.contains(n2)) {
            n1.adjacent.add(n2);
        }
        if (!n2.adjacent.contains(n1)) {
            n2.adjacent.add(n1);
        }
    }

    // 인자가 없으면 0번 Node부터 실행
    void dfs() {
        dfs(0);
    }

    void dfs(int index) {
        // 입력된 값으로 root node를 생성
        Node root = nodes[index];

        // 하나의 스택을 생성
        Stack<Node> stack = new Stack<Node>();

        // 스택에 root node를 입력
        stack.push(root);

        // root node는 스택에 들어갔으니 사용여부를 true로 변환
        root.marked = true;

        while (!stack.isEmpty()) {
            // 스택에서 값 하나를 꺼낸다
            Node r = stack.pop();
            
            // 해당 Node의 인접Node를 중복없이 스택에 넣는다
            for (Node n : r.adjacent) {
                if (n.marked == false) {
                    // 스택에 들어가면서 사용여부를 true로 변환
                    n.marked = true;
                    stack.push(n);
                }
            }
            // 한 Node의 인접Node를 모두 스택에 넣었다면 출력
            visit(r);
        }
    }

    void visit(Node n) {
        System.out.print(n.data + " ");
    }   
}
public class TestDfs {
    public static void main(String[] args) {
        //       (0)
        //      /   \
        //    (1)   (2)
        //   /   \
        // (3)   (4)

        // 위와 같은 Graph를 DFS를 실행한다면 아래와 같이 값을 설정한다
        Graph g = new Graph(5); // 총 5개의 Node를 사용
        
        // 중복된 edge는 한 번만 표기한다
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(1, 4);
        
        g.dfs();

        /*
            기댓값 : 0 1 3 4 2
            실제값 : 0 2 1 4 3 
        */

    }
}

```
보면 실제값과 기댓값이 차이가 난다. 우리는 인접Node가 발생할 경우 왼쪽부터 탐색을 시작했지만 프로그래밍된 결과는 오른쪽부터 탐색을 시작한다.  

##### 이는 edge를 추가할 때 무엇을 먼저 추가하냐에 따라 다르다. DFS에서는 하나의 스택을 사용하므로 나중에 들어간 값이 먼저 출력된다(Last In First Out). 

위의 코드는 인접Node가 여러개일 경우 왼쪽 Node부터 추가했다. 그러므로 오른쪽 Node가 먼저 탐색하게 되고 결과적으로도 먼저 출력하게 되었다. 만약 아래와 같이 인접Node를 입력하면 우리가 기대한 값과 동일한 결과가 출력된다.

```{.java}
// ... 생략
    public static void main(String[] args) {
        Graph g = new Graph(5); // 총 5개의 Node를 사용
        g.addEdge(0, 2);
        g.addEdge(0, 1);
        g.addEdge(1, 4);
        g.addEdge(1, 3);

        g.dfs();

        /*
            기댓값 : 0 1 3 4 2
            실제값 : 0 1 3 4 2 
        */
    }
```

원하는 결과를 눈으로 확인했으므로 이번 포스팅을 기쁘게 마칠 수 있겠다 ㅎㅎ 재귀를 이용한 DFS도 있으니 더 공부하고 싶은 분들은 먼저 구현방법에 대해 생각해보고, 해당 자료를 찾아보기 바란다.

##### 긴 글 읽어주셔서 고맙 ; )
