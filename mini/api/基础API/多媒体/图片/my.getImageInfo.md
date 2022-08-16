# 简介
**my.getImageInfo** 是获取图片信息的 API。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
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
  src:'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
  success:(res)=>{
    console.log(JSON.stringify(res))
  }
})
// 本地临时文件
my.chooseImage({
  success: (res) => {
    my.getImageInfo({
      src:res.apFilePaths[0],
      success:(res)=>{
        console.log(JSON.stringify(res))
      }
    })
  },
})
// 包文件路径
my.getImageInfo({
  src:'/image/api.png', // 注意：包文件路径以项目目录为根目录，与当前页面路径无关。/image/api.png 也可写作 image/api.png，含义相同
  success:(res)=>{
    console.log(JSON.stringify(res))
  }
})
```

## 入参
Object 类型，属性如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| src | String | 是 | 图片路径，支持网络图片路径、[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[包文件路径](https://opendocs.alipay.com/mini/03dt4s#%E4%BB%A3%E7%A0%81%E5%8C%85%E6%96%87%E4%BB%B6)，暂不支持 [本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。<br /> 注: iOS 10.2.70 开始支持[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| width | Number | 图片宽度，单位为 px。 |
| height | Number | 图片高度，单位为 px。 |
| path | String | 图片本地路径。 |
| orientation | String | 返回图片的方向，枚举值见下表。 |
| type | String | 返回图片的格式。 |

#### orientation 参数说明
| **枚举值** | **说明** |
| --- | --- |
| up | 默认。 |
| down | 180 度旋转。 |
| left | 逆时针旋转 90 度。 |
| right | 顺时针旋转 90 度。 |
| up-mirrored	 | 同 up，但水平翻转。 |
| down-mirrored	 | 同 down，但水平翻转。 |
| left-mirrored	 | 同 left，但垂直翻转。 |
| right-mirrored	 | 同 right，但垂直翻转。 |
