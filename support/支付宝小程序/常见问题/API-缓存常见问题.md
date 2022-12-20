## 使用限制
- 缓存数据本地加密存储，通过 API 读取时会自动解密返回。
- 覆盖安装支付宝（不是先删除再安装）、支付宝设置中心清除缓存、关闭小程序，这三种操作均不会导致小程序缓存失效。
- 单个 key 允许存储的最大数据大小为 200KB，单个小程序的缓存总上限为 10MB。
- 小程序缓存默认具有支付宝账号和小程序 ID 两级隔离。
- iOS 客户端支持 iTunes 备份。
- 同步方法会阻塞当前任务，直到同步方法处理返回。异步方法不会阻塞当前任务。

## 常见问题

### 小程序缓存介绍
参考[小程序缓存介绍](https://opendocs.alipay.com/support/01rb0q)。 

### 如何清除支付宝客户端缓存
参考[如何清除支付宝客户端缓存](https://opendocs.alipay.com/support/01rb6x)。 

### 小程序里如何删除缓存数据**
参考[小程序里如何删除缓存数据](https://opendocs.alipay.com/support/01rb94)。 

### 小程序是否支持cookie
小程序针对服务端回设的 cookie 不会禁用掉，会设置到小程序进程中，下次小程序进行请求，会自动将已有的 cookie 带入到服务端请求中。<br />前端获取不到 cookie，也不会对 cookie 做任何操作。小程序不建议使用 cookie，推荐使用小程序 [缓存](https://opendocs.alipay.com/mini/api/qm3ggk)。 

### 小程序与H5本地存储对比

- H5本地存储，这里特指 localStorageh5 的本地存储在做数据存储的时候，只能存储 String 类型的值。当存储的值需要为 Object 类型时，需要在读和写的时候都做一步特殊处理。<br />小程序本地存储支持 String 和 Object 两种数据类型的存储。
- 数据存储的限制同一个支付宝用户，同一个小程序缓存总上限为 10MB，如果数据超过 10MB，所以切勿将太多的数据存在本地，在某些数据不再使用的时候及时清除。当存储数据大于 10MB 时，存储将会失败。
- 由于数据存储存储在本地，当更换设备登录时，存储于之前设备上的数据将不再存在。因此，建议将比较重要的数据存储在服务器，通过请求的方式再次获取数据。 

### 插件和小程序的存储是否互通
插件和小程序的缓存存储不通用，独立隔离。 

### 如何在服务端获取到小程序缓存
小程序通过 my.getStorage 获取到的缓存，可以调用 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 方法把缓存的数据当做参数的方式进行传递到服务端获取。 

### 能一次性取多个缓存的值吗
将数据存储在本地缓存中指定的 key 中的异步接口 [my.getStorage](https://opendocs.alipay.com/mini/api/eocm6v) 不支持传入多个 key 值来获取多个缓存，建议用 for 循环调用 my.getStorage 实现。 

### 缓存API存储的缓存什么时候会被清除
使用了缓存 API 必须使用清除 API，否则缓存不会被清除掉（先删除再安装支付宝可清除）。 

### 小程序中存入的缓存数据多了一对双引号
在调用存入缓存的 API 时使用了 JSON.stringify 导致。 

### 获取缓存数据的同步接口my.getStorageSync获取不到数据。

- 排查是否清除了本地的缓存。
- 排查数据是否存储进入。
- 检查支付宝客户端版本是否过低，建议升级到最新支付宝客户端。 

### 删除本地小程序会使storage清空么
删除本地小程序不会使 storage 清空。小程序缓存可以使用清除本地数据缓存的异步/同步接口进行删除，参考 [缓存 API 概览](https://opendocs.alipay.com/mini/api/qm3ggk)。 

### 小程序缓存到达10MB后会清除之前的数据再写入还是写入报错
当超过 10MB 会无法继续写入，并提示：error 12，数据库存储达到上限时。可以通过删除缓存数据的异步接口 [my.removeStorage](https://opendocs.alipay.com/mini/api/of9hze) 移除不必要的存储。 

### getStorageSync可以设置超时时间么
[my.getStorageSync](https://opendocs.alipay.com/mini/api/ox0wna) 缓存数据本地加密存储，该方法为同步方法不能设置超时时间。 

### 支付宝预授权是否支持设置Cookie
支付宝预授权业务不涉及 cookie 存储问题，预授权数据不建议存储在 cookie 中。 

### 如何更新小程序缓存
可以使用 [my.setStorageSync](https://opendocs.alipay.com/mini/api/cog0du)/[my.setStorage](https://opendocs.alipay.com/mini/api/eocm6v) 存入相同的 key 即可覆盖之前的缓存。<br /> 
