# LeetCode Two Pointer 문제

- 푼 일자: 2025년 2월 6일
- 알고리즘: Two Pointers
- 난이도: ⭐️ (Easy)

### Reverse String

- link: https://leetcode.com/problems/reverse-string/description/

```py
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        end = len(s)-1
        start = 0

        while start < end:
            s[start], s[end] = s[end], s[start]
            start += 1
            end -= 1
```

### Valid Palindrome

- link: https://neetcode.io/problems/is-palindrome

```py
# Reverse로 해결한 문제! 
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        ref = re.sub(r"[^a-zA-Z0-9]","",s).lower()
        return ref == ref[::-1]
```

```py
# 투 포인터로 해결한 문제
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        ref = re.sub(r"[^a-zA-Z0-9]","",s).lower()
        start, end = 0, len(ref)-1

        while start < end:
            if ref[start] != ref[end]:
                return False
            start += 1
            end -= 1

        return True
```

### Valid Palindrome 2

- link: https://leetcode.com/problems/valid-palindrome-ii/description/

- 아래와 같이 하니까 Time Limit Exceeded가 나옴! 
```py
class Solution:
    def validPalindrome(self, s: str) -> bool:
        # 삭제 안해도 대칭일 때! 
        if s == s[::-1]:
            return True
        
        # 최소 1개 삭제해야 대칭일 때! (하나라도 True 나오면 됨)
        for i in range(len(s)):
            new_s = s[:i] + s[i+1:]
            if new_s == new_s[::-1]:
                return True
        
        return False
```

- Two Pointer로 문제 풀기

```py
class Solution(object):
    def validPalindrome(self, s: str) -> bool:
        left, right = 0, len(s) - 1
        while left < right:
            if s[left] != s[right]:
                # one은 오른쪽 문자 삭제
                # two는 왼쪽 문자 삭제
                one, two = s[left:right], s[left + 1:right + 1]
                return one == one[::-1] or two == two[::-1]
            left, right = left + 1, right - 1
        return True  # 끝까지 while한건 원래 팰린드롬이란 얘기
```

### Merge Strings Alternately

- link: https://leetcode.com/problems/merge-strings-alternately/description/

```py
# 내가 맞춘 문제!
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        answer = ""
        loc = 0

        while loc < len(word1) and loc < len(word2):
            answer += word1[loc]
            answer += word2[loc]
            loc += 1

        if loc == len(word1):
            answer += word2[loc:]
        else:
            answer += word1[loc:]

        return answer
```

```py
# 더 빠르게 푼 문제
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        answer = ""
        len1 = len(word1)
        len2 = len(word2)
        
        for i in range(max(len1, len2)):
            if i < len1: 
                answer += word1[i]
            if i < len2:
                answer += word2[i]
        return answer
```

### Remove Duplicates from Sorted Array

- link: https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/
- 아이디어: 둘의 자리를 바꾸는게 아니라 고정된 값을 다른 값으로 땡겨와주는 것! 

```py
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) == 0: return 0

        i = 0 # 고정포인터
        for j in range(1, len(nums)): # 이동포인터
            if nums[i] != nums[j]:
                i += 1
                nums[i] = nums[j]
        return i+1
```