# 알고리즘 정리 

### 이진 탐색 (Binary Search)

- 배열 내부의 데이터가 정렬되어 있을 때 사용할 수 있는 알고리즘
- 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는 과정
- 원소의 개수가 절반씩 줄어든다는 점에서 시간 복잡도가 `O(logN)`

```py
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        if array[mid] == target:
            return mid
        elif array[mid] > target:
            end = mid - 1
        else:
            start = mid + 1
```

### DFS (Depth-First Search; 깊이우선 탐색)

- 특정한 경로로 탐색하다가 특정한 상황에서 최대한 깊숙이 들어가서 노드를 방문한 후, 다시 돌아가 다른 경로로 탐색하는 알고리즘
- 데이터의 개수가 N개인 경우 O(N)의 시간 복잡도를 가짐
- DFS는 스택을 이용한 알고리즘이므로 실제 구현을 재귀 함수를 이용했을 때 간결하게 구현 가능

```py
# DFS 정의
def dfs(graph, v, visited):
    # 현재 노드에 대한 방문 처리
    visited[v] = True
    print(v, end=" ")
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

# 각 노드가 연결된 정보를 리스트 자료형으로 표현
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3.5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현
visited = [False] * 9

dfs(graph, 1, visited)
```

### BFS (Breath-First Search; 넓이우선 탐색)

- 큐 자료구조를 사용해 가까운 노드부터 탐색하는 알고리즘
- 인접한 노드를 반복적으로 큐에 넣도록 알고리즘을 작성하면 자연스럽게 먼저 들어온 것이 나가게 되어 가까운 노트부터 탐색 진행
- 일반적인 경우, 실제 수행 시간은 DFS보다 좋은 편

```py
from collections import deque

# BFS 메서드 정의
def bfs(graph, start, visited):
    queue = deque([start])
    # 현재 노드를 방문 처리 
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        v = queue.popleft()
        print(v, end=' ')
        # 해당 원소와 연결됐지만 아직 방문하지 않은 원소들을 큐에 삽입
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True

# 각 노드가 연결된 정보를 리스트 자료형으로 표현
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3.5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현
visited = [False] * 9

bfs(graph, 1, visited)
```