# 注意
>[!important]
>这个题型一定要记住
>这个代码思路，非常有用！！！！！
```python
dir = [(1, 0), (0, 1), (-1, 0), (0, -1)]

m, n = map(int, input().split())
data = []
for i in range(m): data.append(input().split())

x, y = -1, 0
d = 0
sum = 0
while sum < m * n:
    sum += 1
    now_x, now_y = x + dir[d][0], y + dir[d][1]
    if now_x < 0 or now_x >= m or now_y < 0 or now_y >= n or data[now_x][now_y] == -1:
        d = (d + 1) % 4
        x, y = x + dir[d][0], y + dir[d][1]
    else:
        x, y = now_x, now_y
    
    print(data[x][y], end=' ' if sum != m * n else '')
    data[x][y] = -1
```