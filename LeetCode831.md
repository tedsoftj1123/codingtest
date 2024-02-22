https://leetcode.com/problems/car-fleet/description/

```python
Input: target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]
Output: 3
```

### 사용 알고리즘

- monotonic stack

## 풀이

- 차들이 지나갈 수 있는 도로는 한개
- 어떤 한 차가 **앞에 있는 차의 속도보다 빠르게 달려서 target에 도달하기 전에 앞차와 만나면** Car Fleet상태
- CarFleet상태가 되면 뒤에 있는 차는 앞에 있는 차의 속도에 맞게 달림 → 한 개의 차로 봐도됨

`CarFleet되는지 판변하는방법`

target에 도달하는 시간이 뒤에있는 차가 앞에있는 차보다 빠르면 얘들은 CarFleet상태가 됨

각 차별로 target에 도달하는 시간 공식: (target - position[i]) / speed[i]

따라서

1. input으로 주어진 차들을 speed와 묶어서 오름차순 정렬(도로 상태 표현을 위해)
2. 스택에 position과 speed정보 push
3. 가장 target에 근접한 차들 순으로 그 전 차와 CarFleet상태가 되는지 확인
4. CarFleet상태가되면 앞에차랑 뒤에차는 속도가 앞에 차인 차 한개임으로 push했던 차 정보 pop
5. 모두 돈 다음 stack에 남아있는 요소들의 개수가 CarFleet덩어리들의 개수

```python
def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        pair = [[p, s] for p, s in zip(position, speed)]

        stack = []
        for p, s in sorted(pair)[::-1]: # input을 position별로 오름차순 정렬
            stack.append((target - p) / s) # 현제 차 정보 push
            if len(stack) >= 2 and stack[-1] <= stack[-2]: # CarFleet 판별식
                stack.pop() # CarFleet이면 pop
        return len(stack)
```