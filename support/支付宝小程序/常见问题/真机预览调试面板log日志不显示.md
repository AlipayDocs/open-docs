## 问题描述
真机预览调试面板 log 日志不显示不输出日志。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/b88094b1-d95b-4edf-89c6-13bab27127c5.png#align=left&display=inline&height=371&margin=%5Bobject%20Object%5D&originHeight=464&originWidth=324&status=done&style=none&width=259)

##  解决方案

- 打开调试面板之后再次进入小程序，查看是否能看到日志（建议重新推送真机预览）。
- 检查小程序项目中是否使用了小程序插件，带插件的小程序项目仅支持 IDE 1.12.15 及以上版本 Log 的查看，可以尝试更新 IDE 版本到最新；如果暂不用到插件，可以先注释掉。
