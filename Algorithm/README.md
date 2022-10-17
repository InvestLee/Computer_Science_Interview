
# 알고리즘
코딩 테스트에서는 잘 사용해도 정의에 대해 설명을 professional하게 하지 못하는 경우를 방지하기 위해 각 알고리즘의 정의를 기록
동빈나님의 알고리즘 강의 및 구글링 참조

---
## 깊이 우선 탐색(DFS, Depth-First Search)

- 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘

- 탐색 시작 노드에서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방식

- 스택 자료구조 or 재귀 함수를 사용하며 구체적인 동작은 아래와 같음
  
  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리
  
  2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리   
     방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼냄
  
  3. 더 이상 2번 과정을 수행할 수 없을 때까지 반복

<img src="https://user-images.githubusercontent.com/101415950/194974462-2c650675-1607-4f56-bdb4-9bc5c61b5d45.gif" width="40%" height="40%">
(출처 https://developer-mac.tistory.com/64)

---
## 너비 우선 탐색(BFS, Breadth-First Search)


- 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘

- 탐색 시작 노드에서 시작해서 인접한 노드를 먼저 탐색하는 방식

- Queue 자료구조를 사용하며 구체적인 동작은 아래와 같음
  
  1. 탐색 시작 노드를 큐에 삽입하고 방문 처리
  
  2. 큐에서 노드를 꺼낸 후 해당 노드의 인접 노드 중 방문하지 않은 노드를 모두 큐에 삽입 및 방문처리
  
  3. 더 이상 2번 과정을 수행할 수 없을 때까지 반복

<img src="https://user-images.githubusercontent.com/101415950/194974879-88205f00-14a0-41f0-9219-3f7fad0a6358.gif" width="40%" height="40%">
(출처 https://developer-mac.tistory.com/64)

---
## 유니온 파인드(Union-Find)


- 두 노드가 같은 그래프에 속하는지 판별하는 알고리즘

- 서로소 집합, 상호 베타적 집합(Disjoint_Set)으로도 불림

- 루트 노드를 찾는 Find 연산과 노드를 합치는 Union 연산으로 구성

[Example]
![image](https://user-images.githubusercontent.com/101415950/196175786-def50ef9-1305-4077-b8ec-773fffefb99e.png)

![image](https://user-images.githubusercontent.com/101415950/196175860-e682fef2-915e-4aea-b307-c1d56de620ed.png)

