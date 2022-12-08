
## 字符串转换为十六进制
主要使用 charCodeAt() 方法，此方法返回一个字符的 Unicode 值，该字符位于指定索引位置。
```xml
/*  第一种写法可以在转码后的每个字符前加0x或\\u的标识，后面加空格或制表符。（加标识后可用来转换中文）*/
function str2hex(str){
function str2hex(s){
 var str = "";
         for (var i = 0; i < s.length; i++) {             
            str +="0x"+s.charCodeAt(i).toString(16)+"\\t";         
         }
         return str;
}
/*  第二种写法可以在转码字符串前加0x前缀标识（不加可直接注释：arr.push("0x");）。  适用蓝牙特征值传输。  不可转换中文，会乱码，是由于中文转换后为4个字符，转换成十六进制可以，恢复中文不行：下面转换是以2个字符循环的，中文和字母/数字混在一起后无法判断如何取值*/
function str2hex1(str){
  if(str === ""){    
    return "";
  }
  var arr = [];
  arr.push("0x");//不加"0x"可直接注释：arr.push("0x");  
  for(var i=0;i<str.length;i++){
    arr.push(str.charCodeAt(i).toString(16));
  } 
  return arr.join('');
}
```

## 十六进制转换为字符串
主要使用 fromCharCode()方法，此方法将 Unicode 码转换为与之对应的字符。
```xml
/*对应第一种str2hex转换*/
function hex2str(n) {     
     var str = "";        
     var s = n.split('0x');
        for(var i = 0;i < s.length;i++){
            str += String.fromCharCode(parseInt(s[i],16))+"\\t";
        }        
        return str;
 }
/*对应第二种str2hex1转换*/
function hex2str1(hex) {　　
  var trimedStr = hex.trim();
  var rawStr = trimedStr.substr(0,2).toLowerCase() === "0x" ? trimedStr.substr(2) : trimedStr;
  var len = rawStr.length;
  if(len % 2 !== 0) {
    my.alert("Illegal Format ASCII Code!");
    return "";　
    }　　
  var curCharCode;　　
  var resultStr = [];
  for(var i = 0; i < len;i = i + 2) {
    curCharCode = parseInt(rawStr.substr(i, 2), 16);　　　
    resultStr.push(String.fromCharCode(curCharCode));　
  }　　
  return resultStr.join("");
}
```

## 编写测试示例代码
第一种写法测试示例：
```javascript
Page({onShow() {
    var str = "abcde";    
    console.log(str2hex(str))//输出：0x61\t0x62\t0x63\t0x64\t0x65\t\t   
    console.log(hex2str(str2hex(str)))//输出：a\tb\tc\td\te\t  },});
/*1、字符串转换为十六进制　主要使用 charCodeAt()方法，此方法返回一个字符的 Unicode 值，该字符位于指定索引位置。*/
function str2hex(s){
 var str = "";         
         for (var i = 0; i < s.length; i++) {
         str +="0x"+s.charCodeAt(i).toString(16)+"\\t";
         }
         return str;
 }
/*2、十六进制转换为字符串　　主要使用 fromCharCode()方法，此方法将 Unicode 码转换为与之对应的字符。*/
function hex2str(n) {     
     var str = "";
        var s = n.split('0x');        
        for(var i = 0;i < s.length;i++){            
            str += String.fromCharCode(parseInt(s[i],16))+"\\t";        
        }
        return str; 
 }
```
第二种写法测试示例：
```javascript
Page({onShow() {    
    var str = "abcde";
    console.log(str2hex(str))//输出：0x6162636465    console.log(hex2str(str2hex(str)))//输出：abcde
  },
});
// 字符串转16进制
function str2hex(str){
  if(str === ""){    
    return ""; 
  }  
  var arr = []; 
  arr.push("0x");//不加"0x"可直接注释：arr.push("0x");  
  for(var i=0;i<str.length;i++){  
    arr.push(str.charCodeAt(i).toString(16)); 
  }
  return arr.join('');
}
// 16进制转字符串
function hex2str(hex) {　
  var trimedStr = hex.trim();　
  var rawStr = trimedStr.substr(0,2).toLowerCase() === "0x" ? trimedStr.substr(2) : trimedStr;　
  var len = rawStr.length;　
  if(len % 2 !== 0) {　　
    return "";
  }　　
  var curCharCode;　
  var resultStr = [];　
  for(var i = 0; i < len;i = i + 2) {　　
    curCharCode = parseInt(rawStr.substr(i, 2), 16);　　
    resultStr.push(String.fromCharCode(curCharCode));
  }　
  return resultStr.join("");
}
```
