### 报错描述
receiveData: worker render components is not sync! can not find id from path 或 receiveData: worker render components is not sync! Please check your axml: in pages/scanpaymentcode/scanpaymentcode。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/5b69a213-9d22-46d7-b6b2-801b9a3e2030.png#align=left&display=inline&height=76&margin=%5Bobject%20Object%5D&originHeight=76&originWidth=637&status=done&style=none&width=637)

## 报错原因

- template 中使用自定义组件在 component2 之下可能会触发 not sync 。
- 自定义组件中定义默认 slot 时，可能导致 not sync 。 

## 解决方案

- 不要在 template 中使用自定义组件。
- 排查代码中是否用到了 sync 语法，检查有没有启用 component2 编译 。
- setData 时，对数据深度克隆，排查代码中是不是直接修改了 this.data 里的属性，如有请使用 setData 来修改。
- IDE 左上角 **小程序开发者工具** >** 检查更新**，检查更新升级 IDE 版本到最新版本。
- 建议真机调试/预览上运行调试。

 <br /> 
