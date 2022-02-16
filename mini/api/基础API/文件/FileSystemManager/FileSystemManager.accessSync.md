
# 简介
[FileSystemManager.access](https://opendocs.alipay.com/mini/api/0226oe) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 此 API 暂不支持在 IDE 模拟器上调用，开发中请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 进行测试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
let result =  fs.accessSync(`${my.env.USER_DATA_PATH}/test.txt`);
console.log(result);
```

## 入参

#### string path
要判断是否存在的文件/目录路径。

## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 文件 / 目录不存在。 |
| 10024 | 传入的路径没有读的权限。 |

