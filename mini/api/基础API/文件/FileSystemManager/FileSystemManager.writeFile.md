# 简介

**FileSystemManager.writeFile** 用于对 [本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6) 异步写入。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 代码示例

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
fs.writeFile({
  filePath: `${my.env.USER_DATA_PATH}/test.txt`,
  data: 'some text or arrayBuffer',
  success: res => {
    console.log(res);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 要写入的文件路径（[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)）。 |
| data | String/ArrayBuffer | 是 | 要写入的文本或二进制数据。 |
| encoding | String | 否 | 指定写入文件二进制数据的编码方式，默认值为 utf8。<br />可选值：<ul><li>ascii</li><li>base64</li><li>hex</li><li>binary</li><li>ucs2/ucs-2/utf16le/utf-16le</li><li>utf-8/utf8</li><li>latin1</li></ul> 更多说明见下文 **encoding 参数说明**|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### encoding 参数说明

以 ascii 及其扩展编码
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| ascii <img width="20px"/> | 以 0-127 编码的 ascii 字符集编码 | 如：字符为 a，ascii 码十进制 97 ，编码为二进制 01100001|
| binary | 向下兼容 ascii（0x00-0x7F），0x00-0xFF 的单子节编码方式（和 latin1 相同） | 如：字符为 ÿ ，对应 latin1 字符集十进制为 255，编码为二进制 11111111|
| latin1 | 向下兼容 ascii（0x00-0x7F），0x00-0xFF 的单子节编码方式 | 如：字符 latin1 第 129 个字符，编码为二进制 10000000 |

以 unicode 编码
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| utf8 | 以 unicode 编码，按照 utf8 的一个或多个字节的编码方式（0 ~ 127为单子节，和ascii一致）转化为 utf8 的编码| 如：“汉”字，unicode 为 \u6c49 ，二进制为 110110001001001，转换 utf8 二进制为 11100<b>110</b> 10<b>110001</b> 10<b>001001</b> |
| utf-8 | 同 utf8。 | -- |
| ucs2 | 固定以两个字节转为 unicode ，将二进制的高位字节放后面，低位字节放前面的编码方式 | 如：“你”字，unicode 为 \u4f60 ，二进制为 <b>01001111</b>01100000，转换后二进制 01100000<b>01001111</b> |
| ucs-2 | 同 ucs2。 | -- |
| utf16le| 可看成是 UCS-2 的父集。在没有辅助平面字符（Surrogate Code Points）前，UTF-16 与 UCS-2 所指的是同一意思 | -- |
| utf-16le <img width="20px"/>| 同 utf16le。 | -- |

以 base64 编码
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| base64 | 基于 64 个可打印字符来编码转换二进制数据，把 4 个字节变成 3 个字节的编码方式 | 如：字符 abcd，base64的字符编码二进制 00<b>011010</b> 00<b>011011</b> 00<b>011100</b> 00<b>011101</b> 转换后为三个字节的二进制 01101001 10110111 00011101| 

以 16 进制数字编码
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| hex | 将两个 16 进制数字编码为 8 位二进制的方式| 如：字符为 0f，16 进制数字为 0x0f，转换二进制 00001111 |

## 错误码

| **错误码** | **描述**                                      |
| ---------- | --------------------------------------------- |
| 10024      | 指定的路径没有写的权限。                      |
| 3          | 未知错误，文件写入失败。                      |
| 10028      | 写入文件单个超过 10M 或者写入文件夹超过 50M。 |


# 常见问题
## Q：FileSystemManager.writeFile 写入成功后的文件如何查看？
A：写入成功后，文件路径为 [本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)，位于小程序沙箱中，只能通过小程序 API 访问。可以通过 [FileSystemManager.readdir](https://opendocs.alipay.com/mini/api/0226oi) 查看已保存的本地用户文件目录。
