
# 简介
[FileSystemManager.mkdir](https://opendocs.alipay.com/mini/api/0226oh) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();

const result = fs.mkdirSync(`${my.env.USER_DATA_PATH}/newDir`, false);
console.log(result);
```

## 入参

#### string dirPath
创建的目录路径。

#### boolean recursive
是否在递归创建该目录的上级目录后再创建该目录。如果对应的上级目录已经存在，则不创建该上级目录。如 dirPath 为 a/b/c/d 且 recursive 为 true，将创建 a 目录，再在 a 目录下创建 b 目录，以此类推直至创建 a/b/c 目录下的 d 目录。

## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10024 | 指定路径没有写的权限。 |
| 10025 | 有同名文件或目录。 |
| 10022 | 上级目录不存在。 |

