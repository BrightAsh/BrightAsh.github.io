--- 
title: "깊이 우선 탐색 | DFS" 
date: 2025-04-03 11:00:00 +0900
achieved: 2025-04-03 12:00:00 +0900
math: true
categories: [Algorithm, Search, DFS]
tags: [Algorithm, Search, DFS]
---
---------- 	
> 내가 볼려고 작성한 알고리즘 공부. 
{: .prompt-info } 


# 💾 DFS (깊이 우선 탐색)

## ✅ 1. 개념 이해하기

> **DFS(Depth-First Search)** 는 그래프(또는 트리)를 탐색하는 대표적인 방법 중 하나로, 한 방향으로 끝까지 탐색하고, 막히면 되돌아가 다른 경로를 탐색하는 방식이다.

### DFS는 언제 사용할까?

| 상황 | DFS 사용 이유 |
|------|----------------|
| 모든 경우의 수를 탐색할 때 | 백트래킹 기반 문제에서 활용 |
| 경로가 있는지 여부를 확인할 때 | 깊이 우선으로 빠르게 확인 가능 |
| 재귀적으로 구조가 반복될 때 | 트리 탐색 등에서 유리 |

## ✅ 2. 작동 방식

### 2.1 탐색 흐름

> **DFS는 스택(또는 재귀 호출 스택)을 이용하여 깊이 방향으로 탐색**한다. 즉, 현재 정점에서 갈 수 있는 다음 정점을 하나 선택해 끝까지 가보고, 막히면 되돌아와서 다른 경로를 시도한다.

예시 그래프:

```
   A
  / \
 B   C
 |   |
 D   E
```

A에서 DFS를 시작하면 → `A → B → D → C → E` 순으로 탐색한다.

### 2.2 의사코드

```python
def dfs(node):
    visited[node] = True
    for neighbor in graph[node]:
        if not visited[neighbor]:
            dfs(neighbor)
```

> `visited` 리스트는 이미 방문한 노드를 다시 방문하지 않도록 하기 위한 기록 도구이다.

## ✅ 3. DFS 구현 (재귀 & 스택)

### 3.1 재귀 방식

```python
graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['E'],
    'D': [],
    'E': []
}
visited = set()

def dfs(node):
    if node not in visited:
        print(node, end=' ')
        visited.add(node)
        for neighbor in graph[node]:
            dfs(neighbor)

dfs('A')  # 출력: A B D C E
```

### 3.2 스택 방식 (반복문)

```python
def dfs_stack(start):
    visited = set()
    stack = [start]

    while stack:
        node = stack.pop()
        if node not in visited:
            print(node, end=' ')
            visited.add(node)
            stack.extend(reversed(graph[node]))  # 순서 유지

dfs_stack('A')  # 출력: A B D C E
```

> 재귀는 내부적으로 스택을 사용하므로 두 방식은 같은 구조를 가진다.

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

### DFS 풀이

```python
n, m, start = map(int, input().split())
graph = {i: [] for i in range(1, n+1)}
for _ in range(m):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)

for node in graph:
    graph[node].sort()  # 오름차순 방문

visited = set()
def dfs(v):
    print(v, end=' ')
    visited.add(v)
    for neighbor in graph[v]:
        if neighbor not in visited:
            dfs(neighbor)

dfs(start)
```

## ✅ 5. DFS를 기반으로 하는 알고리즘 기법

### 5.1 백트래킹 (Backtracking)

> **백트래킹은 DFS를 기반으로 하여 조건을 만족하지 않으면 탐색을 중단하고 되돌아가는(Backtrack) 방식의 알고리즘이다.** 모든 경우의 수를 탐색하지만, 가지치기(pruning)를 통해 비효율적인 경로는 빨리 포기한다.

#### 백트래킹 구조 예시

```python
def backtrack(path):
    if len(path) == 목표:
        print(path)
        return

    for 선택 in 후보들:
        if 조건에 맞지 않으면 continue
        path.append(선택)
        backtrack(path)
        path.pop()  # 상태 복구
```

#### 대표 문제 예시

| 문제 | 설명 |
|------|------|
| N-Queen | 같은 행/열/대각선에 말이 겹치지 않도록 배치 |
| 스도쿠 | 숫자를 조건에 맞게 채우기 |
| 순열, 조합 생성 | 모든 가능한 경우 나열 |

