https://leetcode.com/problems/binary-tree-level-order-traversal/

```python
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

### 사용 알고리즘

- binary tree
- bfs

### 풀이

기존 bfs와 동일한 방식으로 트리를 탐색하는데, queue에 level정보를 함께 저장하고 pop될 때 레벨별 해시테이블에 value값 추가, 마지막에 2차원 배열로 변환

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        queue = collections.deque([(root, 0)])
        level = collections.defaultdict(list)
        while queue:
            cur = queue.popleft()
            if cur[0] is None: continue
            level[cur[1]].append(cur[0].val)

            queue.append((cur[0].left, cur[1] + 1))
            queue.append((cur[0].right, cur[1] + 1))
        
        result = []
        for val in level.values(): result.append(val)
        return result
        
```