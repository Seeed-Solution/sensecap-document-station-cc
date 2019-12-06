## 准备工作
- [下载](https://mosquitto.org/download/) 并安装Mosquitto。.

## 获取证书
1.登录SenseCAP云平台： [https://sensecap.seeed.cc](https://sensecap.seeed.cc)

2.前往“Organization/Security Credentials” 

3.点击“Create access key”会产生一对Access ID和对应的Access Key
    {% include image.html file="open_api/stream_api1.png" %}
    
4.点击“Organization”，获取“Organization ID”作为<OrgID>。
    {% include image.html file="open_api/stream_api2.png" %}

## 接收设备消息
下面介绍如何接收您所有设备的消息
1.打开一个终端窗口并执行以下命令。
```ruby
mosquitto_sub \
    -h openstream.api.sensecap.seeed.cc \
    -t '/device_sensor_data/<OrgID>/+/+/+/+' \
    -u 'org-<OrgID>' \
    -P '<Password>' \
    -I 'org-<OrgID>-quickstart' \
    -v
```
请将您刚获取到的Organization ID和Access Key将上面<OrgID>的和<Password>替换掉。

2.启动设备，当设备持续发送消息时，信息的输出格式如下：
```
/device_sensor_data/<OrgID>/<DeviceEUI>/<Channel>/<SensorEUI>/<MeasurementID>
```

```ruby
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4105 {"value":0,"timestamp":1544151824139}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4097 {"value":23,"timestamp":1544151900992}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4101 {"value":101629,"timestamp":1544151901112}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4098 {"value":71,"timestamp":1544151900992}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4099 {"value":69.12,"timestamp":1544151902224}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4100 {"value":437,"timestamp":1544151922137}
```
显示传感器收集的每个数据，包括设备唯一标识Device EUI，设备通道Device Channel，传感器唯一标识Sensor EUI，测量值IDMeasurement ID，测量值Measurement Value和时间戳timestamp。
## 订阅特定字段
将设备通道Device EUI，设备通道Device Channel，传感器唯一标识Sensor EUI，测量值ID Measurement Value替换成从上述消息列表中的特定设备的字段，以便从某个设备或某个通道获取数据。

比如订阅温湿度传感器设备ID为2CF7F12210400083，通道为1，传感器ID为2CF7F13004700089，温度物理量ID为4097的值，用Organization ID和Access Key将下面<OrgID>的和<Password>替换掉，在shell中执行命令
```ruby
mosquitto_sub \
    -h openstream.api.sensecap.seeed.cc \
    -t '/device_sensor_data/<OrgID>/2CF7F12XXXXXXXXX/#' \
    -u 'org-<OrgID>' \
    -P '<Password>' \
    -I 'org-<OrgID>-quickstart' \
    -v
```
执行命令的结果如下：
```ruby
/device_sensor_data/521853156991/2CF7F12210400083/1/2CF7F13004700089/4097 {"value":28,"timestamp":1561373812474}
```
