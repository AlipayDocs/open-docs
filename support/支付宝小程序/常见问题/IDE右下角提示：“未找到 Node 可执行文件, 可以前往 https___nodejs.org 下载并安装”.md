# 说明
IDE 开发工具对 NODEJS 有一定依赖，不安装不保证功能。如 **NPM依赖管理**，不安装会导致不能下载更新 node_modules 中依赖。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/6b6b685e-640a-46a2-953c-8f865420b7ab.png#align=left&display=inline&height=334&margin=%5Bobject%20Object%5D&originHeight=334&originWidth=305&status=done&style=none&width=305)

# 报错描述
IDE 右下角提示：未找到 Node 可执行文件, 可以前往 [https://nodejs.org](https://nodejs.org) 下载并安装。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/ea438312-344a-42e9-a783-49334bc22081.png#align=left&display=inline&height=174&margin=%5Bobject%20Object%5D&originHeight=174&originWidth=405&status=done&style=none&width=405) 

# 原因分析
开发者的本地未安装 Nodejs 或者已经安装 Nodejs 但未配置环境变量，导致 IDE 工具未检测到相关配置弹出提示。 

# 处理方法

## 已安装Nodejs

### 检查环境变量配置
开发者确认本地已经安装 Nodejs，可检查环境变量是否配置，检查方式如下。

1. 电脑左下角搜索 **cmd** 打开命令行，在命令行中输入 `node -v`。不能正常返回 node 版本号则证明没有配置环境变量。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/270ee247-d742-4d3f-aed3-b93eca01c072.png#align=left&display=inline&height=34&margin=%5Bobject%20Object%5D&originHeight=34&originWidth=249&status=done&style=none&width=249)![](https://gw.alipayobjects.com/zos/sptworksff_prod/d80e1378-0fcf-42fd-9bc9-73171e5837a2.png#align=left&display=inline&height=75&margin=%5Bobject%20Object%5D&originHeight=75&originWidth=428&status=done&style=none&width=428) 
2. 鼠标悬停计算机界面 > 右键选择 **属性** >** 高级系统设置 **> **环境变量**。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/59bc4ee6-0900-4ecb-9e37-6e0bc8280b39.png#align=left&display=inline&height=221&margin=%5Bobject%20Object%5D&originHeight=221&originWidth=236&status=done&style=none&width=236)![](https://gw.alipayobjects.com/zos/sptworksff_prod/7a082361-a6d1-465f-8898-05401d3e6318.png#align=left&display=inline&height=447&margin=%5Bobject%20Object%5D&originHeight=447&originWidth=636&status=done&style=none&width=636)
3. 在环境变量/系统变量中找到 path 并编辑，在末尾添加本地 nodejs 安装的路径，如：";D:\\mywork\odeJS\\"（node 安装路径前面用英文分号 ; 隔开）。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/abfaf976-7b9c-4352-8f8d-50be19e62053.png#align=left&display=inline&height=323&margin=%5Bobject%20Object%5D&originHeight=323&originWidth=270&status=done&style=none&width=270)![](https://gw.alipayobjects.com/zos/sptworksff_prod/eea72931-ae2a-4c6c-a9a8-5f274347fac5.png#align=left&display=inline&height=140&margin=%5Bobject%20Object%5D&originHeight=140&originWidth=354&status=done&style=none&width=354)
4. 配置后重新 cmd 打开一个命令行输入：node -v 输出版本号。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/9b5268f4-1914-43b4-9a86-b993aeb591c1.png#align=left&display=inline&height=65&margin=%5Bobject%20Object%5D&originHeight=65&originWidth=279&status=done&style=none&width=279)
5. 重启 IDE。

### 直接在IDE中进行配置

1. 点击提示的 **手动设置node路径** 按钮，会弹出选择可执行文件 > 找到 nodejs 安装目录下的 node.exe。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/743b3535-7ebb-4a26-a064-3de7c6f5a5d1.png#align=left&display=inline&height=324&margin=%5Bobject%20Object%5D&originHeight=324&originWidth=295&status=done&style=none&width=295)
2. 配置后会在提示 **未找到 Npm 可执行文件**，再次点击进行配置 npm，在相同目录的：npm.cmd。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/bf85eea2-eccc-4116-b2cc-08713ba5085a.png#align=left&display=inline&height=114&margin=%5Bobject%20Object%5D&originHeight=114&originWidth=383&status=done&style=none&width=383)![](https://gw.alipayobjects.com/zos/sptworksff_prod/f05e776e-4214-4062-89c3-6bfde32e619e.png#align=left&display=inline&height=339&margin=%5Bobject%20Object%5D&originHeight=339&originWidth=220&status=done&style=none&width=220)
3. IDE 工具左下角 **设置** > **插件** > **Node Package Manager**。<br />**注意：**
   - 设置路径和“手动设置node 路径”按钮选择的路径一致。设置后如果没有生效请重新打开IDE工具。
   - Npm > Node : Path 就是 node 的路径。
   - Npm > Path：就是 npm 的路径。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/8e1d35a1-3025-4568-913a-ff0962fb473a.png#align=left&display=inline&height=161&margin=%5Bobject%20Object%5D&originHeight=161&originWidth=289&status=done&style=none&width=289)![](https://gw.alipayobjects.com/zos/sptworksff_prod/5fd89947-95b3-4e40-857d-15dfa6198ebc.png#align=left&display=inline&height=393&margin=%5Bobject%20Object%5D&originHeight=393&originWidth=530&status=done&style=none&width=530)

## 未安装 Nodejs
请根据提示前往 nodejs 官网进行下载安装 nodejs（[https://nodejs.org/](https://nodejs.org/)），之后根据 **已安装Nodejs **步骤操作完成 nodejs 配置。<br /> 
