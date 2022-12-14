# 简介
my.ap.openURL（Beta）是用于打开 URL 的 API。URL 为第三方 H5 页面或者支付宝官方给出的链接（以 https:// 或者 alipays:// 开头），且必须在 URL 白名单内。

URL 白名单包含两部分：
- 默认的全局白名单，包含以 `https://render.alipay.com/p/` 开头的所有 URL。所有小程序都可直接通过 my.ap.openURL 打开此类 URL。
- 开放范围内的小程序，可通过开放平台控制台 [开发设置](https://open.alipay.com/develop/mini/sub/dev-setting) > **openURL 配置** 自助申请添加其 URL 白名单。申请通过审核以后约 10 分钟生效。  

目标 URL 可能存在短链接/多次跳转等复杂情况，**推荐优先使用[跳转辅助工具](https://apitools.alipay.com/tools/open-url) 进行检测并生成代码**。

## 开放范围
此 API 对应 URL 的白名单申请，暂只开放以下国内经营类目的小程序：
- [城市服务](https://opendocs.alipay.com/b/03al2m#%E5%9F%8E%E5%B8%82%E6%9C%8D%E5%8A%A1) 
- [交通出行](https://opendocs.alipay.com/b/03al2m#%E4%BA%A4%E9%80%9A%E5%87%BA%E8%A1%8C) 
- [医疗健康](https://opendocs.alipay.com/b/03al2m#%E5%8C%BB%E7%96%97%E5%81%A5%E5%BA%B7) 
- [汽车](https://opendocs.alipay.com/b/03al2m#%E6%B1%BD%E8%BD%A6) 
- [电信通讯](https://opendocs.alipay.com/b/03al2m#%E7%94%B5%E4%BF%A1%E9%80%9A%E8%AE%AF) 
- [缴费还款](https://opendocs.alipay.com/b/03al2m#%E7%BC%B4%E8%B4%B9%E8%BF%98%E6%AC%BE) 

## 使用限制
- 此 API 仅支持支付宝企业小程序使用。
- 基础库 2.7.20 或更高版本。使用 1.x 版本的小程序请先 [升级基础库](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)。

# 接口调用

**推荐使用跳转辅助工具检测链接并生成代码：[https://apitools.alipay.com/tools/open-url](https://apitools.alipay.com/tools/open-url)**。

## 示例代码
```javascript
// 打开支付宝官方运营活动页面
// 请将 url 替换为有效的页面地址
my.ap.openURL({
  url: 'https://render.alipay.com/p/404'
});

// 打开第三方页面
my.ap.openURL({
  url: 'https://please.replace.me/page', // 请将 url 替换为后台加白过的跳转地址
  success: (res) => console.log('openURL success'),
  fail: (err) => my.alert({ title: 'openURL fail: ' + JSON.stringify(err) }),
});

// 跳转支付宝客户端内指定模块
my.ap.openURL({
  url: 'alipays://platformapi/startapp?appId=00000000', // 请将 url 替换为后台加白过的跳转地址
  success: (res) => console.log('openURL success'),
  fail: (err) => my.alert({ title: 'openURL fail: ' + JSON.stringify(err) }),
})
```

## 入参
Object 类型，属性如下：
| **属性** | **类型** | **可选** |     **说明**                    |
| ---------- | -------- | --------------------- | --------------------- |
| url      | String   |     否   | 目标地址，必须以 https:// 或 alipays:// 开头。 |

## 错误码
fail 回调的参数为 Object，其 error 属性为错误码，errorMessage 为错误消息。
| **错误码（error）** | **错误消息（errorMessage）** | **解决方案** |  
| ----------          | --------                      | --------------------- |
| 2                   | 参数无效                      | 检查传入的 URL 格式，必须以 https:// 或 alipays:// 开头。  | 
| 6002                | 跳转目标不在白名单            | 确保传入的 URL 以放到 `https://render.alipay.com/p/` 开头，或者在开放平台控制台已添加到 openURL 白名单。   |

