
# 简介
**FileSystemManager.readdir** 读取目录内文件列表。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.readdir({
  dirPath: `${my.env.USER_DATA_PATH}/newDir`,
  success: (res) => {
		console.log(res);
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| dirPath | String | 是 | 目录地址。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| files | Array<String> | 指定目录下的文件名数组。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10024 | 指定路径没有读权限。 |
| 10022 | 目录不存在。 |

