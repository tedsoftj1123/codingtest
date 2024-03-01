https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/

```python
Input: nums = [3,4,5,1,2]
Output: 1
```

### 사용 알고리즘

- binary search

### 풀이

오름차순으로 정렬된 배열을 오른쪽으로 n번 회전하여 배열에서 가장 작은 수를 찾아야함.

O(N)시간복잡도로 배열 전체를 한번 순회하면 찾을 수 있지만 우린 binary search를 이용해 탐색해야하는 요소를 확확 줄여서 O(logN)시간복잡도록 해결하여야함

해당 배열에서 binary search를 하기 위한 특징을 알아보자

- 정석풀이로는 left, right포인터를 양 끝에 두고 mid값을 확인하고 보통은 주어진 target이랑 일치하는지 확인해야되는데 위 경우는 target이 없어 다른 방식으로 접근하여야한다.
- 일단 O(logN)으로 풀기 위해 mid를 기준으로 어떤 조건에 따라 오른쪽 아니면 왼쪽에 최소 값이 없다는걸 보장할 수 있어야된다
- 이는 오름 차순으로 정렬된 배열이 **오른쪽** 으로 회전했다는 사실을 통해 찾을 수 있다.
- 바로 mid의 값이 배열의 오른쪽 끝의 값보다 크면 최소 값은 무조건 오른쪽에 있다는 사실
    - 왜? mid값이 오른쪽 끝 요소보다 작다는건 이 배열이 정렬된 배열이기에 mid값 보다 작은 값든은 오른쪽에 있을 수 없기 때문
    - 따라서 최소값이 있다고 보장할 수 있는 범위는 왼쪽끝부터 자기 인덱스까지이다
- 따라서 이 과정을 반복함으로써 O(logN)의 시간복잡도로 가장 작은 요소를 찾을 수 있다.

```
def findMin(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[right]:
                left = mid + 1
            else:
                right = mid
        return nums[left]
```