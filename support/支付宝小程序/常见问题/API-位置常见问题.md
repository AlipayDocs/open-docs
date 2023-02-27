## 使用限制
- [my.getLocation](https://opendocs.alipay.com/mini/api/mkxuqd) 需基础库 [1.1.1](https://opendocs.alipay.com/mini/framework/lib) 或更高版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。
- 仅支持高德地图 style 与火星坐标系。

## 常见问题 

### my.getLocation是否支持境外定位
暂无境外地图数据，在中国内地（不含港澳台）以外的地区可能无法正常调用此 API。 

### my.getLocation没有返回城市名称
[my.getlocation](https://opendocs.alipay.com/mini/api/mkxuqd)需要设置type大于0才会返回city字段。 

### my.getLocation报error: 2001（用户拒绝给小程序授权）
查看 [my.getLocation报error: 2001（用户拒绝给小程序授权）](https://opendocs.alipay.com/support/01rb4a)。 

### my.getlocation位置授权过后是否能再次弹出授权弹窗
[my.getlocation](https://opendocs.alipay.com/mini/api/mkxuqd) 位置授权过后可以通过小程序右上角 **设置** >** 地理位置**，**按钮关闭 **后再次获取地理位置会再次弹出授权弹窗。 

### 小程序支持搜索中文名展示到地图上吗
可以通过 [my.chooseLocation](https://opendocs.alipay.com/mini/api/location) 使用支付宝内置地图选择地理位置，用中文地名来进行搜索地图，返回相应地理位置数据。 

### 小程序如何把地址转成经纬度
可以使用 [my.chooseLocation](https://opendocs.alipay.com/mini/api/location) 唤起地址选择器，然后输入需要转换的地址名称，点击选择后就会在 success 回调里返回该地址的经纬度信息。 

### my.chooseLocation 支持传入经纬度吗
[my.chooseLocation](https://opendocs.alipay.com/mini/api/location) 是使用支付宝内置地图选择地理位置。入参无法设置经纬度，但在回调函数中会返回 latitude 经度参数和 longitude 纬度参数。 

### 小程序支持搜索中文名展示到地图上吗
可以通过 [my.chooseLocation](https://opendocs.alipay.com/mini/api/location) 使用支付宝内置地图选择地理位置，用中文地名来进行搜索地图，返回相应地理位置数据。 

### 小程序是否能帮用户把手机上的定位开启
小程序上不支持开启用户手机定位权限；可通过 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 权限引导 API 或相关引导提示，引导用户开启定位权限。 

### 小程序里打开地图APP
目前无法直接从小程序唤起打开地图APP，可以通过 [my.openLocation](https://opendocs.alipay.com/mini/api/as9kin) 打开内置地图然后导航打开高德地图APP。 

### my.openLocation在没开启定位的情况iOS点击没反应，Android打开显示的是北京
手机位置功能没有开启导致。 my.openLocation 打开支付宝内置地图功能依赖手机的定位服务功能，可引导用户打开手机位置功能后重试，详情可查看 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide)。<br /> 
