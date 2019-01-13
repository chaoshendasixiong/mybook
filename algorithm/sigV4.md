# 简介

AWS Signature Version 4

## 流程

使用HTTP Authorization存放签名 

* 规范请求
```
<HTTP      Method>\n
<Canonical URI>\n
<Canonical QueryString>\n
<Canonical Headers>\n
<Signed    Headers>\n
<Hashed    Payload> 


/*
param1 HTTP方法 GET or POST
param2 url中的uri URI编码
param3 url中的查询字符串 URI编码
param4 header 小写的name和trim的value列表
param5 header 小写的name列表
param6 请求有效负载的SHA256哈希值的十六进制值 可以不计算使用UNSIGNED-PAYLOAD

最后生成一个字符串 Canonical Request
*/
```

* 创建签名的字符串

```
AWS4-HMAC-SHA256" + "\n" +
timeStampISO8601Format + "\n" +
<Scope> + "\n" +
Hex(SHA256Hash(<Canonical Request>))

/*
param1 哈希算法 HMAC-SHA256
param2 ISO 8601格式的当前UTC时间（例如， 20130524T000000Z）
param3 Scope将生成的签名绑定到特定日期,AWS区域和服务
param4 Canonical Request 进行sha256 再转成16进制
*/
```

* 签名

```
HEX( HMAC-SHA256(SigningKey, StringToSign) )  
```

## 临时凭证

```
access_keyid
secret_access_key
session_token

header 增加 x-amz-security-token: session_token
https://github.com/sidbai/aws-sigv4-c
https://github.com/CollapsarLi/aws_v4_signature_c_sample
```

