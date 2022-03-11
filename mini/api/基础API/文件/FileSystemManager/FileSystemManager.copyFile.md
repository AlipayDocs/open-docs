
# 简介
**FileSystemManager.copyFile** 复制文件（支持复制临时文件、缓存文件、用户文件到本地用户文件位置）。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码

复制缓存文件：
```JavaScript
  let fs = my.getFileSystemManager();
  my.downloadFile({
    url: 'https://gw.alipayobjects.com/os/bmw-prod/61b560b7-b50b-4928-b392-c39a1c4bd0fd.txt',
    success({ apFilePath }) {
      console.log(JSON.stringify(apFilePath))
      fs.copyFile({
        srcPath: apFilePath,
        destPath: `${my.env.USER_DATA_PATH}/bb.txt`,
        success: (res) => {
          console.log(JSON.stringify(res));
          fs.readFile({
            filePath: `${my.env.USER_DATA_PATH}/bb.txt`,
            encoding: "utf8",
            success: (res) => {
              console.log(JSON.stringify(res));
              my.alert({
                content: res.data,
              });
            }
          });
        },
        fail: (err)=>{
          console.log(JSON.stringify(err));
        }
      });
    },
    fail(res) {
      my.alert({
        content: res.errorMessage || res.error,
      });
    },
  });
```

复制用户文件：
```javascript
  let fs = my.getFileSystemManager();
  fs.copyFile({
    srcPath: `${my.env.USER_DATA_PATH}/test/copyFile/path/aa.txt`,
    destPath: `${my.env.USER_DATA_PATH}test/copyFile/path/dest/bb.txt`,
    success: (res) => {
 	  console.log("成功");
    }
  });
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| srcPath | String | 是 | 源文件路径，只可以是普通文件。 |
| destPath | String | 是 | 目标文件路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 源文件不存在 |
| 10023 | 指定路径是一个已存在的目录 |
| 10024 | 指定的路径没有读或者写的权限 |



