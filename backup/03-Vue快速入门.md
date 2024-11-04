## 课程演示代码

https://pan.baidu.com/s/1IsFsMT8y1lhVQKwWFngmSw?pwd=t56j

## 课程视频讲解

https://www.bilibili.com/video/BV1c14y1z7SN/?spm_id_from=333.1296.top_right_bar_window_history.content.click&vd_source=5c34fdff72dc0c2c15c307e789fe5140

## Vue 起步（Vue2）

文档：https://v2.cn.vuejs.org/

**语法如下：**

```javascript
var example1 = new Vue({
  el: '#example-1',
  data: {
    counter: 0
  }
})
```

- `{{ }}` 变量，表达式渲染
- `v-html` html 模板，渲染 html
- `v-model` 绑定值（双向绑定）
- `v-if` `v-else-if` `v-else` 判断
- `v-bind` 简写：绑定属性
- `v-on` 简写 @ 事件绑定
- `v-for` 循环
- 动态 `class style`

---

下载软件 nodejs v16  
安装 node & npm  
npm 配置淘宝镜像：

```bash
npm config set registry http://registry.npm.taobao.org/
```

## Vue 脚手架搭建

`新建目录`：E:\local_blog\Bilibili\代码\小白做毕设

脚手架工具：https://cli.vuejs.org/zh/guide/

```bash
// 在cmd直接运行
npm install -g @vue/cli

vue --version

// 进入目录小白做毕设2024，再运行
vue create vue
```

![image](https://github.com/user-attachments/assets/d46cb95f-8d53-4afe-93dc-37c1222adfd8)

`如上图所示`就是安装成功

之后执行命令：

```bash
cd vue
npm run serve
```

![image](https://github.com/user-attachments/assets/f56d7ff5-d451-4273-b7d6-d54b39da25cf)

`如上图所示即为成功`

## 对脚手架内容进行修改

配置文件`vue.config.js`:

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    port: 7000
  },
  chainWebpack: config =>{
    config.plugin('html')
        .tap(args => {
          args[0].title = "青哥哥好帅啊";
          return args;
        })
  }
})
```

`App.vue`

```vue
<template>
  <div id="app">
    <router-view/>
  </div>
</template>
```

`HomeView.vue`

```vue
<template>
  <div>
    你好你好啊
  </div>
</template>

<script>

export default {
  name: 'HomeView'
}
</script>
```

`router目录下的index.js`

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: () => import('../views/HomeView.vue')
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
```

在`src目录下的assets新建一个css文件夹，新建global.css文件`

```css
* {
    box-sizing: border-box;
}
body {
    color: #333;
    font-size: 14px;
    margin: 0;
    padding: 0;
}
```

