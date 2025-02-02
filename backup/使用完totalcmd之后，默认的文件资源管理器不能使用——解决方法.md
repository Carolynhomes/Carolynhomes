将下面内容保存到文本文件中，并且设置后缀名为.reg，双击运行即可。
```
Windows Registry Editor Version 5.00

; Revert Default
[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell]
@=-

[-HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\openinfiles]

; Revert Win+E
[-HKEY_CURRENT_USER\SOFTWARE\Classes\CLSID\{52205fd8-5dfb-447d-801a-d0b52f2e83e1}]

```