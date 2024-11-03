# 学习资源

- HTML： https://www.runoob.com/html/html-tutorial.html
- CSS： https://www.runoob.com/css/css-tutorial.html
- Vue： https://www.runoob.com/vue2/vue-tutorial.html

# HTML

- div
- span
- h1-h6
- i
- strong
- a
- img
- video
- input
- textarea
- button

![image](https://github.com/user-attachments/assets/e28ac798-17da-4ebe-84b2-7096b1411804)

# CSS 布局思路

```
box-sizing: border-box;` 定义如何计算一个元素的总宽度和总高度，主要设置是否需要加上内边距(padding) 和边框等。`一般全局设置
*{
    box-sizing: border-box;
}
```

## 盒子模型

- 外边距 `marigin` 上右下左
- 内边距 `padding` 上右下左
- 边框 `border` 上右下左 `solid`-实线 `dashed`-虚线 `border:1px dashed black`
- 阴影 `box-shadow: h-shadow v-shadow blur spread color inset;`(`box-shadow: 0 0 10px -2px rgba(0, 0, 0, 5);`) 
- 边角 `border-radius` 上右下左
- 内容

- css 换行 ——`word-wrap: break-word; `属性

![image](https://github.com/user-attachments/assets/95ae1229-78f8-4836-8d29-e865807e23a7)

## Flex 布局

参考文章：https://www.runoob.com/w3cnote/flex-grammar.html

- flex-direction	`row` | `column`
- flex-wrap    `wrap` 不会让我的盒子因为太多，导致挤压变形，会自动换行
- justify-content    `flex-start | flex-end | center | space-between | space-around`
- align-items    `flex-start | flex-end | center | baseline | stretch`

![image](https://github.com/user-attachments/assets/380f3e34-831a-4752-a44f-ad6b2cebfcca)
### 豆瓣网实例

![image](https://github.com/user-attachments/assets/ced86682-4c53-4d95-ba28-7a9b111f9d2e)
![image](https://github.com/user-attachments/assets/7f56b2de-21e5-4a73-9b05-4153ad9ee21f)
# CSS 布局元素

1. 宽度 width

    - 固定宽度   百分比宽度

    - 最大宽度

    - 最小宽度

    - 水平居中  `margin: auto`

2. 高度 height

    - 固定高度（必须）

    - 最大高度

    - 最小高度

    - 行高对齐

3. 字体

    - 颜色 color 十六进制、rgb、英文

    - 大小 font-size

    - 粗细  font-weight bold

4. 背景

    - 颜色网站：https://color.d777.com/

    - 颜色  background-color

    - 图片  background-img: url(...)

5. 定位 position

    - absolute 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位

    - **relative**  生成相对定位的元素，相对于其正常位置进行定位（上下移动行内元素最简单方式）

    - fixed 生成固定定位的元素，相对于浏览器窗口进行定位

6. overflow: hidden scroll

    - `**overflow: hidden;**` - 隐藏超出元素边界的内容。

    - `**overflow: scroll;**` - 始终显示滚动条，即使内容没有溢出。