
# 简介
**FileSystemManager.rmdir** 用于删除目录。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.rmdir({
  dirPath: `${my.env.USER_DATA_PATH}/newDir`,
  recursive: false,
  success: (res) => {
		console.log(res);
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **默认值** | **描述** |
| --- | --- | --- | --- | --- |
| dirPath | String | 是 | - | 要删除的目录路径。 |
| recursive | Boolean | 否 | false | 是否递归删除目录。如果为 true，则删除该目录和该目录下的所有子目录以及文件。 |
| success | Function | 否 | - | 调用成功的回调函数。 |
| fail | Function | 否 | - | 调用失败的回调函数。 |
| complete | Function | 否 | - | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 目录不存在。 |
| 10024 | 指定的路径没有写权限。 |
| 10027 | 目录不为空。 |



