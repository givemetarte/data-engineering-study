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
            end = mid + 1
```
