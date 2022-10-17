
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
## 다익스트라 알고리즘(BFS, Breadth-First Search)

- 최단 경로를 찾는 알고리즘

- 음의 간선이 없을 때 동작

- 최단경로 계산 시 현재 노드에서부터 다른 노드 각각에 대한 최단 거리를 1차원 리스트에 저장하여 갱신

- 노드와 간선 수가 많을 때 다익스트라, 노드의 개수가 적을 때는 플로이드 워셜 알고리즘이 효과적
  
  1. 출발 노드 선택 후 최단 거리 테이블 출발 노드를 제외한 모든 값을 무한으로 초기화
  
  2. 방문하지 않은 노드 중 최단 거리 테이블 내 최단 거리에 있는 노드 선택
 
  3. 선택한 노드를 거쳐 다른 노드로 가는 거리 각각 계산
  
  4. 최단 거리 테이블 내 노드별 거리가 계산한 값보다 클 경우 계산한 값으로 갱신

  5. 2번~4번 과정 불가능할 때까지 반복

<img src="https://user-images.githubusercontent.com/101415950/196177010-28225a74-b08d-42e3-8d05-9e8581d9163e.png" width="80%" height="80%">

(출처 https://www.youtube.com/watch?v=F-tkqjUiik0&list=PLVsNizTWUw7H9_of5YCB0FmsSc-K44y81&index=30)

---
## 유니온 파인드(Union-Find)


- 두 노드가 같은 그래프에 속하는지 판별하는 알고리즘

- 서로소 집합, 상호 베타적 집합(Disjoint_Set)으로도 불림

- 루트 노드를 찾는 Find 연산과 노드를 합치는 Union 연산(두 노드의 루트 노드를 비교하여 한쪽으로 합침)으로 구성

[Example]   
<img src="https://user-images.githubusercontent.com/101415950/196175786-def50ef9-1305-4077-b8ec-773fffefb99e.png" width="80%" height="80%">
<img src="https://user-images.githubusercontent.com/101415950/196175860-e682fef2-915e-4aea-b307-c1d56de620ed.png" width="80%" height="80%">
(출처 https://ip99202.github.io/posts/%EC%9C%A0%EB%8B%88%EC%98%A8-%ED%8C%8C%EC%9D%B8%EB%93%9C(Union-Find)/)
