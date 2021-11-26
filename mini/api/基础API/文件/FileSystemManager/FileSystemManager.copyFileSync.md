
# 简介
[FileSystemManager.copyFile](https://opendocs.alipay.com/mini/api/0226of) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
const result = fs.copyFileSync(
  `${my.env.USER_DATA_PATH}/test/copyFile/path/aa.txt`,
  `${my.env.USER_DATA_PATH}test/copyFile/path/dest/bb.txt`
);
console.log(result);
```

## 入参

#### string srcPath
源文件路径，只可以是普通文件。

#### string destPath
目标文件路径。

## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 源文件不存在。 |
| 10023 | 指定路径是一个已存在的目录。 |
| 10024 | 指定的路径没有读或者写的权限。 |

