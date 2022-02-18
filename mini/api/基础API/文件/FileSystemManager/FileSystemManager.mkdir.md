
# 简介
**FileSystemManager.mkdir** 创建目录。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.mkdir({
  dirPath: `${my.env.USER_DATA_PATH}/newDir`,
  recursive: false,
  success: (res) => {
		console.log(res)
  }
});
```

## 入参
| **属性** | **类型** | **必填** | **默认值** | **描述** |
| --- | --- | --- | --- | --- |
| dirPath | String | 是 | - | 创建的目录路径。 |
| recursive | Boolean | 否 | false | 是否在递归创建该目录的上级目录后再创建该目录。如果对应的上级目录已经存在，则不创建该上级目录。如 dirPath 为 a/b/c/d 且 recursive 为 true，将创建 a 目录，再在 a 目录下创建 b 目录，以此类推直至创建 a/b/c 目录下的 d 目录。 |
| success | Function | 否 | - | 调用成功的回调函数。 |
| fail | Function | 否 | - | 调用失败的回调函数。 |
| complete | Function | 否 | - | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10024 | 指定路径没有写的权限 |
| 10025 | 有同名文件或目录 |
| 10022 | 上级目录不存在 |



