# 自己的思路
举例子进行分析的时候，发现，当前位置距离最远端的位置乘2，就是能生长的最高长度

```python
import os
import sys

# 请在此输入您的代码
n = int(input())
data = [0] * n

start, end = 0, n-1
for i in range(n):
    res = (i - start) * 2 if (i - start) > (end - i) else (end - i) * 2
    print(res)
```
# 答案思路

![Image](https://github.com/user-attachments/assets/2fc08446-cd22-472a-a768-246415148560)
```python
n = int(input())
for i in range(n):
    print(max(i, n-i-1)*2)
```