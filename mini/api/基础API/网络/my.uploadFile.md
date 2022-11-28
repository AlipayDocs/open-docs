# 简介

**my.uploadFile** 上传本地文件到开发者服务器。客户端发起的是一个 HTTPS POST 请求。

## 接入准备

my.uploadFile 只能与白名单中的域名进行通信，使请先在[开放平台控制台-开发设置页面](https://open.alipay.com/develop/mini/sub/dev-setting)配置**服务器域名白名单**：

![|706x73](http://mdn.alipayobjects.com/afts/img/A*xM4NR6VRbfy_8SFDkgXUhQBkAa8wAA/original?bz=openpt_doc&t=JgMQtxsM9S7uH5pPEDbN9wAAAABkMK8AAAAA#align=left&display=inline&height=168&margin=%5Bobject%20Object%5D&originHeight=168&originWidth=1624&status=done&style=stroke&width=1624)

> **注意**：域名白名单会在构建时写入小程序，在新版本中生效，小程序历史版本不受影响。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d1f6c80ce1f38600a43b90ad8730efae.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d5875d1a94433734166ca5760c485107.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .js 示例代码

选择照片并上传的前端代码：

```javascript
my.chooseImage({
  success: res => {
    const path = res.apFilePaths[0];
    console.log(path);
    my.uploadFile({
      url: 'https://...', // 请替换成有效的服务端 url
      fileType: 'image',  //此参数已废弃，无须传入。但目前 IDE 模拟器仍会对该字段做校验，只接受 image / video / audio 三者之一。建议使用真机测试。
      name: 'userfile',
      filePath: path,
      formData: { extra: '其他信息' },
      success: res => {
        my.alert({ title: '上传成功' });
      },
      fail: err => {
        my.alert({ title: '上传失败', content: JSON.stringify(err) });
      },
    });
  },
});
```

### .java 示例代码

接收上传文件的服务端代码：

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Scanner;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.Part;
import javax.servlet.annotation.MultipartConfig;

@MultipartConfig(
  fileSizeThreshold = 1024 * 1024 * 1,
  maxFileSize = 1024 * 1024 * 10,
  maxRequestSize = 1024 * 1024 * 100
)
public class UploadServlet extends HttpServlet {
  @Override
  public void doPost(HttpServletRequest request, HttpServletResponse response)
    throws IOException, ServletException
  {
    Part filePart = request.getPart("userfile");
    String fileSize = filePart == null ? "0" : filePart.getSize() + " bytes";

    if (filePart != null) {
      String fileName = filePart.getSubmittedFileName();
      String filePath = "/tmp/upload" + fileName.substring(fileName.lastIndexOf(".")); // 文件命名，请自行修改
      filePart.write(filePath);
    }

    Part extraPart = request.getPart("extra");
    String extraValue = extraPart == null ? "" : new Scanner(extraPart.getInputStream(), "UTF-8").useDelimiter("\\A").next();

    response.setCharacterEncoding("UTF-8");
    response.getWriter().print("file: " + fileSize + "; extra: " + extraValue);
  }
}
```


### .php 示例代码

接收上传文件的服务端代码：

```php
<?php
function accept_my_upload() {
  $size = 0;
  $path = '';
  if ($file = @$_FILES['userfile']) {
    $name = $file['name'];
    $ext = strrpos($name, '.') === false ? '' : substr($name, strrpos($name, '.'));
    $path = '/tmp/' . time() . round(microtime() * 1000) . $ext; // 文件命名，请自行修改
    if (move_uploaded_file($file['tmp_name'], $path)) {
      $size = $file['size'];
    }
  }
  $extra = @$_POST['extra'];
  echo "file: $size bytes($path); extra: $extra";
}
accept_my_upload();
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 接收上传文件的服务端 url。 |
| filePath | String | 是 | 要上传的文件路径（[本地路径](https://opendocs.alipay.com/mini/03dt4s)）<br> **注意**：目前 IDE 暂不支持本地用户文件。建议使用真机测试。 |
| name | String | 是 | 指定 POST 请求中的文件名，服务端需按此参数取值读取文件数据。 |
| header | Object | 否 | HTTP 请求 Header。其中 content-type 为 multipart/form-data（与 request body 实际格式一致），请勿更改。 |
| formData | Object | 否 | HTTP 请求中的其他数据，每个 key 为字段名，value 为字符串。 |
| fileType | String | 否 | 此参数已废弃，无须传入。<br> **注意**：目前 IDE 模拟器仍会对该字段做校验，只接受 image / video / audio 三者之一。建议使用真机测试。 |
| timeout | Number | 否 | 超时时间，默认值 60000，单位 ms。 |
| hideLoading | Bool | 否 | 是否隐藏 loading 动画。默认值为 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**   | **类型** | **描述**              |
| ---------- | -------- | --------------------- |
| data       | String   | 服务器返回的数据。    |
| statusCode | Number   | HTTP 状态码。         |
| header     | Object   | 服务器返回的 Header。 |

## 错误码

<table>
  <tr>
      <th><b>错误码</b></th>
      <th><b>说明</b></th>
      <th><b>解决方案</b></th>
  </tr>
  <tr>
      <td >4</td>
      <td>未配置域名白名单，无权访问域名</td>
      <td>
          <ul>
              <li>在[开放平台控制台-开发设置页面](https://open.alipay.com/develop/mini/sub/dev-setting)配置**服务器域名白名单**。注意新的域名白名单只对后续构建的小程序版本生效，小程序历史版本的域名白名单固定不变。</li>
              <li>开发调试时，可在 IDE 右上角点击 <b>详情</b> > <b>域名信息</b> 下勾选 <b>忽略 request 域名合法性检查（仅在本地模拟、预览和远程调试时生效）。</b></li>
          </ul>
      </td>
  </tr>
  <tr>
      <td>9</td>
      <td>uploadFile:fail abort</td>
      <td>上传文件中止文件，在上传文件未完成时调用了 UploadTask.abort()。</td>
  </tr>
  <tr>
      <td rowspan="2">11</td>
      <td>文件不存在</td>
      <td>检查本地文件是否存在。</td>
  </tr>
  <tr>
      <td>无效参数</td>
      <td>检查是否有必传项没传；检查是否有字段传错类型。</td>
  </tr>
  <tr>
      <td rowspan="2">12</td>
      <td>java.io.FileNotFoundException:File is not a normal file.</td>
      <td>检查入参 filePath 的有效性。</td>
  </tr>
  <tr>
      <td>上传文件失败</td>
      <td>
          <ul>
              <li>请求失败。稍后重试，或检查网络连接是否有效。</li>
              <li>上传超时。可使用 timeout 设定超时时间。</li>
          </ul>
      </td>
  </tr>
  <tr>
      <td>20</td>
      <td>请求 URL 不支持 HTTP，请使用 HTTPS</td>
      <td>小程序已经不支持 HTTP 请求，请使用 HTTPS。</td>
  </tr>
</table>

## UploadTask

**版本要求：** 支付宝客户端 10.1.35 及以上版本，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

my.uploadFile 返回的对象，可用于监听上传进度变化或取消上传任务。

| **方法**                                       | **描述**             |
| ---------------------------------------------- | -------------------- |
| UploadTask.abort()                             | 中断上传任务         |
| UploadTask.onProgressUpdate(function callback) | 监听上传进度变化事件 |
| UploadTask.onHeadersReceived(function callback) | 监听 HTTP Response Header 事件。会比请求完成事件更早。AppX 2.8.2 且支付宝客户端 10.2.90 及以上版本，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 |
| UploadTask.offHeadersReceived(function callback) | 移除 HTTP Response Header 事件的监听函数。AppX 2.8.2且支付宝客户端 10.2.90 及以上版本，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。 |

### 使用示例

```javascript
const task = my.uploadFile({
  // ... 
});
// onProgressUpdate 示例
task.onProgressUpdate(payload => {
  const { progress, totalBytesWritten, totalBytesExpectedToWrite } = payload;
  console.log(`uploadProgress: ${progress}%`);
});
// abort 示例
task.abort();
// onHeadersReceived 示例
if (my.canIUse('uploadFile.return.onHeadersReceived')) {
  task.onHeadersReceived(header => {
     console.log(header);
  });
// if (my.canIUse('uploadFile.return.offHeadersReceived')) {
//    task.offHeadersReceived();
// }
}
```

其中，payload 参数的含义如下：

- progress：上传进度百分比，取值 0~100
- totalBytesWritten: 已经上传的数据长度，单位 Bytes
- totalBytesExpectedToWrite: 预期需要上传的数据总长度，单位 Bytes

header 参数的含义：开发者服务器返回的 HTTP Response Header

# 常见问题 FAQ

## Q：使用 my.chooseImage 选中的图片，如果转换成 base64？

A：可以使用 FileSystemManager.readFile 先读取文件内容，然后调用 my.arrayBufferToBase64。示例如下：
```javascript
my.chooseImage({
  success: res => {
    const fs = my.getFileSystemManager();
    fs.readFile({
      filePath: `${res.apFilePaths[0]}`,
      // readFile 不传入 encodding 参数，则以 ArrayBuffer 方式读取
      success:({ data }) => {
        const base64 = my.arrayBufferToBase64(data);
        // 
      },
    });
  }
});
```

## Q：my.uploadFile 如何获取服务器返回的错误信息呢？

A：通过 success 回调中的 data 参数获取，或者在服务端自行记录错误日志。

## Q：小程序是否支持上传 excel 文件？

A：真机上小程序并不限制上传类型。可以支持上传 excel。目前 IDE 还是会对 fileType 做强校验，未来会修复，建议先用真机调试。

## Q：my.uploadFile 支持多张图片同时上传吗？

A：my.uploadFile 一次只能上传一张图片，但是可以循环/并发调用。示例：
```javascript
my.chooseImage({
  count: 3, // 最多选择 3 张图片
  success: (res) => {
    for (let path of res.apFilePaths) { // 循环调用 my.uploadFile
      my.uploadFile({
        url: 'https://...', // 请替换成有效的服务端 url
        name: 'userfile',
        filePath: path,
        success: () => {
          console.log(`${path} upload success`);
        },
        fail: () => {
          console.log(`${path} upload fail`);
        }
      });
    }
  }
});
```
