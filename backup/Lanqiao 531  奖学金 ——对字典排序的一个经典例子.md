
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