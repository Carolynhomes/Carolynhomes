`lambda` 函数也被称为匿名函数，它是 Python 中一种创建简单函数的便捷方式。与使用 `def` 关键字定义的普通函数不同，`lambda` 函数没有函数名，通常用于编写一些简单、一次性使用的函数。以下是关于 `lambda` 函数用法的详细总结：

### 基本语法
```python
lambda 参数列表: 表达式
```
- `参数列表`：与普通函数的参数列表类似，可以包含零个或多个参数，多个参数之间用逗号分隔。
- `表达式`：是一个单一的表达式，`lambda` 函数会计算该表达式的值并返回。注意，`lambda` 函数只能包含一个表达式，不能包含复杂的语句块。

### 常见用法

#### 1. 作为 `sorted()` 或 `list.sort()` 的 `key` 参数
在对可迭代对象进行排序时，`lambda` 函数常被用作 `key` 参数，用于指定排序的规则。

**示例**：
```python
students = [('Alice', 20), ('Bob', 18), ('Charlie', 22)]
# 按年龄排序
sorted_students = sorted(students, key=lambda student: student[1])
print(sorted_students)
```
在这个例子中，`lambda student: student[1]` 接收一个元组 `student` 作为参数，并返回元组的第二个元素（即年龄），`sorted()` 函数会根据这个返回值对 `students` 列表进行排序。

#### 2. 作为 `map()`、`filter()` 等函数的参数
`map()` 和 `filter()` 函数可以对可迭代对象的每个元素应用一个函数，`lambda` 函数可以作为这个应用的函数。

- **`map()` 函数示例**：
```python
numbers = [1, 2, 3, 4]
# 对列表中的每个元素进行平方操作
squared_numbers = list(map(lambda x: x ** 2, numbers))
print(squared_numbers)
```
这里，`lambda x: x ** 2` 接收一个数字 `x` 并返回其平方值，`map()` 函数将这个操作应用到 `numbers` 列表的每个元素上。

- **`filter()` 函数示例**：
```python
numbers = [1, 2, 3, 4]
# 过滤出列表中的偶数
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)
```
`lambda x: x % 2 == 0` 接收一个数字 `x`，判断其是否为偶数并返回布尔值，`filter()` 函数根据这个布尔值过滤出 `numbers` 列表中的偶数。

#### 3. 作为回调函数
在一些需要传递函数作为参数的场景中，`lambda` 函数可以作为简单的回调函数使用。

**示例**：
```python
def apply_operation(x, operation):
    return operation(x)

result = apply_operation(5, lambda x: x + 2)
print(result)
```
在这个例子中，`lambda x: x + 2` 作为回调函数传递给 `apply_operation` 函数，对输入的数字进行加 2 操作。

### 注意事项
- **功能限制**：`lambda` 函数只能包含一个表达式，不能包含复杂的语句，如 `if` 语句、`for` 循环等。如果需要实现复杂的逻辑，建议使用 `def` 关键字定义普通函数。
- **可读性**：虽然 `lambda` 函数简洁，但如果表达式过于复杂，会降低代码的可读性。在这种情况下，使用普通函数可能是更好的选择。