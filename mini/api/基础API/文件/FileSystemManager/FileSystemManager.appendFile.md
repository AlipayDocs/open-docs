
# 简介
**FileSystemManager.appendFile** 用于在文件结尾追加内容。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 使用此 API 前，请先在开放平台控制台 **创建小程序**、**添加能力**，参见 [接入准备](https://opendocs.alipay.com/mini/02pk4y) 。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.appendFile({
	filePath: `${my.env.USER_DATA_PATH}/test.txt`,
	data: '{"123":456, ["abc":789, "efg":"333"]}',
	encoding: 'utf8',
	success: (res) => {
		console.log("写入成功")
	}
})
```

## 入参
| **属性** | **类型** | **必填** | **默认值** | **描述** |
| --- | --- | --- | --- | --- |
| filePath | String | 是 | - | 要追加内容的文件路径。 |
| data | String/ArrayBuffer | 是 | - | 要追加的文本或二进制数据。 |
| encoding | String | 否 | utf8 | 指定写入文件的字符编码。 |
| success | Function | 否 | - | 调用成功的回调函数。 |
| fail | Function | 否 | - | 调用失败的回调函数。 |
| complete | Function | 否 | - | 调用结束的回调函数（调用成功、失败都会执行）。 |


### encoding 合法值
| **值** | **说明** |
| --- | --- |
| ascii | - |
| base64 | - |
| hex | - |
| binary | - |
| ucs2/ucs-2/utf16le/utf-16le | - |
| utf-8/utf8 | - |
| latin1 | - |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 指定文件不存在。 |
| 10024 | 指定的路径没有写的权限。 |
| 10025 | 指定路径是一个已经存在的目录。 |



