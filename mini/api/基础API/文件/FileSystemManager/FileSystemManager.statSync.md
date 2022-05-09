# 简介
[FileSystemManager.statSync](https://opendocs.alipay.com/mini/api/022b6o) 的同步版本。

## 使用限制

- 基础库  [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，可查看 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。
- 此 API 暂不支持在 IDE 模拟器上测试，开发中请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 进行测试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// recursive 为 false 时
const fs = my.getFileSystemManager()
const result1 = fs.statSync(`${my.env.USER_DATA_PATH}/testDir`);
if (result1.stats) {
 console.log(result1.stats.isDirectory())
}
// recursive 为 true 时
const result2 = fs.statSync(`${my.env.USER_DATA_PATH}/testDir`, true);
if (result2.stats) {
  for (const path of Object.keys(result2.stats)) {
    const statsObj = result2.stats[path];
    console.log(path, statsObj.stats.isDirectory());
  }
}
```

## 入参

### String path
文件/目录路径。

### Booleab recursive
是否递归获取目录下的每个文件的 Stats 信息。

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| stats | [Stats](https://opendocs.alipay.com/mini/api/stats)/Object | 当 recursive 为 false 时，res.stats 是一个 Stats 对象。当 recursive 为 true 且 path 是一个目录的路径时，res.stats 是一个 Object，key 以 path 为根路径的相对路径，value 是该路径对应的 Stats 对象。 |

### Stats/Object stats
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| mode | Long | - |
| size | Long | 文件大小。 |
| lastAccessedTime | Long | 上次访问时间。 |
| lastModifiedTime | Long | 上次修改时间。 |
