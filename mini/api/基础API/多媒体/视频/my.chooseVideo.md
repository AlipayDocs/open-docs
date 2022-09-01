# 简介

拍摄视频或从手机相册中选视频。

注意：支付宝会将选取的视频文件名重命名为 `.video` 后缀并存到一个临时路径下，不改变视频实际格式。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.chooseVideo({
  sourceType: ['album', 'camera'],
  maxDuration: 60,
  camera: 'back',
  success: (res) => {
    console.log(res);
  },
  fail: (error) => {
    console.log(error);
  },
  complete: () => {
    console.log('调用完成，无论成功和失败都会运行');
  }
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| sourceType | `Array<String>` | 否 | 视频选择的来源。<br />默认为 `['album','camera']`。 |
| compressed | Boolean | 否 | 是否压缩所选择的视频文件。<br />对 iOS 总是有压缩的，只是压缩级别不同。<br />默认为 true。<br /> |
| maxDuration | Number | 否 | 拍摄视频最长拍摄时间，单位秒。<br />默认为 60。 |
| camera | String | 否 | 默认拉起的是前置或者后置摄像头。部分 Android 手机下由于系统 ROM 不支持无法生效。<br />默认为 'back'。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### sourceType 的合法值

| **值** | **说明**           |
| ------ | ------------------ |
| album  | 从相册选择视频。   |
| camera | 使用相机拍摄视频。 |

### camera 的合法值

| **值** | **说明**             |
| ------ | -------------------- |
| back   | 默认拉起后置摄像头。 |
| front  | 默认拉起前置摄像头。 |

### success 回调函数

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| tempFilePath | String | 选定视频的临时文件路径。<br />基础库 [1.11.0](https://docs.alipay.com/mini/framework/compatibility) 及以上版本支持。 |
| duration | Number | 选定视频的时间长度。 |
| size | Number | 选定视频的数据量大小。 |
| height | Number | 返回选定视频的高度。 |
| width | Number | 返回选定视频的宽度。 |

## 错误码

| **错误码** | **描述** | **解决方案** | **支持平台** |
| --- | --- | --- | --- |
| 10 | 用户取消操作。 | 这是用户正常交互流程分支，不需要特殊处理。 | Android |
| 11 | 用户取消操作。 | 这是用户正常交互流程分支，不需要特殊处理。 | iOS |
| 21 | 视频压缩失败。 | 请重试。 | iOS |
| 2001 | 在申请授权时用户拒绝授权。 | 这是用户正常交互流程分支，不需要特殊处理。 | iOS / Android |

# 常见问题 FAQ

## Q：如果系统权限未开启，接口调用报错，如何引导开启系统权限？

A：可以调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启相关系统权限。

## Q: 如何上传用户选择的视频？

A：可以配合 [my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc) 一起使用。

```js
Page({
  uploadFile() {
    my.chooseVideo({
      sourceType: ['album', 'camera'],
      maxDuration: 60,
      camera: 'back',
      success(res) {
        console.log('chooseVideo', res);
        const path = res.tempFilePath;
        console.log(path);
        my.uploadFile({
          url: 'https://httpbin.org/post',
          fileType: 'video',
          fileName: 'user-selected-video',
          filePath: path,
          formData: { extra: '其他信息' },
          success: res => {
            console.log('success res', res);
            my.alert({ title: '上传成功' });
          },
          fail: err => {
            my.alert({ title: '上传失败', content: JSON.stringify(err) });
          },
        });
      },
    });
  },
});
```
