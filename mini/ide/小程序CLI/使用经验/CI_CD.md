MiniU 可被加到到 CI/CD 流程中，方便判断 commit 是否影响小程序的构建。在 ci 中 添加 `miniu mini build` 用于构建小程序。示例如下：

1、在 `package.json` 中添加 ci：

```bash
{
  "devDependencies": {
    "miniu": "^1.6.8"
  },
  "ci": "miniu mini build"
}
```

2、在 yml 里添加 ci 命令：

```bash
stages:
  - test

environments:
  NODE_ENV: "test"

alinode-5:
  stage: test
  aciTags: DOCKER
  agent:
    docker:
      image: */dockerlab/node-ci:3.7.11
      resourceRequirements:
        cpu: 4
        memory: 12
        ephemeral-storage: 30
  script:
    - |
      export PATH=$PWD/node_modules/.bin:/root/.cli:$PATH
      chown -R admin:admin ./
      npm run ci
```

3、commit 后会进行小程序本地构建：

```bash
miniu mini build
没有找到本地编译工具，开始下载
download compiler [====================] 100% 0.0s
download success
17:28:50.207 - compileType: mini, adaptor: alipay, component2: true

17:28:50.211 - 已开启多进程编译

17:28:50.211 - node v12.18.1, cli 6.2.6, pid 70282

17:28:50.880 - warmup - 668ms

17:28:51.21 - Build project config : 35ms

17:28:55.96 - Compiled successfully.


17:28:55.103 - executeCompile tasks cost : 4122ms

17:28:55.177 - Check your file in /miniu_dist/dist.tar.gz (206 KB)
17:28:55.177 - Packed successfully.
```
