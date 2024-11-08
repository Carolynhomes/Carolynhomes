> 仅仅自己学习记录使用，学习具体的，还要去看远春姐自己的详细教程：[https://space.bilibili.com/483684875?spm_id_from=333.337.0.0](https://space.bilibili.com/483684875?spm_id_from=333.337.0.0)

## 打开IDEA 创建新项目

## 用Spring Boot 的方式创建工程

选配置参照下图配好

![](https://cdn.nlark.com/yuque/0/2024/png/35081558/1731055823750-daf33ec0-7994-47b0-b9d4-b2ea92101227.png)

如果没有下载jdk21，可以查看这篇教程下载配置jdk

[最详细jdk安装以及配置环境（保姆级教程）_java_无尽的沉默-GitCode 开源社区](https://gitcode.csdn.net/65e7d8b41a836825ed78a53c.html?dp_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6NDMzNjgxNSwiZXhwIjoxNzIxMjg2NDMzLCJpYXQiOjE3MjA2ODE2MzMsInVzZXJuYW1lIjoic2luYXRfMzQ2NDc4MzYifQ.B81WjxjGx2-qzahGkqZYSUZTqaN77gHpuuYqAjnmZPM)

![](https://cdn.nlark.com/yuque/0/2024/png/35081558/1731056011465-2e1777fc-4752-40c3-8687-b1478daf2d60.png)

> 这里的版本号，不一样也没事，进去之后可以在`pom.xml` 文件里修改版本

到这里，springboot 工程已经创建好了，系统会自动在mycode文件夹里创建一个springboot文件夹。文件夹内容如下：![](https://cdn.nlark.com/yuque/0/2024/png/35081558/1731056103357-03489fc6-a3f7-46da-86ed-84d10e239aac.png)

创建好之后，我们先不用去配置它，我们后面要做**前后端分离的项目**，一般都会**前后端一起打开比较方便**，所以我们先把这个创建好的springboot工程关掉，**把一些idea自动生成的一些文件删掉**，一个干净的springboot项目工程**只需要src和pom.xm**l即可，如下图：

![](https://cdn.nlark.com/yuque/0/2024/png/35081558/1731056150842-54e03e3b-8b95-4ff8-8280-cb447b834233.png)

