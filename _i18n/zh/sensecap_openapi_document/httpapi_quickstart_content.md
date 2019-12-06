## 准备工作
请先向SenseCAP销售那里获得您的SenseCAP帐户，并确保您可以登录SenseCAP 云平台 [https://sensecap.seeed.cc](https://sensecap.seeed.cc).

## 获取Access Key ‌

1. 登录SenseCAP云平台： [https://sensecap.seeed.cc](https://sensecap.seeed.cc)
1. 前往“Organization/Security Credentials”。 ‌ 
1. 点击“Create access key”。
1. 获取“Access ID”和“Access Key”。

{% include image.html file="open_api/api_quickstart1.png" %}

## 获取所有账号下已绑定设备的EUI（设备ID）
使用curl发出HTTP请求。下面的示例将调用API来获取属于您的所有设备的EUI。
```ruby
curl --user "<access_id>:<access_key>" \
     https://sensecap-openapi.seeed.cc/1.0/lists/devices/eui
```
请将您刚获取到的Access ID和Access Key将上面的<access_id>和<access_key>替换掉。然后将会得到和下面一样格式的输出结果：
```ruby
   {
     "code": "0",
     "data": {
       "gateway": [
         "2CF7F1121130003F",
         "2CF7F1100470001A"
       ],
       "node": [
         "2CF7F12210400031",
         "2CF7F12210400005",
         "2CF7F12210400023"
       ]
     },
     "time": 0.314
   }
```

