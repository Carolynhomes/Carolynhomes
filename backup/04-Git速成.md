## 视频教程

https://www.bilibili.com/video/BV1um4y1s7AN/?spm_id_from=333.788.videopod.sections&vd_source=5c34fdff72dc0c2c15c307e789fe5140

## 软件安装

官方下载（比较慢）：https://git-scm.com/downloads

## gitee

注册账号： https://gitee.com/

新建一个仓库，输入名字之后，直接确定即可`（我懒得自己想名字，就跟教程一样了）`

![image](https://github.com/user-attachments/assets/4bd69d8d-7a25-4605-b1da-8e37f4e533d3)
## 步骤

### 先初始化项目目录为git仓库

先进入对应目录下的cmd

> 或者打开git

然后，输入`git init`把这个目录变成一个`git`仓库

>  [!TIP]
>
> 我就是没有把git配置到环境变量，我是直接在目录空白处，git bash打开了

### 本地仓库跟远程的仓库建立连接

建议直接 `--global`

> 在此之前，应先配置一下git
>
> **git config  user.email "[your_email@example.com](mailto:your_email@example.com)"**
>
> `git config  --global user.email "your_email@example.com"`
>
> **git config  user.name "username"**
>
> `**git config --global user.name "username"**`

```bash
git remote add origin https://gitee.com/carolynhomes/honey2024.git
```

`git remote -v` 看看配置

![image](https://github.com/user-attachments/assets/4bd69d8d-7a25-4605-b1da-8e37f4e533d3)
### 新建 `.gitignore`文件

```bash
.idea
node_modules
*.iml
```

加进去

### 暂存代码

暂存代码 **git add . (要注意当前的仓库是否存在旧的仓库文件夹 .git，如果存在要删除掉)**

```git
# 把当前目录除了 .gitignore描述之外的所有文件全部加入到暂存区
git add .
```

然后执行`git status`查看状态，下图是正常状态：

![image](https://github.com/user-attachments/assets/9c52bdac-71de-4752-b1a5-bb278cec076a)
### 提交文件到本地仓库

`git commit -m "初次提交"`

### 推送代码到远程仓库

`git push -u origin "master"`

> 强制覆盖远程仓库
> **git push -f origin "master"**

![image](https://github.com/user-attachments/assets/8ad6a1cd-b811-4ebd-8eba-873d84e96304)
这就是成功了

### idea推送到gitee

![image](https://github.com/user-attachments/assets/0d3f770c-0403-4b14-abad-0083eb208ef7)
修改内容，之后点击 commit，然后输入备注，就可以点第三个

然后弹出来继续点击`push`即可

### 注意

本地没有更新远程仓库的修改，直接提交会提示你错误

![image](https://github.com/user-attachments/assets/6db7995b-3424-4453-ba6d-3f7f983b148d)
**在我们提交代码到远程仓库之前，需要先更新远程仓库的代码到本地**

## git操作

### 基本操作

```bash
# 配置
# 全局配置
git config --global user.email "your_email@example.com"
git config --global user.name "username"
# 仓库配置
git config user.email "your_email@example.com"
git config user.name "username"

git config --global --list
git config --list


# 新建仓库
git init
# 添加远程仓库
git remote add origin ''
# 查看远程仓库
git remote -v

# 添加文件到暂存区
git add .
# 查看状态
git status
# 忽略文件
.gitignore文件

# 提交
git commit -m 'init'

# 拉取远程代码
git pull origin master
# 强制推送代码到远程仓库
git push -f origin master

# 克隆代码
git clone ''
```

### 常用操作

```bash
# 列出本地所有分支
git branch

# 新建一个分支，并切换到该分支
git checkout -b 分支名
# 切换分支
git checkout 分支名
# merge其他分支到当前分支
git merge 分支名

# 暂存
git stash
git stash list
git stash pop [stash]
git stash apply [stash]
git stash drop [stash]
```