https://school.programmers.co.kr/learn/courses/30/lessons/43164

```python
Input: [["ICN", "JFK"], ["HND", "IAD"], ["JFK", "HND"]]
Output: ["ICN", "JFK", "HND", "IAD"]
```

### 사용 알고리즘

- dfs
- backtracking

### 풀이

한 공항에서 갈 수 있는 공항정보 및 티켓정보 를 hashmap을 통해 저장한다. 도착 공항 정보는 공항이름순으로 정렬하여서 결과값이 항상 이름순으로 정렬될 수 있도록함

이후 저장된 hashmap정보를 바탕으로 인청공항으로부터 dfs탐색을 실행하고 입력받은 티겟을 모두 사용하면 해당 path를 반환

```python
import collections

def solution(tickets):
    hashmap = collections.defaultdict(list)
    for i in range(len(tickets)):
        hashmap[tickets[i][0]].append((i, tickets[i][1]))
        hashmap[tickets[i][0]].sort(key=lambda x: x[1])

    results = []

    def dfs(st, used, left, path):
        if left == 0:
            results.append(path)
            return
        for i, to in hashmap[st]:
            if not used[i]:
                used[i] = True
                dfs(tickets[i][1], used, left - 1, path + [to])
                used[i] = False

    dfs("ICN", [False for _ in range(len(tickets))], len(tickets), ["ICN"])
    return results[0]
```