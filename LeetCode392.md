https://leetcode.com/problems/is-subsequence/description/

```python
Input: s = "abc", t = "ahbgdc"
Output: true
```

### 사용 알고리즘

- two pointers

### 풀이

원래 정석은 hash를 사용하는것 같은데 그냥 s, t에 각각 포인터를 두고 값들을 비교하면서 쭉 찾으면 O(N)시간복잡도로 해결할 수 있음

```
def isSubsequence(self, s: str, t: str) -> bool:
        i, j = 0, 0
        while i < len(s) and j < len(t):
            if s[i] == t[j]:
                i += 1
            j += 1
        return i == len(s)
```