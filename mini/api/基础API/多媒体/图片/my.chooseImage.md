# 简介
**my.chooseImage** 是拍照或从本地相册中选择图片的 API。

## 使用限制

- 图片的路径数组在 IDE 上以 .png 为后缀，在真机预览上以 .image 为后缀。请以真机效果为准。
- 出于数据安全考虑， [IoT](https://opendocs.alipay.com/iot/multi-platform/iottenmin) 小程序禁止调用摄像头；请勿在 IoT小程序上调用此 API，否则会造成小程序异常。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1625190721184-d4b7110c-a448-4bf8-a664-7713db4e4812.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.jpeg&originHeight=157&originWidth=127&size=19820&status=done&style=stroke&width=127)

## 效果示例 
![|300X540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1625190728382-c926911d-9f2f-4386-812a-a48fc655f673.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=113733&status=done&style=stroke&width=300)

# 接口调用

## 示例代码


### .axml 示例代码
```html
<!-- API-DEMO page/API/choose-image/choose-image.axml-->
<view class="page">
  <view class="page-section-btns">
     <button type="primary" onTap="selectImage" hover-class="defaultTap">选择图片</button>
  </view>
</view>
```

### .js 示例代码
```javascript
selectImage(){
  my.chooseImage({
    sourceType: ['camera','album'],
    count: 2,
    success: (res) => {
      console.log(res);
      my.previewImage({
        current: 2,
        // res.tempFilePaths本地临时文件列表
        urls: res.tempFilePaths,
      });
    },
    fail:(res)=>{
    // 错误处理的一些自定义操作：推荐以下2种处理方式，具体处理方法可根据业务场景自定义。
    // 方式一：可以直接展示错误码
        my.showToast({type:'fail',content:`错误码：${res.error}`,duration:1000})
    // 方式二：还可以展示错误信息
    //  my.showToast({type:'fail',content:`${JSON.stringify(res)}`,duration:1000})
    },
    complete:()=>{
        // 进行一些调用结束后的操作
        console.log('调用结束，无论成功和失败都会运行')
    }
  })
}
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| count | Number | 否 | 最大可选照片数，默认为 1 张。 |
| sizeType	 | StringArray | 否 | 图片类型。<br />可选值：<ul><li>original：原图。</li><li>compressed：压缩图。</li></ul>默认二者都有。 |
| sourceType | String Array | 否 | 相册选取或者拍照，默认 ['camera','album']。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| tempFilePaths | StringArray | 图片的 [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6) 路径列表。 |
| tempFiles | Array\<Object\> | 图片的 [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6) 列表。 |

#### Array\<Object\> tempFiles 
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| path | String | [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6) 路径。 |
| size | Number | [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6) 大小，单位为 B。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 用户取消操作。 | 这是用户正常交互流程分支，不需要特殊处理。 |
| 2001 | 在申请授权时用户拒绝授权。 | 这是用户正常交互流程分支，不需要特殊处理。 |

# 常见问题 FAQ
## Q：如果系统权限未开启，接口调用报错，如何引导开启系统权限？
A：可以调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启相关系统权限。
