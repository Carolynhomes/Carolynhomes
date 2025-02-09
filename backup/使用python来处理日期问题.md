```python
from datetime import *


date1 = datetime(1901, 1, 1)
date2 = datetime(2000, 12, 31)
print(date1.weekday())  # 输出1，表示周二。注：周一用0，周日用6表示

total_day = date2 - date1
print(total_day // 7)
```

# 例题 2096
【题目描述】小明特别喜欢顺子。顺子指的就是连续的 3 个数字：123、456 等。顺子日期指的就是在日期的 yyyymmdd 表示法中，存在任意连续的三位数是一个顺子的日期。

例如20220123 就是一个顺子日期，因为它包含一个顺子 123；而 20221023 则不是一个顺子日期，它一个顺子也没有。小明想知道在 2022 年一共有多少个顺子日期。
```python
from datetime import *

date1 = datetime(2022, 1, 1)
cnt = 0
for i in range(0, 365):
    s = "%04d%02d%02d" % (date1.year, date1.month, date1.day)
    if "012" in s or "123" in s or "234" in s or "345" in s or \
       "456" in s or "567" in s or "678" in s or "789" in s:
        cnt += 1
    date1 += timedelta(days=1)

print(cnt)

```
```python
import datetime

start = datetime.date(2022, 1, 1)
end = datetime.date(2022, 12, 31)
example = ["012", "123", "234", "345", "456", "567", "678", "789"]
res = 0

while start <= end:
  now_date = start.strftime("%Y%m%d")
  for x in example:
    if x in now_date:
      res += 1
      break
  start += datetime.timedelta(days=1)

print(res)
```
# 例题 2119
【题目描述】2022 年 2 月 22 日 22:20 是一个很有意义的时间，年份为 2022，由 3 个 2 和1 个 0 组成，如果将月和日写成 4 位，为 0222，也由 3 个 2 和 1 个 0 组成，如果将时间中的时和分写成 4 位，还由 3 个 2 和 1 个 0 组成。

小蓝对这样的时间很感兴趣，他还找到了其他类似的例子，如 111 年 10 月 11 日 01:11、2202 年 2 月 22 日 22:02 等。

请问，总共有多少个时间是这种年份写成 4 位、月日写成 4 位、时间写成 4 位后均由 3 个一种数字和 1 个另一种数字组成的。

注意 1111 年 11 月 11 日 11:11 不算，因为它里面没有两种数字。
```python
def check(n):
    """检查数字是否合法，n是排序后的"""
    # 说明只有一种数字
    if n[0] == n[3]: return False
    # 说明第2个数字和第3个数字要相等
    if n[1] != n[2]: return False
    # 说明前三个相等，或者后三个相等
    if n[0] == n[1] or n[2] == n[3]: return True
    return False

year = []
# 0001~9999年
for y in range(1, 10000):
    s = "%04d" % (y)
    s1 = sorted(s)  # 返回的是列表
    if check(s1): year.append(s1)

day = []
for m in range(1, 13):
    for d in range(1, 31):
        # 30, 31都不符合要求
        # 同理2.29, 2.30也不用管
        # 0229 0230 都不满足
        s = "%02d%02d" % (m, d)
        s1 = sorted(s)
        if check(s1): day.append(s1)

hour = []
for h in range(0, 24):
    for m in range(0, 60):
        s = "%02d%02d" % (h, m)
        s1 = sorted(s)
        if check(s1): hour.append(s1)

cnt = 0
for i in year:
    for j in day:
        for k in hour:
            if i == j and i == k:
                cnt += 1

print(cnt)
```