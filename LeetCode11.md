https://leetcode.com/problems/container-with-most-water/description/

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```python
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
```

### 사용 알고리즘

- two pointers

### 풀이

가장 물을 많이 수용할 수 있는 물의 양을 구한다. 이중 for문을 이용해 일일이 다 비교하면 O(N^2)이됨으로 더 효율적인 방법이 필요함 → two pointer

- 왜? 많이 담을 수 있는 기준이 좌우로 넓거나 위로 넓거나인데
- 일단 맨 왼쪽이랑 오른쪽 막대를 선택함으로써 좌우로 가장 넓은 경우의 물의 양을 찾고
- 포인터를 옮길 때 최대한 물을 더 담을 수 있는 방향을 찾도록 처음에 선택한 두 개의 막대기 중 작은 쪽의 포인터를 옮기면됨
- O(N)으로 해결 가능

```python
def maxArea(self, height: List[int]) -> int:
        s = 0
        l = len(height) - 1
        maxContain = -1
        while s < l:
            dff = l - s
            water = height[s] * dff if height[s] < height[l] else height[l] * dff
            if water > maxContain:
                maxContain = water
            if height[s] < height[l]:
                s += 1
            else: l -= 1
        return maxContain
```