# 简介
**my.getAvailableAudioSources** 是获取当前支持的音频输入源的 API。

更多信息，可查看 [音频播放 API 使用说明](https://opendocs.alipay.com/mini/03l3fn)。

## 使用限制

- 基础库 [1.23.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.87 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```html
<!--.axml-->
<view class="btn-area">
  <button type="primary" onTap="getAvailableAudioSources">获取当前支持的音频输入源</button>
</view>
```


```javascript
//.js  
getAvailableAudioSources() {
    my.getAvailableAudioSources(
      {
        success: function(res) {
          my.alert({ content: "success" + JSON.stringify(res)});
          console.log("getAvailableAudioSources success" + JSON.stringify(res));
        },
        fail: function(res) {
          my.alert({content : "fail"});
          console.log("getAvailableAudioSources fail" + JSON.stringify(res));
          if (res) {
            console.log("getAvailableAudioSources fail" + JSON.stringify(res));
          }
        },
        complete: function(res) {
          my.alert({ content: "complete" });
          console.log("getAvailableAudioSources complete" + JSON.stringnify(res));
          if(res) {
            console.log("getAvailableAudioSources complete" + JSON.stringnify(res));
          }
        },
      }
    )
  }
```

## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |


### success 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| audioSources | Array.<String> | 音频输入源，每一项对应一种音频输入源。 |


### audioSource 有效值
| **值** | **说明** | **支持平台** |
| --- | --- | --- |
| auto | 自动设置，默认使用手机麦克风，插上耳麦后自动切换使用耳机麦克风。 | iOS/Android/devtools |
| buildInMic | 手机麦克风。 | iOS |
| headsetMic | 耳机麦克风。 | iOS |
| mic | 麦克风（没插耳麦时是手机麦克风，插耳麦时是耳机麦克风）。 | Android |
| camcorder | 摄像头的麦克风。 | Android |

