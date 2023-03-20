# [알고리즘] BFS(너비 우선 탐색) - Java + BOJ_1206(DFS+BFS)

-   **BFS(breadth-first search) 란?**

BFS는 선입선출 방식으로 탐색하므로 큐를 이용해 구현합니다. 또한, 탐색 시작 노드와 가까운 노드를 우선하여 탐색하므로 목표 노드에 도착하는 경로가 여러 개일 때 최단 경로를 보장합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDUxgf%2Fbtr4ylUI5Zq%2FB1iJk1ZoAzrd2nEiIgpWB0%2Fimg.png)

위의 그래프로 1번 노드를 시작점으로 DFS탐색을 진행하면!

1.  1번과 연결된 노드는 2번 3번 8번이다. 숫자 순서대로 방문하지 않고 만든 자료구조에 값이 들어있는 순서대로 순회하게 된다. 숫자대로 탐색하고 싶다면 자료구조를 미리 정렬하는 것이 좋다. 앞으론 정렬을 했다고 가정한다.
2.  1번노드 큐에 추가(큐 데이터 = (1))
3.  1번과 연결된 노드 2번 3번 8번 을 순서대로 순회한다. 큐에 2, 3, 8 추가(방문순서 : 1 -> 2 -> 3 -> 8) (큐 데이터 = (1,2,3,8))
4.  큐의 선입선출 방식이 적용되기 때문에 1번 노드가 방문하지 않은 노드가 없기 때문에 큐에서 삭제해준다.(큐 데이터 = (2,3,8)) 그 다음 2번 노드로 이동하게 되고, 2번 노드에서는 연결된 6번 노드를 방문하면서 큐에 추가하게 되고(큐 데이터 = (2,3,8,6)), 2번 노드는 큐에서 삭제된다.(큐 데이터 = (3,8,6))(방문순서 : 1 -> 2 -> 3 -> 8 -> 6)
5.  큐의 다음 첫 순서인 3번 노드로 방문해서 연결된 5번 노드를 추가(큐 데이터 = (3,8,6,5)), 방문한 3번 노드 삭제(큐 데이터 = (8,6,5))(방문순서 : 1 -> 2 -> 3 -> 8 -> 6 -> 5)
6.  다음 큐 순서인 8번 노드와 6번노드는 연결된 다른 노드들이 방문한 것을 확인하였기에 그냥 poll()해준다.(큐데이터 = (5))
7.  그 다음 순서인 5번을 방문하고 연결된 4번, 7번 노드를 큐에 추가(큐데이터 = (5,4,7))해주고, 방문한 5번 노드를 큐에서 삭제해준다.(큐데이터 = (4,7)) (방문순서 : 1 -> 2 -> 3 -> 8 -> 6 -> 5)
8.  다음 큐 순서인 4번을 방문(방문순서 : 1 -> 2 -> 3 -> 8 -> 6 -> 5 -> 4)하고 큐에서 삭제해준다.(큐데이터 = (7))
9.  다음 큐 순서인 7번 노드를 방문(방문순서 : 1 -> 2 -> 3 -> 8 -> 6 -> 5 -> 4 -> 7)하고 큐에서 삭제 (큐데이터 = ())

큐랑 방문순서를 동시에 써놔서 보기 힘들 수도 있지만.... 잘 읽어보면 이해하는 데 도움이 될 것 같다.

이제 탐색 원리를 이해했으니 문제를 풀며 활용해보자!

---

-   출처

[https://www.acmicpc.net/problem/1260](https://www.acmicpc.net/problem/1260)

[1260번: DFS와 BFS

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사

www.acmicpc.net](https://www.acmicpc.net/problem/1260)

---

-   문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

---

-   **입력**

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

---

-   **출력**

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

---

-   **입출력 예시**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCwfbe%2Fbtr4Yuh81xw%2FP88qytJ6Mh8monnOChbTn0%2Fimg.png)

---

-   **문제분석**

이번 문제는 BFS와 DFS를 기본적으로 이해하고 있는지를 묻는 문제이다.

1.  인접 리스트에 그래프를 저장한다.
2.  방문 배열을 선언 후 입력 길이에 맞춰 초기화한다.
3.  문제에서 작은 번호의 노드부터 탐색한다고 했으므로 그래프를 오름차순으로 정렬해주었다.
4.  BFS탐색!

DFS는 따로 주석을 달지 않았다.

[https://ji95.tistory.com/9](https://ji95.tistory.com/9)

참고하면 좋을 듯 하다.

[\[알고리즘\] DFS(깊이 우선 탐색) - Java + BOJ\_11724(DFS활용)

DFS(Depth-first search) 란? DFS란 이름에서 알 수 있듯이 연결된 노드를 따라서 계속 방문을 한 후에 더 이상 연결된 노드들이 없을 때, 전 노드로 되돌아가고 다시 연결된 노드를 따라서 탐색을 진행

ji95.tistory.com](https://ji95.tistory.com/9)

---

-   **코드**

``` java
import java.util.*;

public class BOJ_1206 {
    static boolean[] visited; //방문배열
    static ArrayList<Integer>[] A; //그래프 데이터 저장 인접 리스트

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt(); //노드 개수
        int M = sc.nextInt(); //엣지 개수
        int start = sc.nextInt(); //시작점
        A = new ArrayList[N+1]; 
        for (int i = 1; i <=N; i++) {
            A[i] = new ArrayList<Integer>();
        }
        for (int i = 0; i < M; i++) { //그래프 데이터 저장
            int S = sc.nextInt();
            int E = sc.nextInt();
            A[S].add(E);
            A[E].add(S);
        }
        for (int i = 1; i <= N; i++) { //그래프 데이터 오름차순 정렬
            Collections.sort(A[i]);
        }
        visited = new boolean[N+1];
        DFS(start);
        System.out.println();
        visited = new boolean[N+1];
        BFS(start);
        System.out.println();
    }

    public static void DFS(int node) { 
        System.out.print(node + " ");
        if (visited[node]) {
            return;
        }
        visited[node] = true;
        for (int i : A[node]) {
            if (visited[i] == false) {
                DFS(i);
            }
        }
    }
    public static void BFS(int node) {
        Queue<Integer> queue = new LinkedList<>(); //연결형 큐 선언 및 초기화
        queue.add(node); //방문할 노드를 큐에 추가
        visited[node] = true; //방문 체크

        while (!queue.isEmpty()) { //큐가 안비어있으면(큐가 비어 있을 때까지)
            int now_node = queue.poll(); //큐에서 노드 데이터 가져오기(큐에서 방문한 노드 제거)
            System.out.print(now_node + " ");
            for (int i : A[now_node]) { //현재 노드의 연결 노드 중 미방문 노드를 큐에 삽입하고 방문 배열에 기록하기
                if (!visited[i]) { 
                    visited[i] = true;
                    queue.add(i);
                }
            }
        }
    }

}
```