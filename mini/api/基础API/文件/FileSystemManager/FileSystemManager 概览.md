# 简介
**FileSystemManager** 文件管理器，可通过 [my.getFileSystemManager](https://opendocs.alipay.com/mini/0226oc) 获取。如何接入以及更多介绍信息，可查看 [文件管理器](https://opendocs.alipay.com/mini/introduce/022rw2)。

## 使用限制
- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 使用 **FileSystemManager** 前，请先在开放平台控制台 **创建小程序**、**添加能力**，可查看 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 概览
| **名称** | **功能说明** |
| --- | --- |
| [FileSystemManager.access](https://opendocs.alipay.com/mini/api/0226oe) | 判断文件/目录是否存在。 |
| [FileSystemManager.accessSync](https://opendocs.alipay.com/mini/api/025027) | [FileSystemManager.access](https://opendocs.alipay.com/mini/api/0226oe) 的同步版本。 |
| [FileSystemManager.appendFile](https://opendocs.alipay.com/mini/api/0228qi) | 用于在文件结尾追加内容。 |
| [FileSystemManager.appendFileSync](https://opendocs.alipay.com/mini/api/025028) | [FileSystemManager.appendFile](https://opendocs.alipay.com/mini/api/0228qi) 的同步版本。 |
| [FileSystemManager.copyFile](https://opendocs.alipay.com/mini/api/0226of) | 复制文件（支持复制临时文件、缓存文件到沙箱文件）。 |
| [FileSystemManager.copyFileSync](https://opendocs.alipay.com/mini/api/024ytt) | [FileSystemManager.copyFile](https://opendocs.alipay.com/mini/api/0226of) 的同步版本。 |
| [FileSystemManager.getFileInfo](https://opendocs.alipay.com/mini/api/0226og) | 获取该小程序下的本地临时文件或本地缓存文件信息。 |
| [FileSystemManager.getSavedFileList](https://opendocs.alipay.com/mini/api/0228qj) | 获取该小程序下已保存的本地缓存文件列表。 |
| [FileSystemManager.mkdir](https://opendocs.alipay.com/mini/api/0226oh) | 创建目录。 |
| [FileSystemManager.mkdirSync](https://opendocs.alipay.com/mini/api/024ytu) | [FileSystemManager.mkdir](https://opendocs.alipay.com/mini/api/0226oh) 的同步版本。 |
| [FileSystemManager.readdir](https://opendocs.alipay.com/mini/api/0226oi) | 读取目录内文件列表。 |
| [FileSystemManager.readdirSync](https://opendocs.alipay.com/mini/api/024ytv) | [FileSystemManager.readdir](https://opendocs.alipay.com/mini/api/0226oi) 的同步版本。 |
| [FileSystemManager.readFile](https://opendocs.alipay.com/mini/api/0226oj) | 用于读取本地文件内容。 |
| [FileSystemManager.readFileSync](https://opendocs.alipay.com/mini/api/025029) | [FileSystemManager.readFile](https://opendocs.alipay.com/mini/api/0226oj) 的同步版本。 |
| [FileSystemManager.removeSavedFile](https://opendocs.alipay.com/mini/api/0229pv) | 删除该小程序下已保存的本地缓存文件。 |
| [FileSystemManager.rename](https://opendocs.alipay.com/mini/api/0229pw) | 用于重命名文件，可以把文件从 oldPath 移动到 newPath。 |
| [FileSystemManager.renameSync](https://opendocs.alipay.com/mini/api/024ytw) | [FileSystemManager.rename](https://opendocs.alipay.com/mini/api/0229pw) 的同步版本。 |
| [FileSystemManager.rmdir](https://opendocs.alipay.com/mini/api/0229px) | 用于删除目录。 |
| [FileSystemManager.rmdirSync](https://opendocs.alipay.com/mini/api/024ytx) | [FileSystemManager.rmdir](https://opendocs.alipay.com/mini/api/0229px) 的同步版本。 |
| [FileSystemManager.saveFile](https://opendocs.alipay.com/mini/api/022b6n) | 用于保存临时文件到本地。此接口会移动临时文件，因此调用成功后，tempFilePath 将不可用。 |
| [FileSystemManager.saveFileSync](https://opendocs.alipay.com/mini/api/02502a) | [FileSystemManager.saveFile](https://opendocs.alipay.com/mini/api/022b6n) 的同步版本。 |
| [FileSystemManager.stat](https://opendocs.alipay.com/mini/api/022b6o) | 用于获取文件 Stats 对象。 |
| [FileSystemManager.statSync](https://opendocs.alipay.com/mini/api/024whe) | 同步获取文件的状态信息。 |
| [FileSystemManager.unlink](https://opendocs.alipay.com/mini/api/022b6p) | 用于删除文件。 |
| [FileSystemManager.unlinkSync](https://opendocs.alipay.com/mini/api/024whc) | [FileSystemManager.unlink](https://opendocs.alipay.com/mini/api/022b6p) 的同步版本。 |
| [FileSystemManager.unzip](https://opendocs.alipay.com/mini/api/0229q3) | 用于解压文件。 |
| [FileSystemManager.writeFile](https://opendocs.alipay.com/mini/api/022b6s) | 用于写文件。 |
| [FileSystemManager.writeFileSync](https://opendocs.alipay.com/mini/api/024whd) | [FileSystemManager.writeFile](https://opendocs.alipay.com/mini/api/022b6s) 的同步版本。 |
