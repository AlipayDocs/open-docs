# 场景说明
本文主要说明在小程序场景下 [获取会员手机号](https://opendocs.alipay.com/mini/api/getphonenumber) 和 [获取运动步数](https://opendocs.alipay.com/mini/api/gxuu7v) 时，通过前端授权后返回的 AES 加密密文在服务器端如何实现解密。<br />关于解密前的验签步骤，请参考 [如何使用密钥](https://opendocs.alipay.com/common/055tfz)。 

# AES 解密说明

- AES 解密函数：设 AES 解密函数为 D，则 P = D(K，C)，其中 C 为密文，K 为密钥，P 为明文。也就是说，把密文 C 和密钥 K 作为解密函数的参数输入，则解密函数会输出明文 P。
- AES 是个基本算法，实现 AES 有几种模式： ECB、CBC、CFB 、OFB、CTR 。 

小程序获取会员手机号和获取运动步数返回的报文是由 AES 加密过的密文，采用 CBC 模式。

- AES 密钥：即在支付宝页面上生成的 AES 密钥。
- 原文：res.response 为完整的报文数据。
- 加密算法：AES/CBC/PKCS5Padding。 

# 前端返回的报文
res.response 为完整的报文数据，示例如下（为了展示方便，报文示例均作了 JSON 的美化处理） 。
```
{
  "response": "hvDOnibG0DPcOFPNubK3DEfLQGL4=",  
  "sign": "OIwk7zfZMp5GX78Ow==",  
  "sign_type": "RSA2", 
  "encrypt_type": "AES", 
  "charset": "UTF-8"}
```
 其中，各字段说明如下 。

| **字段名** | **字段说明** | **必填** |
| --- | --- | --- |
| response | 报文（密文） | 是 |
| sign | 对 response 报文的签名 | 是 |
| sign_type | 加签算法 | 否（应用维度配置的加签算法，小程序默认为RSA2） |
| encrypt_type | 加密算法 | 否（默认为AES） |
| charset | 验签和解密用的字符集 | 否（默认为UTF-8） |


# Java
验签与解密处理：无论是否涉及解密，Java 服务端处理逻辑都可以按照下述逻辑处理（以下代码仅作为示例代码，生产环境使用请注意异常处理逻辑） 。<br />若小程序加签方式为证书方式，验签可查看 [公钥证书异步通知验签](https://opendocs.alipay.com/common/055tfz#%E5%BC%82%E6%AD%A5%E9%80%9A%E7%9F%A5%E9%AA%8C%E7%AD%BE) 。
```
String response = "小程序前端提交的";
//1. 获取验签和解密所需要的参数
Map<String, String> openapiResult = JSON.parseObject(response,            
           new TypeReference<Map<String, String>>() {            }, Feature.OrderedField);
           String signType = "RSA2";
           String charset = "UTF-8";
           String encryptType = "AES";
           String sign = openapiResult.get("sign");
           String content = openapiResult.get("response");
           //如果密文的boolean isDataEncrypted = !content.startsWith("{");boolean signCheckPass = false;
//2. 验签
String signContent = content;
String signVeriKey = "你的小程序对应的支付宝公钥（为扩展考虑建议用appId+signType做密钥存储隔离）";
String decryptKey = "你的小程序对应的加解密密钥（为扩展考虑建议用appId+encryptType做密钥存储隔离）";
//如果是加密的报文则需要在密文的前后添加双引号
if (isDataEncrypted) {    
    signContent = "\\"" + signContent + "\\"";}try {
    signCheckPass = AlipaySignature.rsaCheck(signContent, sign, signVeriKey, charset, signType);} catch (AlipayApiException e) {        //验签异常, 日志}
if(!signCheckPass) {    //验签不通过（异常或者报文被篡改），终止流程（不需要做解密）    
    throw new Exception("验签失败");}
//3. 解密
String plainData = null;
if (isDataEncrypted) {    
    try {
       AlipayEncrypt.decryptContent(content, encryptType, decryptKey, charset);
    } catch (AlipayApiException e) {        
        //解密异常, 记录日志       
       throw new Exception("解密异常");    
    }} else {    
    plainData = content;}
```

- AlipaySignature、AlipayEncrypt 使用的是 [开放平台服务端SDK](https://opendocs.alipay.com/open/54/103419/)。
- 请额外依赖下述三个 JAR 包：
   - [bcprov-jdk15on](https://mvnrepository.com/artifact/org.bouncycastle/bcprov-jdk15on)
   - [fastjson](https://mvnrepository.com/artifact/com.alibaba/fastjson)
   - [commons-logging](https://mvnrepository.com/artifact/commons-logging/commons-logging)
- 示例代码中 JSON 处理采用 fastjson 处理。此处一定要使用 Feature.OrderedField，否则会出现参数顺序问题导致验签失败。 

# C#
C#和.NET都可参考本示例。<br />可以基于自己的语言实现解密逻辑，也可以参考[服务端SDK](https://opendocs.alipay.com/open/54/103419/)的相应语言的底层解密方法，例如：
```
//参考AlipayEncrypt.cs文件的以下方法
public static string AesDencrypt(string encryptKey, string bizContent, string charset)
```
C#服务端处理逻辑示例代码如下 ：
```
string response = "小程序前端提交的";

//1. 获取验签和解密所需要的参数
IDictionary openapiResult = Jayrock.Json.Conversion.JsonConvert.Import(response) as IDictionary;

string signType;
if (openapiResult.Contains("sign_type"))
{
    signType = openapiResult["sign_type"].ToString();
}
else
{
    signType = "RSA2";
}

string charset;
if (openapiResult.Contains("charset"))
{
    charset = openapiResult["charset"].ToString();
}
else
{
    charset = "UTF-8";
}

string encryptType;
if (openapiResult.Contains("encrypt_type"))
{
    encryptType = openapiResult["encrypt_type"].ToString();
}
else
{
    encryptType = "AES";
}

string sign = openapiResult["sign"]..ToString();
string content = openapiResult["response"].ToString();

//如果密文的
bool isDataEncrypted = !content.StartsWith("{", StringComparison.Ordinal);
bool signCheckPass = false;

//2. 验签
string signContent = content;
string signVeriKey = "你的小程序对应的支付宝公钥（为扩展考虑建议用appId+signType做密钥存储隔离）";
string decryptKey = "你的小程序对应的加解密密钥（为扩展考虑建议用appId+encryptType做密钥存储隔离）";
//如果是加密的报文则需要在密文的前后添加双引号
if (isDataEncrypted)
{
    signContent = "\"" + signContent + "\"";
}
try
{
    signCheckPass = AlipaySignature.RSACheckContent(signContent, sign, signVeriKey, charset, signType);
}
catch (Exception ex)
{
    //验签异常, 日志
    throw new Exception("验签失败", ex);
}
if (!signCheckPass)
{
    //验签不通过（异常或者报文被篡改），终止流程（不需要做解密）
    throw new Exception("验签失败");
}

//3. 解密
string plainData = null;
if (isDataEncrypted)
{
    try
    {
        plainData = AlipayEncrypt.AesDencrypt(decryptKey, content, charset);
    }
    catch (Exception ex)
    {
        //解密异常, 记录日志
        throw new Exception("解密异常", ex);
    }
}
else
{
    plainData = content;
}
```

- AlipaySignature、AlipayEncrypt 使用的是 [开放平台服务端SDK](https://opendocs.alipay.com/open/54/103419/) 。
- Jayrock.Json.Conversion.JsonConvert 使用的是 jayrock-json 库中的工具类。

# PHP
AopEncrypt.php 文件中的 mcrypt_decrypt() 仅支持 7.0 以下版本。PHP 版本 7.0 以上 mcrypt_decrypt() 和 mcrypt_encrypt 废弃，AES 解密需要使用 openssl_decrypt 和 openssl_encrypt。<br />可以基于自己的语言实现解密逻辑，也可以参考 [服务端SDK](https://opendocs.alipay.com/open/54/103419/) 的相应语言的底层解密方法，例如：
```
//参考AopEncrypt.php的以下方法（由于密文是base64字符串，均为ASCII字符，所以不存在字符集问题）
function decrypt($str,$screct_key)
```

## PHP版本7.0以下
示例代码如下：
```
<?php
//引入AES解密require_once 'aop/AopEncrypt.php';
//aes密钥$screct_key="AES密钥";
//解密信息$str="t1lNwi+MMnr8syLTau+KIabIN4TEnprJ35BSXdfxvr8hSnSzXUUw7F4wjv56LgWuqb3vta1xdgpaFL8jCNTy+w==";
//验签代码$flag = decrypt($str,$screct_key);
//print_r($flag);
  echo $flag;?>
```

## PHP版本7.0以上
示例代码如下：
```
<?php//获取手机号解密public function openSign() {        
        $aesKey="MB4I9*****";//AES密钥       
        $content="Ho5y3nixH0tSnYWw8p/HMTO1bIONKSYd7BfkbI+ww4qgJEXKMYFWnSwjXN2B9YwvsKBYykK2gva2v1jfnQVSNQ==";  
        $result=openssl_decrypt(base64_decode($content), 'AES-128-CBC', base64_decode($aesKey),OPENSSL_RAW_DATA);   
        $v = json_decode($result, true);        
        print_r($v);//
        echo $v
    }
  ?>
```

# NodeJS
示例代码
```
const crypto = require('crypto');
let key = '' //解密的
key let crypted ='' //密文
crypted = new Buffer(crypted, 'base64').toString('binary'); 
key = new Buffer(key, 'base64'); 
var iv = new Buffer(16, 0);
var decipher = crypto.createDecipheriv('aes-128-cbc', key, iv);
var decoded = decipher.update(crypted, 'binary', 'utf8'); 
decoded += decipher.final('utf8'); //打印解密结果
console.log(decoded);
```

# python
可以基于自己的语言实现解密逻辑，也可以参考 [服务端SDK](https://opendocs.alipay.com/open/54/103419/) 的相应语言的底层解密方法，例如：
```
#参考EncryptUtils.py的以下方法
def aes_decrypt_content(encrypted_content, encrypt_key, charset)
```
如果直接引用报如下错误，需要对 aes_decrypt_content 中的 iv 做 .encode("utf8") 处理。<br />![](https://gw.alipayobjects.com/zos/workflow/workflow/202003131584068275172_4a47a0db6e60853dedfcfdf08a5ca249.png#align=left&display=inline&height=118&margin=%5Bobject%20Object%5D&originHeight=131&originWidth=935&status=done&style=none&width=842)<br />处理后代码：
```
def aes_decrypt_content(encrypted_content, encrypt_key, charset):
    encrypted_content = base64.b64decode(encrypted_content)
    iv = '\\0' * BLOCK_SIZE   
    cryptor = AES.new(base64.b64decode(encrypt_key), AES.MODE_CBC, iv.encode("utf8"))#对iv做encode("utf8")处理  
    content = unpad(cryptor.decrypt(encrypted_content))   
    if PYTHON_VERSION_3:
         content = content.decode(charset) 
         return content
```
解密代码：
```
# -*- coding=utf-8-*-from alipay.aop.api.util import EncryptUtils"""aes解密"""class AESUtil:
    key = 'uHyEdPksZljlVVzXuxxak=='#需要更换成自己的AES密钥  
    charset='utf-8' 
    resContent = 't1lNwi+MMnr8syLTau+KIabIN4TEnprJ35BSXdfxvrTy+w=='#需要更换成自己的密文  
    content=EncryptUtils.aes_decrypt_content(resContent,key,charset)  
    print(content)#{"code":"10000","msg":"Success","mobile":"158683368xxxx"}
```
 <br /> 
