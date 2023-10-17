https://www.acmicpc.net/problem/20436

- 구현 문제
- 키보드판 입력시 따로 입력하지 말고 list()쓰면 된다
- 간단한거 빨리 구현하는 연습 

```python
from collections import deque

lt_char, rt_char = input().split()
dest = list(input())

mapp = [list('qwertyuiop'),
        list('asdfghjkl'),
        list('zxcvbnm')]
diction = {}
for x, i in enumerate(mapp):
    for y, ii in enumerate(i):
      diction[ii] = (x, y)

lt_x, lt_y = diction[lt_char]
rt_x, rt_y = diction[rt_char]

answer = 0
queue = deque(dest)

while queue:
    char = queue.popleft()
    ith_x, ith_y = diction[char]
    # 자음 or 모음
    if (ith_x==0 and ith_y<=4) or (ith_x==1 and ith_y<=4) or (ith_x==2 and ith_y<=3):
      answer += abs(ith_x - lt_x) + abs(ith_y - lt_y)
      # print(f'{char}, {abs(ith_x - lt_x) + abs(ith_y - lt_y)}')
      lt_x, lt_y = ith_x, ith_y
    else:
      answer += abs(ith_x - rt_x) + abs(ith_y - rt_y)
      # print(f'{char}, {abs(ith_x - rt_x) + abs(ith_y - rt_y)}')
      rt_x, rt_y = ith_x, ith_y
    answer += 1
    # print('plus 1')
print(answer)
```