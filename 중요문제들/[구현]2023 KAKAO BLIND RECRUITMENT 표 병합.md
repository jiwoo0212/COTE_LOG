# 2023 KAKAO BLIND RECRUITMEN 표 병합

- 구현문제
- 카카오공식 풀이와 비슷한 발상. but merge테이블에 루트가 되는 위치의 좌표만 저장하는 것이 아니라 머지된 그룹의 모든 좌표를 리스트에 담는 것으로 생각
- 그러나 머지된 칸의 대표되는 칸의 좌표만 있으면 됌
- 공식풀이 로직대로 구현하고 프로그래머스 토론란의 모든 테케 통과하는데도 몇개 테케가 통과가 안된다....
- 시간상 디버깅안했지만 얻은 것은 테이블에서 어떤 것을 결합할 때 모든 값을 고려하기 보다 하나의 시작점만 고려하는 생각해보기

```python
from copy import deepcopy

def solution(commands):
    answer = []
    grid = [[ 'EMPTY' for _ in range(51)] for _ in range(51)]
    merged = [[() for _ in range(51)] for _ in range(51)]
    for i in range(51):
        for ii in range(51):
            merged[i][ii] = (i, ii)
    for i in commands:
        comm = i.split()
        if comm[0] == 'UPDATE':
            # print('update!!')
            if len(comm)==4:
                _, r, c, val = comm
                r, c = int(r), int(c)
                x, y = merged[r][c]
                grid[x][y] = val
            else:
                # print('update2')
                _, val1, val2 = comm
                for r in range(51):
                    for c in range(51):
                        if grid[r][c]==val1:
                            grid[r][c] = val2

        elif comm[0] == 'MERGE':
            # print('merge!')
            _, r1, c1, r2, c2 = comm
            r1, c1, r2, c2 = int(r1), int(c1), int(r2), int(c2)
            if (r1, c1)==(r2, c2):
                continue
            x1, y1 = merged[r1][c1]
            x2, y2 = merged[r2][c2]
            for row in range(51):
                for col in range(51):
                    if merged[row][col]==(x2, y2):
                        merged[row][col] = (x1, y1)
            if grid[x1][y1]=='EMPTY' and grid[x2][y2]!='EMPTY':
                grid[x1][y1] = grid[x2][y2]
                
                    
        elif comm[0] == 'UNMERGE':
            # print('UNMERGE')
            _, r, c = comm
            r, c = int(r), int(c)
            x,y = merged[r][c]
            tmp = grid[x][y]
            # print('tmp', tmp)
            for row in range(51):
                for col in range(51):
                    if merged[row][col]==merged[r][c]:
                        merged[row][col] = (row, col)
                        grid[row][col] = 'EMPTY'
            grid[r][c] = tmp
                        
        elif comm[0] == 'PRINT':
            # print('print')
            _, r, c = comm
            r, c = int(r), int(c)
            x, y = merged[r][c]
            answer.append(grid[x][y])
        # for row in range(5):
        #     print(grid[row][:5])
        # for row in range(5):
        #     print(merged[row][:5])
        # print('-'*20)
    return answer
                
        
                    
                    
                            
                            
                        
```
