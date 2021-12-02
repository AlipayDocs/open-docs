小程序 IDE 支持用可视化的 Git 管理工具管理项目代码。

**说明：** 自1.0 版本开始 Git 更新为 SCM。操作步骤无变更。

## 一、初始化 Git
当项目目录中没有 Git 仓库时，可以直接初始化 Git（`git init`）。

![|257x166](https://mdn.alipayobjects.com/afts/img/A*n-hGQrXffisAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=I62OJGPrrp3yj2YG-tUhWgAAAABkMK8AAAAA#align=left&display=inline&height=166&margin=%5Bobject%20Object%5D&originHeight=166&originWidth=257&status=done&style=none&width=257)

## 二、暂存更改
可以选择一键暂存所有的更改（`git add .`），也可以 hover 到单个文件上选择暂存。

![|723x436](https://mdn.alipayobjects.com/afts/img/A*mGdLSrUSLcQAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=TZaG-O6SrghSxMCindIZZAAAAABkMK8AAAAA#align=left&display=inline&height=448&margin=%5Bobject%20Object%5D&originHeight=448&originWidth=743&status=done&style=none&width=743)

## 三、提交更改
将暂存的更改进行本地提交（`git commit -m 'xxx'`）

![|256x444](https://mdn.alipayobjects.com/afts/img/A*XSbOTobzE6oAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=1UE9pjPjLVsZZRWyzE2s1QAAAABkMK8AAAAA#align=left&display=inline&height=444&margin=%5Bobject%20Object%5D&originHeight=444&originWidth=256&status=done&style=none&width=256)

点击状态为 **M** 的文件查看 diff。

![|723x217](https://mdn.alipayobjects.com/afts/img/A*VuOfTIdbZTYAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=j8WXY5peVav6KjeolXgOogAAAABkMK8AAAAA#align=left&display=inline&height=308&margin=%5Bobject%20Object%5D&originHeight=308&originWidth=1024&status=done&style=none&width=1024)

## 四、推送到远端仓库
添加远程仓库（`git remote add origin xxxxxx`）并推送至远程仓（`git push origin`）。

![|434x861](https://mdn.alipayobjects.com/afts/img/A*o6m7RpN7rdgAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=FZmkxAPN8RvBkmNLTdKySwAAAABkMK8AAAAA#align=left&display=inline&height=861&margin=%5Bobject%20Object%5D&originHeight=861&originWidth=434&status=done&style=none&width=434)
