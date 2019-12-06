## The Connection Information
- Host: sensecap-openstream.seeed.cc
- Port: 1883 for MQTT, or 8083 for MQTT Over WebSocket
- ClientID: org-&#60;Organization ID&#62;-&#60;Random ID&#62;, replace &#60;Orgnization ID&#62; with you got from dashboard, and replace &#60;Random ID&#62; with you randomly generated Numbers and lowercase letters.
- Username:  org-&#60;Organization ID&#62;, replace &#60;Organization ID&#62; with you got from dashboard.
- Password: Is your organization access key.

## Publish And Subscribe Model
SenseCAP OpenStream API implements "Publish And Subscribe Model", as the MQTT protocol does. You can connect your server to SenseCAP OpenStream API through MQTT or MQTT over WebSocket to communicate with the standard pub-sub protocol.

You can "publish" commands to platforms or devices and "subscribe" to receive messages. "subscribe" is the most common way to continuously monitor the telemetry data from devices.

## Message Topic
### Receive All Devices' Telemeasuring Data
Topic: /device_sensor_data/&#60;OrgID&#62;/+/+/+/+
### Receive Specified Device's Telemeasuring Data 
Topic Format: /device_sensor_data/&#60;OrgID&#62;/&#60;DeviceEUI&#62;/&#60;Channel&#62;/&#60;SensorEUI&#62;/&#60;MeasurementID&#62;

Field | Description
---|---
OrgID | Your "Organization ID", you can find this on https://sensecap.seeed.cc. You own a unique Organization ID, and all the topics will need it.
DeviceEUI | The device EUI
Channel | A physical socket on the device for a sensor to be connected
SensorEUI | The sensor's ID
MeasurementID | Please refer to "List of Measurement IDs" in this documentation

{% include note.html content='"+" means that there is no filtering condition for this field, matching all possible configurations. So, "/+/+/+/+" means to listen for all "&#60;DeviceEUI&#62;", "&#60;Channel&#62;", "&#60;SensorEUI&#62;", "&#60;MeasurementID&#62;"' %}

Topic can specify filtering conditions to implement listening on specified devices, channels and telemeasuring data types. For example, you can only listen for Device whose device ID is "2F000000000000", then you can replace the &#60;DeviceEUI&#62; field with 2F000000000000

The "2F000000000000" in this example must be a device that you have already bound to your account. And you should always remember to replace &#60;OrgID&#62; with your own "Organization ID".

## Message Body
### New Telemeasuring Data
```ruby
{
    "value": 437,
    "timestamp": 1544151922137
}
```
This is a sensor telemeasuring data message uploaded by a device, which conforms to the JSON format and can be parsed by JSON parser. In general, for most functional requirements, a body needs to be used in conjunction with some fields in the topic.


Field | Description
---|---
value | Sensor's Measurement Value
timestamp | Time to measure data, unit millisecond


