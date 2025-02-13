# LeetCode Array & Hash 문제

- 푼 일자: 2025년 2월 6일
- 알고리즘: Array & Hash
- 난이도: ⭐️ (Easy)

### Concatenation of Array
- link: https://leetcode.com/problems/concatenation-of-array/description/ 
```py
# 내 풀이
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        n = len(nums)
        ans = [0] * 2*n  # 2n해서 오류남..ㅋㅋ 
        ans[:n+1] = nums
        ans[n:] = nums  # 처음에 n+1로 해서 오류남..ㅋㅋ
        return ans

# 더 정답스러운 풀이 
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [0] * (2 * n)  # Create a new list of size 2n
        for i in range(n):
            result[i] = nums[i]      # Copy the first part
            result[i + n] = nums[i]  # Copy the second part
        return result
```

### Contains Duplicate
- link: https://neetcode.io/problems/duplicate-integer

```py
# 내 풀이
class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        if len(nums) != len(set(nums)):
            return True
        else:
            return False
```

### Valid Anagram
- link: https://neetcode.io/problems/is-anagram
- Anagram의 정의는 정반대로 구성된 것이 아니라, 두 단어의 문자 구성이 같다면(각 문자의 개수가 동일하다면) 아나그램임. 예를 들어 "anagram"과 "nagaram"도 아나그램이라고 볼 수 있음

```py
# Anagram 구하기! (거꾸로해도 이효리 같은거!)
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
            
        return sorted(s) == sorted(t)
```
- 해시 테이블(딕셔너리)로 해결하는 문제
- `countS[s[i]] = 1 + countS.get(s[i], 0)`은 외우자! 해시테이블로 빠르게 문자 등장 횟수를 세는 방법!

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

### Two Sum

- link: https://neetcode.io/problems/two-integer-sum
- 처음엔 간단히 Brute Force로 풀었는데 시간복잡도가 O(N^2)이라 다른 방법을 찾아봄
- 해시맵을 사용해서 다음과 같이 풀 수 있음 
- 아이디어는 index와 value로 dict를 만든 다음에 뺀 값이 그 dict에 있는지 확인하고, index가 다른지 본다!

```py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        indices = {}  # value -> index

        for i, v in enumerate(nums):
            indices[v] = i
        
        for i, v in enumerate(nums):
            diff = target - v
            if diff in indices and indices[diff] != i:
                return sorted([indices[diff], i])
```

### Longest Common Prefix

- link: https://leetcode.com/problems/longest-common-prefix/description/
- 아이디어: (1) 가장 길이가 짧은 단어 찾기, (2) 가로로 한개씩 보기 Or 세로로 보기?
- 이건 풀지못했음!!! 외워라!!!

```py
# 이 방식은 1ms가 걸림
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs: #빈 배열이면
        	return ''
        minStr = min(strs, key = len)

        # 가로로 하나씩 맞는지 확인! -> 같지 않다면 그 이전까지 제공
        for i, x in enumerate(minStr):
        	for other in strs:
            	if other[i] !=x:
                	return minStr[:i]
        return minStr  # for문이 다 돌아갔다면 그럼 이게 정답인거지! 
```
- 이건 잘 모르겠음...!
```py
# 이 방식은 0ms가 걸림
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        res=""
        for i in range(len(strs[0])):
            for s in strs:
                if i==len(s) or s[i] != strs[0][i]:
                    return res
            res+= strs[0][i]
        return res
```

### Remove Element

- link: https://leetcode.com/problems/remove-element/description/ 
- 문제를 이해하기가 힘들었는데... 굳이 val와 같은 원소를 삭제하지 않아도 됨. "_"로 바꿔주지도 않아도 됨
- 정수 리스트 nums에서 val에 해당하는 정수 요소를 제거하고, nums에서 val 값과 다른 요소의 갯수 k를 리턴nums의 처음 k번째 이후의 요소는 어떤 요소가 와도 상관이 없다.

```py
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        k = 0  # 저장할 인덱스 
        for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]
                k += 1
        return k
```

### Problem List

- link: https://leetcode.com/problems/majority-element/
- 최적화 방법이 잘 이해안감...

```py
# 내가 맞춘 풀이: 10ms 걸림! -> 최적화 필요
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        n = len(nums)
        uniques = set(nums)
        answer = 0
        
        for num in uniques:
            # num의 등장횟수 세기
            count = 0
            for j in nums:
                if j == num:
                    count += 1
            # majority 조건 만족하고 이전의 answer와 다를때! 
            if count > (n/2) and answer != num:
                answer = num

        return answer
```

