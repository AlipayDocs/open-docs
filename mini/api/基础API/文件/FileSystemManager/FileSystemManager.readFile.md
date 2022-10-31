# 简介

**FileSystemManager.readFile** 用于异步读取 [本地文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6) 和 [代码包文件](https://opendocs.alipay.com/mini/03dt4s#%E4%BB%A3%E7%A0%81%E5%8C%85%E6%96%87%E4%BB%B6) 内容。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 读取小程序`代码包文件`前需在 mini.project.json 中配置可读取的小程序文件。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .json 示例代码

读取小程序`代码包文件`时，需要在 mini.project.json 中配置文件路径。下例中 `resource` 为根目录（app.json 所在目录）下的文件，* 代表任意文件名：

```json
{
  "include": ["resource/*.txt", "resource/*.json", "resource/*.mp3"]
}
```

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
fs.readFile({
  filePath: `resource/test.txt`, // 读取代码包文件。也可传入 `${my.env.USER_DATA_PATH}/hello.txt` 读取已保存的本地用户文件
  encoding: 'utf8',
  success: res => {
    console.log('文件内容: ' + res.data);
  },
  fail: res => {
    my.alert({ title: 'readFile fail', content: JSON.stringify(res) })
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 文件路径（支持[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)、[代码包文件](https://opendocs.alipay.com/mini/03dt4s#%E4%BB%A3%E7%A0%81%E5%8C%85%E6%96%87%E4%BB%B6)）。 |
| encoding | String | 否 | 指定读取文件数据时使用的编码方式。如果不传 encoding，则以 ArrayBuffer 格式读取文件的二进制内容。可选值：<ul><li>ascii</li><li>base64</li><li>hex</li><li>binary</li><li>ucs2/ucs-2/utf16le/utf-16le </li><li>utf-8/utf8</li><li>latin1</li></ul> 更多说明见下文 **encoding 参数说明** |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数将收到一个 Object 类型的参数，包含以下属性：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | string/ArrayBuffer | 文件内容。 |
| dataType | String | 输出的数据类型。如果入参不传 encoding 则为 "ArrayBuffer"，否则为 "string"。 |

### encoding 参数说明

编码为 ascii 及其扩展字符
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| ascii <img width="20px"/> | 基于拉丁字母的单子节编码方式，以 0-127 编码为 ascii 字符集 | 如：二进制（01100001），十进制（97），编码字符为 a |
| binary | 向下兼容 ascii（0x00-0x7F），从 0x00-0xFF 的单子节编码方式（和 latin1 相同） | 二进制（11111111）对应十进制为 255，十六进制为 0xff，编码字符为 ÿ |
| latin1 | 向下兼容 ascii（0x00-0x7F），从 0x00-0xFF 的单子节编码方式 | 如：二进制（10000000），十六进制为 0x80，编码字符为 latin1 第 129 个字符 |

编码为 unicode 字符
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| utf8 | 按照 utf8 的一个或多个字节的编码方式（0 ~ 127为单子节，和ascii一致），将二进制数据转换为 unicode 编码的编码方式 | 如：二进制 11100<b>110</b> 10<b>110001</b> 10<b>001001</b>，转换 unicode 后为 110110001001001 对应16进制为 6c49，\u6c49 对应字符为 “汉” |
| utf-8 | 同 utf8。 | -- |
| ucs2 | 将二进制的高位字节放后面，低位字节放前面，固定以两个字节转为 unicode 的编码方式， | 如：二进制 01100000<b>01001111</b>，16 进制 0x604f，编码转换后为<b>01001111</b>01100000，16 进制为 0x4f60，\u4f60 的字符为“你” |
| ucs-2 | 同 ucs2。 | -- |
| utf16le| 可看成是UCS-2的父集。在没有辅助平面字符（Surrogate Code Points）前，UTF-16 与 UCS-2 所指的是同一的意思 | -- |
| utf-16le <img width="20px"/>| 同 utf16le。 | -- |

编码为 base64 字符
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| base64 | 把3个字节变成4个字节，基于 64 个可打印字符来表示二进制数据的编码方式 | 如：二进制（01101001 10110111 00011101）base64 编码转换后为（00<b>011010</b> 00<b>011011</b> 00<b>011100</b> 00<b>011101</b>），对应字符为 abcd 。 | 

编码为 16 进制数字字符
|  **可选值**  | **说明** | **举例** |
| ---| --- | --- |
| hex | 将 8 位二进制数字以两个 16 进制数字编码的方式| 如：二进制（00001111），16 进制为 0x0f，编码字符为 0f |

## 错误码

| **错误码** | **描述**               |
| ---------- | ---------------------- |
| 10022      | 文件/目录不存在。      |
| 10024      | 指定的路径没有读权限。 |
| 3          | 文件读取未知错误。     |

# 常见问题
## Q：如何读取 json 文件？
A：可以取 encoding 值为 utf8 读取文件，如：
```javascript
let fs = my.getFileSystemManager();
fs.readFile({
  filePath: 'resource/test.json', // 代码包里的 json 文件
  encoding: 'utf8',
  complete: res => {
    console.log(JSON.parse(res.data));
  },
});
```
## Q：音频文件、图片文件 怎么读取？
A：通常以 base64 读取，如：
```javascript
let fs = my.getFileSystemManager();
fs.readFile({
  filePath: 'resource/test.mp3', // 代码包里的音频文件
  encoding: 'base64',
  complete: res => {
    console.log(res.data); // 获得 base64 编码的音频内容。
  },
});
```
