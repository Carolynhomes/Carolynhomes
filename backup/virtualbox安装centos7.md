## 在virtualbox安装centos7

![Image](https://github.com/user-attachments/assets/e04ad614-0a39-40d3-953f-be67ae8a46d0)

![Image](https://github.com/user-attachments/assets/fe56c3b0-ffbc-46bd-9ee3-72da0a7480e4)

![Image](https://github.com/user-attachments/assets/30e91f6b-ff91-46bf-9ff5-faba36e9b84c)

![Image](https://github.com/user-attachments/assets/3bae63f3-3758-4e93-8ad5-b71d3a0b584a)

然后进入选择新建的虚拟电脑，进入设置

![Image](https://github.com/user-attachments/assets/8d3605b5-b7cf-489b-9fea-6ce780d01a27)

![Image](https://github.com/user-attachments/assets/9cca3538-5cec-4b91-bd2b-3725eb41b4b8)

然后启动即可，进入后选择第一个选项，然后分区可以直接自动分区，也可以手动设置（自定义），设置密码：123456，用户名默认是root

设置一下网络，然后重启

![Image](https://github.com/user-attachments/assets/00f14b87-80b8-409c-b5c4-d75765abed9f)

进去之后可能运行`ip addr`之后不显示ip地址

那此时进入，网卡配置文件

`vi /etc/sysconfig/network-scripts/ifcfg-<interface_name（网卡名）>`

把onboot设置为yes，重启`systemctl restart NetworkManager`即可。

然后再运行`ip addr`即可显示了，然后再使用ssh客户端连接即可