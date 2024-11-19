题目链接：https://www.lanqiao.cn/problems/2141/learning/

> 难，我嘞个豆，只会简单的暴力，但是暴力，运行不出来，貌似要等五分钟才运行的出来~~~
>
> 最后，求助了GPT，啧

```python
def generate_palindromes(min_value, max_value):
    """
    Generate all palindromes within the range [min_value, max_value].
    A palindrome is a number that reads the same forwards and backwards.

    Parameters:
        min_value (int): The minimum value of the range.
        max_value (int): The maximum value of the range.

    Returns:
        list: A list of palindromes within the given range.
    """
    palindromes = []
    min_len = len(str(min_value))  # Determine the minimum number of digits
    max_len = len(str(max_value))  # Determine the maximum number of digits

    for length in range(min_len, max_len + 1):  # Iterate through possible lengths
        half_len = (length + 1) // 2  # Only generate the first half of the number
        for half in range(10 ** (half_len - 1), 10 ** half_len):  # All possible first half digits are generated
            if length % 2 == 0:  # For even-length palindromes
                palindrome = int(str(half) + str(half)[::-1])  # Mirror the half to create the palindrome
            else:  # For odd-length palindromes
                palindrome = int(str(half) + str(half)[-2::-1])  # Mirror excluding the middle digit
            if min_value <= palindrome <= max_value:  # Only include valid numbers in the range
                palindromes.append(palindrome)

    return palindromes


def is_mountain_number(num):
    """
    Check if a number is a mountain number.
    A mountain number is a palindrome where digits first increase or stay the same,
    then decrease or stay the same.

    Parameters:
        num (int): The number to check.

    Returns:
        bool: True if the number is a mountain number, False otherwise.
    """
    s = str(num)  # Convert the number to a string
    peak_reached = False  # Track whether the peak (start of decreasing) is reached
    for i in range(len(s) - 1):
        if not peak_reached:
            if s[i] > s[i + 1]:  # Check if digits start decreasing
                peak_reached = True
        if peak_reached:
            if s[i] < s[i + 1]:  # If digits increase again after decreasing, it's not a mountain
                return False
    return True  # Passed all checks, it's a mountain number


def count_mountain_numbers(min_value, max_value):
    """
    Count all mountain numbers within the range [min_value, max_value].
    Combines the generation of palindromes and checking for the mountain property.

    Parameters:
        min_value (int): The minimum value of the range.
        max_value (int): The maximum value of the range.

    Returns:
        int: The count of mountain numbers in the given range.
    """
    palindromes = generate_palindromes(min_value, max_value)  # Generate all palindromes in range
    return sum(1 for num in palindromes if is_mountain_number(num))  # Count those that are mountain numbers


# Optimized calculation for the given range
start = 2022  # Start of the range
end = 2022222022  # End of the range
optimized_count = count_mountain_numbers(start, end)  # Count mountain numbers

print(optimized_count)  # Result: Total number of mountain numbers

```

他这个代码：

> [!important]
>
> 是先把所有的在2022，2022222022的长度给确定下来
>
> 然后先把满足4——10这个长度的回文数全部生成，这样循环的次数就会少很很很多
>
> 生成的过程，也很有意思：是先把当前长度的回文数的到达顶峰的前一半给确定，然后生成的
>
> ​	就是他会遍历当前长度的所有数字，比如长度为4的时候，他会	取当前长度的一半，也就是2来进行回文的生成，遍历从10——1	00，这个就是精髓了啊，我嘞个豆
>
> 之后的生成回文数的方法，也要记得
>
> > int(str(half) + str(half)[::-1])  偶数的处理
>
> > int(str(half) + str(half)[-2::-1])  奇数的处理
>
> 这俩 绝了啊真的是
>
> 再之后判断递增递减， 也值得记一下
>
> 它设置了一个是否到达顶峰的变量 peak_reached
>
> 然后，如果到达了之后，就是前一个比后一个大，否则就是小
>
> 哎，处理方式 叹为观止（`纯碎是我技术不行 啊哈哈哈哈`）
>
> 
>
> 而且其中的返回方式，也是学不会的，列表生成式，求个和?
>
> `return sum(1 for num in palindromes if is_mountain_number(num))`

