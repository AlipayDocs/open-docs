
## 错误码
10 

## 报错描述
my.choosePhoneContact 选择本地联系人报错 error:10,errorMessage:"没有权限获取手机号码"。 

## 涉及接口
[my.choosePhoneContact](https://opendocs.alipay.com/mini/api/blghgl)

## 报错原因
用户禁止了支付宝客户端获取手机系统通讯录的访问权限。 

## 解决方案
引导用户打开支付宝客户端对手机通讯录的访问权限（可使用权限引导API：[my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide)）。

### 支付宝客户端操作
**我的** tab > **设置** > **隐私** > **系统权限管理** > **通讯录** 按照提示开启通讯录的访问权限。

### 移动端操作
**系统设置** >** 应用管理** > **支付宝** > **权限 **> **通讯录** 按照提示开启通讯录的访问权限。<br /> 

###  
