题目链接：https://www.lanqiao.cn/problems/2140/learning/
自己的代码：
```python
today = 6
count = 0  # 代表20的count次方
res = 1

while count < 22:
    res = (res * 20) % 7
    count += 1

    ans = (today + res) % 7
    if ans == 0:
        ans = 7

print(ans)
```

改写的代码：
```python
today = 6  # 当前星期六
remainder = pow(20, 22, 7)  # 直接计算 20^22 对 7 的余数
next_day = (today + remainder) % 7 or 7  # 计算结果，0 表示星期日

print(next_day)
```
- Python 的内置函数 `pow(base, exp, mod)`用于计算 `(base^exp) % mod`
- **or的作用**

> [!tip]
> 在 Python 中，or 表达式会返回第一个“真值”，规则如下：
> 它会从左到右依次检查两个值。
> - 如果第一个值是“假值”（False、0、None 等），它就会返回第二个值。
> - 如果第一个值是“真值”（非零数字、非空字符串等），它就直接返回第一个值。