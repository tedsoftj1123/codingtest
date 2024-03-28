https://leetcode.com/problems/diameter-of-binary-tree/description/

```python
Input: root = [1,2,3,4,5]
Output: 3
```

### 사용 알고리즘

- binary tree
- dfs
- backtracking

### 풀이

먼저 문제를 작은 단위로 나누어보자. 문제 요구사항에 따르면 루트 노드의 diameter, 지름은 왼쪽 자식 트리의 깊이 + 오른쪽 자식 트리의 깊이 이다.

그렇다면 노드의 최대 깊이가 입력 받은 루트 노드의 왼쪽 트리 깊이 + 오른쪽 트리 깊이냐? 그건 또 아닐 수가 있다. 만약 오른쪽 또는 왼쪽 트리의 diameter가 더 크다면 최종 결과는 해당 트리의 diameter가 된다.

해당 로직을 dfs로 구현하면 쉽게 해결할 수 있다. 함수에선 왼쪽 트리와 오른쪽 트리의 깊이 중 더 큰 값을 반환하고 동시에 두 갚의 합이 최종 결과보다 크면 저장한다.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.ans = 0
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        def d(n: Optional[TreeNode]) -> int:
            if not n: return 0
            l, r = d(n.left), d(n.right)
            self.ans = max(self.ans, l + r)
            return 1 + max(l, r)
        d(root)
        return self.ans
        
```