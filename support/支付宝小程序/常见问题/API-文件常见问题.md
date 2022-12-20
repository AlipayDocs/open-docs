## 使用限制
- **my.openDocument 基础库** [1.15.0 ](https://opendocs.alipay.com/mini/framework/lib)或更高版本，**支付宝客户端** 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。**my.openDocument** 只支持在真机上测试，无法在 IDE 上调试。
- **my.getSavedFileInfo 基础库** [1.3.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **my.getFileInfo基础库** [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **my.saveFile、my.getSavedFileList、my.removeSavedFile** 需**基础库** [1.13.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本，**支付宝客户端** 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 

## 常见问题

### my.saveFile保存的文件是否有大小限制，如何查看保存到本地的文件

- [my.saveFile](https://opendocs.alipay.com/mini/api/xbll1q) 是保存文件到本地（本地文件大小总容量限制：10 MB）的 API。
- 调用 my.saveFile 成功后，Android 系统可在 **手机存储/alipay/pictures/文件位置 **查看保存的文件；iOS 系统无法查看被隐藏的目录路径。 

### 小程序支持打开pdf和excel吗
小程序不支持打开 excel 文件，但小程序可通过 [my.openDocument ](https://opendocs.alipay.com/mini/api/mwpprc)打开 pdf 文件，暂时只支持预览。 

### getFileInfo size 的单位是什么
[my.getFileInfo](https://opendocs.alipay.com/mini/api/file)  返回数据中的 size 文件大小单位是字节，例如：<br />返回的数据值  size=100，即文件大小为 100 字节。 

### my.openDocument失败

- 版本需求：支付宝客户端版本 10.1.60 及以上版本，基础库版本 1.15.0 及以上版本，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 在新页面打开文件预览，暂时只支持预览 PDF 格式文件。
- 测试须知：my.openDocument 只支持在真机上测试，无法在 IDE 上调试。 

### my.openDocument是否支持IDE预览
暂不支持，my.openDocument 目前只支持在真机上测试，无法在 IDE 上调试。 

### my.openDocument如何设置标题
my.openDocument 无法设置标题，打开文件预览显示的是 pdf 文件的标题。<br /> 
