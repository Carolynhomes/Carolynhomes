# 自己写的，翻阅了资料
```python
n = int(input())
students = {}
for i in range(n):
    chinese, math, english = map(int, input().split())
    total_score = chinese + math + english
    students[i+1] = [chinese, math, english, total_score]

# 定义排序规则函数
def sort_key(item):
    key, value = item
    # 对需要降序排序的元素取负
    return [-value[3], -value[0], key]

sorted_items = sorted(students.items(), key=sort_key)

top = 1
for item in sorted_items:
    if top <= 5:
        print(item[0], item[1][3])
        top += 1
```

# 答案的写法
```python
n = int(input())
scores = []
for i in range(n):
    score = list(map(int, input().split()))
    # 学号、总分、语、数、英
    scores.append([i+1, sum(score)] + score)

# 按总分、语文成绩的顺序排序，学号缺省是从小到大
index = reversed((1, 2))
for i in index:
    scores.sort(key=lambda x: x[i], reverse=True)
    # scores = sorted(scores,key=lambda x:x[i],reverse=True)

for i in range(5):
    print(scores[i][0], scores[i][1])
```
## 代码逻辑梳理
`index = reversed((1, 2))`：创建一个迭代器，依次返回 2 和 1。这意味着先按语文成绩排序，再按总分排序。

`for i in index:`：遍历 index 中的元素，先使用语文成绩作为排序键对 scores 列表进行降序排序，然后再使用总分作为排序键进行降序排序。**这样就能保证最终的排序结果先按总分降序，总分相同的情况下按语文成绩降序。**

最后通过 `for i in range(5): print(scores[i][0], scores[i][1]) `输出排名前 5 的学生的学号和总分。
示例说明
# 第三种答案
```python
import functools

# 1 表示逆序，-1表示升序
def cmp(n1, n2):
    if n1[1] != n2[1]:
        # 总分不一样，高分在前
        return -1 if n1[1] > n2[1] else 1
    elif n1[2] != n2[2]:
        # 总分一样，语文成绩高的在钱
        return -1 if n1[2] > n2[2] else 1
    else:
        # 都一样的话，学号小的在前面
        return 1 if n1[0] > n2[0] else 1

n = int(input())
scores = []
for i in range(n):
    score = list(map(int, input().split()))
    # 学号、总分、语、数、英
    scores.append([i+1, sum(score)] + score)

scores.sort(key=functools.cmp_to_key(cmp))
# scores = sorted(scores, key=functools.cmp_to_key(cmp))
    

for i in range(5):
    print(scores[i][0], scores[i][1])
```