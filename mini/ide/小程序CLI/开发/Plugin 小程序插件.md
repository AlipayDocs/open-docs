
# 小程序插件
有插件小程序的，需要在 Auth 进行登录授权，授权完成后可在 Plugin 面板看到所使用插件的具体版本。比如在插件依赖里是"*"，在这里则会清晰看到具体的是什么版本。而对于没有插件权限的，Plugin 面板也会给出提示。

![|723x413](https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*rJsIQIjm3u0AAAAAAAAAAAAAARQnAQ#align=left&display=inline&height=670&margin=%5Bobject%20Object%5D&originHeight=1102&originWidth=1928&status=done&style=none&width=1172)

# 插件没有权限
使用小程序插件报错没有权限，比如：

![|723x102](https://gw.alipayobjects.com/mdn/rms_dfc0fe/afts/img/A*-kfrQa_yz6MAAAAAAAAAAAAAARQnAQ#align=left&display=inline&height=165&margin=%5Bobject%20Object%5D&originHeight=284&originWidth=2020&status=done&style=none&width=1172)

解决方法：

1. 确保在 Auth 标签页里已经授权登录。
1. 查看当前小程序是否有该插件的使用权限
   - 使用已上架的插件，参考文档：[插件订购](https://opendocs.alipay.com/mini/plugin/plugin-order)。
   - 与开发中的插件联调，参考文档：[插件联调](https://opendocs.alipay.com/mini/plugin/test)。
