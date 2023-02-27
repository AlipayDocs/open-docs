### Q：小程序右上角的分享与收藏可以设置颜色吗？
A：这是默认的，无法设置颜色。

### Q：小程序胶囊按钮内的菜单页是否可以支持自定义修改？
![Screenshot_2022-03-01-17-01-25-138_com.eg.android.AlipayGphone.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/179989/1646125456044-f81c2702-8a8a-4daf-adeb-aa2315be7611.jpeg#align=left&display=inline&height=118&margin=%5Bobject%20Object%5D&name=Screenshot_2022-03-01-17-01-25-138_com.eg.android.AlipayGphone.jpg&originHeight=212&originWidth=1080&size=37001&status=done&style=stroke&width=600)<br />
A：目前小程序胶囊按钮内的菜单页暂不支持自定义修改。

### Q：小程序胶囊按钮可以隐藏吗？可以去除吗？
A：不可以隐藏，不可以去除。

### Q：导航栏的字体颜色可以自定义修改吗？ 
A：可以通过 [my.setNavigationBar](https://opendocs.alipay.com/mini/api/xwq8e6) 设置导航栏前景色 frontColor。<br />
**说明：** frontColor 的颜色包括返回键、标题、收藏和右上角胶囊按钮，仅支持 #ffffff 和 #000000，从基础库 [2.7.24](https://opendocs.alipay.com/mini/framework/lib) 开始支持。

### Q：如何开通添加到首页的功能？
A：支付宝客户端 10.1.95 及以上版本中符合准入规则的小程序应用默认右上角菜单中显示 **添加到首页** 功能；如未显示证明不符合准入规则的要求，准入规则暂不对外。

### Q：如何判断小程序是否收藏？
A：调用 my.getMenuButtonBoundingClientRect，通过 optionMenuStatus 字段判断。optionMenuStatus 为 Favorite 表示已收藏，UnFavorite 表示未收藏。

### Q：是否有相关API监听添加到首页功能？
A：没有提供相关API。

### Q：是否有API监听收藏/取消收藏功能？
A：没有提供相关API。

### Q：如何隐藏页面的回退按钮？
A：暂无 API 可以直接隐藏页面的回退按钮。可以先通过 my.reLaunch 进行页面跳转，在被跳转的页面里调用 my.hideBackHome 隐藏返回首页按钮。

