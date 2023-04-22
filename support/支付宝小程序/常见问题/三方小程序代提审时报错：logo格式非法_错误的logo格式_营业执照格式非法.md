## 问题描述
[alipay.open.mini.version.audit.apply](https://opendocs.alipay.com/mini/03l9bq)（小程序提交审核接口）调用报：INVALID_LOGO（logo 格式非法）、INVALID_LOGO_EXT（错误的logo格式）、INVALID_LICENSE_PIC_EXT（营业执照格式非法）。 

## 问题原因
提审时会返回 logo 格式非法、营业执照格式非法等错误，这种错误一般是开发者在使用 PS 或者其它软件保存图片为 JPG 格式时，默认的模式是 CMYK 模式（这是给印刷机用的），会导致图片转换失败，例如下图所示。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/18e6d735-ae79-4b5e-be41-4cdb879be01d.png#align=left&display=inline&height=711&margin=%5Bobject%20Object%5D&originHeight=971&originWidth=1024&status=done&style=none&width=750)

## 解决方案
图片保存为 RGB 模式，不要使用默认的 CMYK 模式。<br /> <br /> 
