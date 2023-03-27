## 报错描述
HTTP 413 错误 （ Request entity too large 请求实体太大 ）“the server responded with a status of 413 (Request Entity Too Large)”。 

## 报错原因

- Request entity too large 请求实体太大，超过 get 请求限制。
- 上传文件过大，服务器有使用 nginx 做反向代理。 

## 解决方案

- HTTP 请求方式如果是 get，建议改成 post。
- 修改 nginx 配置文件，配置客户端请求大小和缓存大小。
   - 输入命令：vim /etc/nginx/nginx.conf。
   - 在 http{} 中输入：
```
client_max_body_size 8M;(设置客户端请求体最大值) 
client_body_buffer_size 128k;(配置请求体缓存区大小) 
fastcgi_intercept_errors on;
```

   - 重启 nginx 服务：service nginx restart。

 
