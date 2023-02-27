
# 场景说明
如何在小程序中使用 lottie 动画组件。

# 使用限制
支持支付宝 10.1.35 版本及以上。<br />

# 接入前准备

- 让 UI 设计师使用 AE 工具制作 lottie 动画，制作完成后导出。
- UI 设计师已完成的物料资源请先在 Lottie 平台 上做一次检测，保证物料包的内容文件符合小程序规范。![](https://gw.alipayobjects.com/zos/sptworksff_prod/6f5d7aaf-190c-4c72-aca0-fbf78a305403.png#align=left&display=inline&height=694&margin=%5Bobject%20Object%5D&originHeight=694&originWidth=2124&status=done&style=none&width=2124)

**说明**：有关 Lottie 的详细信息请查看 [lottie 动画](https://opendocs.alipay.com/mini/component/lottie)文档中提供的关联资料： Lottie 官方文档 和 Lottie 官方支持能力列表。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/93b4c40e-fef9-4519-bd54-610361b2fd25.png#align=left&display=inline&height=118&margin=%5Bobject%20Object%5D&originHeight=118&originWidth=933&status=done&style=none&width=933)

## 在小程序中使用在线lottie动画

1. 将 lottie 导出后放到三方或者商家自己的在线地址中，需要保证外网能够正在下载和访问该资源。 例如：[https://gw.alipayobjects.com/os/basement_prod/1af0a9dc-110a-4a59-9084-a03d45686c8c.zip](https://gw.alipayobjects.com/os/basement_prod/1af0a9dc-110a-4a59-9084-a03d45686c8c.zip)
2. 使用一下流程在小程序中接入即可。
```html
<lottie
  a:if="{{isCanIUse}}"
  autoplay="{{item.autoplay}}" 
  id="{{item.id}}"
  djangoId="{{item.djangoId}}"
  repeatCount="{{item.repeatCount}}"
  placeholder="{{item.placeholder}}"
  onDataReady="dataReady"
  onDataLoadReady="dataLoadReady"
  onAnimationCancel="animationCancel"
  class="item"></lottie><view a:else>{{item.desc}}</view>
<view>
  <button type="primary" onTap="handlePlay">
    播放
  </button>
  <button type="primary" onTap="handleStop">
    停止播放
  </button>
  <button type="primary" onTap="handlePause">
    暂停播放
  </button></view>
```

```javascript
Page({
  data: {
    // 
    isCanIUse: my.canIUse('lottie'),
    item: {
      id : 'homeItem', // 需要保证是字符串
      desc : 'Django自动播放,低端设备降级',
      autoplay : true, // 是否自动播放
      djangoId: 'https://gw.alipayobjects.com/os/basement_prod/1af0a9dc-110a-4a59-9084-a03d45686c8c.zip',
      // 存放在服务器中lottie动画的在线地址
      placeholder:'https://gw.alipayobjects.com/mdn/rms_e345fe/afts/img/A*nu3GTaHqJ9AAAAAAAAAAAAAAARQnAQ524560995883_icon_S.png',
      // 兜底图或者降级图地址
      optimize : true, // 是否允许降级
      repeatCount : -1, // 循环次数
    } 
  },
  onLoad() {},
  // 播放
  onReady() {
    // 获取lottie实例
    this.lottieContext = my.createLottieContext('homeItem');
  },
  handlePlay() {
    this.lottieContext.play();
  },
  // 停止播放
  handleStop() {
    this.lottieContext.stop();
  },
  // 暂停播放
  handlePause() {
    this.lottieContext.pause();
  },
  // 数据下载+视图创建完成
  dataReady(event) {
    console.log(event, 'dataReady');
  },
  // 数据变化
  dataLoadReady(e) {
    console.log(e, 'dataLoadReady')
  },
  // 动画停止
  animationCancel(e) {
    console.log(e)
  }});
```

## 使用本地的lottie资源在小程序中使用
将本地项目的根目录新建一个lottie文件夹，在文件中放入lottie文件。结构参考如下。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/84fdf8be-dd06-4f16-982f-da25e0942ab6.png#align=left&display=inline&height=308&margin=%5Bobject%20Object%5D&originHeight=308&originWidth=299&status=done&style=none&width=299)<br />在小程序中使用：
```html
<lottie
  a:if="{{isCanIUse}}"
  assetsPath="{{item.assetsPath}}" 
  autoplay="{{item.autoplay}}" 
  id="{{item.id}}"
  path="{{item.path}}" 
  repeatCount="{{item.repeatCount}}"
  placeholder="{{item.placeholder}}"
  speed="{{item.speed}}"
  onDataReady="dataReady"
  onDataLoadReady="dataLoadReady"
  onAnimationCancel="animationCancel"
  ></lottie><view a:else>{{item.desc}}</view>
<view>
  <button type="primary" onTap="handlePlay">
    播放
  </button>
  <button type="primary" onTap="handleStop">
    停止播放
  </button>
  <button type="primary" onTap="handlePause">
    暂停播放
  </button></view>
```

```javascript
Page({
  data: {
    // 
    isCanIUse: my.canIUse('lottie'),
    item: {
      id : 'homeItem', // 需要保证是字符串
      desc : 'Django自动播放,低端设备降级',
      autoplay : true, // 是否自动播放
      djangoId: 'https://gw.alipayobjects.com/os/basement_prod/1af0a9dc-110a-4a59-9084-a03d45686c8c.zip',
      // 存放在服务器中lottie动画的在线地址
      placeholder:'https://gw.alipayobjects.com/mdn/rms_e345fe/afts/img/A*nu3GTaHqJ9AAAAAAAAAAAAAAARQnAQ524560995883_icon_S.png',
      // 兜底图或者降级图地址
      optimize : true, // 是否允许降级
      repeatCount : -1, // 循环次数
    } 
  },
  onLoad() {},
  // 播放
  onReady() {
    // 获取lottie实例
    this.lottieContext = my.createLottieContext('homeItem');
  },
  handlePlay() {
    this.lottieContext.play();
  },
  // 停止播放
  handleStop() {
    this.lottieContext.stop();
  },
  // 暂停播放
  handlePause() {
    this.lottieContext.pause();
  },
  // 数据下载+视图创建完成
  dataReady(event) {
    console.log(event, 'dataReady');
  },
  // 数据变化
  dataLoadReady(e) {
    console.log(e, 'dataLoadReady')
  },
  // 动画停止
  animationCancel(e) {
    console.log(e)
  }});
```
| **属性** | **类型** | **默认值** | **必填** | **描述** | **最低版本** |
| --- | --- | --- | --- | --- | --- |
| autoplay | Boolean | false | false | 是否自动播放 | - |
| path | String | 空 | false | Lottie 资源地址。包含近端（包内地址）和远端（网络）的 JSON 文件地址。<br />与 djangoId 二选一 | - |
| speed | Float | 1.0 | false | 播放速度。正数为正向播放，负数负向播放 | - |
| repeatCount | Number | 0 | false | 循环次数。<br />- 如果是负数表示无限次

- 如果是 0 表示不循环，播放一次

- 如果是 1 表示循环一次，播放两次

 | 10.1.80 |
| autoReverse | Boolean | false | false | 是否自动回播 | - |
| assetsPath | String | - | false | 资源地址。<br />"/" 表明是小程序根目录 | 10.1.50 |
| placeholder | String | - | true | 兜底图或者降级图地址。<br />1. 支持本地资源，案例：'/image/lottie/lottie2_default.png'

2. 支持 http 的 cdn 地址、近端地址。

3. 小程序场景不支持 djangoId。

 | 10.1.52 |
| djangoId | String | - | false | Lottie 在线资源。远端的 Zip 文件地址。Lottie 组件会执行 MD5 校验、解压、获取等过程，在过程中显示 placeHolder 图片。<br />与 path 二选一 | 10.1.52 |
| md5 | String | - | false | 在线资源的 md5 校验。<br />`djangoId=``https://b.zip`<br />可以使用 b.zip 加密获取 md5 值<br />`md5="77c6c86fc89ba94cc0a9271b77ae77d2"`。 | 10.1.52 |
| optimize | Boolean | false | false | 降级。降级是指如遇低端设备，Lottie 会降级展示为 placeHolder。<br />当 optimize 为 true ，并且传入了 placeHolder 时，在低端设备上只会展示 placeHolder，不展示 Lottie。<br />低端设备如下所示：<br />- iOS ：小于等于 iPhone6P

- Android：内存容量小于 3G

 | 10.1.52 |


# 实例方法
| **方法名** | **描述** | **参数** | **默认值** | **最低版本** |
| --- | --- | --- | --- | --- |
| play | 开始播放 | - | - | - |
| stop | 停止播放 | - | - | - |
| pause | 暂停 | - | - | - |
| setSpeed | 设置播放速度<br />正数为正向播放，负数负向播放 | value:numeric value | 1 | - |
| goToAndStop(value) | goto 到 value 并停在该进度。<br />示例：goToAndStop({value: 对应的值]}) | value: numeric value.进度 [0.0～1.0] | - | - |
| goToAndPlay(value) | goto 到 value 并从该进度开始播。<br />示例：goToAndPlay({value: 对应的值]}) | value: numeric value.进度 [0.0，1.0] | - | - |
| playFromMinToMaxProgress(min,max) | 从最小到最大的进度区间进行播放。<br />示例：playFromMinToMaxProgress({min:对应的值,max:对应的值}) | min：最小进度<br />max：最大进度<br />百分比<br />[0.0，1.0] | - | - |
| playFromMinToMaxFrame(min,max) | 从最小到最大的 Frame 区间进行播放。<br />示例：<br />playFromMinToMaxFrame({min:对应的值,max:对应的值}) | min：最小帧<br />max：最大帧<br />整数值 | - | - |
| downgradeToPlaceholder | 当前 Lottie 视图指定降级为展示 placeholder | - | - | 10.1.52 |


# 监听事件
当使用方法调用 pause 和 stop 时，都会先后收到 animationCancel、animationEnd 两个事件。

| **事件名** | **描述** | **参数** | **最低版本** |
| --- | --- | --- | --- |
| onDataReady | 数据下载+视图创建完成 | - | - |
| onDataFailed | 数据加载失败 | - | - |
| onDnimationStart | 动画开始 | - | - |
| onDnimationEnd | 动画彻底结束 | - | - |
| onDnimationRepeat | 动画一次重播结束 | - | 10.1.52 |
| onDnimationCancel | 动画取消 | 业务调用 Cancel 时回调 | - |
| onDataLoadReady | 参数化时，数据准备完成，等待业务传入参数化值 | - | 10.1.72 |

