https://school.programmers.co.kr/learn/courses/30/lessons/150365

# 미로 탈출 명령어

## 핵심은 break
bfs로 단순히 구현하면 당연히 시간초과된다.

break문이 핵심이다. 

더욱 빠른 알파벳 경로로 가는게 가능하다? -> 뒤의 다른 방향으로는 탐색안해도 된다.

그외에도 알파벳순이기때문에 처음 정답을 발견한다면? -> 정답임

## 그외

- impossible 되는 경우는 최단거리가 아닌 돌아서 갈때 k를 만족못하는 경우 외에도 그냥 최단거리로도 k만족하면서 못가는 경우도 고려해야함
- 고민 30분 이상 하고 안되면 그냥 다른 방법으로 빠르게 시도 or 솔루션 보자 시간낭비 ㄴㄴ
- 그리디하게 or 규칙 기반으로 풀려고 했는데 케이스정리하다가 시간다감


```python
from collections import deque
def solution(n, m, x, y, r, c, k):
    if (k-abs(x-r)+abs(y-c))%2!=0:
        return 'impossible'
    if abs(x-r)+abs(y-c)>k:
        return 'impossible'
    x -=1
    y -=1
    r -=1
    c-=1
    answer = ''
    dx = [1, 0, 0, -1]
    dy = [0, -1, 1, 0]
    pos = ['d','l','r','u']
    queue = deque([(x,y,0,'')])
    while queue:
        x,y,step, his = queue.popleft()
        if x==r and y==c and step==k:
            return his
        for i in range(4):
            nx, ny = x+dx[i], y+dy[i]
            if nx<0 or nx>n-1 or ny<0 or ny>m-1:
                continue
            if abs(nx-r)+abs(ny-c)>k-step-1:
                continue
            queue.append([nx, ny, step+1, his+pos[i]])
            break
    # return 'impossible'
```