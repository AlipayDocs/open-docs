## 问题描述
点击 IDE 真机预览调试面板中的 command 可以输入哪些命令进行哪些操作。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/b4bcd464-eb14-431c-9b16-25c79ea4f15d.png#align=left&display=inline&height=464&margin=%5Bobject%20Object%5D&originHeight=464&originWidth=324&status=done&style=none&width=324)

## 解决方案
command 执行框相当于是在一个普通的 JS 文件里，不是在 Page 或者 App 的上下文中。

- 可以手动输入/执行 my. 的小程序 API（this. 的无法执行）。例如：常用 my.clearStorageSync() 清除缓存。
- 手动输入的 this、my 之类，在 log 输出对应的日志。

 <br /> 
