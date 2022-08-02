# 简介
my.getServerTime 是获取当前支付宝服务器时间（从 1970 年 1 月 1 日 0 时 0 分 0 秒（UTC）距离当前时间的毫秒数）的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a3b3b0843841d6a92ad0275006cc89ab.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-server-time?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 


### .js 示例代码

```javascript
// API-DEMO page/API/get-server-time/get-server-time.js
Page({
  getServerTime(){
    my.getServerTime({
      success: (res) => {
        my.alert({
          content: res.time,
        });
      },
    });
  }
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| time | Number | 获取当前支付宝服务器时间，返回一个数值，代表从 1970 年 1 月 1 日 0 时 0 分 0 秒（UTC）距离当前时间的毫秒数。 |

# 常见问题 FAQ

## Q：my.getServerTime 获取到的时间戳怎么格式化为日期时间？
A：
- 可以使用Day.js插件进行格式化。文档链接：[https://dayjs.fenxianglu.cn/](https://dayjs.fenxianglu.cn/)
- 也可以通过如下方法进行转化：
```javascript
//app.js , 在app.js的onLaunch中添加以下方法全局绑定
Date.prototype.Format = function(fmt) {
  function getYearWeek(date) {
    var date1 = new Date(date.getFullYear(), date.getMonth(), date.getDate());
    var date2 = new Date(date.getFullYear(), 0, 1);

    //获取1月1号星期（以周一为第一天，0周一~6周日）
    var dateWeekNum = date2.getDay() - 1;
    if (dateWeekNum < 0) {
      dateWeekNum = 6;
    }
    if (dateWeekNum < 4) {
      //前移日期
      date2.setDate(date2.getDate() - dateWeekNum);
    } else {
      //后移日期
      date2.setDate(date2.getDate() + 7 - dateWeekNum);
    }
    var d = Math.round((date1.valueOf() - date2.valueOf()) / 86400000);
    if (d < 0) {
      var date3 = new Date(date1.getFullYear() - 1, 11, 31);
      return getYearWeek(date3);
    } else {
      //得到年数周数
      var year = date1.getFullYear();
      var week = Math.ceil((d + 1) / 7);
      return week;
    }
  }

  var o = {
    "M+": this.getMonth() + 1, //月份
    "D+": this.getDate(), //日
    "h+": this.getHours(), //小时
    "m+": this.getMinutes(), //分
    "s+": this.getSeconds(), //秒
    "q+": Math.floor((this.getMonth() + 3) / 3), //季度
    S: this.getMilliseconds(), //毫秒
    "W+": getYearWeek(this), //周数
  };
  if (/(Y+)/.test(fmt))
    fmt = fmt.replace(
      RegExp.$1,
      (this.getFullYear() + "").substr(4 - RegExp.$1.length)
    );
  for (var k in o)
    if (new RegExp("(" + k + ")").test(fmt)) {
      fmt = fmt.replace(
        RegExp.$1,
        RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length)
      );
    }
  return fmt;
};

//在使用的地方直接调用即可
(new Date(time)).Format("YYYY-MM-DD hh:mm:ss") //1970-01-01 00:00:00
(new Date(time)).Format("YYYY-M-D h:m:s")   // 1970-1-1 0:0:0
```
