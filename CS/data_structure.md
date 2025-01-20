# 자료구조 (Data Structure)

- 작성일: 2025년 1월 20일 

### 자료구소란? 

- 데이터를 표현하고 관리하고 처리하기 위한 구조
- 가장 기초 개념으로 스택과 큐가 언급됨

### 스택(stack) 

- 데이터를 순서대로 저장하고 삭제하는 방법 제공, 후입선출(Last in, First Out; LIFO)
- 스택의 가장 대표적인 예시는 웹 브라우저의 뒤로가기 기능 (뒤로가기 버튼을 누를 때마다 가장 최근에 방문한 페이지부터 역순으로 이동)
- 파이썬에서 별도의 라이브러리를 사용하지 않고 `append()`와 `pop()`만 사용하면 됨 

```py
stack = []

# 삽입(5) - 삽입(2) - 삽입(3) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
stack.append(5)
stack.append(2)
stack.append(3)
stack.pop()
stack.append(1)
stack.append(4)
stack.pop()

print(stack)  # 최하단 원소부터 출력
print(stack[::-1])  # 최상단 원소부터 출력
```

### 큐(queue) 

- 가장 먼저 삽입된 요소가 가장 먼저 제거됨, 선입선출(First in, First Out; FIFO)
- 보통 `collections` 모듈에서 제공하는 `deque` 자료구조를 활용

```py
from collections import deque

queue = deque()

# 삽입(5) - 삽입(2) - 삽입(3) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
queue.append(5)
queue.append(2)
queue.append(3)
queue.popleft()
queue.append(1)
queue.append(4)
queue.popleft()

print(queue)  # 먼저 들어온대로 출력
queue.reverse()  # 다음 출력을 위해 역순으로 변경
print(queue)  # 나중에 들어온 원소부터 출력
```