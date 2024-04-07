https://leetcode.com/problems/combination-sum/description/

```python
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
```

### 사용 알고리즘

- dfs
- backtracking

### 풀이

[2, 3, 6, 7]이 있을때 target숫자인 7을 만들기 위해서 먼저 0번째 인덱스로부터 시작, 다음 숫자가 가능 한 경우는 0번째 인덱스 포함 input 배열의 끝까지이고 해당 경우의 수들을 for문을 사용해서 반복하고 해당 숫자의 인덱스로부터 다시 같은 연산을 수행하면 모든 경우의 수를 탐색할 수 있고, 각 경우의 수들 중 sum과 같은 합이 나오는 경우 해당 숫자까지 도달한 루트를 결과값에 저장

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        result = []
        def dfs(nums, sum, path):
            nonlocal result
            if sum >= target:
                if sum == target:
                    result.append(path)
                return

            for i in range(len(nums)):
                dfs(nums[i:], sum + nums[i], path + [nums[i]])
            
        dfs(candidates, 0, [])
        return result
```