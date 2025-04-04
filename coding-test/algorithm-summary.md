# 알고리즘 정리 

### 목록

- [Array & Hash](#array--hash)
- [투 포인터](#투-포인터-two-pointer)
- [슬라이딩 윈도우](#슬라이딩-윈도우-sliding-window)
- [스택과 큐](#스택과-큐-stack--queue)
- [정렬](#정렬-sort)
- [이진 탐색](#이진-탐색-binary-search)
- [BFS](#bfs-breath-first-search-넓이우선-탐색)
- [DFS](#dfs-depth-first-search-깊이우선-탐색)
- [다이나믹 프로그래밍](#다이나믹-프로그래밍-dynamic-programming)

### Array & Hash

#### Hash Table
- 해시 테이블이란 해시함수를 사용해 키를 해시값으로 매핑하고, 이 해시값을 인덱스 삼아 데이터의 값을 키와 함께 저장하여 검색을 빠르게 하기 위한 자료 구조 
- 단순히 말해, 키와 값을 쌍으로 저장하는 자료구조이고, 파이썬에서 dict 타입이 해시테이블을 기반으로 만들어진 자료구조
- 이 자료구조의 주요 특징은 빠른 검색, 삽입, 삭제로, 해시 함수를 이용해 데이터의 저장위치를 빠르게 계산해서 매우 효율적인 성능을 보임


- 아래 예시는 [문자별 등장횟수를 해시테이블을 활용](https://neetcode.io/problems/is-anagram)해 구하는 방법! 
    - 개별 문자와 등장횟수를 key-value 형태로 저장
    - `dict.get(x, 0)`은 x가 key인 value를 가져오지만 없다면 0으로 출력이란 의미

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
- 주로 '정렬이 된 배열'을 대상으로 투 포인터를 사용함
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
    - 거꾸로 정렬하는 것도 기억하기! 

```py
def solution(nums1, nums2, n, m):
    answer = [0] * (n+m)  # 새로운 배열을 n+m 크기로 초기화
    i = n -1  # nums1의 마지막 원소 인덱스
    j = m -1  # nums2의 마지막 원소 인덱스
    k = n+m-1 # answer 배열의 마지막 원소 인덱스

    while i >= 0 and j >= 0:  # 두 리스트의 원소를 모두 확인할 때까지 반복
        if nums1[i] >= nums2[j]:  
            answer[k] = nums1[i]  # 더 큰 값을 answer의 뒤쪽에 삽입
            i -= 1  # nums1에서 다음 값 비교
        else:
            answer[k] = nums2[j]  # nums2 값이 더 크면 해당 값 삽입
            j -= 1  # nums2에서 다음 값 비교
        k -= 1  # answer의 다음 위치로 이동
    
    # nums1의 모든 원소가 answer에 추가되었고 nums2의 원소가 남아있는 경우
    if i < 0: 
        answer[:k+1] = nums2[:k+1]
    
    # nums2의 모든 원소가 answer에 추가되었고 nums1의 원소가 남아있는 경우
    if j < 0:
        answer[:k+1] = nums1[:k+1]
    
    return answer
```

### 슬라이딩 윈도우 (Sliding Window)

- 슬라이딩 윈도우란 고정 사이즈의 윈도우가 이동하면서 윈도우 내에 있는 데이터를 이용해 문제를 풀이하는 알고리즘을 의미함
- 정렬이 된 배열에 사용하는 투 포인터와 달리, 슬라이딩 윈도우는 정렬 여부에 관계없이 활용된다는 차이가 있음
- 윈도우 사이즈는 고정이며, 좌 또는 우 한쪽 방향으로만 이동함


### 스택과 큐 (Stack & Queue)

- 스택은 LIFO(Last-In-First-Out, 후입선출)로, 가장 마지막에 넣은 요소를 가장 먼저 꺼냄
- 큐는 FIFO(First-In-First-Out, 선입선출)로, 가장 처음에 넣은 요소를 가장 먼저 꺼냄


### 정렬 (Sort)
#### 선택 정렬 (Selection Sort)

- 가장 작은 것을 선택에 앞으로 보내는 과정을 반복적으로 수행
- 시간 복잡도는 O(N^2)로, 데이터의 개수가 10,000개 이상이면 정렬 속도가 급격히 느려짐
- 특정 리스트에서 가장 작은 데이터를 찾는 일이 코딩 테스트에서 잦으므로 익숙해질 필요가 있음

```py
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(array)):
    min_index = i  # 가장 작은 원소의 인덱스
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

- 가장 많이 사용되는 정렬 알고리즘
- 기준 데이터(= 피벗)을 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방식
- 퀵 정렬이 끝나는 조건은 현재 리스트의 데이터 개수가 1인 경우 (이미 정렬되어 있고 분할 불가능)
- 퀵 정렬의 평균 시간 복잡도는 O(NlogN)이지만, 최악의 경우 시간복잡도가 O(N^2)이 됨
    - 이미 데이터가 정렬이 되어 있는 경우는 매우 느리게 동작함

```py
array = [7,5,9,0,3,1,6,2,4,8]

def quick_sort(array):
    # 리스트가 하나 이하의 원소만을 담고 있다면 종료
    if len(array) <= 1:
        return array
    
    pivot = array[0] # 피벗은 가장 첫번째 원소
    tail = array[1:] # 피벗을 제외한 리스트 

    left_side = [x for x in tail if x <= pivot] # 분할된 왼쪽 부분
    right_side = [x for x in tail if x > pivot] # 분할된 오른쪽 부분

    # 분할 이후 왼쪽과 오른쪽 부분에서 각각 정렬을 수행하고, 전체 리스트를 반환
    return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```

#### 계수 정렬 (Count Sort)

- 데이터의 크기 범위(정수, 1,000,000)가 제한되어 정수 형태로 표현되어 있을 때만 유효
    - 예를 들어, 0 이상 100 이하인 성적 데이터를 정렬할 때 계수 정렬이 효과적
- 일반적으로 별도의 리스트를 선언하고 그안에 정렬에 대한 정보를 담기 때문에 데이터의 크기가 한정됨
- 모든 데이터가 양의 정수인 상황에서 데이터의 개수를 N, 데이터의 최댓값을 K라고 할 때 시간복잡도는 O(N+K)

```py
array = [7,5,9,0,3,1,6,2,4,8]

# 모든 범위를 포함하는 리스트 선언 (모든 값은 0으로 초기화)
# 리스트에서 가장 큰 값을 찾고 인덱스로 표현되기 때문에 1 추가
count = [0] * (max(array)+1)

for i in range(len(array)):
    count[array[i]] += 1

for i in range(len(count)):
    for j in range(count[i]):
        print(i, end=' ') # 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력
```

#### 라이브러리를 활용한 정렬

- 튜플인 경우 정렬하기 

```py
array = [('홍길동', 95), ('이순신', 77)]
sorted_array = sorted(array, key=lambda x: x[1])
```

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

### 다이나믹 프로그래밍 (Dynamic Programming)

- 완전 탐색으로 풀기 어려울 때, 다음 조건을 만족하면 다이나믹 프로그래밍을 사용할 수 있음 
    1. 큰 문제를 작은 문제로 나눌 수 있다.
    2. 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다.
- 피보나치 수열과 같이 점화식으로 표현가능한 문제에 대해 다이나믹 프로그래밍을 적용할 수 있음 
- 다음과 같이 중간 값을 저장할 dp 테이블을 만듦!

```py
# 앞서 계산된 결과를 저장하기 위한 DP 테이블 초기화
dp = [0] * 100

# 첫번째, 두번째 피보나치 수는 1
dp[1] = 1
dp[2] = 1
n = 99

# 피보나치 함수 반복문으로 구현 (보텀업 다이나믹 프로그래맹)
for i in range(3, n+1):
    dp[i] = dp[i-1] + dp[i-2]

print(dp[n])
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