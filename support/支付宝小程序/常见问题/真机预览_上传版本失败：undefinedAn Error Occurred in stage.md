## 问题描述
真机预览/上传版本失败：undefinedAn Error Occurred in stage<br />
案例--真机预览日志/上传版本日志报错：build & pack failed: undefinedAn Error Occurred in stage [pack]<br />
Error: 文件名或者文件夹名中不允许出现 @ 符号，images\\refresh@2x.png，请调整后重试。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/ef716e42-7e84-4119-800e-4eee6916a2ac.png#align=left&display=inline&height=255&margin=%5Bobject%20Object%5D&originHeight=255&originWidth=616&status=done&style=none&width=616)<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/95b717d4-bfd2-468c-8ba2-f7b15f7c9450.png#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=678&status=done&style=none&width=678)

## 解决方案
小程序项目中文件名或者文件夹名中不允许出现 @ 符号。根据日志提示，找到对应路径的文件，重命名该文件去除”@“符号后重新真机预览/上传版本。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/5a7a6c27-849b-42df-b768-bcb7700e7a13.png#align=left&display=inline&height=198&margin=%5Bobject%20Object%5D&originHeight=198&originWidth=684&status=done&style=none&width=684)
