## 场景分析
商家 H5 被多个小程序进行内嵌，想根据 APPID 展示不同的内容，小程序没有提供 web-view 直接获取小程序 APPID 的方法，可以通过在 H5 URL 后面携带 APPID 参数然后获取该参数，或者使用小程序与 web-view 交互进行获取。 

## 处理方法

### URL 后面携带 APPID 参数

#### 小程序 axml 代码
```html
<web-view src="www.abc.com?appid=123456" />
```

#### H5 中获取 APPID
```javascript
function GetRequest(str) {
    var url = str ? str : decodeURI(location.search); //获取url中"?"符后的字串
    var theRequest = new Object();
    if (url.indexOf('?') != -1) {
        url = url.substr(1);
    }
    if (url) {
        var strs = url.split('&');
        for (var i = 0; i < strs.length; i++) {
            var srtArry = strs[i].split('=');
            var y = srtArry.shift();
            theRequest[y] = unescape(srtArry.join('='));
        }
    }
    return theRequest;
}
```

### 小程序与web-view交互方法

#### 小程序中将 APPID 发送给 H5
```javascript
this.webViewContext.postMessage({'appid': '2019*********'});
```

#### 然后 H5 中获取 APPID
```javascript
<script type="text/javascript" src="https://appx/web-view.min.js"></script>
  my.onMessage = function(e) {
    console.log(e); // {'appid': '2019*********'}
  }
```
 
