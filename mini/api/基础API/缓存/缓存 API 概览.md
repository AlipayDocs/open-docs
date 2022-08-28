开启本地缓存数据，进行存储、获取和删除等控制。

单个小程序的缓存总上限为 10MB。

同步方法会阻塞当前任务，直到同步方法处理返回。异步方法不会阻塞当前任务。

| **操作** | **同步** | **异步** | **描述** |
| --- | --- | --- | --- |
| 存储 | [my.setStorageSync](/mini/api/cog0du) | [my.setStorage](/mini/api/eocm6v) | 数据存储在本地缓存中指定的 key 中的接口，会覆盖掉原来该 key 对应的数据。 |
| 读取 | [my.getStorageSync](/mini/api/ox0wna) | [my.getStorage](/mini/api/azfobl) | 获取缓存数据的接口。 |
| 清除 | [my.clearStorageSync](/mini/api/ulv85u) | [my.clearStorage](/mini/api/storage) | 清除本地数据缓存的接口。 |
| 删除 | [my.removeStorageSync](/mini/api/ytfrk4) | [my.removeStorage](/mini/api/of9hze) | 删除缓存数据的接口。 |
| 获取相关信息 | [my.getStorageInfoSync](/mini/api/uw5rdl) | [my.getStorageInfo](/mini/api/zvmanq) | 获取当前 storage 的相关信息的接口。 |
