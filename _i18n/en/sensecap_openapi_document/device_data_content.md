## list device EUIs

{% include method.html method='GET' content='{host}/1.0/lists/devices/eui' des = 'this is a quick method to get all device EUIs belonging to the organization' %}
{% include params.html title='Query Parameters' params='offset' type = 'number' des='current page number, start from 1, default = 1' option='OPTIONAL'%}
{% include params.html title='' params='length' type = 'string' des='the number of rows in page, default = 20' option='OPTIONAL'%}
### response
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
### Example request
```java
curl --request GET \
  --url {host}/1.0/lists/devices/eui \
  --user '<username>:<password>'
```
## get the latest data of the device 

{% include method.html method='GET' content='{host}/1.0/devices/data/:node_eui/latest' des = '' %}

A node may have multiple channels, each channel is a physical socket for a sensor to be connected. A sensor may produce multiple measurements. e.g. A temperature and humidity sensor will output temperature and humidity value. We call this temperature value a measurement, similarly we call humidity value another measurement.

This API will output the latest value of every measurement, from the sensor installed at specified channel. If the channel parameter is omitted, all sensors at all channels will be included. If a channel had installed different sensors before, the latest measurement of previous sensors will be included as well.

{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='Node EUI' option='required'%}
{% include params.html title='Query Parameters' params='measure_id' type = 'string' des='sensor measurement ID,<br> eg. measure_id=4097' option='OPTIONAL'%}
{% include params.html title='' params='channel' type = 'string' des='query data from this channel, if omitted,<br> measurements of all channels will be returned' option='OPTIONAL'%}
### response
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
### Example request
```java
curl --request GET \
     --url {host}/1.0/devices/data/:node_eui/latest?measure_id:measure_id&channel:channel \
     --user '<username>:<password>' \
     --include
```

## get the history data of the device

{% include method.html method='GET' content='{host}/1.0/devices/data/:node_eui/raw' des = 'Get the history data of a specified node.' %}

The maximum number of data points returned per channel is 400. If the number of data points of a channel in the specified time range is larger than 400, the latest 400 data points will be returned.
If the time range is omitted, the latest data will be returned.

{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='Node EUI' option='required'%}
{% include params.html title='Query Parameters' params='measure_id' type = 'string' des='sensor measurement ID,<br> eg. measure_id=4097' option='OPTIONAL'%}
{% include params.html title='' params='channel' type = 'string' des='query data from this channel, if omitted,<br> measurements of all channels will be returned' option='OPTIONAL'%}
{% include params.html title='' params='limit' type = 'number' des='the number of records you want to query, max is 400' option='OPTIONAL'%}
{% include params.html title='' params='time_start' type = 'number' des='timestamp, unit millisecond' option='OPTIONAL'%}
{% include params.html title='' params='time_end' type = 'number' des='timestamp, unit millisecond' option='OPTIONAL'%}
### response
```java
/*
A data set is identified by channel and measurement ID, which means that the same channel may have multiple data sets if it had installed different sensors with different measurement ID. e.g. Channel 1 had installed light sensor then carbon dioxide sensor, then there will be two data sets related with channel 1 - {"channel": "1", "name": "Light", "points": [...], ...} and {"channel": "1", "name": "CO2", "points": [...], ...}.
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
### Example request
```java
curl --request GET \
  --url {host}/1.0/devices/data/:node_eui/raw?limit=:limit&time_start=:time_start&time_end=:time_end \
  --user '<username>:<password>' \
  --include
```

## get the segment data of the device

{% include method.html method='GET' content='{host}/1.0/devices/data/:node_eui/segment' des = '' %}

Segment a huge data set into small ones, then output the average value and peak value of each small segment.
The small segment is described with time length, e.g. 60 minutes. 

{% include params.html title='Path Parameters' params='node_eui' type = 'string' des='Node EUI' option='required'%}
{% include params.html title='Query Parameters' params='measure_id' type = 'string' des='sensor measurement ID,<br> eg. measure_id=4097' option='OPTIONAL'%}
{% include params.html title='' params='channel' type = 'string' des='query data from this channel, if omitted,<br> measurements of all channels will be returned' option='OPTIONAL'%}
{% include params.html title='' params='segment' type = 'string' des='time length of segment, unit minute' option='OPTIONAL'%}
{% include params.html title='' params='time_start' type = 'string' des='timestamp, unit millisecond' option='OPTIONAL'%}
{% include params.html title='' params='time_end' type = 'string' des='timestamp, unit millisecond' option='OPTIONAL'%}
### response
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
### Example request
```java
curl --request GET \
  --url {host}/1.0/devices/data/:node_eui/segment?measure_id:measure_id&channel:channel&segment:segment&time_start:time_start&time_end:time_end \
  --user '<username>:<password>' \
  --include
```