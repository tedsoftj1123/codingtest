https://leetcode.com/problems/balanced-binary-tree/description/

```python
Input: root = [3,9,20,null,null,15,7]
Output: true
```

### 사용 알고리즘

- binary tree
- dfs

### 풀이

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d911241-a612-47be-bc81-7c7d65dec65c/d176b7cb-eaf7-483f-a1f3-cdfae9c766e3/Untitled.png)

주어진 트리가 균형트리인지 확인해야함.

`균형 트리란?`

- 노드의 왼쪽 노드의 깊이와 오른쪽 노드의 깊이의 차이가 1 이하인 트리

dfs를 이용해 리프노드까지 가고, 계산한 왼쪽노드, 오른쪽 노드의 깊이 중 더 깊은 값 + 1을 반환하면됨

값을 구하는 과정에서 오른쪽 노드깊이와 왼쪽 노드깊이의 차이가 2이상이면 결과값 flase반환

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.result = True
    def dfs(self, node: Optional[TreeNode]):
        if node is None: return 0
        l = self.dfs(node.left)
        r = self.dfs(node.right)
        if abs(l - r) > 1: self.result = False
        return max(l, r) + 1

    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        self.dfs(root)
        return self.result
```