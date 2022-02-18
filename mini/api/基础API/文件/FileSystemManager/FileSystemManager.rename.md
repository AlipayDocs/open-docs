
# 简介
**FileSystemManager.rename** 用于重命名文件，可以把文件从 oldPath 移动到 newPath。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.rename({
  oldPath: `${my.env.USER_DATA_PATH}/test.txt`,
  newPath: `${my.env.USER_DATA_PATH}/test_new.txt`,
  success: (res) => {
		consoloe.log(res);
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| oldPath | String | 是 | 源文件路径，可以是普通文件或目录。 |
| newPath | String | 是 | 新文件路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 源文件不存在 |
| 10024 | 指定源文件或者目标文件没有写权限 |

