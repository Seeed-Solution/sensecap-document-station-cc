## 获取网关列表

{% include method.html method='GET' content='{host}/1.0/lists/gateway' des = '获取网关的列表信息' %}
{% include params.html title='Query Parameters' params='offset' type = 'number' des='当前页码，从1开始，默认为1' option='OPTIONAL'%}
{% include params.html title='' params='length' type = 'string' des='每页获取的数量，默认为20' option='OPTIONAL'%}
### 返回示例
```java
{
    "code": "0",
    "data": {
        "page": {
            "count": "8"
        },
        "list": [
            {
                "dev_eui": "2CF7F1120410001D",               // gateway EUI, equipment unique identity
                "dev_name": "gtw seeed 2018csc",             // gateway name
                "dev_area": "Asia",                          // gateway area, Europe America Asia
                "dev_country": "CHN",                        // name country, defined by customer
                "online_status": "0",                        // 1 online, 0 offline
                "description": "organization first gateway", // desc something
                "activate_time": "1543990216000",            // when the customer activates the device, unit milliseconds
                "latestmsg_time": "1543990216000",           // the latest message time, unit milliseconds
                "production_time": "1539747273000",          // the gateway production time, unit milliseconds
                "frequency": "CN_470_510",                   // frequency
                "position": {                                // geographic, set by customer        
                    "lat": "22.2235",                        // geographic.latitude
                    "lon": "113.21",                         // geographic.longitude
           
                "ver_hardware": "1.0.3",                     // hardware version
                "ver_software": "1.0.2",                     // software version
                "antenna_placement": "indoor",               // antenna placement, set by customer
            }
        ]
    }
}
```
### 请求示例
```java
curl --request GET \
     --url {host}/1.0/lists/gateway?offset=1&length=2 \
     --user '<username>:<password>'
```

## 获取网关详情

{% include method.html method='GET' content='{host}/1.0/gateway/:gateway_eui' des = '获取指定网关的详情信息' %}
{% include params.html title='Path Parameters' params='gateway_eui' type = 'string' des='设备唯一标识' option='REQUIRED'%}
### 返回示例
```java
{
    "code": "0",
    "data": {
        "dev_eui": "2CF7F1120410001D",     // gateway EUI, equipment unique identity
        "dev_name": "gtw seeed 2018csc",   // gateway name
        "dev_area": "Asia",                // gateway area, Europe America Asia
        "dev_country": "CHN",              // name country, defined by customer
        "group_name": "Group for Dev",     // the group name, if customer set a group for the device
        "access_read": "68B04B2BD1AE8367A4B501BF1C478024DC901A18657AAEBEB4C07AE9B10A0B15",    // device access code for read
        "access_write": "D978F7DF08B3C933CB6C0A23F303F1460572E60348E240C8432FB482FC11A7A3",   // device access code for write
        "online_status": "0",                         // 1 online, 0 offline
        "description": "organization first gateway",  // desc something
        "activate_time": "1543990216000",             // when the customer activates the device, unit milliseconds
        "latestmsg_time": "1543990216000",            // the latest message time, unit milliseconds
        "production_time": "1539747273000",           // the gateway production time, unit milliseconds
        "frequency": "CN_470_510",                    // frequency
        "position": {                                 // geographic, set by customer        
            "lat": "22.2235",                         // geographic.latitude
            "lon": "113.21"                           // geographic.longitude
    
        "ver_hardware": "1.0.3",                      // hardware version
        "ver_software": "1.0.2",                      // software version
        "antenna_placement": "indoor",                // antenna placement, set by customer
    }
}
```
### 请求示例
```java
curl --request GET \
     --url {host}/1.0/gateway/:gateway_eui \
     --user '<username>:<password>'
```

## 更新网关详情信息

{% include method.html method='PATCH' content='{host}/1.0/gateway/:gateway_eui' des = '更新网关的详情信息，以下Body Parameters需选填任意一个或多个' %}
{% include params.html title='Path Parameters' params='gateway_eui' type = 'string' des='设备唯一标识' option='REQUIRED'%}
{% include params.html title='Body Parameters' params='group_unique_name' type = 'string' des='设备组的唯一标识' option='OPTIONAL'%}
{% include params.html title='' params='dev_name' type = 'string' des='设备名称' option='OPTIONAL'%}
{% include params.html title='' params='dev_country' type = 'string' des='ISO 3166-1 国家/地区代码,<br>例如代码“CHN”表示中国' option='OPTIONAL'%}
{% include params.html title='' params='position' type = 'object' des='{"lon":"longitude", "lat":"latitude", "alt":"altitude"}' option='OPTIONAL'%}
{% include params.html title='' params='description' type = 'object' des='网关的自定义描述' option='OPTIONAL'%}
{% include params.html title='' params='antenna_placement' type = 'object' des=' enum:indoor|outdoor' option='OPTIONAL'%}
### 返回示例
```java
{
    "code":"0",
    "data":""
}
```
### 请求示例
```java
curl --request PATCH \
     --url {host}/1.0/gateway/:gateway_eui \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"dev_name":"Example for Developer"}' \
     --include
```

