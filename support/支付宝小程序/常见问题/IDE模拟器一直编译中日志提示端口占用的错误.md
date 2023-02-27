## 问题描述
打开 IDE 的时候，发现模拟器在不停地编译中，打开编译日志，提示端口占用的错误（Something is already running on port 49347）<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/2e7678e5-7ea2-4e17-897e-1f260b060d4d.png#align=left&display=inline&height=171&margin=%5Bobject%20Object%5D&originHeight=342&originWidth=826&status=done&style=none&width=413)<br />或提示 Dev server is ready on http:127.0.0.。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/5bca2387-fdcc-41d8-913a-c2e686fe167f.jpg#align=left&display=inline&height=147&margin=%5Bobject%20Object%5D&originHeight=586&originWidth=1660&status=done&style=none&width=415)

## 报错原因
端口被占用导致。

## 解决方案
在本机配置 hosts（C:\\Windows\\System32\\drivers\\etc）：127.0.0.1 localhost。
