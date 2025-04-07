--- 
title: "너비 우선 탐색 | BFS" 
date: 2025-04-04 11:00:00 +0900
achieved: 2025-04-04 12:00:00 +0900
math: true
categories: [Algorithm, Search, BFS]
tags: [Algorithm, Search, BFS]
---
---------- 	
> 내가 볼려고 작성한 알고리즘 공부. 
{: .prompt-info } 


# 💾 BFS (너비 우선 탐색)

## ✅ 1. 개념 이해하기

> **BFS(Breadth-First Search)** 는 시작 노드에서 가까운 노드부터 차례대로 탐색해 나가는 방식이다. DFS가 한쪽으로 깊이 파고든다면, BFS는 **동시에 여러 방향으로 펼쳐가며 탐색**한다.

### BFS는 언제 사용할까?

| 상황 | BFS 사용 이유 |
|------|----------------|
| 최단 거리 탐색 | 같은 비용일 때 가장 짧은 경로 보장 |
| 모든 경로를 계층적으로 탐색할 때 | 레벨 단위 탐색에 적합 |
| 그래프에서 거리 계산이 필요할 때 | 방문 순서 = 거리 순서 |

## ✅ 2. 작동 방식

### 2.1 탐색 흐름

> **BFS는 큐(Queue)를 이용해서 탐색**한다. 가장 먼저 들어온 노드부터 꺼내어 인접 노드를 모두 방문하고, 그다음 노드로 넘어가는 식이다.

예시 그래프:

```
   A
  / \
 B   C
 |   |
 D   E
```

A에서 BFS를 시작하면 → `A → B → C → D → E` 순으로 탐색한다.

### 2.2 의사코드

```python
from collections import deque

def bfs(start):
    queue = deque([start])
    visited[start] = True

    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if not visited[neighbor]:
                visited[neighbor] = True
                queue.append(neighbor)
```

> 큐를 사용하면 방문 순서대로 탐색이 진행되어, **탐색 레벨이 일정하게 유지**된다.

## ✅ 3. BFS 구현 (기본 코드)

```python
from collections import deque

graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['E'],
    'D': [],
    'E': []
}
visited = set()

def bfs(start):
    queue = deque([start])
    visited.add(start)

    while queue:
        node = queue.popleft()
        print(node, end=' ')
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

bfs('A')  # 출력: A B C D E
```

## ✅ 4. 실전 예제 - 백준 1260번: DFS와 BFS

### 문제 요약

- 정점 N개, 간선 M개
- 주어진 시작점부터 DFS/BFS 수행 결과 출력

### 입력 예시

```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

### BFS 풀이

```python
from collections import deque

n, m, start = map(int, input().split())
graph = {i: [] for i in range(1, n+1)}
for _ in range(m):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)

for node in graph:
    graph[node].sort()

def bfs(start):
    visited = set()
    queue = deque([start])
    visited.add(start)

    while queue:
        node = queue.popleft()
        print(node, end=' ')
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

bfs(start)
```

## ✅ 5. BFS를 기반으로 하는 알고리즘 기법

### 5.1 최단 거리 탐색

> BFS는 **모든 간선의 비용이 같을 때 최단 경로를 보장**한다. 따라서 미로, 게임판, 거리 계산 등에서 자주 쓰인다.

#### 예시: 2차원 미로 최단 거리 찾기

```python
from collections import deque

def bfs(x, y):
    queue = deque()
    queue.append((x, y))
    visited[x][y] = 1  # 시작 거리

    while queue:
        x, y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx < n and 0 <= ny < m and maze[nx][ny] == 1:
                if visited[nx][ny] == 0:
                    visited[nx][ny] = visited[x][y] + 1
                    queue.append((nx, ny))
