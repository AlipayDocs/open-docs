# 简介

**my.rsa** 提供 RSA 加解密能力。RSA（非对称加密）使用的加密密钥（公钥）与解密密钥（私钥）不同，公钥是公开信息，私钥需要保密。

请在小程序运行环境使用公钥进行加密，在服务端使用私钥进行解密。私钥请保存在服务端（若私钥放在客户端，容易泄露而导致安全问题）。

可使用 [支付宝开放平台开发助手](https://opendocs.alipay.com/common/02kipl) 生成密钥对。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a4737ff1b162321a58c4ec83af8c74a1.jpeg#align=left&display=inline&height=170&margin=%5Bobject%20Object%5D&originHeight=170&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/756b932e9bcab5a239a4e31840c80e19.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

小程序端加密：

```javascript
Page({
  data: {
    inputValue: '',
    outputValue: '',
  },
  onInput: function (e) {
    this.setData({ inputValue: e.detail.value });
  },
  onEncrypt: function () {
    my.rsa({
      action: 'encrypt',
      text: this.data.inputValue,
      // 设置公钥，需替换你自己的公钥
      key:
        'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDKmi0dUSVQ04hL6GZGPMFK8+d6\n' +
        'GzulagP27qSUBYxIJfE04KT+OHVeFFb6K+8nWDea5mkmZrIgp022zZVDgdWPNM62\n' +
        '3ouBwHlsfm2ekey8PpQxfXaj8lhM9t8rJlC4FEc0s8Qp7Q5/uYrowQbT9m6t7BFK\n' +
        '3egOO2xOKzLpYSqfbQIDAQAB',
      success: result => {
        this.setData({ outputValue: result.text });
      },
      fail(e) {
        my.alert({
          content: e.errorMessage || e.error,
        });
      },
    });
  },
});
```

### .java 示例代码

#### 服务端解密

服务端解密示例代码：

```java
	/**
	* 测试用例
	*/
	// 密钥需要注意的是生成密钥时选择格式：PKCS8(java适用)
	static String privateKey="MIICcwIBADANBgkqhkiG9w0BAQEFAASCAl0wggJZAgEAAoGBAJ7UdweIrNol3OI/Cu2aVbvaBoPH7QOWFoamFVTBaSaW9Yd3qa15WuvsazkIdp/xj1clt+SgcfxoRameGT2FgfL4m5A9iNgCCQrohWljr22dGt2tXjb4NE8lLAOp8quoFtg1ij1101LI7+6LFgk8shXB2tFMxS7X2h5JIhUC8BNZAgMBAAECf2W/toEdDZ6yos5NlLKiLEorYgEKEsw5WjToMMIbJUGTc7dU8V4wYA7DZe0jftr35NvvTd8o6dzI79e5cHH5FUWKXqEldMqeTzFfPLPgyAaevxDvyBO3Z6mCkIA1ptNLfj47JTdpabc2al6qFZfJfOro+ufT/aIE1pWoLF/GARECQQD2rLyhBiRZfFf9bnUAWaG3RNE5i7Ef7t64DBZO9frZe660a8Xk8Yxzi7KMviq9aIY6LgsV1Ake2W97CcbGNtBrAkEApNWV7YwqLRM8yBO3VIflzsbtuk3RjicwjxzJzkLhR91xvWQDLx50L7kt0e1SNcuVJw3Xr0yGfPNAw4vE9FQMSwJAewyn+9tIfqscaXuUOdx8YyOdCwu4C6nox/6fkjv6KkscVzv7t70WxvzE0Jh8UYe2jYcyWG0xL4Zfqgyyb2YgiQJAKxltyl8L6B1Pl0EQfpnKDPcW0c/nKzQ0DjeIzNXP8eqFAvBTpM5hstjIkktrY4WHyl5kNwHbaHByTq8NIJWZYQJASWfwM30dJ5YAVq3ZMYkY0AeyQuJptdW4m3UJZWb2HyNU/KfPnGJ+OEO2A7XaFeRfO177RUvCqiwPAL4Y4pFvdw==";
	// 加密算法RSA
	public static final String KEY_ALGORITHM = "RSA";//使用默认的算法
	// RSA最大解密密文大小; 需要注意，如果用的是2048位密钥，这里需要改为256; 1024密钥是 128
	private static final int MAX_DECRYPT_BLOCK = 256/2;
	public static void main(String[] args) throws Exception {
		test();
	}
	public static void test() throws Exception {
		System.out.println("—— 私钥解密 ——");
		String encodedDataStr=new String(Base64.getEncoder().encode(encodedData));//加密后问密文需要使用Base64编码然后转换成string返回前端
		System.out.println("---:base64处理:  " + encodedDataStr);
		byte[] decodedData = decrypt_PrivateKey(encodedData, privateKey);//解密
		String str = new String(decodedData);
		System.out.println("解密后内容:  " + str);//小程序服务端加解密!
	}
	/**
	 *
	 * 私钥解密
	 * @param encryptedData      已加密数据
	 * @param privateKey    私钥(BASE64编码)
	 * @return
	 * @throws Exception
	 */
	public static byte[] decrypt_PrivateKey(byte[] encryptedData, String privateKey) throws Exception {
		byte[] keyBytes = Base64.getDecoder().decode(privateKey.getBytes());//使用JDK的util包下的base64实现解码
		PKCS8EncodedKeySpec pkcs8KeySpec = new PKCS8EncodedKeySpec(keyBytes);
		KeyFactory keyFactory = KeyFactory.getInstance(KEY_ALGORITHM);//使用KeyFactory工厂处理私钥
		Key privateK = keyFactory.generatePrivate(pkcs8KeySpec);
		Cipher cipher = Cipher.getInstance(keyFactory.getAlgorithm());//使用Cipher.getInstance解密
		cipher.init(Cipher.DECRYPT_MODE, privateK);
		int inputLen = encryptedData.length;
		ByteArrayOutputStream out = new ByteArrayOutputStream();
		int offSet = 0;
		byte[] cache;
		int i = 0;        // 对数据分段解密
		while (inputLen - offSet > 0) {
			if (inputLen - offSet > MAX_DECRYPT_BLOCK) {
				cache = cipher.doFinal(encryptedData, offSet, MAX_DECRYPT_BLOCK);
			} else {
				cache = cipher.doFinal(encryptedData, offSet, inputLen - offSet);
			}
			out.write(cache, 0, cache.length);
			i++;
			offSet = i * MAX_DECRYPT_BLOCK;
		}
		byte[] decryptedData = out.toByteArray();
		out.close();
		return decryptedData;
	}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| action | String | 是 | 使用 RSA 加密还是 RSA 解密。可选值为：<br /><ul><li> encrypt：加密。</li><li>decrypt：解密。</li></ul> |
| text | String | 是 | 算法输入。加密时传入明文，解密时传入密文（base64 编码）。RSA key 为 1024 位时，最多支持 117 个字节。 |
| key | String | 是 | RSA 密钥。PKCS8 格式。<br />加密使用公钥，解密使用私钥。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| text | String | 算法输出。加密时得到密文（base64 编码），解密时得到明文。 |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | String   | 错误码。   |
| errorMessage | String   | 错误信息。 |

## 错误码

| **错误码** | **错误消息** | **解决方案**            |
| ---------- | -------- | ----------------------- |
| 10         | h5RSA param(text and key) must not be empty | 传入了空 key 或空 text，请检查。  |
| 11         | Encrypt key error | 检查传入的 key 是否有效（PKCS8 格式）。 |
| 11         | Encrypt error | 如果 key 为 1024 位，请检查输入的 text 是否超过长度限制（117 字节）。 |
| 11         | Decrypt key error | 检查传入的 key 是否有效（PKCS8格式）。 |
| 11         | Decrypt error | 1，检查传入的 key 是否正确（与加密 key 匹配）；<br>2，key 为 1024 位时，请确保可能的输出 text 不超过 117 字节。 |

# Bug & Tip
* `tip` IDE 模拟器上的 my.rsa 对输入 text 的长度限制大于真机，请以真机为准。

# 常见问题 FAQ

## Q：加解密的公私钥如何生成？

A：可以使用 [支付宝开放平台开发助手](https://opendocs.alipay.com/common/02kipl) 生成密钥。
