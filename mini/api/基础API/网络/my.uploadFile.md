# 简介

**my.uploadFile** 是上传本地资源到开发者服务器的 API，客户端发起的是一个 HTTPS POST 请求。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。
> 请登录 [开放平台控制台](https://open.alipay.com/dev/workspace) > 点击要配置的小程序，进入小程序详情页 > **设置** > **开发设置** > **服务器域名白名单** 中配置域名白名单。小程序在以下 API 调用时只能与白名单中的域名进行通讯：HTTPS 请求（my.request）、上传文件（my.uploadFile）。
>
> ![|706x73](http://mdn.alipayobjects.com/afts/img/A*xM4NR6VRbfy_8SFDkgXUhQBkAa8wAA/original?bz=openpt_doc&t=JgMQtxsM9S7uH5pPEDbN9wAAAABkMK8AAAAA#align=left&display=inline&height=168&margin=%5Bobject%20Object%5D&originHeight=168&originWidth=1624&status=done&style=stroke&width=1624)
>
> **注意**：域名添加或删除后仅对新版本小程序生效，老版本仍使用修改前的域名配置。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d1f6c80ce1f38600a43b90ad8730efae.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d5875d1a94433734166ca5760c485107.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .json 示例代码

**注意**：案例仅供参考，建议使用自己的地址进行测试。
```json
{
    "defaultTitle": "Upload File"
}
```
### .axml 示例代码
```html
<!-- API-DEMO page/upload-file/upload-file.axml -->
<view class="page">
  <button type="primary" onTap="uploadFile">上传图片</button>
</view>
```
### .js 示例代码
```javascript
// API-DEMO page/API/upload-file/upload-file.js
Page({
  uploadFile() {
    my.chooseImage({
      chooseImage: 1,
      success: res => {
        const path = res.apFilePaths[0];
        console.log(path);
        my.uploadFile({
          url: 'https://httpbin.org/post',
          fileType: 'image',
          fileName: 'file',
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
  },
});
```

### .java 示例代码

上传文件的服务端代码：
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
  fileSizeThreshold = 1024 * 1024 * 1, // 1 MB
  maxFileSize = 1024 * 1024 * 10,      // 10 MB
  maxRequestSize = 1024 * 1024 * 100   // 100 MB
)
public class UploadServlet extends HttpServlet {

    @Override
    public void doPost(HttpServletRequest request, HttpServletResponse response)
        throws IOException, ServletException
    {
        Part filePart = request.getPart("file");
        String fileSize = filePart == null ? "0" : filePart.getSize() + " bytes";
        
        if (filePart != null) {
            String fileName = filePart.getSubmittedFileName();
            String filePath = "/tmp/upload" + fileName.substring(fileName.lastIndexOf("."));
            filePart.write(filePath);
        }
        
        Part extraPart = request.getPart("extra");
        String extraValue = extraPart == null ? "" : new Scanner(extraPart.getInputStream(), "UTF-8").useDelimiter("\\A").next();
        
        response.setCharacterEncoding("UTF-8");
        response.getWriter().print("file: " + fileSize + "; extra: " + extraValue);
    }
    
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 开发者服务器地址。 |
| filePath | String | 是 | 要上传文件资源的本地路径。 |
| fileName | String | 是 | 文件名，即对应的 key，开发者在服务器端通过这个 key 可以获取到文件二进制内容。 |
| fileType | String | 是 | 文件类型支持图片、视频、音频，对应的值分别为 "image"、"video"、"audio"。 |
| hideLoading | Bool | 否 | 是否隐藏 loading 图（默认值为 false）。 |
| header | Object | 否 | HTTP 请求 Header。 |
| formData | Object | 否 | HTTP 请求中其他额外的 form 数据。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | String | 服务器返回的数据。 |
| statusCode | Number | HTTP 状态码。 |
| header | Object | 服务器返回的 Header。 |

## 错误码

<table>
    <tr>
        <th><b>错误码</b></th>
        <th><b>说明</b></th>
        <th><b>解决方案</b></th>
    </tr>
    <tr>
        <td rowspan="3">4</td>
        <td>无权限调用（N22104）</td>
        <td>
            <ol>
                <li>确认小程序应用是否授权给了三方应用，三方应用是否添加了 <b>JSAPI 基础包</b> 功能包。可尝试添加 <b>JSAPI 基础包</b> 功能包后，重新授权、重新推送预览调试或者直接解除三方应用授权，重新推送预览调试。</br><b>说明</b>：小程序应用授权给三方应用后，小程序在真机上的运行使用的是三方应用的功能包，不再是使用小程序自身的功能包。</li>
                <li>若是小程序应用 <b>JSAPI 基础包</b> 功能包没有或者不全，建议删除小程序应用，重新创建一个新小程序应用来调试。</li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>无权限调用（N22106）</td>
        <td rowspan="2">
            <ul>
                <li>配置请求白名单，请预先登录 <a href="https://open.alipay.com/dev/workspace">开放平台控制台</a> > 点击要配置的小程序，进入小程序详情页 > <b>设置</b> > <b>开发设置</b> > <b>服务器域名白名单</b> 中配置域名白名单。域名添加或删除后仅对新版本生效，老版本仍使用修改前的域名配置。</li>
                <li>若是账号问题，不能登录管理后台配置，开发版测试可以先在 IDE 右上角点击 <b>详情</b> > <b>域名信息</b> 下勾选 <b>忽略 request 域名合法性检查（仅在本地模拟、预览和远程调试时生效）</b>或 <b>忽略 Webview 域名合法性检查（仅在本地模拟、预览和远程调试时生效）</b>，再预览调试请求。</li>
                <li>建议做下兼容，不要使用 my.saveFile 保存文件后返回的 apFilePath 作为上传 filePath 的入参。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>无权限调用此接口</td>
    </tr>
    <tr>
        <td>9</td>
        <td>uploadFile:fail abort</td>
        <td>上传文件中止文件，在上传文件未完成时调用了 UploadTask.abort()。</td>
    </tr>
    <tr>
        <td rowspan="2">11</td>
        <td>not have permission to upload</td>
        <td>出于安全策略，不能使用 my.saveFile 保存文件后返回的 apFilePath 作为上传 filePath 的入参。</td>
    </tr>
    <tr>
        <td>文件不存在</td>
        <td>检查本地文件是否存在。</td>
    </tr>
    <tr>
        <td rowspan="2">12</td>
        <td>java.io.FileNotFoundException:File is not a normal file.</td>
        <td>文件未找到 / 文件不是一个正常的文件，确认 filePath 入参的正确性，必须是本地定位符，可使用 <a href="https://opendocs.alipay.com/mini/api/media/image/my.chooseimage">my.chooseImage</a> 在相册选择图片后返回的地址。</td>
    </tr>
    <tr>
        <td>上传文件失败</td>
        <td>
            <ul>
                <li>文件过大。</li>
                <li>上传时间超过 30s。</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>13</td>
        <td>没有权限</td>
        <td>检查权限设置。</td>
    </tr>
    <tr>
        <td>20</td>
        <td>请求 URL 不支持 HTTP，请使用 HTTPS</td>
        <td>小程序已经不支持 HTTP 请求，请使用 HTTPS。</td>
    </tr>
</table>

## UploadTask
**版本要求：** 支付宝客户端 10.1.35 及以上版本，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

监听上传进度变化，取消上传任务的对象。

### 方法
| **方法** | **描述** |
| --- | --- |
| UploadTask.abort() | 中断上传任务 |
| UploadTask.onProgressUpdate(function callback) | 监听上传进度变化事件 |

### 示例代码
```javascript
const task = my.uploadFile({
  url: '请使用自己服务器地址',
  fileType: 'image',
  fileName: 'file',
  filePath: '...',
});
task.onProgressUpdate(payload => {
  const { progress, totalBytesWritten, totalBytesExpectedToWrite } = payload;
})
task.abort()
```

其中，payload 参数的含义如下：

- progress: 上传进度
- totalBytesWritten: 当前长度
- totalBytesExpectedToWrite: 总长度

# 常见问题 FAQ

## Q：小程序上传图片可以自动转成 Base64 (基于 64 个可打印字符来表示二进制数据的方法)吗？
A：小程序暂不支持图片转成 Base64。

## Q：my.uploadFile 如何获取服务器返回的错误信息呢？
A：解决方案：

1. 可以通过 success 回调中的 data 参数获取。
2. 可以在服务端增加一个日志获取接口。如果上传失败，就请求到日志获取接口获取详细的失败日志。

## Q：my.uploadFile 默认超时时间是多少？是否可以设置默认延长时间？
A：my.uploadFile 默认超时时间是 30s，目前无法设置默认延长时间。

## Q：使用 my.uploadFile 上传文件，为何报错 error:12？
A：上传失败导致报错 error:12 ，造成上传失败的可能原因有：
1. 文件过大。
2. 上传时间超过 30s。
3. 没有权限。
4. 文件未找到 / 文件不是一个正常的文件。

## Q：使用 my.uploadFile 上传图片至后台，接收的是二进制图片，再从后台发送小程序前台对应的二进制图片，小程序前台是如何解析呢？
A：上传图片是服务端通过二进制流接受图片，之后服务端只需提供对应的图片在服务器上的位置地址就可以。

## Q：调用 my.uploadfile，为何报错: error: 4，无权限调用此接口？
A：请求的 URL 没有配置白名单，建议添加 URL 的域名为白名单。

## Q：小程序是否支持上传 excel 文件？
A：目前 my.uploadFile 上传文件类型支持图片、视频、音频，暂不支持其他类型的文件。

## Q：my.uploadFile 支持多张图片同时上传吗？
A：my.uploadFile 暂不支持多张图片同时上传，一次只能上传一张图片。

