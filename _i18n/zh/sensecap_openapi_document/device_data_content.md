## 设备数据API

{% include method.html method='GET' content='{host}/1.0/lists/devices/eui' des = '这是一个获取组织账号下所有设备EUI的便捷方法。' %}
### 返回示例
```java
{
    "code": "0",
    "data": {
        "gateway": [
            "2CF7F1........",
            "2CF7F1........",
            "2CF7F1........"
        ],
        "node": [
            "2CF7F1........",
            "2CF7F1........",
            "2CF7F1........",
            "2CF7F1........",
            "2CF7F1........"
        ]
    }
}
```
### 请求示例
```java
curl --request GET \
  --url {host}/1.0/lists/devices/eui \
  --user '<username>:<password>'
```
## 获取设备最新数据

{% include method.html method='GET' content='{host}/1.0/devices/data/:node_eui/latest' des = '' %}

一个节点可以有多个通道，每个通道是用于连接传感器的物理接口。传感器可以产生多个测量值。例如温湿度传感器会输出温度值和湿度值。我们称这个温度值和湿度值为两个测量值。
这个API可以从安装在某个指定channel的传感器中获取每个测量值的最新值。如果不传channel参数，就会返回这个设备的所有通道的所有传感器测量值。如果设备之前安装过其他传感器，也会在返回结果中包含以前的传感器测量值。

{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='节点设备唯一标识' option='required'%}
{% include params.html title='Query Parameters' params='measure_id' type = 'string' des='传感器的测量值ID' option='OPTIONAL'%}
{% include params.html title='' params='channel' type = 'string' des='返回该通道下的测量值，<br> 如果不传参则默认返回所有通道的测量值' option='OPTIONAL'%}
### 返回示例
```java
{
  "code": "0",
  "data": [
    {
      "channel": "1",                   // channel number
      "points": [                       // latest data points
        {
          "name": "Soil Temperature",   // the measurement name
          "unit": "℃",                  // the measurement unit
          "value": "13.75",             // the measurement value
          "created": "1545013573"       // when the record is created (timestamp, unit second)
        },
        {
          "name": "Soil Humidity",
          "unit": "%RH",
          "value": "19",
          "created": "1545013573"
        }
      ]
    }
  ]
}
```
### 请求示例
```java
curl --request GET \
     --url {host}/1.0/devices/data/:node_eui/latest?measure_id:measure_id&channel:channel \
     --user '<username>:<password>' \
     --include
```

## 获取设备历史数据

{% include method.html method='GET' content='{host}/1.0/devices/data/:node_eui/raw' des = '获取指定传感器节点设备的历史数据。' %}

返回条数最多为400条。如果指定时间范围内的数据大于400条，则返回该时间范围内最新的400条数据。如果不传时间范围参数，将直接返回最新数据。

{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='节点设备唯一标识' option='required'%}
{% include params.html title='Query Parameters' params='measure_id' type = 'string' des='传感器的测量值ID' option='OPTIONAL'%}
{% include params.html title='' params='channel' type = 'string' des='返回该通道下的测量值，<br> 如果不传参则默认返回所有通道的测量值' option='OPTIONAL'%}
{% include params.html title='' params='limit' type = 'number' des='要查询的记录条数，最多400条' option='OPTIONAL'%}
{% include params.html title='' params='time_start' type = 'number' des='时间戳，单位是毫秒' option='OPTIONAL'%}
{% include params.html title='' params='time_end' type = 'number' des='时间戳，单位是毫秒' option='OPTIONAL'%}
### 返回示例
```java
/*
数据集由通道和测量值ID标识，这意味着如果相同的通道安装过具有不同测量值ID的不同传感器，则可能返回多个数据集。例如通道1安装了光照传感器，并且在此之前安装过二氧化碳传感器，将有可能导致有两个与通道1相关的数据集 - {"channel":"1","name":"Light","points":[...],...} and {"channel":"1","name":"CO2","points":[...],...}。
*/
{
    "code": "0",
    "data": [
        {                               // data set 
            "channel": "1",             // channale number
            "channel_name": "channel alias name",
            "name": "Air Temperature",  // measurement name
            "unit": "℃",                // measurement unit
            "points": [                 // measurement data points
                {
                    "value": "8",                // measurement value
                    "created": "1545990300348"   // timestamp, unit millisecond
                },
                {
                    "value": "7",
                    "created": "1545989996049"
                }
            ]
        },
        {
            "channel": "2",
            "channel_name": "the 2nd channel",
            "name": "Air Humidity",
            "unit": "%RH",
            "points": [
                {
                    "value": "59",
                    "created": "1545990300348"
                },
                {
                    "value": "68",
                    "created": "1545989996049"
                },
                {
                    "value": "68",
                    "created": "1545989996060"
                }
            ]
        }
    ],
    "time": 0.297
}
```
### 请求示例
```java
curl --request GET \
  --url {host}/1.0/devices/data/:node_eui/raw?limit=:limit&time_start=:time_start&time_end=:time_end \
  --user '<username>:<password>' \
  --include
```

## 获取设备数据段

{% include method.html method='GET' content='{host}/1.0/devices/data/:node_eui/segment' des = '' %}

将庞大的数据段分成小数据段，然后输出每个小段的平均值和峰值。用时间长度描述小段，例如：60分钟。

{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='节点设备唯一标识' option='required'%}
{% include params.html title='Query Parameters' params='measure_id' type = 'string' des='传感器的测量值ID' option='OPTIONAL'%}
{% include params.html title='' params='channel' type = 'string' des='返回该通道下的测量值，<br> 如果不传参则默认返回所有通道的测量值' option='OPTIONAL'%}
{% include params.html title='' params='limit' type = 'string' des='要查询的记录条数，最多400条' option='OPTIONAL'%}
{% include params.html title='' params='time_start' type = 'string' des='时间戳，单位是毫秒' option='OPTIONAL'%}
{% include params.html title='' params='time_end' type = 'string' des='时间戳，单位是毫秒' option='OPTIONAL'%}
### 返回示例
```java
{
  "code": "0",
  "data": [
    {
      "channel": "1",           // channale number
      "channel_name": "channel alias name",
      "name": "Wind Direction", // measurement name
      "unit": "°",              // measurement unit
      "list": [                 // segment list
        {
          "created": "1545181200",  // timestamp, unit second
          "avg": "30",              // avgrage value of the segment
          "peak": "90"              // peak value of the segment
        },
        {
          "created": "1545182200",  
          "avg": "31",              
          "peak": "93"              
        }
      ]
    }
  ]
}
```
### 请求示例
```java
curl --request GET \
  --url {host}/1.0/devices/data/:node_eui/segment?measure_id:measure_id&channel:channel&segment:segment&time_start:time_start&time_end:time_end \
  --user '<username>:<password>' \
  --include
```