### 5.2 연결 요소 탐색

- DFS는 그래프에서 연결된 모든 노드를 찾는 데 유용하다. 예: 연결 요소의 개수 구하기

### 5.3 경로 찾기/미로 탐색

- DFS로 목적지까지 도달할 수 있는지 확인하거나 경로 자체를 추적할 수 있다.

## ✅ 6. DFS를 활용한 응용 문제

| 문제 유형 | 설명 |
|------------|----------------------------|
| 미로 찾기 | 갈 수 있는 경로 끝까지 탐색 |
| 섬의 개수 | 2차원 배열을 그래프로 보고 DFS |
| 단어 변환 | 한 단계씩 변환하여 탐색 |
| N-Queen | 백트래킹으로 모든 배치 경우 탐색 |

### 예시: "섬의 개수" 문제 (2차원 DFS)

```python
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

def dfs(x, y):
    if x < 0 or x >= n or y < 0 or y >= m:
        return
    if grid[x][y] == 0:
        return
    grid[x][y] = 0  # 방문 처리
    for i in range(4):
        dfs(x + dx[i], y + dy[i])
```

## ✅ 7. DFS 연습 문제 추천

| 난이도 | 문제 링크 |
|--------|------------|
| ⭐ | [백준 11724 - 연결 요소의 개수](https://www.acmicpc.net/problem/11724) |
| ⭐⭐ | [백준 4963 - 섬의 개수](https://www.acmicpc.net/problem/4963) |
| ⭐⭐⭐ | [프로그래머스 - 단어 변환](https://school.programmers.co.kr/learn/courses/30/lessons/43163) |
| ⭐⭐⭐⭐ | [백준 9663 - N-Queen](https://www.acmicpc.net/problem/9663) |


## ✅ 8. 문제 풀이

- 백준 11724 - 연결 요소의 개수

```py
import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline 
n, m = map(int, input().split())
d = {i: [] for i in range(1, n+1)}
v = [False] * (n+1)
for _ in range(m):
    a, b = map(int, input().split())
    d[a].append(b)
    d[b].append(a)
def dfs(k):
    v[k] = True
    for r in d[k]:
        if not v[r]:
            dfs(r)
cnt = 0
for i in range(1, n+1):
    if not v[i]:
        dfs(i)
        cnt += 1
print(cnt)
```

> 이슈 1: 런타임 에러 (RecursionError)
> - **원인**: DFS가 재귀방식으로 구현되어 있고, 파이썬의 기본 재귀 까지 보호할 수 있는 개수는 1000개 정도 → 큰 입력에서 **재귀 까지 넘어갈 경우 오류 발생**
> - **해결**: sys.setrecursionlimit(10**6) → 재귀 까지 한도 높이기

> 이슈 2: 시간 초과 (TLE)
> **원인**: `input()` 메서드는 입력 속도가 느린 편 → 개수가 많은 것이 바퀴로 **시간 초과**의 주원이 됨
> **해결**: `sys.stdin.readline()` 사용 통해 입력 속도 개정

| 항목 | input() | sys.stdin.readline() | sys.stdin.read() |
|------|---------|----------------------|------------------|
| 입력 단위 | 한 줄 | 한 줄 | 전체 입력 |
| 반환 문자열 | 개행 제거됨 (`\n` 없음) | 개행 포함됨 (`\n` 있음) | 전체 문자열 (개행 포함) |
| 내부 동작 | `sys.stdin.readline()` 호출 + `rstrip('\n')` + 예외 처리 등 | `sys.stdin`의 C 버퍼에서 직접 한 줄 읽음 | `sys.stdin`의 C 버퍼에서 **전부 한 번에** 읽음 |
| 속도 | 가장 느림 | 빠름 | 가장 빠름 |
| 왜 느림/빠름? | 매 호출마다 `readline()` + 문자열 처리 → 오버헤드 큼 | 줄당 1회 `C-level` I/O 호출 | **1번만** I/O 호출 → 반복 입력 없음 |
| 반복 호출 가능 | ✅ 가능 | ✅ 가능 | ❌ 불가능 (한 번에 끝) |
| 메모리 효율 | 매우 좋음 (선형 입력 처리) | 매우 좋음 | 다소 높음 (전체 입력을 메모리에 올림) |
| 적절한 상황 | 간단한 문제, 입력 적을 때 | 입력 줄 많고 빠른 처리 필요할 때 | 입력량 매우 많고 빠른 일괄 처리 필요할 때 |



- 백준 4963 - 섬의 개수

```py
import sys
sys.setrecursionlimit(10000)
input = sys.stdin.readline
w, h = map(int,input().split())
result = []
def dfs(x,y):
    v[x][y] = True
    for dx,dy in [(-1,-1),(-1,0),(-1,1),(1,1),(1,0),(1,-1),(0,-1),(0,1)]:
        nx, ny = x+dx,y+dy
        if 0 <= nx < h and 0 <= ny < w and not v[nx][ny] and g[nx][ny] == 1:
            dfs(nx,ny)
while w!=0 and h!=0:
    g = []
    v = [[False for _ in range(w)] for _ in range(h)]
    cnt = 0
    for _ in range(h):
        g.append(list(map(int,input().split())))
    
    for i in range(h):
        for j in range(w):
            if g[i][j] !=0 and not v[i][j]:
                dfs(i,j)
                cnt+=1
    print(cnt)
    w, h = map(int,input().split())
```
> 이슈 1: 잘못된 섬 개수 출력 (`Wrong Answer`)
> - **원인**: 방문 처리 배열(`v`)을 `[[False]*w]*h`로 생성  
>   → 이 방식은 같은 리스트를 `h`번 참조하는 **얕은 복사(shallow copy)**  
>   → 하나의 행만 수정해도 **모든 행이 동시에 수정**됨
> - **결과**: `v[i][j]`를 방문 처리했을 때, **다른 줄까지 같이 방문 처리**되어  
>   → **탐색이 조기에 끝나고**, **일부 섬이 탐색되지 않음**
> - **해결**: 리스트 내포를 사용해 각 행을 **독립적으로 생성**  
> v = [[False for _ in range(w)] for _ in range(h)]


- 프로그래머스 - 단어 변환

```py
def solution(begin, target, words):
    v = [False for _ in range(len(words))]
    answer = []
    def dfs(word,cnt):
        if word == target:
            answer.append(cnt)
            return
        
        for i,w in enumerate(words):
            if not v[i] and sum(1 for a,b in zip(word,w) if a==b) == len(word)-1:
                v[i] = True
                dfs(w,cnt+1)
                v[i] = False
                
    dfs(begin,0)
    return min(answer) if answer else 0
```
- 백준 9663 - N-Queen (실패)

```py
n = int(input())
answer = 0
g = [[0 for _ in range(n)] for _ in range(n)]
def queen(j,i,v):
    g[j][i] += v
    for idx in range(n):
        if idx != j:
            g[j][idx] += v
    for idx in range(n):
        if idx != i:
            g[idx][i] += v 
    for idx in range(1,n):
        if j+idx < n and i+idx < n:
            g[j+idx][i+idx] += v
        if j-idx >= 0 and i-idx >= 0:
            g[j-idx][i-idx] += v
        if j-idx >= 0 and i+idx < n:
            g[j-idx][i+idx] += v
        if j+idx < n and i-idx >= 0:
            g[j+idx][i-idx] += v
def dfs(j=0):
    global answer
    if j == n:
        answer +=1
        return
    for i in range(n):
        if g[j][i] ==0:
            queen(j,i,1)
            dfs(j+1)
            queen(j,i,-1)
dfs()
print(answer)
```
> 이슈 1: 시간 초과 (TLE)
> - **원인**: 2차원 배열로 위협 범위를 일일이 표시하고 있어서 N이 커질수록 연산량이 많아짐
> - **해결**: ??

```py
import sys
input = sys.stdin.readline

def backtrack(row):
    global count
    if row == N:
        count += 1
        return
    for col in range(N):
        if not cols[col] and not diag1[row + col] and not diag2[row - col + N - 1]:
            cols[col] = diag1[row + col] = diag2[row - col + N - 1] = True
            backtrack(row + 1)
            cols[col] = diag1[row + col] = diag2[row - col + N - 1] = False

N = int(input())
count = 0

# 최적화를 위한 체크 배열
cols = [False] * N
diag1 = [False] * (2 * N - 1)  # ↘ 방향 대각선
diag2 = [False] * (2 * N - 1)  # ↙ 방향 대각선

backtrack(0)
print(count)
```
> GPT 답