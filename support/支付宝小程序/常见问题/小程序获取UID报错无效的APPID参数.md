
## 报错详情
在调用 [alipay.system.oauth.token](https://opendocs.alipay.com/open/02ailc) 接口时报无效的 APPID 参数。

## 报错原因
该报错是由于 APPID 值无效/错误或者 APPID 与授权 code 不一致造成的。 

## 解决方法

- 检查传入的 APPID 是否正确，是否有空格或其它符号。 
- 若是三方代商家获取 UID，检查是否有传 app_auth_token，并且 app_auth_token 与前端获取授权 code 是同一个小程序。
   - 检查小程序前端使用的是模板 APPID 还是小程序 APPID。
   - 如果前端是模板 APPID，调接口的时候如要传入模板授权给三方的 app_auth_token。
   - 如果前端是小程序 APPID，调接口的时候需要传入小程序授权给三方的 app_auth_token。
- IDE 关联的小程序与服务端接口调用的 APPID 不一致也会造成该错误，检查下 IDE 关联的小程序与服务端接口传入的 APPID 是否一致。<br />![](https://gw.alipayobjects.com/zos/workflow/workflow/202003061583497795964_311ca2feb39fb68a8aee66b734b1ea8c.png#align=left&display=inline&height=152&margin=%5Bobject%20Object%5D&originHeight=152&originWidth=438&status=done&style=none&width=438)


 <br /> 
