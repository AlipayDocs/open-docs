## 问题描述
PHP 语言三方代小程序设置/获取AES密钥报错 Call to undefined function mcrypt_get_block_size()。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/f9ea72b1-f1aa-4cea-b536-118041d28db2.png#align=left&display=inline&height=581&margin=%5Bobject%20Object%5D&originHeight=581&originWidth=1261&status=done&style=none&width=1261)

## 报错原因
PHP7.1 以上已经不支持 mcrypt_get_block_size（**已被废弃**）导致。 

## 解决方案

- 更新 [SDK](https://opendocs.alipay.com/support/01rayi) 到最新版本。
- 在 SDK 的 aop 目录下找到 AopEncrypt.php 文件使用下面代码替换文件中的代码，重试。<br />
![](https://gw.alipayobjects.com/zos/sptworksff_prod/c6b398c9-8122-4405-90bc-e93358a65afd.png#align=left&display=inline&height=353&margin=%5Bobject%20Object%5D&originHeight=353&originWidth=502&status=done&style=none&width=502)
```php
<?php
/** *   加密工具类 * * User: jiehua * Date: 16/3/30 * Time: 下午3:25 */
/** * 加密方法 * @param string $str * @return string */function encrypt($str, $screct_key){   
    //AES, 128 模式加密数据 CBC   
    $screct_key = base64_decode($screct_key);  
    $str = trim($str);   
    $str = addPKCS7Padding($str);    
    //设置全0的IV  
    $iv = str_repeat("\\0", 16); 
    $encrypt_str = openssl_encrypt($str, 'aes-128-cbc', $screct_key, OPENSSL_NO_PADDING, $iv);    
    return base64_encode($encrypt_str);}
/** * 解密方法 * @param string $str * @return string */function decrypt($str, $screct_key){   
    //AES, 128 模式加密数据 CBC   
    $str = base64_decode($str);
    $screct_key = base64_decode($screct_key);    
    //设置全0的IV  
    $iv = str_repeat("\\0", 16);   
    $decrypt_str = openssl_decrypt($str, 'aes-128-cbc', $screct_key, OPENSSL_NO_PADDING, $iv);
    $decrypt_str = stripPKSC7Padding($decrypt_str);    return $decrypt_str;}
/** * 填充算法 * @param string $source * @return string */function addPKCS7Padding($source){   
    $source = trim($source);
    $block = 16;
    $pad = $block - (strlen($source) % $block);    
    if ($pad <= $block) {
        $char = chr($pad);
        $source .= str_repeat($char, $pad);
    }
    return $source;}
/** * 移去填充算法 * @param string $source * @return string */function stripPKSC7Padding($source){    
    $char = substr($source, -1);    
    $num = ord($char);    
    if ($num == 62) return $source;
    $source = substr($source, 0, -$num);
    return $source;}
```
