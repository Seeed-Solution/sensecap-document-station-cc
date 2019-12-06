## HTTP方法
SenseCAP API使用五种HTTP方法来访问：
- GET
    - 发出GET请求以获取数据。 GET请求永远不会更新或更改您的数据，因为它们是安全且幂等的。
- POST
    - 使用POST请求创建新资源。 例如，向设备组发出创建新组的POST请求。
- PATCH
    - 发出PATCH请求更新资源。对于PATCH请求，您只需要提供需要更改的数据即可。
- PUT
    - 使用PUT请求创建或更新资源。这对于同步订阅服务器数据非常有用。
- DELETE
    - 发出DELETE请求以删除资源。
    
{% include note.html content="如果您的运营商不允许GET或POST以外的HTTP操作，请使用HTTP Method tunneling —— 一种通过POST方法隧道传输任何HTTP方法的机制，但需要在X-HTTP-Method-Override头文件中包含您打算使用的方法。" %}

## HTTP 的请求和响应
使用HTTP基本身份验证对请求进行身份验证。

### HTTP基本身份验证
HTTP基本身份验证是RESTfull API身份验证最常见的方法之一。我们使用Access ID作为用户名，Access Key作为密码。各种HTTP客户端库基本都会支持基本身份验证，在本文档中，我们使用curl通过——user选项来指定基本身份验证凭据。

您可以通过[SenseCAP云平台](https://sensecap.seeed.cc/portal)来创建Access Key。 请参阅HTTP API 快速入门，了解如何获取访问密钥。

### API 响应
所有响应字段都遵循小写和下划线约定

#### 字符串响应成功
```ruby
   {
       "code":"0",
       "data":"
           // string
       "
   }
```

#### 对象响应成功
```ruby
   {
       "code":"0",
       "data":{
           // object
       }
   }
```
#### 数组响应成功
```ruby
   {
       "code":"0",
       "data":[
           // Array
       ]
   }
```
#### 响应错误
```ruby
   {
       "code":"1001",
       "msg":"error message"
   }
```
