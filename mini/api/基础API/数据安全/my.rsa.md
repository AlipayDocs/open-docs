
# 简介
**my.rsa** 是非对称加密的 API。

加密与解密过程分别放置在客户端与服务端，私钥也放在服务端（若私钥放在客户端，容易泄露而导致安全问题）。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a4737ff1b162321a58c4ec83af8c74a1.jpeg#align=left&display=inline&height=170&margin=%5Bobject%20Object%5D&originHeight=170&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/756b932e9bcab5a239a4e31840c80e19.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 1. 小程序端加密、解密

### .js 示例代码
```javascript
// .js
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
     text: this.data.outputValue,
     // 设置公钥，需替换你自己的公钥
     key: 'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDKmi0dUSVQ04hL6GZGPMFK8+d6\n' +
     'GzulagP27qSUBYxIJfE04KT+OHVeFFb6K+8nWDea5mkmZrIgp022zZVDgdWPNM62\n' +
     '3ouBwHlsfm2ekey8PpQxfXaj8lhM9t8rJlC4FEc0s8Qp7Q5/uYrowQbT9m6t7BFK\n' +
     '3egOO2xOKzLpYSqfbQIDAQAB', 
     success: (result) => {
       this.setData({ outputValue: result.text });
     },
     fail(e) {
       my.alert({
         content: e.errorMessage || e.error,
       });
     },
   });
 },
 onDecrypt: function () {
   my.rsa({
     action: 'decrypt',
     text: this.data.inputValue,
     // 设置私钥，需替换你自己的私钥
     key: 'MIICdwIBADANBgkqhkiG9w0BAQEFAASCAmEwggJdAgEAAoGBAMqaLR1RJVDTiEvo\n' +
     'ZkY8wUrz53obO6VqA/bupJQFjEgl8TTgpP44dV4UVvor7ydYN5rmaSZmsiCnTbbN\n' +
     'lUOB1Y80zrbei4HAeWx+bZ6R7Lw+lDF9dqPyWEz23ysmULgURzSzxCntDn+5iujB\n' +
     'BtP2bq3sEUrd6A47bE4rMulhKp9tAgMBAAECgYBjsfRLPdfn6v9hou1Y2KKg+F5K\n' +
     'ZsY2AnIK+6l+sTAzfIAx7e0ir7OJZObb2eyn5rAOCB1r6RL0IH+MWaN+gZANNG9g\n' +
     'pXvRgcZzFY0oqdMZDuSJjpMTj7OEUlPyoGncBfvjAg0zdt9QGAG1at9Jr3i0Xr4X\n' +
     '6WrFhtfVlmQUY1VsoQJBAPK2Qj/ClkZNtrSDfoD0j083LcNICqFIIGkNQ+XeuTwl\n' +
     '+Gq4USTyaTOEe68MHluiciQ+QKvRAUd4E1zeZRZ02ikCQQDVscINBPTtTJt1JfAo\n' +
     'wRfTzA0Lvgig136xLLeQXREcgq1lzgkf+tGyUGYoy9BXsV0mOuYAT9ldja4jhJeq\n' +
     'cEulAkEAuSJ5KjV9dyb0RIFAz5C8d8o5KAodwaRIxJkPv5nCZbT45j6t9qbJxDg8\n' +
     'N+vghDlHI4owvl5wwVlAO8iQBy8e8QJBAJe9CVXFV0XJR/n/XnER66FxGzJjVi0f\n' +
     '185nOlFARI5CHG5VxxT2PUCo5mHBl8ctIj+rQvalvGs515VQ6YEVDCECQE3S0AU2\n' +
     'BKyFVNtTpPiTyRUWqig4EbSXwjXdr8iBBJDLsMpdWsq7DCwv/ToBoLg+cQ4Crc5/\n5DChU8P30EjOiEo=',
     success: (result) => {
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

### 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| action | String | 是 | 使用 RSA 加密还是 RSA 解密。可选值为：<br /><li> **encrypt**  为加密。</li><li> **decrypt**  为解密。</li>|
| text | String | 是 | 要处理的文本，加密为原始文本，解密为 Base64 编码格式文本。 |
| key | String | 是 | RSA 密钥。<br />加密使用公钥，解密使用私钥。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


#### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| text | String | 经过处理过后得到的文本，加密为 Base64编码文本，解密为原始文本。 |


#### fail 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误信息。 |


### 错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 10 | 参数错误 | 建议检查参数是否正确。 |
| 11 | key 错误 | 建议检查 key 是否正确。 |


## 2. 服务端加密、解密

### JAVA 加密示例代码
```java
	/**    
	 * 公钥加密     
	 * @param data     源数据     
	 * @param publicKey    公钥(BASE64编码)    
	 * @return     
	 * @throws Exception     
	 */    
	public static byte[] encrypt_PublicKey(byte[] data, String publicKey) throws Exception {  
		byte[] keyBytes = Base64.getDecoder().decode(publicKey);//使用JDK的util包下的base64实现解码
		X509EncodedKeySpec x509KeySpec = new X509EncodedKeySpec(keyBytes);       
		KeyFactory keyFactory = KeyFactory.getInstance(KEY_ALGORITHM);//使用KeyFactory工厂处理公钥
		Key publicK = keyFactory.generatePublic(x509KeySpec);        // 对数据加密        
		Cipher cipher = Cipher.getInstance(keyFactory.getAlgorithm());//使用Cipher.getInstance加密        
		cipher.init(Cipher.ENCRYPT_MODE, publicK);        
		int inputLen = data.length;        
		ByteArrayOutputStream out = new ByteArrayOutputStream();        
		int offSet = 0;        
		byte[] cache;        
		int i = 0;        // 对数据分段加密       
		while (inputLen - offSet > 0) {           
			if (inputLen - offSet > MAX_ENCRYPT_BLOCK) {                
				cache = cipher.doFinal(data, offSet, MAX_ENCRYPT_BLOCK);            
			} else {                
				cache = cipher.doFinal(data, offSet, inputLen - offSet);            
			}            
			out.write(cache, 0, cache.length);            
			i++;            
			offSet = i * MAX_ENCRYPT_BLOCK;        
		}        
		byte[] encryptedData = out.toByteArray();        
		out.close();        
		return encryptedData;    
	}
