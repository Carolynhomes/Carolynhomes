> 亲测生效
1. 打开注册表：Win+R → regedit

2. 定位 HKEY_CLASSES_ROOT\Directory\shell，修改 shell 默认值为 TC

3. 在 shell 下新建一个子项 TC

4. 在 TC 下继续新建一个子项 Command，修改默认值为：
`"C:\TotalCommander\TOTALCMD64.EXE" "/R=%1"`
（第一个引号内的加重字体代表 TC 的安装路径，以个人电脑为准）