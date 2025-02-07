# LeetCode Stack 문제

- 푼 일자: 2025년 2월 6일
- 알고리즘: Stack
- 난이도: ⭐️ (Easy)

### Baseball Game

- link: https://leetcode.com/problems/baseball-game/description/
- 리스트에서 맨 뒤에꺼 삭제하는 방법은 `pop()` 사용! 

```py
class Solution:
    def calPoints(self, operations: List[str]) -> int:
        records = []

        for l in operations:
            if l == 'C':
                records.pop()
            elif l == '+':
                records.append(records[-1]+records[-2])
            elif l == 'D':
                records.append(records[-1]*2)
            else:
                records.append(int(l))
        return sum(records)
```

### Valid Parentheses

- link: https://neetcode.io/problems/validate-parentheses

```py
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        table = {
            '}':'{',']':'[',')':'('
        }

        for char in s:
            # 여는 괄호인 경우 추가
            if char in table.values():
                stack.append(char)
            # stack이 비어있지 않고 닫는 괄호 왼쪽에 여는 괄호가 있는 경우
            elif stack and table[char] == stack[-1]:
                stack.pop()
            # 닫는 괄호 옆에 여는 괄호가 없다면 Flase
            else:
                return False
        
        # stack에 여는 괄호가 남아있다면 
        if stack:
            return False
        return True
```