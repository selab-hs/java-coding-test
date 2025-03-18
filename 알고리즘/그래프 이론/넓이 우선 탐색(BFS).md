* 맹목적 탐색 바업 중 하나
* 시작 정점을 방문한 후 시작 정점에 인접한 모든 정점들을 우선 방문하는 방법
* 더 이상 방문하지 않은 정점이 없을 때까지 방문하지 않은 모든 정점들에 대해서 너비 우선 검색을 적용한다
* Queue를 사용하는 것이 알고리즘 구현에 쉽다

<br>

# 탐색 방법
1. 루트에서 시작한다
2. 자식 노드들을 큐에 저장한다
3. 큐에 저장된 노드들을 차례로 방문한다. 또한 각각의 자식들을 큐에 저장한다
4. 위의 과정을 반복한다 
5. 모든 노드를 방문하면 탐색을 마친다

![img.png](https://i.namu.wiki/i/IcucoK-TWgZDWsQX_rsIsfOyIMDB-3ITuJvonriCgGcB1271eevU5w1rcjxCcvhqtt7IHvrYgeerrL775cwxsQ.gif)

<br>

# 특징

* DFS와의 가장 큰 차이로 여러 갈래 중 무한한 길이를 가지는 경로가 존재하고 탐색 목표가 다른 경로에 존재하는 경우 DFS로 탐색할 시에는 무한한 길이의 경로에서 영원히 종료를 막지 못한다
* BFS의 경우 모든 경로를 동시에 진행하기 때문에 무한한 길이를 가지는 경로를 탐색할 수 있다.
* 주어진 그래프에서 최단 경로를 알아내기 용이하다

```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String[] args) {

        // 그래프를 2차원 배열로 표현해줍니다.
        // 배열의 인덱스를 노드와 매칭시켜서 사용하기 위해 인덱스 0은 아무것도 저장하지 않습니다.
        // 1번인덱스는 1번노드를 뜻하고 노드의 배열의 값은 연결된 노드들입니다.
        int[][] graph = {{}, {2, 3, 8}, {1, 6, 8}, {1, 5}, {5, 7}, {3, 4, 7}, {2}, {4, 5}, {1, 2}};
        // 방문처리를 위한 boolean배열 선언
        boolean[] visited = new boolean[9];

        bfsQueue(1,graph,visited).forEach(System.out::println);
    }


    static Queue<Integer> bfsQueue(int start, int[][] graph, boolean[] visited) {
        Queue<Integer> sequence = new LinkedList<>();
        Queue<Integer> nextSequence = new LinkedList<>();
        nextSequence.offer(start);
        visited[start] = true;
        //큐가 빌 때까지 반복
        while (!nextSequence.isEmpty()) {
            int nodeIndex = nextSequence.poll();
            sequence.offer(nodeIndex);
            //큐에서 꺼낸 노드와 연결된 노드들 체크
            for (int i = 0; i < graph[nodeIndex].length; i++) {
                int temp = graph[nodeIndex][i];
                //방문하지 ㅇ낳았으면 방문처리 후 큐에 넣기
                if(!visited[temp]) {
                    visited[temp] = true;
                    nextSequence.offer(temp);
                }
            }
        }
        return sequence;
    }
}
```

* 구현에 큐를 사용하니 더욱 편하다.
* 방문해야 할 노드의 큐와 이미 방문한 순서를 따로 저장해야한다
