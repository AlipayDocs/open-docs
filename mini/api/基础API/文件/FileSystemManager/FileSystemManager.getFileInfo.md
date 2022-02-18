
# 简介
**FileSystemManager.getFileInfo** 获取该小程序下的本地临时文件或本地缓存文件信息。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.getFileInfo({
  filePath: `${my.env.USER_DATA_PATH}/test.txt`,
  success: (res) => {
	  console.log(res);
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 文件路径。 |
| digestAlgorithm | String | 否 | 文件编码，默认 md5。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| size | Number | 文件大小，以字节为单位。 |


## 错误码
| **错误码** | **描述** |
| --- | --- |
| 10024 | 指定文件没有读的权限。 |

