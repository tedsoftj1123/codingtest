https://leetcode.com/problems/reorder-list/description/

```python
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

### 사용 알고리즘

- two pointers
- linked list

### 풀이

input으로 들어온 연결리스트값들을 배열로 넣고

맨 처음과 끝에 포인터를 두어 좌우 번갈아가면서 해당 값을 업데이트해주면됨

```
def reorderList(self, head: Optional[ListNode]) -> None:
        buf = head
        stack = []
        while buf:
            stack.append(buf.val)
            buf = buf.next
        
        l, r = 0, len(stack) - 1
        rev = False
        while l <= r and head:
            if rev:
                head.val = stack[r]
                r -= 1
            else:
                head.val = stack[l]
                l += 1
            rev = not rev
            head = head.next
```