
# 简介
保存视频到系统相册。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，可查看 [接入准备](https://opendocs.alipay.com/mini/02p2m1)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 开发者工具暂不支持此能力，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// 本地路径
my.chooseVideo({
  sourceType: ['album','camera'],
  maxDuration: 60,
  camera: 'back',
  success(res) {
    my.saveVideoToPhotosAlbum({
     filePath: res.tempFilePath,
      complete(res2) {
       console.log(res2);
      }
    });
  }
})
// 网络路径
my.saveVideoToPhotosAlbum({
  filePath:'http://flv.bn.netease.com/tvmrepo/2012/7/C/7/E868IGRC7-mobile.mp4',
  complete(res) {
    console.log(res);
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 视频文件路径，支持网络路径、[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)，暂不支持[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### 错误码
| **错误码** | **说明** |
| --- | --- |
| 2 | 参数无效，没有传 filePath 参数。 |
| 15 | 没有开启相册权限(iOS only)。 |
| 16 | 手机相册存储空间不足(iOS only)。 |
| 17 | 保存图片过程中的其他错误。 |

