# LeetCode Binary Search 문제

- 푼 일자: 2025년 2월 7일
- 알고리즘: Binary Search
- 난이도: ⭐️ (Easy)

### Binary Search

- link: https://neetcode.io/problems/binary-search
- 투 포인터와 다르게, 이분 탐색은 mid값을 +1, -1한다는 것! 
- while 구문 안에 mid가 업데이트 되어야 함! 

```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        start, end = 0, len(nums)-1

        while start <= end:
            mid = (start+end) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                start = mid + 1
            else:
                end = mid - 1
        
        return -1
```

### Search Insert Position

- link: https://leetcode.com/problems/search-insert-position/description/
- 타깃이 정확히 없는 경우는 start의 위치를 반환해야 최적의 위치일 수 있음! 


```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        start, end = 0, len(nums)-1

        while start <= end:
            mid = (start + end) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                start = mid+1 
            else:
                end = mid-1

        return start
```

### Guess Number Higher or Lower

- link: https://leetcode.com/problems/guess-number-higher-or-lower/description/

```py
# The guess API is already defined for you.
# @param num, your guess
# @return -1 if num is higher than the picked number
#          1 if num is lower than the picked number
#          otherwise return 0
# def guess(num: int) -> int:

class Solution:
    def guessNumber(self, n: int) -> int:
        start, end = 1, n

        while start <= end:
            mid = (start+end)//2
            if guess(mid) == 0:
                return mid
            elif guess(mid) == 1:
                start = mid + 1
            else:
                end = mid - 1
```