```

### 5.2 다중 시작점 BFS

> 시작점이 여러 개인 경우, 초기 큐에 여러 위치를 넣고 동시에 퍼뜨려 나간다.

#### 예시 문제: 토마토 익히기 (백준 7576)

## ✅ 6. BFS 응용 문제 유형

| 문제 유형 | 설명 |
|------------|----------------------------|
| 최단 거리 | 시작점에서 다른 노드까지 거리 계산 |
| 레벨 단위 탐색 | 트리에서 깊이별 노드 처리 |
| 영역/덩어리 개수 | 연결된 블록 수 세기 (섬의 개수 등) |
| 전염, 확산 | 다중 시작점에서 동시에 확산 (토마토, 불 퍼짐 등) |

## ✅ 7. BFS 연습 문제 추천

| 난이도 | 문제 링크 |
|--------|------------|
| ⭐ | [백준 2178 - 미로 탐색](https://www.acmicpc.net/problem/2178) |
| ⭐⭐ | [백준 7576 - 토마토](https://www.acmicpc.net/problem/7576) |
| ⭐⭐⭐ | [백준 1697 - 숨바꼭질](https://www.acmicpc.net/problem/1697) |
| ⭐⭐⭐⭐ | [프로그래머스 - 게임 맵 최단거리](https://school.programmers.co.kr/learn/courses/30/lessons/1844) |


- 백준 2178 - 미로 탐색
```py
import sys
from collections import deque
input = sys.stdin.readline
n, m = map(int,input().split())
g = [list(map(int, list(input().strip()))) for _ in range(n)]
v = [[False] * m for _ in range(n)]
q = deque([(0,0,1)])
v[0][0] = True

while q:
    x, y, cnt = q.popleft()
    if x == n-1 and y == m-1:
        print(cnt)
        exit()
    
    for dx, dy in [(-1,-0),(1,0),(0,1),(0,-1)]:
        nx,ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < m and g[nx][ny] == 1 and not v[nx][ny]:
            v[nx][ny] = True
            q.append((nx,ny,cnt+1))
```

- 백준 7576 - 토마토
```py
import sys
from collections import deque
input = sys.stdin.readline

m, n = map(int,input().split())
g = [list(map(int,input().split())) for _ in range(n)]

ik = []
for i in range(n):
    for j in range(m):
        if g[i][j] == 1:
            ik.append((i,j,0))

q = deque(ik)
answer = 0
while q:
    x, y, cnt = q.popleft()
    answer = max(answer,cnt)
    for dx, dy in [(-1,0),(1,0),(0,-1),(0,1)]:
        nx, ny = dx +x, dy + y
        if 0<=nx<n and 0<=ny<m and g[nx][ny] == 0:
            g[nx][ny] = 1
            q.append((nx,ny,cnt+1))
      
for i in range(n):
    for j in range(m):
        if g[i][j] == 0:
            print(-1)
            exit()
print(answer)

```
- 백준 1697 - 숨바꼭질
```py
from collections import deque
n, k = map(int,input().split())
q = deque([(n,0)])
v = [False] * 100001
v[n] = True

while q:
    x, cnt = q.popleft()
    if x == k:
        print(cnt)
        exit()
    for nx in [x+1,x-1,x*2]:
        if 0 <=nx<=100000 and not v[nx]:
            v[nx] = True
            q.append((nx,cnt+1))
```

- 프로그래머스 - 게임 맵 최단거리
```py
from collections import deque

def solution(maps):
    n,m =len(maps),len(maps[0])
    v = [[False]*m for _ in range(n)]
    q = deque([(0,0,1)])
    
    while q:
        x,y,cnt = q.popleft()
        
        if x == n-1 and y == m-1:
            return cnt
        
        for dx,dy in [(-1,0),(1,0),(0,1),(0,-1)]:
            nx,ny = x+dx,y+dy
            
            if 0<=nx<n and 0<=ny<m and not v[nx][ny] and maps[nx][ny]==1:
                v[nx][ny] = True
                q.append((nx,ny,cnt+1))
    return -1
```