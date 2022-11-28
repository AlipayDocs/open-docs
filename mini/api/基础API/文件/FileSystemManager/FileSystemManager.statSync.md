# 简介

[FileSystemManager.statSync](https://opendocs.alipay.com/mini/api/022b6o) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// recursive 为 false 时
const fs = my.getFileSystemManager();
const result1 = fs.statSync(`${my.env.USER_DATA_PATH}/testDir`);
if (result1.stats) {
  console.log(result1.stats.isDirectory());
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

文件或目录路径。支持 [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。

### Booleab recursive

是否递归获取目录下的每个文件的 Stats 信息，不传时默认为 false。

## 返回值

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| stats | Object | 当 recursive 为 false 时，res.stats 是一个 [Stats](https://opendocs.alipay.com/mini/api/stats) 对象。当 recursive 为 true 且 path 是一个目录的路径时，res.stats 是一个 Object，key 是以 path 为根路径的相对路径，value 是该路径对应的 [Stats](https://opendocs.alipay.com/mini/api/stats) 对象。 |

### Stats/Object stats

| **属性**         | **类型** | **描述**       |
| ---------------- | -------- | -------------- |
| mode             | Number     | 文件的类型和存取的权限。         |
| size             | Number     | 文件大小。     |
| lastAccessedTime | Number     | 上次访问时间。 |
| lastModifiedTime | Number     | 上次修改时间。 |
