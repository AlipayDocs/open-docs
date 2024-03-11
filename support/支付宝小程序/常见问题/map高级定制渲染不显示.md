## 报错描述
map 高级定制渲染不显示。

## 报错原因

- IDE 模拟器中不支持 map 高级定制渲染。
- 未开启 component2。
- 引入的 axml 文件放到了 pages 目录下。
- mini.project.json 未设置 。
```
"include": [   "*/*.xml" ]
```

## 解决方案

- 在真机上调试。
- IDE 右上角** 详情** 中开启 component2。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/190001a3-2c34-4196-a64a-4a1c33be03d7.png#align=left&display=inline&height=587&margin=%5Bobject%20Object%5D&originHeight=587&originWidth=1570&status=done&style=none&width=1570)
- 引入的 axml 文件不可在 pages 目录下，建议设置如下图引入的 axml 文件的layout文件与pages文件平级。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/ec640de7-8882-41c0-8d59-11de305c748c.png#align=left&display=inline&height=678&margin=%5Bobject%20Object%5D&originHeight=678&originWidth=899&status=done&style=none&width=899)
- mini.project.json 中配置 include。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/37668a7a-24ba-4fb5-80fc-9df36dda794a.png#align=left&display=inline&height=465&margin=%5Bobject%20Object%5D&originHeight=465&originWidth=739&status=done&style=none&width=739)

 <br /> 
