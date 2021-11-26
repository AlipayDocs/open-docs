
# 简介
**my.createLottieContext** 是传入 lottie id，返回一个 lottieContext 上下文的 API。lottie id 为开发者在对应 lottie 标签中自由命名的 ID 属性。

通过 lottieContext 可以操作一个 lottie 组件。更多信息，请参见 [lottie 动画](https://opendocs.alipay.com/mini/component/lottie)。

## 使用限制

- 支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
开发者在 .axml 文件中写入如下代码，命名 lottie id。lottie id 为开发者在对应 lottie 标签中自由命名的 ID 属性，例如下方代码中的 myLottie 。
```html
<!--.axml-->
<lottie
          assets-path="{{item.assetsPath}}" 
          autoplay="{{item.autoplay}}" 
          id="myLottie"
          django-id="{{item.djangoId}}"
          path="{{item.path}}" 
          repeat-count="{{item.repeatCount}}"
          placeholder="{{item.placeholder}}"
          class="item">
  </lottie>
```
开发者在 .js 文件中写入如下代码：
```javascript
//.js
var lottieContext = my.createLottieContext('myLottie');
lottieContext.play();
```

### lottieContext 方法列表
| **方法名** | **参数** | **类型** | **描述** |
| --- | --- | --- | --- |
| play | 无 | - | 开始播放。 |
| stop | 无 | - | 停止播放。 |
| pause | 无 | - | 暂停。 |
| setSpeed({value:$value}) | $value:数字<br />播放速度，默认为 1 倍速，负数代表倒序播放。 | Float | 设置播放速度。正数为正向播放，负数负向播放。<br />**默认值：** 1<br />**示例**：`setSpeed({value:1.5})` |
| goToAndStop({value:$value}) | $value:数值<br />范围为 [0.0~1.0]。 | Float | 跳转至 value 并停在该进度。<br />**示例**：goToAndStop({value: 对应的值]}) |
| goToAndPlay({value:$value}) | $value:数值<br />范围为 [0.0~1.0]。 | Float | 跳转至 value 并从该进度开始播放。<br />**示例**：goToAndPlay({value: 对应的值]}) |
| playFromMinToMaxProgress({min:$min,max:$max}) | $min:最小进度<br />$max:最大进度<br />范围为 [0.0~1.0]。 | Float | 从最小到最大的进度区间进行播放。<br />**示例**：playFromMinToMaxProgress({min:对应的值,max:对应的值}) |
| playFromMinToMaxFrame({min:$min,max:$max}) | $min:最小帧<br />$max:最大帧 | Integer | 从最小到最大的 Frame 区间进行播放。<br />**示例**：<br />playFromMinToMaxFrame({min:对应的值,max:对应的值}) |
| downgradeToPlaceholder | 无 | - | 当前 Lottie 视图指定降级为展示 placeholder。<br />**版本要求：**支付宝客户端 10.1.52 或更高版本。 |

