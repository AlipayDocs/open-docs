
## 说明
在开发小程序过程中，需要使用到类似 Vue 中的 store 状态管理能力，开发者可利用 mini 扩展组件中提供的 herculex 依赖库实现，文本只讲述依赖安装和使用示例，具体介绍参考依赖**README.md**文件。

## 安装依赖

### npm 安装 herculex

#### 命令行
```javascript
npm install herculex --save.
```

#### IDE npm 依赖管理安装
直接输入 herculex 运行安装。

#### ![](https://gw.alipayobjects.com/zos/sptworksff_prod/af5d938e-bc22-4c8a-8615-1cb49790a5b2.jpg#align=left&display=inline&height=245&margin=%5Bobject%20Object%5D&originHeight=245&originWidth=303&status=done&style=none&width=303)

### 使用
在项目 node_modules 目录中找到 herculex，并打开 **README.md **文件了解库的信息及其使用。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/7d3c6ec4-bcbe-4ef6-b854-e16bf9824e00.png#align=left&display=inline&height=740&margin=%5Bobject%20Object%5D&originHeight=740&originWidth=1172&status=done&style=none&width=1172)

## 使用示例
在页面目录中新建一个 store.js 文件，在文件头引入 **herculex **并 **export default new Store({)}**，如：
```javascript
import Store from 'herculex';// \btodo: 契约未知 数据处理层后面再加
export 
default new Store({  
  state: {
    userInfo: {},  
  },
  plugins: [    
    'logger',  
  ],  
  actions: {
    // 请求页面数据    
    async loadPageData({ commit }) {
      return commit('loadPageDataAction', {        
        userInfo:{name:"test"},      
      });   
    } 
  },
});
```
在 Page.js 中 import 引入 store.js，Page 使用 store.register 封装起来。
```javascript
import store from './store';
const { PAGETYPE } = constant;// 获取应用实例
const app = getApp();
Page(store.register({  
  onReady() {},  
  onShow() {}, 
  onLoad() {  
    // 初始化页面数据   
    this.dispatch('loadPageData'); 
  },
}));
```

### 运行日志
![](https://gw.alipayobjects.com/zos/sptworksff_prod/3f9830cd-3ca7-429e-84bf-d1c32d148114.png#align=left&display=inline&height=265&margin=%5Bobject%20Object%5D&originHeight=265&originWidth=1067&status=done&style=none&width=1067)<br /> <br /> 
