
# 简介
[FileSystemManager.rename](https://opendocs.alipay.com/mini/api/0229pw) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
const result = fs.renameSync(
  `${my.env.USER_DATA_PATH}/test.txt`,
  `${my.env.USER_DATA_PATH}/test_new.txt`
);
console.log(result);
```

## 入参

#### string oldPath
源文件路径，可以是普通文件或目录。

#### string newPath
新文件路径。

## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 源文件不存在。 |
| 10024 | 指定源文件或者目标文件没有写权限。 |

