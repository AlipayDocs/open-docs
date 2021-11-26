
# 简介
[FileSystemManager.rmdir](https://opendocs.alipay.com/mini/api/0229px) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
const result = fs.rmdirSync(
  `${my.env.USER_DATA_PATH}/newDir`,
  false
);
console.log(result);
```

## 入参

#### string dirPath
要删除的目录路径。

#### boolean recursive
是否递归删除目录。若为true则删除该目录和该目录下的所有子目录以及文件。

## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 目录不存在。 |
| 10024 | 指定的路径没有写权限。 |
| 10027 | 目录不为空。 |

