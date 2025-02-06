# 백준 2470 두 용액

- 푼 일자: 2025년 1월 17일
- 걸린 시간: 54분 30초 (해결 못해서 해답을 찾아봄)
- 링크: https://leetcode.com/problems/merge-sorted-array/description/
- 알고리즘: 투 포인터
- 난이도: ⭐️

### 풀이법

- 투 포인터라는 문제라고 생각해야 풀 수 있는 문제
- 라이브로 이중 for문을 생각했다가 결국 문제를 풀지 못했음...! 
- 멘토링 때 푼 문제는 nums1에 추가해야 한다는 조건이 충족되지 못했기 때문에 다시 풀었음 

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


