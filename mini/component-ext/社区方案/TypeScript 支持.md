社区和官方都提供了小程序的类型定义。

## mini-types

### 安装

```shell
npm install mini-types --save
```

### 使用

在 `tsconfig.json` 文件中指定 `types` 配置。

```json
{
   "compilerOptions": {
      "types" : ["mini-types"]
   }
}
```

## [推荐] @mini-types/alipay

由官方维护的支付宝小程序类型定义。

### 安装

```shell
npm install @mini-types/alipay --save
```

### 使用

在 `tsconfig.json` 文件中指定 `types` 配置。

```json
{
   "compilerOptions": {
      "types" : ["@mini-types/alipay"]
   }
}
```

此外，也可以使用 [`typeRoots`](https://www.typescriptlang.org/tsconfig#typeRoots) 来配置：

```json
{
   "compilerOptions": {
      "typeRoots" : ["./node_modules/@mini-types"]
   }
}
```

## 反馈

如果您发现了任何问题，欢迎给我们提 [issue](https://github.com/ant-mini-program/mini-types/issues)。