## 从组织中删除网关

{% include method.html method='DELETE' content='{host}/1.0/gateway/:gateway_eui' des = '删除某个网关与组织账号的绑定关系，删除后，还可以通过SenseCAP 的APP将网关绑定回来。' %}
{% include params.html title='Path Parameters' params='gateway_eui' type = 'string' des='设备的唯一标识' option='REQUIRED'%}
### 返回示例
```java
{
    "code":"0",
    "data":""
}
```
### 请求示例
```java
curl --request DELETE \
     --url {host}/1.0/gateway/:gateway_eui \
     --user '<username>:<password>'
```

## 获取节点列表

{% include method.html method='GET' content='{host}/1.0/lists/node' des = '获取节点的列表' %}
{% include params.html title='Query Parameters' params='offset' type = 'number' des='当前页码，从1开始，默认为1' option='OPTIONAL'%}
{% include params.html title='' params='length' type = 'string' des='每页获取的数量，默认为20' option='OPTIONAL'%}
### 返回示例
```java
{
    "code": "0",
    "data": {
        "page": {
            "count": "28"                           // total number 
        },
        "list": [
            {
                "dev_eui": "2CF7F12004100005",      // node EUI, equipment unique identity
                "dev_name": "Example for Dev",      // node name
                "dev_area": "Europe",               // node area, Europe America Asia
                "dev_country": "CHN",               // name country, defined by customer
                "online_status": "1",               // 1 online, 0 offline
                "battery_status": "1",              // 1 node battery for good, 0 node battery for bad
                "description": "describe",          // desc something
                "activate_time": "1543990216000",   // when the customer activates the device, unit milliseconds
                "latestmsg_time": "1543990216000",  // the latest message time, unit milliseconds
                "production_time": "1539747273000", // the node production time, unit milliseconds
                "frequency": "EU_863_870",          // frequency
                "msg_count": "12",                  // the total number of message that have been sent by the device
                "ver_hardware": "1.3",              // hardware version
                "ver_software": "1.2"              // software version
            }
        ]
    }
}
```
### 请求示例
```java
curl --request GET \
     --url {host}/1.0/lists/node?offset=1&length=2 \
     --user '<username>:<password>'
```

## 获取节点详情 

{% include method.html method='GET' content='{host}/1.0/node/:node_eui' des = '获取指定节点的详情' %}
{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='设备唯一标识' option='REQUIRED'%}
### 返回示例
```java
{
    "code": "0",
    "data": {
        "dev_eui": "2CF7F12004100005",      // node EUI, equipment unique identity
        "dev_name": "Example for Dev",      // node name
        "dev_area": "Europe",               // node area, Europe America Asia
        "dev_country": "CHN",               // name country, defined by customer
        "group_name": "Group for Dev",      // the group name, if customer set a group for the device
        "access_read": "9872A8956A444FEF6A2B08625534D311F444714FE5887AF338E42456EEDD8E16",    // device access code for read
        "access_write": "3D4474E08EDC039EB3EC2C3827666446D8D6C2D31741F8FA271AD9AFA6B4A12D",   // device access code for write
        "online_status": "1",               // 1 online, 0 offline
        "battery_status": "1",              // 1 node battery for good, 0 node battery for bad
        "description": "describe",          // desc something
        "activate_time": "1543990216000",   // when the customer activates the device, unit milliseconds
        "latestmsg_time": "1543990216000",  // the latest message time, unit milliseconds
        "production_time": "1539747273000", // the node production time, unit milliseconds
        "frequency": "EU_863_870",          // frequency
        "msg_count": "12",                  // the total number of message that have been sent by the device
        "ver_hardware": "1.3",              // hardware version
        "ver_software": "1.2",              // software version
        "sensors": [                   // the sensors mounted on the device, some devices can mounted more than one sensor
            {
                "sensor_eui": "2CF7F13004200016",           // sensor EUI
                "sensor_name": "Temperature and Humidity",  // sensor name
                "sensor_channel": "1",                      // the channel name or channel tag on which the sensor is mounted on the device
                "sensor_measure": [                         // some sensor have more than one measure
                    {
                        "id": "4097",                       // measure id
                        "name": "Air Temperature"           // measure name
                    },
                    {
                        "id": "4098",
                        "name": "Air Humidity"
                    }
                ]
            }
        ]
    }
}
```
### 请求示例
```java
curl --request GET \
     --url {host}/1.0/node/:node_eui \
     --user '<username>:<password>'
```

## 更新节点详情信息

{% include method.html method='PATCH' content='{host}/1.0/node/:node_eui' des = '更新节点详情信息，以下Body Paramerters需选填任意一个或多个' %}
{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='设备唯一标识' option='REQUIRED'%}
{% include params.html title='Body Parameters' params='dev_name' type = 'string' des='设备名称' option='OPTIONAL'%}
{% include params.html title='' params='group_unique_name' type = 'string' des='想移动到的组的group_unique_name' option='OPTIONAL'%}
{% include params.html title='' params='description' type = 'string' des='节点的自定义描述' option='OPTIONAL'%}
### 返回示例
```java
{
    "code":"0",
    "data":""
}
```
### 请求示例
```java
curl --request PATCH \
     --url {host}/1.0/gateway/:gateway_eui \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"dev_name":"Example for Developer"}' \
     --include
```