```

### JAVA 解密示例代码
```java
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

### JAVA 测试用例
```java
	/**
	* 测试用例
	*/
	//密钥需要注意的是生成密钥时选择格式：PKCS8(java适用)    
	static String publicKey="MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCe1HcHiKzaJdziPwrtmlW72gaDx+0DlhaGphVUwWkmlvWHd6mteVrr7Gs5CHaf8Y9XJbfkoHH8aEWpnhk9hYHy+JuQPYjYAgkK6IVpY69tnRrdrV42+DRPJSwDqfKrqBbYNYo9ddNSyO/uixYJPLIVwdrRTMUu19oeSSIVAvATWQIDAQAB";    
	static String privateKey="MIICcwIBADANBgkqhkiG9w0BAQEFAASCAl0wggJZAgEAAoGBAJ7UdweIrNol3OI/Cu2aVbvaBoPH7QOWFoamFVTBaSaW9Yd3qa15WuvsazkIdp/xj1clt+SgcfxoRameGT2FgfL4m5A9iNgCCQrohWljr22dGt2tXjb4NE8lLAOp8quoFtg1ij1101LI7+6LFgk8shXB2tFMxS7X2h5JIhUC8BNZAgMBAAECf2W/toEdDZ6yos5NlLKiLEorYgEKEsw5WjToMMIbJUGTc7dU8V4wYA7DZe0jftr35NvvTd8o6dzI79e5cHH5FUWKXqEldMqeTzFfPLPgyAaevxDvyBO3Z6mCkIA1ptNLfj47JTdpabc2al6qFZfJfOro+ufT/aIE1pWoLF/GARECQQD2rLyhBiRZfFf9bnUAWaG3RNE5i7Ef7t64DBZO9frZe660a8Xk8Yxzi7KMviq9aIY6LgsV1Ake2W97CcbGNtBrAkEApNWV7YwqLRM8yBO3VIflzsbtuk3RjicwjxzJzkLhR91xvWQDLx50L7kt0e1SNcuVJw3Xr0yGfPNAw4vE9FQMSwJAewyn+9tIfqscaXuUOdx8YyOdCwu4C6nox/6fkjv6KkscVzv7t70WxvzE0Jh8UYe2jYcyWG0xL4Zfqgyyb2YgiQJAKxltyl8L6B1Pl0EQfpnKDPcW0c/nKzQ0DjeIzNXP8eqFAvBTpM5hstjIkktrY4WHyl5kNwHbaHByTq8NIJWZYQJASWfwM30dJ5YAVq3ZMYkY0AeyQuJptdW4m3UJZWb2HyNU/KfPnGJ+OEO2A7XaFeRfO177RUvCqiwPAL4Y4pFvdw==";    
	//加密算法RSA    
	public static final String KEY_ALGORITHM = "RSA";//使用默认的算法     
	//RSA最大加密明文大小   
	private static final int MAX_ENCRYPT_BLOCK = 117;    
	//RSA最大解密密文大小  ; 需要注意，如果用的是2048位密钥，这里需要改为256 ; 1024密钥是 128 
	private static final int MAX_DECRYPT_BLOCK = 256/2;
	public static void main(String[] args) throws Exception {    
		test(); 
	}  
	static void test() throws Exception {       
		System.out.println("—— 公钥加密 —— 私钥解密 ——");        
		String source = "小程序服务端加解密!";//需要加密的原文
		System.out.println("加密前原文:  " + source);        
		byte[] data = source.getBytes();        
		byte[] encodedData = encrypt_PublicKey(data, publicKey);//加密        
		System.out.println("加密后内容:  " + new String(encodedData));//没有处理过的密文字符串        
		String   encodedDataStr=new String(Base64.getEncoder().encode(encodedData));//加密后问密文需要使用Base64编码然后转换成string返回前端
		System.out.println("---:base64处理:  " + encodedDataStr);        
		byte[] decodedData = decrypt_PrivateKey(encodedData, privateKey);//解密        
		String str = new String(decodedData);        
		System.out.println("解密后内容:  " + str);//小程序服务端加解密!  
	}
```
