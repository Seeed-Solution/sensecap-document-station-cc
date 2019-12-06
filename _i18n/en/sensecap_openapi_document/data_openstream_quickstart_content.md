## Setup
- Install or [download](https://mosquitto.org/download/) Mosquitto.

## Credentials
Browse [https://sensecap.seeed.cc](https://sensecap.seeed.cc),  navigate to "User -> Organization -> Secret  Credentials", create a full access "Access Key", set down it as <Password>, and also "Organization ID" as <OrgID>.
## Receive Devices' Messages
Let’s listen for all of your devices' messages.

1.Open a terminal window and execute the following command.
```ruby
mosquitto_sub \
    -h openstream.api.sensecap.seeed.cc \
    -t '/device_sensor_data/<OrgID>/+/+/+/+' \
    -u 'org-<OrgID>' \
    -P '<Password>' \
    -I 'org-<OrgID>-quickstart' \
    -v
```
You should replace <OrgID> and <Password> with the ones you set down from "Credentials".

2.Power up devices, while devices keep sending messages, you should see outputs like:
```ruby
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4105 {"value":0,"timestamp":1544151824139}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4097 {"value":23,"timestamp":1544151900992}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4101 {"value":101629,"timestamp":1544151901112}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4098 {"value":71,"timestamp":1544151900992}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4099 {"value":69.12,"timestamp":1544151902224}
/device_sensor_data/xxxx/2CF7F12XXXXXXXXX/1/2CF7F13XXXXXXXXX/4100 {"value":437,"timestamp":1544151922137}
```
It shows each data collected by sensors, with Device EUI , Device Channel,  Sensor EUI, Measurement ID, Measurement Value, and  timestamp, see the reference for more details.
## Subscribe a Specific Field
You can also subscribe a specific field in the topic, so that you could get the data from a single device, or a single channel.
```ruby
mosquitto_sub \
    -h openstream.api.sensecap.seeed.cc \
    -t '/device_sensor_data/<OrgID>/2CF7F12XXXXXXXXX/#' \
    -u 'org-<OrgID>' \
    -P '<Password>' \
    -I 'org-<OrgID>-quickstart' \
    -v
```
You should replace <OrgId> and <Password> with what you got from "Credentials", and replace 2CF7F12XXXXXXXXX with the Device EUI you own.

Congratulations! Now you know how to monitor and receive messages via MQTT. Go build something awesome!