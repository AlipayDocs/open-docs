小程序 API 调用失败时，会返回对应的异常错误码。您可以对照以下错误码信息，查找解决方法。

| **错误码** | **API** | **说明** | **解决方案** |
| --- | --- | --- | --- |
| -1 | [my.createInnerAudioContext](https://opendocs.alipay.com/mini/00bg4q)，[my.getBackgroundAudioManager](https://opendocs.alipay.com/mini/00bifu) | 未知错误。 | - |
| 1 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 请求未结束，就跳转到其他页面。 | 请求完成后再进行页面跳转。 |
| 1 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3)，[my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 未知错误。 | - |
| 2 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 网络链接已存在。 | 一个支付宝小程序在一段时间内只能保留一个 WebSocket 连接。如果当前已存在 WebSocket 连接，那么会自动关闭该连接，并重新创建一个新的 WebSocket 连接。 |
| 2 | [my.ap.navigateToAlipayPage](https://opendocs.alipay.com/mini/api/navigatetoalipaypage) | 参数错误，打开失败。 | <br />- 检查 H5 页面链接地址，修改错误的 H5 页面链接。

- 部分支付宝运营、业务页面目前暂不开放跳转。

 |
|  |  |  | 
|  |  |  | 
| 2 | [my.saveImage](https://opendocs.alipay.com/mini/006ldd) | 参数无效，没有传 URL 参数。 | 检查 URL 参数。 |
| 2 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 参数错误。 | <br />- 可能是链接过长导致，建议参数放在 data 中处理。

- 确保请求时传递的数据正常、格式正确，可以在请求前打印入参数据日志。

 |
| 2 | [my.getSavedFileInfo](https://opendocs.alipay.com/mini/api/qrx6ze) | 接口参数无效。 | 检查接口参数。 |
| 3 | [my.getRunScene](https://opendocs.alipay.com/mini/api/runscene)，[my.ap.updateAlipayClient](https://opendocs.alipay.com/mini/api/updatealipayclient) | 未知错误 | - |
| 3 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | URL 参数为空。 | 替换 URL 链接。 |
| 3 | [my.addPhoneContact](https://opendocs.alipay.com/mini/api/contact) | fail ${detail}。<br />调用失败，detail 中是详细信息。 | - |
| 4 | [my.getBatteryInfo](https://opendocs.alipay.com/mini/api/nrnziy)，[my.getBatteryInfoSync](https://opendocs.alipay.com/mini/api/vf7vn3)，[my.calculateRoute](https://opendocs.alipay.com/mini/api/calculate-route) | 无权限调用 | 暂未开放个人小程序对于 [my.getBatteryInfo](https://opendocs.alipay.com/mini/api/nrnziy)，[my.getBatteryInfoSync](https://opendocs.alipay.com/mini/api/vf7vn3)，[my.calculateRoute](https://opendocs.alipay.com/mini/api/calculate-route) 等 API 的使用权限。如需调用请在 IDE 关联企业小程序后重新进行真机调试或真机预览。 |
| 4 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 无法识别的 URL 格式。 | 替换 URL 链接。 |
| 4 | [my.getAddress](https://opendocs.alipay.com/mini/api/lymgfk) | 用户拒绝授权响应。无权调用该接口。 | 提示用户接受授权响应。 |
| 5 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | URL 必须以 ws 或者 wss 开头。 | 替换 URL 链接。 |
| 6 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 连接服务器超时。 | 稍后重试。 |
| 7 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 服务器返回的 HTTPS 证书无效。 | 小程序必须使用 HTTPS/WSS 发起网络请求。请求时系统会对服务器域名使用的 HTTPS 证书进行校验，如果校验失败，则请求不能成功发起。由于系统限制，不同平台对于证书要求的严格程度不同。为了保证小程序的兼容性，建议开发者按照最高标准进行证书配置，并使用相关工具检查现有证书，确保其符合要求。 |
|  |  |  | 
| 8 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 服务端返回协议头无效。 | 从 2019 年 5 月开始新创建的小程序，默认强制使用 HTTPS 和 WSS 协议，不再支持 HTTP 和WS 协议。 |
| 9 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | WebSocket 请求没有指定 Sec-WebSocket-Protocol 请求头。 | 请指定 Sec-WebSocket-Protocol 请求头。 |
| 10 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3)，[my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) | WebSocket 与服务器还未建立连接或连接断开，导致无法发送消息。 | 请正常连接服务器后再调用 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) 发送数据消息，可通过 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 监听事件来判断与服务器建立正确连接。<br />**注意**：通过 WebSocket 连接发送数据，需要先使用 [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) 发起连接，在 [my.onSocketOpen](https://opendocs.alipay.com/mini/api/itm5og) 回调之后再调用 [my.sendSocketMessage](https://opendocs.alipay.com/mini/api/mr91d1) 发送数据。 |
|  |  |  | 
|  |  |  | 
| 10 | [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) | 用户授权获取用户信息失败。 | **报错原因**<br />1. [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize) 唤起用户信息授权弹窗时，用户没有点击“拒绝”或“同意”，直接关闭了弹窗或按了退回键。 

1. 用户没有授权，但切换小程序到后台，从其他入口再次进入了小程序。 

**解决方案**<br />1. 为了创造更良好的支付宝小程序用户体验，不允许在小程序的首屏引导用户授权。需要在用户充分了解小程序的业务内容后再引导用户授权，建议将小程序授权环节放在业务流程中。 

1. 建议在需要获取用户信息前，增加获取权限的用途和引导提示，引导用户接受小程序授权，增加用户体验。 

1. 在授权失败时做引导处理，重新调用 [my.getAuthCode](https://opendocs.alipay.com/mini/api/openapi-authorize)  授权。

 |
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
| 10 | [my.rsa](https://opendocs.alipay.com/mini/api/data-safe) | 参数错误。 | 确保参数格式正确。 |
| 10 | [my.scan](https://opendocs.alipay.com/mini/api/scan) | 用户取消操作后返回。 | 用户正常交互流程分支，不需要特殊处理。 |
| 10 | [my.chooseAlipayContact](https://opendocs.alipay.com/mini/api/ui-contact)，[my.choosePhoneContact](https://opendocs.alipay.com/mini/api/blghgl) | 没有权限。 | 检查权限限制。 |
| 10 | [my.getSavedFileInfo](https://opendocs.alipay.com/mini/api/qrx6ze) | 无权限访问。 | 检查权限限制。 |
| 11 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 无权调用该接口。 | 确保请求域名添加了域名白名单，开发版测试可以点击  IDE 右上角 > **详情**，勾选 **忽略 httpRequest 域名合法性检查**。<br />**注意**：新版本上架，一定要添加 **服务器域名白名单**，否则会出现异常。 |
|  |  |  | 
| 11 | [my.chooseAlipayContact](https://opendocs.alipay.com/mini/api/ui-contact)，[my.choosePhoneContact](https://opendocs.alipay.com/mini/api/blghgl) | 用户取消操作（或设备未授权使用通讯录）。 | 设备授权使用通讯录。 |
| 11 | [my.chooseImage](https://opendocs.alipay.com/mini/006ld2) | 用户取消操作。 | 用户正常交互流程分支，不需要特殊处理。 |
| 11 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 确认定位相关权限已开启。 | 提示用户确认手机已给支付宝 APP 获取定位权限。 |
| 11 | [my.scan](https://opendocs.alipay.com/mini/api/scan) | 操作失败。 | 具体原因需要查看客户端协助排查。 |
| 11 | [my.rsa](https://opendocs.alipay.com/mini/api/data-safe) | key 错误。 | 确保 key 正确。 |
| 11 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 消息发送失败。 | 稍后重试。 |
| 11 | [my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc) | 文件不存在。 | 确保本地文件存在。 |
| 11 | [my.addPhoneContact](https://opendocs.alipay.com/mini/api/contact) | 用户取消操作。 | 用户正常交互流程分支，不需要特殊处理。 |
| 11 | [my.setLocatedCity](https://opendocs.alipay.com/mini/api/yw382g) | 参数类型错误。 | 确保参数类型正确。 |
| 11 | [my.datePicker](https://opendocs.alipay.com/mini/api/ui-date) | 用户取消操作。 | 用户正常交互流程分支，不需要特殊处理。 |
| 12 | [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4) | 蓝牙未打开。 | 请尝试打开蓝牙。 |
| 12 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 网络异常，请稍后再试。 | 提示用户检查当前网络。 |
| 12 | [my.connectSocket](https://opendocs.alipay.com/mini/api/vx19c3) | 无法申请更多内存来读取网络数据。 | 请检查内存。 |
| 12 | [my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc) | 上传文件失败。 | 造成上传失败的可能原因有：<br />- 文件过大。

- 上传时间超过 30 秒（s）。

- 没有权限。

 |
| 12 | [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) | 下载失败。 | 检查网络和服务器。 |
| 12 | [my.getSavedFileInfo](https://opendocs.alipay.com/mini/api/qrx6ze) | 文件不存在。 | 检查传入的文件地址。 |
| 12 | [my.setLocatedCity](https://opendocs.alipay.com/mini/api/yw382g) | 必填参数为空。 | 请确保参数 locatedCityId、locatedCityName 已填写。 |
| 12 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 网络出错。 | 确保网络环境正常，服务器稳定。 |
| 13 | [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4) | 与系统服务的链接暂时丢失。 | 请尝试重新连接。 |
| 13 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 定位失败，请稍后再试。 | 提示用户再次尝试。 |
| 13 | [my.uploadFile](https://opendocs.alipay.com/mini/api/kmq4hc)，[my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) | 没有权限。 | 检查权限设置。 |
| 13 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 超时。 | 确保网络环境正常，服务器正常响应。若请求需要时间长，可适当设置超时时间 timeout。 |
| 13 | [my.setLocatedCity](https://opendocs.alipay.com/mini/api/yw382g) | locatedCityId 不匹配。 | 请确保与 [my.chooseCity](https://opendocs.alipay.com/mini/api/ui-city) 接口的 onLocatedComplete 的 locatedCityId 保持一致。 |
| 14 | [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4) | 未授权支付宝使用蓝牙功能。 | 授权支付宝使用蓝牙功能。 |
| 14 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 业务定位超时。 | 提示用户再次尝试。 |
| 14 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 解码失败。 | 确保前后端请求和响应数据格式一致。<br />如：返回数据格式 text 与入参 dataType 值 JSON 不一致而导致接口报错，请修改后台返回数据格式为 JSON。 |
|  |  |  | 
| 15 | [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4) | 未知错误。 | - |
| 15 | [my.saveImage](https://opendocs.alipay.com/mini/006ldd) | 没有开启相册权限（**注意**：仅在 iOS 上可用）。 | 确保打开相机权限。 |
| 15 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 传参失败。 | 小程序页面传参如果做 urlencode，需要把整体参数进行编码。 |
| 16 | [my.saveImage](https://opendocs.alipay.com/mini/006ldd) | 手机相册存储空间不足（**注意**：仅在 iOS 上可用）。 | 优化存储空间内存。 |
| 17 | [my.saveImage](https://opendocs.alipay.com/mini/006ldd) | 保存图片过程中的其他错误。 | 检查诊断日志。 |
| 19 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | HTTP 错误。 | <br />- 请确认请求 URL 地址在外网能正常请求，且符合 HTTPS 协议。小程序真机测试时，是线上环境的正式请求，不能使用局域网本地请求。

- 一般如 HTTP 404、500、504 等异常错误，建议打开 **IDE 调试器 > Network** 可以查看具体的错误信息，然后根据对应 HTTP 错误码对症处理。

- 可能是 SSL 证书不正确导致的，建议更换网站 SSL 证书。

 |
|  |  |  | 
|  |  |  | 
| 20 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 请求已被停止 / 服务端限流。 | 确认请求的服务器能正常请求和响应。 |
| 20 | [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) | 请求的 URL 不支持 HTTP。 | 使用符合 HTTPS 协议的下载链接 。 |
| 23 | [my.request](https://opendocs.alipay.com/mini/api/owycmh) | 代理请求失败。 | 确保代理配置正确。 |
| 99 | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | iOS 客户端用户点击忘记密码导致快捷界面退出。 | - |
| 400 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 读 ups 信息超时。 | 检查读 ups 信息。 |
| 1002 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 播放器内部错误。 | 检查播放器内部。 |
| 1005 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 网络连接失败。 | 检查网络连接。 |
| 1006 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 数据源错误。 | 检查数据源。 |
| 1007 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 播放器准备失败。 | 检查播放器。 |
| 1008 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 网络错误。 | 检查网络。 |
| 1009 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 搜索视频出错（源出错的一种）。 | 检查视频源。 |
| 1010 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 准备超时，也可认为是网络太慢或数据源太慢导致的播放失败。 | 检查因网络或数据原因导致的超时错误。 |
| 1023 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 播放中内部错误（FFmpeg 内错误）。 | 检查 FFmpeg。 |
| 2001 | [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) | 用户拒绝给小程序授权。 | 提示用户接受小程序授权。 |
| 2004 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 播放过程中加载时间超时。 | 检查并重试。 |
| 3001 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | audio 渲染出错。 | 检查 audio 渲染。 |
| 3002 | [my.createVideoContext](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) | 硬解码错误。 | 检查硬解码。 |
| 4000 | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 订单处理失败。 | 检查订单。 |
| 4011 | [my.openDocument](https://opendocs.alipay.com/mini/api/mwpprc) | 无效的文件路径，或者传入路径没有权限访问。 | 检查传入的文件路径。 |
| 4012 | [my.openDocument](https://opendocs.alipay.com/mini/api/mwpprc) | 预览文件不存在。 | 确保文件路径对应的文件存在。 |
| 4013 | [my.openDocument](https://opendocs.alipay.com/mini/api/mwpprc) | 文件类型暂不支持。 | 目前暂仅支持 PDF 文件格式的预览。 |
| 6001 | [my.paySignCenter](https://opendocs.alipay.com/mini/006v6d)，[my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay)，[my.getAddress](https://opendocs.alipay.com/mini/api/lymgfk) | 用户中途取消。 | 请用户重新签约。 |
| 6002 | [my.paySignCenter](https://opendocs.alipay.com/mini/006v6d)，[my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 网络连接错误。 | 检查网络连接后重试。 |
| 6004 | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 处理结果未知（有可能已经成功）。 | 请通过 [alipay.trade.query](https://opendocs.alipay.com/apis/api_1/alipay.trade.query) 接口查询订单的支付状态。 |
| 7001 | [my.paySignCenter](https://opendocs.alipay.com/mini/006v6d) | 签约结果未知（有可能已经签约成功）。 | 根据外部签约号查询签约状态。 |
| 7002 | [my.paySignCenter](https://opendocs.alipay.com/mini/006v6d) | 协议签约失败。 | 稍后重试。 |
| 8000 | [my.tradePay](https://opendocs.alipay.com/mini/api/openapi-pay) | 正在处理中。支付结果未知（有可能已经支付成功）。 | 请通过 [alipay.trade.query](https://opendocs.alipay.com/apis/api_1/alipay.trade.query) 接口查询订单的支付状态。 |
| 10000 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 未初始化蓝牙适配器。 | 调用 [my.openBluetoothAdapter](https://opendocs.alipay.com/mini/api/kunuy4)，进行蓝牙适配器初始化。 |
| 10001 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 当前蓝牙适配器不可用。 | 检查当前设备对 BLE 的支持情况，并开启蓝牙功能。 |
| 10001 | [my.createInnerAudioContext](https://opendocs.alipay.com/mini/00bg4q)，[my.getBackgroundAudioManager](https://opendocs.alipay.com/mini/00bifu) | 系统错误。 | 请检查手机系统，并重试。 |
| 10002 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 没有找到指定设备。 | 检查 deviceId，并确认已开启目标蓝牙外设的广播。 |
| 10002 | [my.createInnerAudioContext](https://opendocs.alipay.com/mini/00bg4q)，[my.getBackgroundAudioManager](https://opendocs.alipay.com/mini/00bifu) | 网络错误。 | 请检查网络设置，并重试。 |
| 10003 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 连接失败。 | 检查 deviceId，并确认已开启目标蓝牙外设的广播。 |
| 10003 | [my.createInnerAudioContext](https://opendocs.alipay.com/mini/00bg4q)，[my.getBackgroundAudioManager](https://opendocs.alipay.com/mini/00bifu) | 文件错误。 | 请检查文件，并重试。 |
| 10004 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 没有找到指定服务。 | 检查 serviceId，并确认目标外设已拥有该服务。 |
| 10004 | [my.createInnerAudioContext](https://opendocs.alipay.com/mini/00bg4q)，[my.getBackgroundAudioManager](https://opendocs.alipay.com/mini/00bifu) | 格式错误。 | 请检查格式问题，并重试。 |
| 10005 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 没有找到指定特征值。 | 确保 characteristicId 正确、检查目标外设特定 service 下已具备该特征。 |
| 10006 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 当前连接已断开。 | 连接断开，重新连接。 |
| 10007 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 当前特征值不支持此操作。 | 检查特征值具备读、写、通知等功能。 |
| 10008 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 其余所有系统上报的异常。 | 其他未知错误，具体问题具体分析。 |
| 10009 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | Android 系统特有，系统版本低于 4.3 不支持 BLE。 | 提示用户该安卓系统版本不支持使用。 |
| 10010 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 没有找到指定描述符。 | 使用正确的 serviceId、characteristicId。 |
| 10011 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 设备 ID 不可用，或为空。 | 使用正确的 deviceId。 |
| 10012 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 服务 ID 不可用，或为空。 | 使用正确的 serviceId。 |
| 10013 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 特征 ID 不可用，或为空。 | 使用正确的 characteristicId。 |
| 10014 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 发送的数据为空或格式错误。 | 确保写数据或者 HEX 转化正确。 |
| 10015 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 操作超时。 | 重新操作。 |
| 10016 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 缺少参数。 | 检查调用的参数，并重新操作。 |
| 10017 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 写入特征值失败。 | 写失败。确保外设特征支持写操作，不要断开连接。 |
| 10018 | [蓝牙 API](https://opendocs.alipay.com/mini/api/ucd2lh) | 读取特征值失败。 | 读失败。确保外设特征支持读操作，不要断开连接。 |
| 11000 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 系统或设备不支持。 | 检查系统或设备版本。 |
| 11001 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 蓝牙服务不可用。 | 检查蓝牙服务。 |
| 11002 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 位置服务不可用。 | 检查位置服务权限。 |
| 11003 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 位置服务权限禁止。 | 检查位置服务权限。 |
| 11004 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 已经开始搜索。 | - |
| 11006 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | UUID 格式错误。 | 检查 UUID 格式。 |
| 11008 | [my.onBeaconServiceChange](https://opendocs.alipay.com/mini/api/rq1dl7)，[my.onBeaconUpdate](https://opendocs.alipay.com/mini/api/kvdg9y)，[my.getBeacons](https://opendocs.alipay.com/mini/api/yqleyc)，[my.startBeaconDiscovery](https://opendocs.alipay.com/mini/api/cy1g7k)，[my.stopBeaconDiscovery](https://opendocs.alipay.com/mini/api/yp5owa) | 参数错误，UUID 数组为空。 | 检查传入的参数。 |
| 20000 | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber)，[my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 系统繁忙。 | 请重试。 |
| 40001 | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber)，[my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 应用未设置默认签名类型。 | 重新保存密钥，或者设置小程序的应用网关地址。 |
| 40002 | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber)，[my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 加密异常。 | 重新设置[ AES 密钥](https://opendocs.alipay.com/open/common/104567)。 |
| 40003 | [my.getPhoneNumber](https://opendocs.alipay.com/mini/api/getphonenumber)，[my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh)，[my.getRunData](https://opendocs.alipay.com/mini/api/gxuu7v) | 无效的授权关系。 | 检查授权设置。 |
| 40006 | [my.getOpenUserInfo](https://opendocs.alipay.com/mini/api/ch8chh) | ISV 权限不足。 | 确保小程序已添加获取会员基础信息功能包。 |


## 地图、计算路径 API 错误码对照表
小程序地图 API [my.createMapContext](https://opendocs.alipay.com/mini/api/ui-map)、计算路径 API  [my.calculateRoute](https://opendocs.alipay.com/mini/api/calculate-route) 错误码请参见：

- [Andriod 地图错误码对照表](https://lbs.amap.com/api/android-sdk/guide/map-tools/error-code)<br />
- [iOS 地图错误码对照](https://lbs.amap.com/api/ios-sdk/guide/map-tool/errorcode/)<br />
