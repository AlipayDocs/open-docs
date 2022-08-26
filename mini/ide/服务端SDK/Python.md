## 简介

Python 语言适用于 Python 2.7 及以上的开发环境且仅提供通用版 SDK。

## 下载地址

[PyPI 项目依赖](https://pypi.org/project/alipay-sdk-python/3.3.398/)

## 示例代码

### 普通调用示例

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import logging
from alipay.aop.api.AlipayClientConfig import AlipayClientConfig
from alipay.aop.api.DefaultAlipayClient import DefaultAlipayClient
from alipay.aop.api.domain.AlipayTradeCreateModel import AlipayTradeCreateModel
from alipay.aop.api.request.AlipayTradeCreateRequest import AlipayTradeCreateRequest
from alipay.aop.api.response.AlipayTradeCreateResponse import AlipayTradeCreateResponse
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s %(levelname)s %(message)s',
    filemode='a',)
logger = logging.getLogger('')
if __name__ == '__main__':
    # 实例化客户端
    alipay_client_config = AlipayClientConfig()
    alipay_client_config.server_url = 'https://openapi.alipaydev.com/gateway.do'
    alipay_client_config.app_id = '请填写appi_id'
    alipay_client_config.app_private_key = '请填写开发者私钥去头去尾去回车，单行字符串'
    alipay_client_config.alipay_public_key = '请填写支付宝公钥，单行字符串'
    client = DefaultAlipayClient(alipay_client_config, logger)
    # 构造请求参数对象
    model = AlipayTradeCreateModel()
    model.out_trade_no = "20150320010101001";
    model.total_amount = "88.88";
    model.subject = "Iphone6 16G";
    model.buyer_id = "2088102177846880";
    request = AlipayTradeCreateRequest(biz_model=model)
    # 执行API调用
    try:
        response_content = client.execute(request)
    except Exception as e:
        print(traceback.format_exc())
    if not response_content:
        print("failed execute")
    else:
        # 解析响应结果
        response = AlipayTradeCreateResponse()
        response.parse_response_content(response_content)
        # 响应成功的业务处理
        if response.is_success():
            # 如果业务成功，可以通过response属性获取需要的值
            print("get response trade_no:" + response.trade_no)
        # 响应失败的业务处理
        else:
            # 如果业务失败，可以从错误码中可以得知错误情况，具体错误码信息可以查看接口文档
            print(response.code + "," + response.msg + "," + response.sub_code + "," + response.sub_msg)
```

### 图片上传接口调用示例

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import logging
from alipay.aop.api.AlipayClientConfig import AlipayClientConfig
from alipay.aop.api.DefaultAlipayClient import DefaultAlipayClient
from alipay.aop.api.FileItem import FileItem
from alipay.aop.api.request.AlipayOfflineMaterialImageUploadRequest import AlipayOfflineMaterialImageUploadRequest
from alipay.aop.api.response.AlipayOfflineMaterialImageUploadResponse import AlipayOfflineMaterialImageUploadResponse
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s %(levelname)s %(message)s',
    filemode='a',)
logger = logging.getLogger('')
if __name__ == '__main__':
    # 实例化客户端
    alipay_client_config = AlipayClientConfig()
    alipay_client_config.server_url = 'https://openapi.alipaydev.com/gateway.do'
    alipay_client_config.app_id = '请填写appi_id'
    alipay_client_config.app_private_key = '请填写开发者私钥去头去尾去回车，单行字符串'
    alipay_client_config.alipay_public_key = '请填写支付宝公钥，单行字符串'
    client = DefaultAlipayClient(alipay_client_config, logger)
    # 构造请求参数对象
    request = AlipayOfflineMaterialImageUploadRequest()
    request.image_name = "我的店"
    request.image_type = "jpg"
    file = open("/Users/foo/Downloads/test.jpg", "rb")
    request.image_content = FileItem(file_name="test.jpg", file_content=file.read())
    file.close()
    # 执行API调用
    try:
        response_content = client.execute(request)
    except Exception as e:
        print(traceback.format_exc())
    if not response_content:
        print("failed execute")
    else:
        # 解析响应结果
        response = AlipayOfflineMaterialImageUploadResponse()
        response.parse_response_content(response_content)
        # 响应成功的业务处理
        if response.is_success():
            # 如果业务成功，可以通过response属性获取需要的值
            print("get response image_url:" + response.image_url)
        # 响应失败的业务处理
        else:
            # 如果业务失败，可以从错误码中可以得知错误情况，具体错误码信息可以查看接口文档
            print(response.code + "," + response.msg + "," + response.sub_code + "," + response.sub_msg)
```

### 用户授权接口调用示例

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import logging
from alipay.aop.api.AlipayClientConfig import AlipayClientConfig
from alipay.aop.api.DefaultAlipayClient import DefaultAlipayClient
from alipay.aop.api.constant.ParamConstants import *
from alipay.aop.api.domain.AlipayEbppInvoiceTitleListGetModel import AlipayEbppInvoiceTitleListGetModel
from alipay.aop.api.request.AlipayEbppInvoiceTitleListGetRequest import AlipayEbppInvoiceTitleListGetRequest
from alipay.aop.api.response.AlipayEbppInvoiceTitleListGetResponse import AlipayEbppInvoiceTitleListGetResponse
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s %(levelname)s %(message)s',
    filemode='a',)
logger = logging.getLogger('')
if __name__ == '__main__':
    # 实例化客户端
    alipay_client_config = AlipayClientConfig()
    alipay_client_config.server_url = 'https://openapi.alipaydev.com/gateway.do'
    alipay_client_config.app_id = '请填写appi_id'
    alipay_client_config.app_private_key = '请填写开发者私钥去头去尾去回车，单行字符串'
    alipay_client_config.alipay_public_key = '请填写支付宝公钥，单行字符串'
    client = DefaultAlipayClient(alipay_client_config, logger)
    # 构造请求参数对象
    model = AlipayEbppInvoiceTitleListGetModel()
    model.user_id = "2088102177492087"
    request = AlipayEbppInvoiceTitleListGetRequest(biz_model=model)
    # 添加auth_token
    udf_params = dict()
    udf_params[P_AUTH_TOKEN] = "auth_token，使用时替换成正确的token"
    request.udf_params = udf_params
    # 执行API调用
    try:
        response_content = client.execute(request)
    except Exception as e:
        print(traceback.format_exc())
    if not response_content:
        print("failed execute")
    else:
        # 解析响应结果
        response = AlipayEbppInvoiceTitleListGetResponse()
        response.parse_response_content(response_content)
        # 响应成功的业务处理
        if response.is_success():
            # 如果业务成功，可以通过response属性获取需要的值
            print("get response trade_no:" + response.trade_no)
        # 响应失败的业务处理
        else:
            # 如果业务失败，可以从错误码中可以得知错误情况，具体错误码信息可以查看接口文档
            print(response.code + "," + response.msg + "," + response.sub_code + "," + response.sub_msg)
```

<br />
