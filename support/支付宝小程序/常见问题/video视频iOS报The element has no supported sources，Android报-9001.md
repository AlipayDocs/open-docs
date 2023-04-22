## 报错描述
video 视频 iOS 报The element has no supported sources，Android 提示无法继续播放（-9001）。 <br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/69e4f4a0-d005-4b22-945d-678ccfe6b840.png#align=left&display=inline&height=247&margin=%5Bobject%20Object%5D&originHeight=247&originWidth=197&status=done&style=none&width=197)

## 报错原因

- 在优酷上传时视频隐私设置选择为 **完全公开**。
- 不是用开发小程序的支付宝主账号登录上传。

![](https://gw.alipayobjects.com/zos/sptworksff_prod/db93e76a-9c27-46b7-b361-5534b4053c2b.png#align=left&display=inline&height=257&margin=%5Bobject%20Object%5D&originHeight=257&originWidth=498&status=done&style=none&width=498)

## 解决方案
使用 [视频播放](https://opendocs.alipay.com/mini/api/media/video/my.createvideocontext) 提供的上传链接。<br />**注意：**

- 请使用开发小程序的支付宝主账号登录，否则视频无法上传，无法获取到视频编码及定向支付宝小程序播放的设置。
- 隐私设置选择 **仅小程序可播-只能在支付宝小程序可播放**。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/5d8634d7-31b0-4fae-91c2-f84db937a673.png#align=left&display=inline&height=358&margin=%5Bobject%20Object%5D&originHeight=358&originWidth=1371&status=done&style=none&width=1371)
- 视频发布后隐私设置为 **密码保护**。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/293778c8-3234-44fc-b0cd-49c567998128.png#align=left&display=inline&height=148&margin=%5Bobject%20Object%5D&originHeight=148&originWidth=845&status=done&style=none&width=845)
