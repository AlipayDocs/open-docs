
# 简介
[FileSystemManager.readdir](https://opendocs.alipay.com/mini/api/0226oi) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。
- 此 API 暂不支持在 IDE 模拟器上测试，开发中请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 进行测试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
const result = fs.readdirSync(`${my.env.USER_DATA_PATH}/dir`);
console.log(result);
```

## 入参

#### string dirPath
目录地址。

## 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| files | `Array<String>` | 指定目录下的文件名数组。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10024 | 指定路径没有读权限。 |
| 10022 | 目录不存在。 |



