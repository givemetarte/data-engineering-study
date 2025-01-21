# 알고리즘 정리 

### 목록

- [이진 탐색](#이진-탐색-binary-search)
- [BFS](#bfs-breath-first-search-넓이우선-탐색)
- [DFS](#dfs-depth-first-search-깊이우선-탐색)

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

- 특정한 경로로 탐색하다가 특정한 상황에서 최대한 깊숙이 들어가서 노드를 방문한 후, 다시 돌아가 다른 경로로 탐색하는 알고리즘 (한 놈만 깊이 팬다!)
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

- 큐 자료구조를 사용해 가까운 노드부터 탐색하는 알고리즘 (다양한 경우를 고려해 )
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

### 선택 정렬 (Selection Sort)

- 가장 작은 것을 선택에 앞으로 보내는 과정을 반복적으로 수행
- 시간 복잡도는 O(N^2)로, 데이터의 개수가 10,000개 이상이면 정렬 속도가 급격히 느려짐
- 특정 리스트에서 가장 작은 데이터를 찾는 일이 코딩 테스트에서 잦으므로 익숙해질 필요가 있음

```py
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(array)):
    min_index = i
    for j in range(i+1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i]

print(array)
```

### 삽입 정렬 (Insertion Sort)

- 특정한 데이터를 적절한 위치에 삽입하는 방식으로, 특정한 데이터가 적절한 위치에 들어가기 전까지 그 앞의 데이터는 이미 정렬되어 있다고 가정함
- 시간 복잡도는 O(N^2)이지만, 선택 정렬과 비교했을 때 현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작함

```py
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(1, len(array)):
    for j in range(i, 0, -1):  # 인덱스 i부터 1까지 감소하며 반복하는 문법
        if array[j] < array[j-1]:
            array[j]], array[j-1] = array[j-1], array[j]
        else:
            break

print(array)
```

### 퀵 정렬 (Quick Sort)

### 계수 정렬 (Count Sort)

