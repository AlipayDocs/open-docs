## 问题描述
my.openLocation 在没开启定位的情况下 iOS 点击没反应且 fail 返回{"error":10,errorMessage:"获取授权失败"}，Android 打开显示的是北京。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/05297c81-7dcc-4fd4-a996-f0201297dcfe.jpg#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=304&status=done&style=none&width=304)![](https://gw.alipayobjects.com/zos/sptworksff_prod/ae75c343-df21-41d8-ae11-2d423270a42b.jpg#align=left&display=inline&height=530&margin=%5Bobject%20Object%5D&originHeight=670&originWidth=310&status=done&style=none&width=245)<br /> 

## 问题原因
手机位置功能没有开启导致。 

## 解决方案
my.openLocation 打开支付宝内置地图功能依赖手机的定位服务功能，可引导用户打开手机位置功能后重试（可接入[my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide)）。<br /> <br /> 
