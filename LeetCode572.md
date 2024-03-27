https://leetcode.com/problems/subtree-of-another-tree/description/

```python
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```

### 사용 알고리즘

- binary tree
- bfs
- dfs

### 풀이

먼저 입력받은 root노드를 탐색하고, subRoot의 값과 같은 경우 해당 노드를 루트로하는 트리가 입력받은 subRoot와 같은 형태를 가지는지 dfs로 탐색하여 해결한다.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def check(self, target1: Optional[TreeNode], target2: Optional[TreeNode]) -> bool:
        if target1 is None and target2 is None:
            return True
        elif target1 is None or target2 is None:
            return False

        leftCheck = self.check(target1.left, target2.left) and target1.val == target2.val
        rightCheck = self.check(target1.right, target2.right) and target1.val == target2.val

        if leftCheck and rightCheck:
            return True
        else: return False

    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        queue = collections.deque([root])
        while queue:
            buf = queue.popleft()
            if buf == None: continue
            if buf.val == subRoot.val and self.check(buf, subRoot):
                return True
            queue.append(buf.left)
            queue.append(buf.right)
        return False
        

        
```