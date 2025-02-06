# 알고리즘 정리 

### 목록

- [정렬](#정렬-sort)
- [이진 탐색](#이진-탐색-binary-search)
- [BFS](#bfs-breath-first-search-넓이우선-탐색)
- [DFS](#dfs-depth-first-search-깊이우선-탐색)

### Array & Hash

#### Hash Table
- 해시 테이블이란 해시함수를 사용해 키를 해시값으로 매핑하고, 이 해시값을 인덱스 삼아 데이터의 값을 키와 함께 저장하여 검색을 빠르게 하기 위한 자료 구조 
- 단순히 말해, 키와 값을 쌍으로 저장하는 자료구조이고, 파이썬에서 dict 타입이 해시테이블을 기반으로 만들어진 자료구조
- 이 자료구조의 주요 특징은 빠른 검색, 삽입, 삭제로, 해시 함수를 이용해 데이터의 저장위치를 빠르게 계산해서 매우 효율적인 성능을 보임
- 아래 예시는 문자별 등장횟수를 해시테이블을 활용해 구하는 방법! 

```py
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        countS, countT = {}, {}

        for i in range(len(s)):
            countS[s[i]] = 1 + countS.get(s[i], 0) # 누적해서 더하기! 
            countT[t[i]] = 1 + countT.get(t[i], 0) # 누적해서 더하기
        return countS == countT
```



### 투 포인터 (Two Pointer)

- 리스트에 순차적으로 접근해야 할 때 2개의 점의 위치를 기록하면서 처리하는 알고리즘을 의미함
- 리스트에 담긴 데이터에 순차적으로 접근해야 할 때는 '시작점'과 '끝점' 2개의 점으로 접근할 데이터의 범위를 표현할 수 있음! 
- 투 포인터 알고리즘을 활용해 '특정한 합을 가지는 부분 연속 수열 찾기'를 풀 수 있음 

```py
n = 5 # 데이터의 개수
m = 5 # 찾고자하는 부분합
data = [1,2,3,2,5] # 전체 수열

count = 0
interval_sum = 0
end = 0

for start in range(n):
    while end < n and interval_sum < m:
        interval_sum += data[end]
        end += 1
    if interval_sum == m:
        count += 1
    interval_sum -= data[start]

print(count)
```

- 투 포인터 알고리즘을 활용해 '정렬되어 있는 두 리스트의 합집합'(정렬된 합집합 구하기)을 풀수 있음 

```py
# nums1에 num2를 포함해 정렬하기
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i = m-1
        j = n-1
        k = m+n-1

        while j >= 0:  # j가 -1이 되면 모든 인자를 다 정렬한 것이니까! 
            if i >= 0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                i -= 1
            else:
                nums1[k] = nums2[j]
                j -= 1
            k -= 1
```
```py
# nums1과 nums2를 정렬한 새로운 배열 생성하기
def solution(nums1, nums2, n, m):
    answer = [0] * (n+m)
    i = n -1
    j = m -1
    k = n+m-1

    while i >= 0 and j >= 0:  # and 조건인 것을 잊지 말기! 
        if nums1[i] >= nums2[j]:
            answer[k] = nums1[i]
            i -= 1
        else:
            answer[k] = nums2[j]
            j -= 1
        k -= 1
    
    if i < 0: 
        answer[:k+1] = nums2[:k+1]
    if j < 0:
        answer[:k+1] = nums1[:k+1]
    return answer
```

### 정렬 (Sort)
#### 선택 정렬 (Selection Sort)

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

#### 삽입 정렬 (Insertion Sort)

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

#### 퀵 정렬 (Quick Sort)

#### 계수 정렬 (Count Sort)




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

### 기타 파이썬 문법

#### 정규표현식

- `^`는 뒤의 것을 남긴다는 의미! 
```py
# 영문 소문자, 대문자, 숫자만 남긴다는 의미 
ref = re.sub(r"[^a-zA-Z0-9]","",s).lower()
# 자모, 한글, 공백은 제거한다는 의미 
ref = re.sub(r"[ㄱ-ㅣ가-힣\s],"",s)
```