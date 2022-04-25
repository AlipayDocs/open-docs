# 简介
**FileSystemManager.saveFile** 用于保存临时文件到本地。此接口会移动临时文件，因此调用成功后，tempFilePath 将不可用。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，可查看 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码

保存为本地用户文件：

```javascript
let fs = my.getFileSystemManager();
my.chooseImage({
  count: 1,
  success(res) {
  	fs.saveFile({
      tempFilePath: res.apFilePaths[0],
      filePath: `${my.env.USER_DATA_PATH}/img.png`,
      success: (res1) => {
        console.log(res1.savedFilePath);
      }
    })
  }
});
```

保存为本地缓存文件：

```JavaScript
let fs = my.getFileSystemManager();
my.downloadFile({
  url: 'https://img.alicdn.com/tfs/TB1x669SXXXXXbdaFXXXXXXXXXX-520-280.jpg',
  success({ apFilePath }) {
    console.log(JSON.stringify(apFilePath))
    fs.saveFile({
      tempFilePath: apFilePath,
      success: (res1) => {
        console.log(res1.savedFilePath)
      }
    })
  },
  fail(res) {
    my.alert({
      content: res.errorMessage || res.error,
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| tempFilePath | String | 是 | 临时存储文件路径。 |
| filePath | String | 否 | 要存储的文件路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

**说明**：如果不传，默认存储在小程序缓存目录。

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **名称** | **类型** | **描述** |
| --- | --- | --- |
| savedFilePath | String | 存储后的文件路径。 |


## 错误码
| **错误码** | **描述** |
| --- | --- |
| 10022 | 指定文件不存在。 |
| 10024 | 指定的路径没有写的权限。 |

