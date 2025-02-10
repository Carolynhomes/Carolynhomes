# 思路
自己写的时候其实题目都不太理解，当然也是没写出来的

# 答案

![Image](https://github.com/user-attachments/assets/74ed2529-c835-442a-a6d9-6823db313988)

![Image](https://github.com/user-attachments/assets/6c093a0b-2a4a-4dab-a00b-c618ca3d422a)

```python
from math import *
import os
import sys

# 请在此输入您的代码
n, s = map(int, input().split())
data = list(map(int, input().split()))

data.sort()
avg = s / n
sum = 0

for i in range(n):
    if data[i] * (n - i) < s:
        sum += pow(data[i]-avg, 2)
        s -= data[i]
    else:
        cur_avg = s / (n - i)
        sum += pow(cur_avg-avg, 2) * (n - i)
        break

print("{:.4f}".format(sqrt(sum/n)))

```