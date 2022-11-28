
## 说明
组件可以通过 this.$page 拿到小程序页面实例，然后将组件实例挂载到小程序页面实例上进行相互调用。

## 步骤一 将父组件，子组件分别挂载到所属页面实例上

### 父组件- /component/fu/fu.js
```javascript
  didMount() {    this.$page.fu = this; // 通过此操作可以将组件实例挂载到所属页面实例上  },
```

### 子组件- /component/zi/zi.js
```javascript
 didMount() {    this.$page.zi = this; // 通过此操作可以将组件实例挂载到所属页面实例上  },
```

## 步骤二 通过页面实例实现相互调用

### 小程序页面调用父组件，子组件方法
```javascript
//调用组件内method方法  
  this.zi.zimethod()this.fu.fumethod()//更改组件内data值this.fu.setData({      
      test:'123'   
    }) this.zi.setData({
    test:'123'  
    })
```

### 父组件调用子组件内方法
```javascript
//调用子组件method方法
this.$page.zi.zimethod()////更改子组件内data值 
this.$page.zi.setData({
      test:'123'    
    })
```

### 子组件调用父组件内方法 
```javascript
//调用父组件method方法
this.$page.fu.zimethod()////更改父组件内data值 
this.$page.fu.setData({
      test:'123'  
    })
```

