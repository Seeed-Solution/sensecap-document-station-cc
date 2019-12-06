## 创建新设备组

{% include method.html method='POST' content='{host}/1.0/group' des = '此功能用于创建新设备组，上限为50组。' %}
{% include params.html title='Body Parameters' params='name' type = 'string' des='自定义组名称' option='required'%}
### 返回示例
```ruby
{
    "code": "0",
    "data": {
        "name": "custom group name",
        "unique_name": "39AE810FF660B42F"
    }
}
```
### 请求示例
```ruby
curl --request POST \
     --url '{host}/1.0/group' \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"name":"device group name"}' \
     --include
```

## 更新设备组信息

{% include method.html method='PATCH' content='{host}/1.0/group/:unique_name' des = '更新组的名称' %}
{% include params.html title='Path Parameters' params='unique_name' type = 'string' des='设备组的唯一标识' option='required'%}
{% include params.html title='Body Parameters' params='name' type = 'string' des='设备组的新名称' option='required'%}
### 返回示例
```ruby
{
  "code": "0",
  "data": ""
}
```
### 请求示例
```ruby
curl --request PATCH \
     --url '{host}/1.0/group/:unique_name' \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"name":"new name of the device group"}' \
     --include
```

## 删除设备组

{% include method.html method='DELETE' content='{host}/1.0/group/:unique_name' des = '删除一个设备组，删除后该组内的设备将自动移到默认组中' %}
{% include params.html title='Path Parameters' params='unique_name' type = 'string' des='设备组的唯一标识' option='required'%}
### 返回示例
```ruby
{
  "code": "0",
  "data": ""
}
```
### 请求示例
```ruby
curl --request DELETE \
     --url '{host}/1.0/group/:unique_name' \
     --user '<username>:<password>' \
     --header 'content-type: application/json' \
     --include
```

## 获取设备组列表

{% include method.html method='DELETE' content='{host}/1.0/lists/group' des = '获取所有设备组' %}
### 返回示例
```ruby
{
    "code": "0",
    "data": [
        {
          "name": "group1",
          "group_unique_name": "220BD4AD87EB6B68",
          "dev_cnt": "3",
          "online_cnt": "1",
          "created": "1563947209000"
        }
    ]
}
```
### 请求示例
```ruby
curl --request GET \
     --url '{host}/1.0/lists/group' \
     --user '<username>:<password>' \
     --include
```

## 获取设备组和组内的设备列表

{% include method.html method='DELETE' content='{host}/1.0/lists/group/devices' des = '获取所有的组以及每个组内的设备。' %}

其中有一个默认组是虚拟组，他的group_unique_name为空。所有的设备绑定时如果未指定组，将会默认分配到默认组中，之后可以用户可以自由分配设备到其他组中。
### 返回示例
```java
{
  "code": "0",
  "data": {
    "node": [
      {
        "group_name": "Default",
        "group_unique_name": "",
        "devices": []
      },
      {
        "group_name": "device group name",
        "group_unique_name": "DAF6EECDCDCA6BB2",
        "devices": [
          {
            "dev_eui": "2CF7F12004100005",
            "dev_name": "device name of LoRa node",
            "lon": "113.32134",
            "lat": "22.4523",
            "online_status": "1",   // "0"表示电池低电量，“1”表示电池电量正常 
            "battery_status": "1"   // "0"表示设备离线，“1”表示设备在线
          }
        ]
      }
    ]
  }
}
```
### 请求示例
```ruby
curl --request GET \
     --url '{host}/1.0/lists/group/devices' \
     --user '<username>:<poassword>' \
     --header 'content-type: application/json' \
     --include
```

## 移动设备到其它组

{% include method.html method='DELETE' content='{host}/1.0/group/:unique_name/devices' des = '' %}
{% include params.html title='Path Parameters' params='unique_name' type = 'string' des='要移动到的组的unique_name' option='required' %}
{% include params.html title='Body Parameters' params='eui' type = 'string' des='设备唯一标识' option='required' %}
### 返回示例
```ruby
{
  "code": "0",
  "data": ""
}
```