## 从组织中删除节点

{% include method.html method='DELETE' content='{host}/1.0/node/:node_eui' des = '删除某个节点与组织账号的绑定关系，删除后，可以通过SenseCAP 的APP将节点进行重新绑定。' %}
{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='设备唯一标识' option='REQUIRED'%}
### 返回示例
```java
{
    "code":"0",
    "data":""
}
```
### 请求示例
```java
curl --request DELETE \
     --url {host}/1.0/node/:node_eui \
     --user '<username>:<password>' \
```

## 获取传感器测量值列表

{% include method.html method='GET' content='{host}/1.0/lists/sensor/measure' des = '获取所有传感器的物理测量值列表，同时你也可以在附录 - 传感器类型表中查看到这个信息。' %}
### 返回示例
```java
{
    "code": "0",
    "data": [
        {
            "sensor_id": "1009",
            "sensor_name": "Wind Speed",
            "sensor_measure": [
                {
                    "measure_id": "4112",
                    "measure_name": "Wind Direction",
                    "measure_unit": "°"
                },
                {
                    "measure_id": "4105",
                    "measure_name": "Wind Speed",
                    "measure_unit": "m/s"
                }
            ]
        },
        {
            "sensor_id": "1008",
            "sensor_name": "Wind Direction",
            "sensor_measure": [
                {
                    "measure_id": "4104",
                    "measure_name": "Wind Direction",
                    "measure_unit": "°"
                }
            ]
        },
        {
            "sensor_id": "1006",
            "sensor_name": "Soil temperature and humidity",
            "sensor_measure": [
                {
                    "measure_id": "4103",
                    "measure_name": "Soil Humidity",
                    "measure_unit": "%RH"
                },
                {
                    "measure_id": "4102",
                    "measure_name": "Soil Temperature",
                    "measure_unit": "°C"
                }
            ]
        },
        {
            "sensor_id": "1005",
            "sensor_name": "Atmospheric Pressure",
            "sensor_measure": [
                {
                    "measure_id": "4101",
                    "measure_name": "Atmospheric Pressure",
                    "measure_unit": "Pa"
                }
            ]
        },
        {
            "sensor_id": "1004",
            "sensor_name": "Carbon Dioxide",
            "sensor_measure": [
                {
                    "measure_id": "4100",
                    "measure_name": "Carbon Dioxide",
                    "measure_unit": "Vol"
                }
            ]
        },
        {
            "sensor_id": "1003",
            "sensor_name": "Light Intensity",
            "sensor_measure": [
                {
                    "measure_id": "4099",
                    "measure_name": "Light Intensity",
                    "measure_unit": "Lux"
                }
            ]
        },
        {
            "sensor_id": "1001",
            "sensor_name": "Air Temperature and Humidity",
            "sensor_measure": [
                {
                    "measure_id": "4098",
                    "measure_name": "Air Humidity",
                    "measure_unit": "%RH"
                },
                {
                    "measure_id": "4097",
                    "measure_name": "Air Temperature",
                    "measure_unit": "℃"
                }
            ]
        }
    ],
    "time": 1.958
}
```
### 请求示例
```java
curl --request GET \
     --url {host}/1.0/lists/sensor/measure \
     --user '<username>:<password>' \
```
## 校验设备eui和code

{% include method.html method='POST' content='{host}/1.0/device/check_eui' des = '校验设备的eui和code是否匹配，用于设备绑定前的校验' %}
{% include params.html title='Body Parameters' params='eui' type = 'string' des='设备eui' option='required'%}
{% include params.html title='' params='code' type = 'string' des='设备code' option='required'%}

### 返回示例
```java
{
    "code": "0",
    "data": {
        "check": "1"  // 0-校验失败,1-检验通过
    },
    "time": 0.261
}
```
### 请求示例
```java
curl --request POST \
     --url '{host}/1.0/device/check_eui' \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"code":"device code","eui":"device eui"}' \
     --include
```
## 绑定设备

{% include method.html method='POST' content='{host}/1.0/device/bind' des = '将设备绑定到账户下' %}
{% include params.html title='Body Parameters' params='eui' type = 'string' des='设备eui' option='required'%}
{% include params.html title='' params='code' type = 'string' des='设备code' option='required'%}
{% include params.html title='' params='device_name' type = 'string' des='设备名称' %}
{% include params.html title='' params='group_unique_name' type  = 'string' des='群组unique_name，可通过群组列表接口获取'%}
{% include params.html title='' params='lon' type  = 'string' des='设备位置，经度' %}
{% include params.html title='' params='lat' type  = 'string' des='设备位置，纬度' %}
### 返回示例
```java
{
    "code": "0",
    "data": {},
    "time": 0.261
}
```
### 请求示例
```java
curl --request POST \
     --url '{host}/1.0/device/check_eui' \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"code":"device code","eui":"device eui"}' \
     --include
```