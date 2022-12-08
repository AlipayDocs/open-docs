
## lifestyle组件不显示
- 小程序和生活号必须是同一支付宝账号。
- 确认是否与当前小程序关联的生活号。生活号和小程序关联的方法，可查看 [建立小程序与生活号之间的绑定关系](https://opendocs.alipay.com/support/01rb0x)。
- 确认组件 lifestyle 中生活号 ID 即生活号 APPID 是否正确。
- 小程序须上架一次，生活号需为上线状态。
- 属性 onFollow 控制关注生活号组件不显示状态是否正确。
- 建议使用真机预览模式进行调试。
- 关注生活号组件支持版本：SDK 1.3.0 / 支付宝 10.1.5 及更高级版本。 

## life-follow组件不显示

- 确认组件 lifestyle 中 sceneId 是否正确，其审核状态为 **已审核**。
- 小程序须上架一次，生活号需为上线状态。
- life-follow 组件支持应用于小程序页面，不支持应用于 H5 页面和 NATIVE 页面。
- 组件配置信息需**经过审核后才能应用**。一般审核过程较快。如果审核未通过，可编辑修改信息后重新提交审核。
- 组件可判断用户关注状态，即用户当前是未关注该生活号，还是已关注。**针对未关注用户支持弹出组件，已关注用户则不弹出。**
- **针对单个组件 ID，用户关闭组件总共达 3 次，则不再会再展示给用户**。
- 建议使用真机预览模式调试。

![](https://gw.alipayobjects.com/zos/sptworksff_prod/c2fe89ce-0b69-4ed3-a5a1-61e71e220a0f.png)

## 相关文档

- [关注/跳转生活号组件](https://opendocs.alipay.com/mini/introduce/bntnry)
- [管理生活号](https://opendocs.alipay.com/b/03al92)

 
