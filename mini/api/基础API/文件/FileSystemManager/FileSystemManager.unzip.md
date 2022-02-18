
# 简介
**FileSystemManager.unzip** 用于解压文件。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager()
fs.unzip({
  zipFilePath: `${my.env.USER_DATA_PATH}/tesy.zip`,
  targetPath: '${my.env.USER_DATA_PATH}/test',
  success(res) {
    console.log(res)
  },
  fail(res) {
    console.error(res)
  }
})
```

## 入参说明
| **名称** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| zipFilePath | String | 是 | 源文件路径，只可以是 zip 压缩文件。 |
| targetPath | String | 是 | 目标目录路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10024 | 指定的源文件路径没有读权限或指定的目标文件路径没有写权限。 |
| 10022 | 源文件不存在或上层目录不存在。 |
| 3 | 未知错误，解压失败。 |

