## 错误码
1 

## 报错描述
HTTP 请求，my.request 网络请求报 error: 1（请求没有结束，就跳转到了另一个页面）。 

## 涉及接口
[my.request](https://opendocs.alipay.com/mini/api/owycmh)

## 报错原因
在当前页面进行 my.request 网络请求，请求没有结束就进行页面跳转到新页面导致请求失败。 

## 解决方案

- 建议请求完成后再进行页面跳转，可以在页面加上对应的加载提示（如：[my.showLoading](https://opendocs.alipay.com/mini/api/bm69kb)）。
- 如需强行做页面跳转操作，建议加上 [RequestTask.abort()](https://opendocs.alipay.com/mini/api/owycmh#%E8%BF%94%E5%9B%9E%E5%80%BC%20RequestTask) 中断请求任务。

示例代码：
```javascript
// 返回 RequestTask，可以调用 abort 方法取消请求
const task = my.request({url: 'https://httpbin.org/post'})task.abort();
```
 <br /> 
