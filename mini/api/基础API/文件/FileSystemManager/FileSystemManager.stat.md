# 简介

**FileSystemManager.stat** 用于获取本地文件的 Stats 对象。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// recursive 为 false 时
const fs = my.getFileSystemManager();
fs.stat({
  path: `${my.env.USER_DATA_PATH}/testDir`,
  success: res => {
    console.log(res.stats.isDirectory());
  },
});

// recursive 为 true 时
fs.stat({
  path: `${my.env.USER_DATA_PATH}/testDir`,
  recursive: true,
  success: res => {
    if (res.stats) {
      for (const path of Object.keys(res.stats)) {
        const statsObj = res.stats[path];
        console.log(path, statsObj.stats.isDirectory());
      }
    }
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| path | String | 是 | 本地文件/目录路径。支持[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。 |
| recursive | Boolean | 否 | 是否递归获取目录下的每个文件的 Stats 信息。<br />**默认值**：false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| stats | Object | 当 recursive 为 false 时，res.stats 是一个 [Stats](https://opendocs.alipay.com/mini/api/stats) 对象。当 recursive 为 true 且 path 是一个目录的路径时，res.stats 是一个 Object，key 是以 path 为根路径的相对路径，value 是该路径对应的 [Stats](https://opendocs.alipay.com/mini/api/stats) 对象。 |

#### Stats/Object stats

| **属性**         | **类型** | **描述**                |
| ---------------- | -------- | ----------------------- |
| mode             | Number     | 文件的类型和存取的权限. |
| size             | Number     | 文件大小。              |
| lastAccessedTime | Number     | 上次访问时间。          |
| lastModifiedTime | Number     | 上次修改时间。          |
