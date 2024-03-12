https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/

```python
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

### 사용 알고리즘

- linked list
- fast and slow pointers

### 풀이

!https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg

주어진 Linked List는 단방향이기 때문에 해당 리스트의 끝을 찾아도 뒤로 돌아갈 수 없다.

이를 해결하기 위해 two pointer를 이용하여 문제를 해결할 수 있다.

1. 처음 노드에 slow pointer, 그리고 입력받은 n - 1 만큼 떨어진 곳에 fast pointer를 둔다.
2. slow, fast 포인터를 오른쪽으로 한노드씩 계속 움직여 fast포인터가 List의 끝에 갈때까지 반복
3. fast 포인터가 끝에 닿았다는것은 끝에서 부터 n - 1만큼 떨어진 곳에 slow포인터가 위치함
4. 문제는 n만큼 떨어진 곳에있는 노드를 제거하는것이기때문에 [slow.next](http://slow.next) = slow.next.next로 할당하여 노드를 제거한다.
5. 끗

EdgeCase

- 위와같은 방식으로 문제를 해결하였을 때 문제점이 존재한다.
- 만약 지워야하는 노드가 첫번째 노드라면? 원래 방식은 지워야하는 노드 이전 노드에서 [slow.next](http://slow.next) = [slow.next.next](http://slow.next.next) 이런식으로 노드를 지웠는데 이 방식이 안먹힘
- 근데 이제 지워야하는 노드가 첫번째인경우는 fast 포인터가 리스트끝을 넘어가기 때문에(None) fast포인터를 먼저 옮기는 과정에서 최종결과의 fast포인터가 None이면 결과값을 head.next를 넘겨주면됨

```
def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        l, r = head, head

        for _ in range(n):
            r = r.next
        if not r: return head.next

        while r.next:
            l, r = l.next, r.next
        l.next = l.next.next

        return head
```