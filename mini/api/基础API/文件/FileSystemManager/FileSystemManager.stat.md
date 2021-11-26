
# 简介
**FileSystemManager.stat** 用于获取文件 Stats 对象。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// recursive 为 false 时
const fs = my.getFileSystemManager()
fs.stat({
  path: `${my.env.USER_DATA_PATH}/testDir`,
  success: res => {
    console.log(res.stats.isDirectory())
  }
})

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
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **默认值** | **描述** |
| --- | --- | --- | --- | --- |
| path | String | 是 | - | 文件/目录路径。 |
| recursive | Boolean | 否 | false | 是否递归获取目录下的每个文件的 Stats 信息。 |
| success | Function | 否 | - | 调用成功的回调函数。 |
| fail | Function | 否 | - | 调用失败的回调函数。 |
| complete | Function | 否 | - | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| stats | [Stats](https://opendocs.alipay.com/mini/api/stats)/Object | 当 recursive 为 false 时，res.stats 是一个 Stats 对象。当 recursive 为 true 且 path 是一个目录的路径时，res.stats 是一个 Object，key 以 path 为根路径的相对路径，value 是该路径对应的 Stats 对象。 |


#### stats 对象
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| mode | Long | 文件的类型和存取的权限. |
| size | Long | 文件大小。 |
| lastAccessedTime | Long | 上次访问时间。 |
| lastModifiedTime | Long | 上次修改时间。 |

