## 报错描述
引用第三方组件报错：Component is not defined。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/a031d3ec-70cc-46e2-8dc1-da65cccff2d7.png#align=left&display=inline&height=240&margin=%5Bobject%20Object%5D&originHeight=618&originWidth=1928&status=done&style=none&width=750)

## 问题原因
引用第三方组件报 Component is not defined 组件未定义，安装方式错误导致。

## 解决方案
不要使用 tnpm 安装组件，用 npm 安装组件。<br />
建议直接通过 IDE 自动安装依赖：选中相关目录，在运行依赖/开发依赖中输入包名称并回车即可。详情可查看 [NPM 包管理](https://opendocs.alipay.com/mini/ide/npm-manage)。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/e7132e44-f771-4a8c-a1a8-c68d86228517.png#align=left&display=inline&height=370&margin=%5Bobject%20Object%5D&originHeight=375&originWidth=317&status=done&style=none&width=313)![](https://gw.alipayobjects.com/zos/sptworksff_prod/354a4370-0e84-4b65-8669-cf81dd8ef2bf.png#align=left&display=inline&height=370&margin=%5Bobject%20Object%5D&originHeight=489&originWidth=304&status=done&style=none&width=230)
