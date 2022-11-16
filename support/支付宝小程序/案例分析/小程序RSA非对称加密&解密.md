# 背景说明
[my.rsa](https://opendocs.alipay.com/mini/api/data-safe) 用于信息加密，防止信息被篡改。加密与解密过程分别放置在客户端与服务端，且私钥放在服务端，如果私钥放在客户端易泄露将导致安全问题。<br />**注意**：

- 此功能不同于服务端调用接口的签名和验签，仅用于小程序数据传输时的加密。
- 请不要使用小程序应用上配置的密钥来做加/解密数据，必须重新使用工具生成密钥，否则会有安全隐患。<br />

## 注意事项

- my.rsa 支持密钥 1024 或者 2048 进行加密解密。可以用代码（如 Java）自行实现或者使用 [支付宝开放平台密钥工具](https://opendocs.alipay.com/common/02kipk) 生成密钥。
- my.rsa 小程序采用的是公钥加密、私钥解密的方式。
- text 加密解密的文本是 String 类型。
- 使用参数 action 来选择 rsa 加密或 rsa 解密。<br />**值：**
   - encrypy(加密)
   - decrypt(解密)
- 参数 key 可填写 rsa 密钥。<br />**注意：** 加密使用公钥，解密使用私钥。

# 示例代码
小程序前端加密解密示例。<br />**注意**：示例中使用的密钥，只是为了便于测试，集成时请务必自行生成一对密钥。

## 小程序加密
```
my.rsa({
        action: 'encrypt',        
        text: '我觉得小程序加密很简单，你觉得呢', //示例中使用的密钥，只是为了便于测试，集成时请务必自行生成一对密钥。        
        key: 'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCe1HcHiKzaJdziPwrtm'+             
        'lW72gaDx+0DlhaGphVUwWkmlvWHd6mteVrr7Gs5CHaf8Y9XJbfkoHH8aEW'+             
        'pnhk9hYHy+JuQPYjYAgkK6IVpY69tnRrdrV42+DRPJSwDqfKrqBbYNYo9d'+             
        'dNSyO/uixYJPLIVwdrRTMUu19oeSSIVAvATWQIDAQAB',
        success: (result) => {
          console.log(result.text)//打印加密后的密文（密文是通过base64编码后的字符串）:E//A3WDW2GZI7iasTHFBpssIRuAwvYMDwfQiv64lj10nrEnNVf81ZkLU7Ek42a9Mr+JzhGG6QPr5oANQmm5qVY+0mYuMXc0bSF5Q2rshUZkfYPRql5dfJWMz9/eXTJEA0Un242JGQUxCI0ae0Eh3C8chbEVM06gt/KeMWY/+fe0=        
        },
        fail(e) {          
          my.alert({
            content: e.errorMessage || e.error,          
          });
        },
      });
```

## 小程序解密
```
//示例中使用的密钥，只是为了便于测试，集成时请务必自行生成一对密钥。
my.rsa({        
        action: 'decrypt',        
        text: 'E//A3WDW2GZI7iasTHFBpssIRuAwvYMDwfQiv64lj10nrEnNVf81ZkLU7Ek42a9Mr+JzhGG6QPr5oANQmm5qVY+0mYuMXc0bSF5Q2rshUZkfYPRql5dfJWMz9/eXTJEA0Un242JGQUxCI0ae0Eh3C8chbEVM06gt/KeMWY/+fe0=',
        key: 'MIICcwIBADANBgkqhkiG9w0BAQEFAASCAl0wggJZAgEAAoGBAJ7UdweIrNol3OI/Cu2aVbva'+ 
        'BoPH7QOWFoamFVTBaSaW9Yd3qa15WuvsazkIdp/xj1clt+SgcfxoRameGT2FgfL4m5A9iNgC'+    
        'CQrohWljr22dGt2tXjb4NE8lLAOp8quoFtg1ij1101LI7+6LFgk8shXB2tFMxS7X2h5JIhUC'+    
        '8BNZAgMBAAECf2W/toEdDZ6yos5NlLKiLEorYgEKEsw5WjToMMIbJUGTc7dU8V4wYA7DZe0j'+    
        'ftr35NvvTd8o6dzI79e5cHH5FUWKXqEldMqeTzFfPLPgyAaevxDvyBO3Z6mCkIA1ptNLfj47'+      
        'JTdpabc2al6qFZfJfOro+ufT/aIE1pWoLF/GARECQQD2rLyhBiRZfFf9bnUAWaG3RNE5i7Ef'+          
        '7t64DBZO9frZe660a8Xk8Yxzi7KMviq9aIY6LgsV1Ake2W97CcbGNtBrAkEApNWV7YwqLRM8'+           
        'yBO3VIflzsbtuk3RjicwjxzJzkLhR91xvWQDLx50L7kt0e1SNcuVJw3Xr0yGfPNAw4vE9FQM'+        
        'SwJAewyn+9tIfqscaXuUOdx8YyOdCwu4C6nox/6fkjv6KkscVzv7t70WxvzE0Jh8UYe2jYcy'+         
        'WG0xL4Zfqgyyb2YgiQJAKxltyl8L6B1Pl0EQfpnKDPcW0c/nKzQ0DjeIzNXP8eqFAvBTpM5h'+         
        'stjIkktrY4WHyl5kNwHbaHByTq8NIJWZYQJASWfwM30dJ5YAVq3ZMYkY0AeyQuJptdW4m3UJ'+         
        'ZWb2HyNU/KfPnGJ+OEO2A7XaFeRfO177RUvCqiwPAL4Y4pFvdw==',//使用的是1024位密钥的私钥解密        
        success: (result) => {          
          console.log(result.text);//打印解密后的内容：我觉得小程序加密很简单，你觉得呢
        },        
        fail(e) {          
          my.alert({
           content: e.errorMessage || e.error,
        });        
       },
      });
```

## 服务器端的加密/解密
以下以 Java 为例。

### 公钥加密
```
 /**
     * 公钥加密
     * @param data
     *            源数据
     * @param publicKey
     *            公钥(BASE64编码)
     * @return
     * @throws Exception
     */
    public static byte[] encrypt_PublicKey(byte[] data, String publicKey) throws Exception {
        byte[] keyBytes = Base64.getDecoder().decode(publicKey);//使用JDK的util包下的base64实现解码
        X509EncodedKeySpec x509KeySpec = new X509EncodedKeySpec(keyBytes);
        KeyFactory keyFactory = KeyFactory.getInstance(KEY_ALGORITHM);//使用KeyFactory工厂处理公钥
        Key publicK = keyFactory.generatePublic(x509KeySpec);
        // 对数据加密
        Cipher cipher = Cipher.getInstance(keyFactory.getAlgorithm());//使用Cipher.getInstance加密
        cipher.init(Cipher.ENCRYPT_MODE, publicK);
        int inputLen = data.length;
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        int offSet = 0;
        byte[] cache;
        int i = 0;
        // 对数据分段加密
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

### 私钥解密
```
/**
     * <P>
     * 私钥解密
     * @param encryptedData
     *            已加密数据
     * @param privateKey
     *            私钥(BASE64编码)
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
        int i = 0;
        // 对数据分段解密
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

### 测试
```
package HttpServlet;
 
import java.io.ByteArrayOutputStream;
import java.security.Key;
import java.security.KeyFactory;
import java.security.spec.PKCS8EncodedKeySpec;
import java.security.spec.X509EncodedKeySpec;
import java.util.Base64;
 
import javax.crypto.Cipher;
 
public class luntan {
//密钥需要注意的是生成密钥时选择格式：PKCS8(Java适用)
    static String publicKey="MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCe1HcHiKzaJdziPwrtmlW72gaDx+0DlhaGphVUwWkmlvWHd6mteVrr7Gs5CHaf8Y9XJbfkoHH8aEWpnhk9hYHy+JuQPYjYAgkK6IVpY69tnRrdrV42+DRPJSwDqfKrqBbYNYo9ddNSyO/uixYJPLIVwdrRTMUu19oeSSIVAvATWQIDAQAB";
    static String privateKey="MIICcwIBADANBgkqhkiG9w0BAQEFAASCAl0wggJZAgEAAoGBAJ7UdweIrNol3OI/Cu2aVbvaBoPH7QOWFoamFVTBaSaW9Yd3qa15WuvsazkIdp/xj1clt+SgcfxoRameGT2FgfL4m5A9iNgCCQrohWljr22dGt2tXjb4NE8lLAOp8quoFtg1ij1101LI7+6LFgk8shXB2tFMxS7X2h5JIhUC8BNZAgMBAAECf2W/toEdDZ6yos5NlLKiLEorYgEKEsw5WjToMMIbJUGTc7dU8V4wYA7DZe0jftr35NvvTd8o6dzI79e5cHH5FUWKXqEldMqeTzFfPLPgyAaevxDvyBO3Z6mCkIA1ptNLfj47JTdpabc2al6qFZfJfOro+ufT/aIE1pWoLF/GARECQQD2rLyhBiRZfFf9bnUAWaG3RNE5i7Ef7t64DBZO9frZe660a8Xk8Yxzi7KMviq9aIY6LgsV1Ake2W97CcbGNtBrAkEApNWV7YwqLRM8yBO3VIflzsbtuk3RjicwjxzJzkLhR91xvWQDLx50L7kt0e1SNcuVJw3Xr0yGfPNAw4vE9FQMSwJAewyn+9tIfqscaXuUOdx8YyOdCwu4C6nox/6fkjv6KkscVzv7t70WxvzE0Jh8UYe2jYcyWG0xL4Zfqgyyb2YgiQJAKxltyl8L6B1Pl0EQfpnKDPcW0c/nKzQ0DjeIzNXP8eqFAvBTpM5hstjIkktrY4WHyl5kNwHbaHByTq8NIJWZYQJASWfwM30dJ5YAVq3ZMYkY0AeyQuJptdW4m3UJZWb2HyNU/KfPnGJ+OEO2A7XaFeRfO177RUvCqiwPAL4Y4pFvdw==";
    //加密算法RSA
    public static final String KEY_ALGORITHM = "RSA";//使用默认的算法
 
    //RSA最大加密明文大小
    private static final int MAX_ENCRYPT_BLOCK = 117;
     // RSA最大解密密文大小
    private static final int MAX_DECRYPT_BLOCK = 256/2;//需要注意，如果用的是2048位密钥，这里需要改为256；1024密钥是128
    public static void main(String[] args) throws Exception {
    test();
 
}
    static void test() throws Exception {
        System.out.println("公钥加密——私钥解密");
        String source = "我觉得小程序加密很简单，你觉得呢";//需要加密的原文
        System.out.println("加密前原文：\ \ " + source);
        byte[] data = source.getBytes();
        byte[] encodedData = encrypt_PublicKey(data, publicKey);//加密
        System.out.println("加密后内容：\ \ " + new String(encodedData));//没有处理过的密文字符串
        String   encodedDataStr=new String(Base64.getEncoder().encode(encodedData));//加密后问密文需要使用Base64编码然后转换成string返回前端:PPn5ifDPU+DMG8D9jOJbnkEutwvthWfWwa3qfYK0Hl50doR2X6n3ANGzVrXbdfsMOPzIDCG8a8fbpPH+PXCS5fDX4fFdAnak8mhoJ/1qdJfwfXRtlINYchQQgp97Nr/kpGkZOEximE4oTNiSDLTbvz9yCfgA46lCYyrw13V3YWs=
        System.out.println("---:base64处理：\ \ " + encodedDataStr);
        byte[] decodedData = decrypt_PrivateKey(encodedData, privateKey);//解密
        String str = new String(decodedData);
        System.out.println("解密后内容: \ \ " + str);//我觉得小程序加密很简单，你觉得呢
    }
    
}
```

