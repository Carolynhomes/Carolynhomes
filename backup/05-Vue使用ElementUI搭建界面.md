# ElementUI 官网

https://element.eleme.cn/#/zh-CN/component/installation

# Vue 安装 ElementUI

用 idea 打开你的项目目录，然后打开终端 terminal，

```
cd vue
```

然后运行 `npm i element-ui -S`

**没搞定的检查下 npm 镜像，修改镜像源为淘宝**

```
npm config set registry https://registry.npmmirror.com
```

查看 npm 镜像

```
npm config get
```

或者安装 `nrm`，管理 `npm`镜像

```
npm install nrm -g
nrm` 切换镜像为 `taobao
nrm ls
nrm use taobao
nrm current
```

![img](https://cdn.nlark.com/yuque/0/2023/png/751015/1691587364456-35f880ef-8189-483c-a750-bc94eb09e3d4.png#averageHue=%232e2e2d&clientId=ua3fd209b-0afa-4&from=paste&height=207&id=u802a3d1d&originHeight=259&originWidth=778&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=40110&status=done&style=none&taskId=u981a5c3d-0330-4cf1-bc5b-0149edbca68&title=&width=622.4)![img](https://cdn.nlark.com/yuque/0/2023/png/751015/1691587394872-94ee0aa1-50c9-499f-85a0-a08954064fc5.png#averageHue=%2331302f&clientId=ua3fd209b-0afa-4&from=paste&height=49&id=uab0f175a&originHeight=61&originWidth=646&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=7987&status=done&style=none&taskId=u2de55129-8987-4b8e-9a67-b39cbd70daa&title=&width=516.8)![img](https://cdn.nlark.com/yuque/0/2023/png/751015/1691587411488-655ba39b-fd4f-47fa-8b97-195253540685.png#averageHue=%23302e2d&clientId=ua3fd209b-0afa-4&from=paste&height=167&id=u2ae2e71b&originHeight=209&originWidth=684&originalType=binary&ratio=1.25&rotation=0&showTitle=false&size=32886&status=done&style=none&taskId=u6f770321-88c7-4020-8a26-773321c27ba&title=&width=547.2)

# Vue 配置安装 ElementUI

在 `main.js`里引入下面的内容

```javascript
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI, { size: 'small' });
```

上面代码作用：在你的Vue项目中引入并注册Element UI库，同时指定使用小号尺寸的组件。这样，你就可以在项目中方便地使用Element UI提供的组件和样式了。

`el-row` + `el-col` 利用这两个基础组件，可实现，下面内容：

- `el-row` 组件用于创建行，是 `el-col` 组件的容器。在使用栅格布局时，`el-row` 组件会包含多个 `el-col` 组件，以形成一行中的多个列。
- `el-col` 组件用于创建列，是布局中的一个单元。你可以指定列的 `span` 属性来确定列占据的栅格数，`el-col` 组件可以包含任意内容，如文本、图片、链接等。
- 详细参数信息，去官网查即可

https://element.eleme.cn/#/zh-CN/component/installation

# 按钮 button

属性：type、plain、round、circle
circle 按钮使用 icon 设置图标
禁用状态
文字按钮（可改变颜色）
事件：click

```vue
<el-button>默认按钮</el-button>
<el-button type="primary">主要按钮</el-button>
```

# 表单元素 Form

 输入框
type
show-password
clearable
suffix-icon="el-icon-date"

```vue
<el-input v-model="input" placeholder="请输入内容"></el-input>
```

强制要求你必须有v-model

## 输入建议表单

```vue
<el-autocomplete style="width: 300px" placeholder="请输入内容，我来帮你猜一猜" :fetch-suggestions="querySearch"
:trigger-on-focus="false" v-model="value3"></el-autocomplete>


// js代码
coffees: [{ value: '1星巴克咖啡' },{ value: '1栖巢咖啡' }, {value: '2瑞幸咖啡'}, {value: '3库迪咖啡'}]
// 值必须带value

querySearch(query, cb) {  // callback
  let result =  query ? this.coffees.filter(v => v.value.includes(query)) : this.coffees
  console.log(result)
  cb(result);
}
```

# **下拉框**

clearable
multiple
filterable 可搜索

```vue
<el-select v-model="value" placeholder="请选择">
  <el-option value="青哥哥"></el-option>
  <el-option value="亲哥哥"></el-option>
  <el-option value="情哥哥"></el-option>
</el-select>

<el-select v-model="value" placeholder="请选择">
  <el-option
    v-for="item in options"
    :key="item.value"
    :label="item.label"
    :value="item.value">
  </el-option>
</el-select>
```

# **单选**

```vue
<el-radio-group v-model="radio">
  <el-radio label="男"></el-radio>
  <el-radio label="女"></el-radio>
</el-radio-group>
```

# **多选**

```vue
<el-checkbox-group v-model="checkList">
  <el-checkbox label="复选框 A"></el-checkbox>
  <el-checkbox label="复选框 B"></el-checkbox>
</el-checkbox-group>
```

# **日期时间**

format
value-format

```vue
<el-date-picker v-model="date" type="date" placeholder="选择日期"></el-date-picker>
<el-date-picker v-model="datetime" type="date" placeholder="选择日期时间"></el-date-picker>

<el-date-picker v-model="daterange" type="daterange"
      start-placeholder="开始日期"
      end-placeholder="结束日期">
</el-date-picker>
```

# **表格 el-table**

```vue
<el-table :data="tableData" border :header-cell-style="{ background: 'aliceblue', fontSize: '16px' }">
  <el-table-column label="序号" prop="id" align="center"></el-table-column>
  <el-table-column label="名称" prop="name" align="center"></el-table-column>
  <el-table-column label="年龄" prop="age" align="center"></el-table-column>
  <el-table-column label="地址" prop="address" align="center"></el-table-column>
  <el-table-column label="操作">
    <template v-slot="scope">
      <el-button type="primary" @click="edit(scope.row)">编辑</el-button>
    </template>
  </el-table-column>
</el-table>

tableData: [
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
        {  name: '青哥哥哥', address: '安徽省合肥市', id: 1, age: '30' },
      ],
```

# **提示信息**

message
notify
confirm

```vue
// alert(row.name)
// this.$message.success(row.name)
// this.$message.warning(row.name)
// this.$notify.success(row.name)

this.$confirm('这是什么个玩意儿？', '提示', {
  type: 'warning'
}).then(res => {
  this.$message.success("ok 我点击了确认")
}).catch(() => {
  this.$message.warning("ok 我点击了取消")
})
```

