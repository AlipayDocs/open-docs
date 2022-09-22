# 简介

**my.getImageInfo** 是获取图片信息的 API。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1625191567539-f1858c43-e4a1-4140-a9fb-4bcaf76ce8b3.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.jpeg&originHeight=157&originWidth=127&size=19988&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1625191577132-ffa7b7bd-5fab-4f7c-9593-37ddca3bb9ba.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=177212&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 网络图片路径
my.getImageInfo({
  src: 'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
  success: res => {
    console.log(JSON.stringify(res));
  },
});
// 本地临时文件
my.chooseImage({
  success: res => {
    my.getImageInfo({
      src: res.apFilePaths[0],
      success: res => {
        console.log(JSON.stringify(res));
      },
    });
  },
});
// 包文件路径
// 包文件需要在根目录下的 mini.project.json 中配置要读取的小程序文件内容，例子如下：
{
  "include": ["image/*.png"]
}
// 配置之后才能访问到包文件，不然会报 12 错误码
my.getImageInfo({
  src: '/image/api.png', // 注意：包文件路径与当前页面路径无关。/image/api.png 也可写作 image/api.png，含义相同，都是从项目根目录算起
  success: res => {
    console.log(JSON.stringify(res));
  },
});

```

## 入参

Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| src | String | 是 | 图片路径，支持网络图片路径、[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[包文件路径](https://opendocs.alipay.com/mini/03dt4s#%E4%BB%A3%E7%A0%81%E5%8C%85%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。其中本地用户文件路径客户端 10.2.70 开始支持，之前的客户端版本存在兼容性问题。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

| **属性**    | **类型** | **描述**                       |
| ----------- | -------- | ------------------------------ |
| width       | Number   | 图片宽度，单位为 px。          |
| height      | Number   | 图片高度，单位为 px。          |
| path        | String   | 图片本地路径。                 |
| orientation | String   | 返回图片的方向。枚举值如下：</br> <li>up：默认方向，对应 [Exif](http://sylvana.net/jpegcrop/exif_orientation.html) 中的 1。或无 orientation 信息。</li><li>up-mirrored：同 up，但镜像翻转，对应 Exif 中的 2。</li><li>down：旋转180度，对应 Exif 中的 3。<li>down-mirrored：同 down，但镜像翻转，对应 Exif 中的 4。</li><li>left-mirrored：同 left，但镜像翻转，对应 Exif 中的 5。</li><li>right：顺时针旋转90度，对应 Exif 中的 6。</li><li>lright-mirrored：同 right，但镜像翻转，对应 Exif 中的 7。</li><li>left：逆时针旋转90度，对应 Exif 中的 8。</li> |
| type        | String   | 返回图片的格式。枚举值如下：</br> <li>png</li><li>jpg</li><li>gif</li><li>webp</li><li>hevc</li><li>bmp</li><li>heic</li>|


