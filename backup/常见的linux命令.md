# 关机 重启
重启：`sudo reboot`
关机：`sudo shutdown now`

# 查看ip地址
`ip addr`

# sudo
用于以超级用户（root）或其他用户的权限执行命令

**常用选项**

-u 用户：以指定用户身份执行命令。

-l：列出当前用户的 sudo 权限。

-s：启动 root 用户的 shell。

-i：模拟 root 用户的登录环境。

# yum
主要作用是管理软件包，包括安装、更新、删除和查询等操作。


# docker相关命令
重启docker服务，验证配置的一系列命令：

```bash
sudo systemctl daemon-reload #重新加载systemd的配置文件
sudo systemctl restart docker #重启docker
docker info #验证配置
```

`docker search mysql` 搜索仓库中 `mysql` 相关的镜像

搜索 Stars 数超过 100 的 mysql 镜像：`docker search --filter=stars=100 mysql`

`docker pull mysql:5.7` 下载MySQL 5.7 镜像

`docker images` 查看镜像是否下载成功



