https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/

```python
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
```

### 사용 알고리즘

- binary tree
- dfs

### 풀이

주어진 p, q노드의 최대 깊이 조상 노드를 찾아야됨 input tree는 이진 탐색 트리이다.

`**이진 탐색 트리란?**`

- 노드의 왼쪽 노드의 값은 항상 현제 노드보다 작고 오른쪽 노드의 값은 현제 노드보다 크다.

주어진 p, q가 input tree에 존재하지 않는 경우는 없기 때문에 BST의 특징을 이용해서 p, q노드에 도달하기 위한 경로(ex. 1 → 2 → 5→ 7)를 각각 계산하고 두 경로에서 겹치는 경로 중 가장 깊은 노드를 반환하면 됨

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def __init__(self):
        self.path = []

    def dfs(self, cur: 'TreeNode', target: 'TreeNode'):
        self.path.append(cur)
        if cur == target:
            return

        if target.val < cur.val:# 작으면 왼쪽
            self.dfs(cur.left, target)
        else:# 크면 오른쪽
            self.dfs(cur.right, target)

    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        self.dfs(root, p)
        pPath = self.path # 루트에서 p까지 가는 경로
        self.path = []

        self.dfs(root, q) # 루드에서 q까지 가는 경로
        qPath = self.path

        result = None
        for i in range(min(len(qPath), len(pPath))):# 같은 경로 중 가장 깊이가 깊은 노드 반환
            if qPath[i] == pPath[i]: result = pPath[i]
        return result
        
```