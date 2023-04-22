## 报错描述
IDE 推送真机预览，调试面板上出现提示“setData(...) can only update a mounted component. This usually means you called setData() on a unmounted component”。 

### 完整案例报文
setData(...) can only update a mounted component. This usually means you called setData() on a unmounted component. Please check the code for the "/components/settlement/settlement" component of "pages/home/home" page. 

## 报错原因
自定义组件没有渲染完成或者已销毁的情况下进行 setData 出现。 

## 解决方案
该报错不影响执行。建议在自定义组件 didMount 之后或者 didUnmount 之前调用 setData()。<br /> <br /> 
