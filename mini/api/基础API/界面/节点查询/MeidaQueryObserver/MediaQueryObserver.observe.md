开始监听页面 media query 变化情况。

## 参数

### Object descriptor
media query 描述符。描述符需包含至少一个属性。

| **属性** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
| minWidth | Number | 否 | 页面最小宽度（ px 为单位） |
| maxWidth | Number | 否 | 页面最大宽度（ px 为单位） |
| width | Number | 否 | 页面宽度（ px 为单位） |
| minHeight | Number | 否 | 页面最小高度（ px 为单位） |
| maxHeight | Number | 否 | 页面最大高度（ px 为单位） |
| height | Number | 否 | 页面高度（ px 为单位） |
| orientation | landscape &#124; portrait | 否 | 屏幕方向（ landscape 或 portrait ） |


### Function callback 
监听 media query 状态变化的回调函数。

#### 参数

##### Object res
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| matches | Boolean | 页面的当前状态是否满足所指定的 media query。 |


