MiniU 提供了两种 mock 能力，一种是本地 mock，在用户项目内创建 mock 文件，我们称为本地 mock；另外一种是使用 Anymock 服务，提供在 Anymock 服务端配置数据，请求远程接口 mock 数据；**推荐用户使用本地 mock**，创建 mock 更简单，操作更直观，实时生效。以下分别介绍在开发小程序过程中使用这两种 mock 能力。

## 本地 mock
![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320073643-48354cbd-db4a-4da7-96ef-cfa8d3748fee.png#align=left&display=inline&height=1288&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1288&originWidth=1925&size=407769&status=done&style=none&width=1925)

### 添加 mock
本地 mock 面板集成在 Monitor 面板中，如上图勾选“Mock 面板”，即可打开 mock 面板。可以通过三种方式创建 mock：

1. 选中 monitor 条目，打开请求详情面板，详情面板上有“创建 mock”按钮，点击按钮创建基于当前请求返回数据的 mock；
1. 双击 monitor 条目，也会基于当前请求和返回数据创建 mock；
1. 在 Mock 面板上，有“新增”按钮，创建 mock；

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320098528-d85a70b4-bed7-4b20-9757-186a7bcc24b4.png#align=left&display=inline&height=1004&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1004&originWidth=1500&size=268833&status=done&style=none&width=1500)

创建 mock 后，在 mock 面板中即可看到新建的 mock 条目，通过编辑 mock 修改返回的 mock 数据。**注意：** 相同的请求可以创建多调 mock 数据，但只返回开启的第一条 mock。建议可以单独关闭其他相同请求的 mock 条目，如下图，三条“/api/todos”mock 数据，但只启用第二条：

![|723x500](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320128627-677e9ec1-1b7e-4782-8999-3d71dc214c37.png#align=left&display=inline&height=1794&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1794&originWidth=2598&size=578290&status=done&style=none&width=2598)

### mock 文件存放位置
本地 mock 用户创建的 mock 数据保存在用户项目内，如下图，mock 的所有数据保存在“.miniu/mock”文件夹下；mock 文件下分请求类型区分为 HTTP、JSAPI 文件夹。

![|723x710](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320147523-4aefa49d-48b2-4ae1-b50a-85edaf294d91.png#align=left&display=inline&height=752&margin=%5Bobject%20Object%5D&name=image.png&originHeight=752&originWidth=766&size=164017&status=done&style=none&width=766)

### 提交 mock 到代码仓库
为了方便开发只分享 mock 数据，可以把本地用户填写的 mock 数据提交到版本管理工具仓库中；如下在 Git 版本管理工具中，在.gitignore 文件中，添加以下配置，取消忽略.miniu 文件夹内的 mock 文件夹；
```plain
# 添加以下三行配置到.gitignore
!.miniu
.miniu/*
!.miniu/mock
```

## Anymock
Mock 面板支持使用 Anymock 能力[https://anymock.alipay.com/](https://anymock.alipay.com/)进行小程序 mock，包括[my.request](https://opendocs.alipay.com/mini/api/owycmh)及[其他小程序 API](https://opendocs.alipay.com/mini/api)。

在配置中填入 Anymock 项目 token 即可使用 Anymock 能力，Anymock 使用流程详情请参见：[https://www.yuque.com/anymock/docs/intro](https://www.yuque.com/anymock/docs/intro)。

![|723x469](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320177983-1feb404a-09c8-4732-8b66-b9525c4b0798.png#align=left&display=inline&height=1794&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1794&originWidth=2766&size=526788&status=done&style=none&width=2766)

### 配置 Token
在 Anymock 网站上，如下图，在项目复制项目 token

![|723x449](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320197001-29b4cdb7-ca6a-4327-9be5-5db79682330a.png#align=left&display=inline&height=1376&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1376&originWidth=2218&size=279603&status=done&style=none&width=2218)

配置在 Mock 面板中的 Anymock 的项目 Token 中，这样远程的 mock 数据就可以加载显示，并能新建和编辑 mock 内容。

![|723x469](https://cdn.nlark.com/yuque/0/2021/png/179989/1618320217351-ad1f5695-d238-4b8d-a537-fbd7b64ae075.png#align=left&display=inline&height=1794&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1794&originWidth=2766&size=497889&status=done&style=none&width=2766)

## 本地 mock 与 Anymock 关系
本地 mock 和 Anymock 使用不冲突，可以同时启用。也可以只是用其中一个 mock 功能。

### 优先级
如果一个请求同时在本地 mock 和 Anymock 同时命中，**优先返回本地 mock 的数据**。推荐使用本地 mock，创建 mock、修改 mock 都更简单直观。

