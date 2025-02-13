# LeetCode Sliding Window 문제

- 푼 일자: 2025년 2월 7일
- 알고리즘: Sliding Window
- 난이도: ⭐️ (Easy)

### Contains Duplicate 2

- link: https://leetcode.com/problems/contains-duplicate-ii/description/
- Brute Force로 풀기 

```py
# 시간 초과되는 풀이
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        for i in range(len(nums)):
            for j in range(len(nums)):
                if i != j:
                    if (nums[i] == nums[j]) and (abs(i-j) <= k):
                        return True
        return False
```

- key, value 형태의 해시 딕셔너리를 사용해서 풀기 

```py
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        s = {}  # value --> index 

        for i in range(len(nums)):
            if nums[i] in s and abs(s[nums[i]] - i) <= k:
                return True  # 같은 숫자가 k 이하 거리 내에서 등장하면 True 반환
                
            s[nums[i]] = i  # 현재 숫자의 인덱스를 업데이트

        return False  # 중복을 발견하지 못하면 False 반환
```

### Best Time to Buy and Sell Stock

- link: https://neetcode.io/problems/buy-and-sell-crypto
- Sliding Window와 Two Pointers를 사용한 풀이
    - 최소 매수 가격을 유지하면서 최대 매도 가격을 갱신하는 방식으로 진행

```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = float('inf') # 최소 매수가격 (무한대로 초기화)
        max_profit = 0 # 최대 이익 (초기값 0)

        for price in prices:
            # 최소 매수가격이 더 작게 업데이트
            if min_price > price:
                min_price = price

            # 손익계산
            profit = price - min_price
            max_profit = max(max_profit, profit) # 최대 이익갱신
        
        return max_profit
```