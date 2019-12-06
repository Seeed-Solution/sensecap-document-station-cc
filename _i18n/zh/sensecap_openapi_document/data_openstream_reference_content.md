## 连接信息
- Host: sensecap-openstream.seeed.cc
- 端口：MQTT的端口：1883 ；MQTT Over WebSocket的端口：8083。 
- Client ID：格式为org-&#60;Organization ID&#62;-&#60;Random ID&#62;, &#60;Orgnization ID&#62; 可以在您的后台Organization页面中获取,  &#60;Random ID&#62; 使用您自己随机生成的数字和小写字母。
- Username：格式为org-&#60;Organization ID&#62;，&#60;Organization ID&#62;可以在您的后台Organization中获取。
- Password：在Web页面获取Access Key

## 发布和订阅模型
SenseCAP Data OepnStream API 服务实现了标准化的发布/订阅模型，平台通过MQTT代理实现了该模型，并具有端到端的消息交互通信功能。该服务还支持MQTT Over Websocket标准协议。

通过publish方法，您可以向设备发送控制命令。 通过subscribe方法，您可以订阅并监听设备上报的传感器遥测数据消息。

## 消息主题
### 接收所有设备的遥测数据
/device_sensor_data/&#60;OrgID&#62;/+/+/+/+
### 接收指定设备的遥测数据
主题格式：/device_sensor_data/&#60;OrgID&#62;/&#60;DeviceEUI&#62;/&#60;Channel&#62;/&#60;SensorEUI&#62;/&#60;MeasurementID&#62;

字段 | 描述
---|---
OrgID | 您的组织ID，可以从后台中的Organization页面中获取。
DeviceEUI | 传感器设备唯一标识
Channel | 一个设备上的物理接口，用于连接传感器，默认为1
SensorEUI | 传感器探头的唯一标识
MeasurementID | 测量值ID，具体测量值的清单详见附录

{% include note.html content='“+”表示此字段没有过滤条件，能够匹配所有。所以，“/ + / + / + / +”表示监听所有“&#60;DeviceEUI&#62;”，“&#60;Channel&#62;”，“&#60;SensorEUI&#62;”，“&#60;MeasurementID&#62;”' %}

主题可以指定过滤条件，以实现对指定设备，通道和远程测量数据类型的监听。 例如，如果您只想侦听设备ID为“2F000000000000”的设备，可以用2F000000000000替换字段&#60;DeviceEUI&#62;。

上面的“2F000000000000”设备必须是已经绑定到您组织账号中的设备。而且&#60;OrgID&#62;字段是必填的。
## 消息主体
### 新的测量数据
```ruby
{
    "value": 437,
    "timestamp": 1544151922137
}
```
这是一个由设备上传的传感器远程测量数据消息，其符合JSON格式并且可以被JSON解析器解析。 通常，对于大多数功能需求，主体需要与主题中的某些字段结合一起使用。

字段 | 描述
---|---
value | 传感器的测量数值
timestamp | 数据的时间戳，单位为毫秒


