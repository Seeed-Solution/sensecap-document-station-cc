## create a new device group

{% include method.html method='POST' content='{host}/1.0/group' des = 'create a new device group, you can only create up to 50 groups.' %}
{% include params.html title='Body Parameters' params='name' type = 'string' des='custom group name' option='required'%}
### response
```ruby
{
    "code": "0",
    "data": {
        "name": "custom group name",
        "unique_name": "39AE810FF660B42F"
    }
}
```
### Example request
```ruby
curl --request POST \
     --url '{host}/1.0/group' \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"name":"device group name"}' \
     --include
```

## update device group information

{% include method.html method='PATCH' content='{host}/1.0/group/:unique_name' des = 'update the device group name' %}
{% include params.html title='Path Parameters' params='unique_name' type = 'string' des='the unique name of a device group' option='required'%}
{% include params.html title='Body Parameters' params='name' type = 'string' des='the new name of device group' option='required'%}
### response
```ruby
{
  "code": "0",
  "data": ""
}
```
### Example request
```ruby
curl --request PATCH \
     --url '{host}/1.0/group/:unique_name' \
     --user '<username>:<password>' \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data '{"name":"new name of the device group"}' \
     --include
```

## delete a device group

{% include method.html method='DELETE' content='{host}/1.0/group/:unique_name' des = 'delete a device group and the devices will be moved to the Default group.' %}
{% include params.html title='Path Parameters' params='unique_name' type = 'string' des='the unique name of a device group' option='required'%}
### response
```ruby
{
  "code": "0",
  "data": ""
}
```
### Example request
```ruby
curl --request DELETE \
     --url '{host}/1.0/group/:unique_name' \
     --user '<username>:<password>' \
     --header 'content-type: application/json' \
     --include
```

## list device group

{% include method.html method='DELETE' content='{host}/1.0/lists/group' des = 'get the list of all groups' %}
### response
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
### Example request
```ruby
curl --request GET \
     --url '{host}/1.0/lists/group' \
     --user '<username>:<password>' \
     --include
```

## list device group with devices

{% include method.html method='DELETE' content='{host}/1.0/lists/group/devices' des = 'List all groups and devices in each group' %}

The Default group is a virtual group, its group_unique_name is empty. All devices will be claimed into the Default group, users could then reorganize them with different groups.
### response
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
            "online_status": "1",  //  "0" offline, "1" online 
            "battery_status": "1"  //  "0" battery low power, "1" battery power OK
          }
        ]
      }
    ]
  }
}
```
### Example request
```ruby
curl --request GET \
     --url '{host}/1.0/lists/group/devices' \
     --user '<username>:<poassword>' \
     --header 'content-type: application/json' \
     --include
```

## move device to other group

{% include method.html method='DELETE' content='{host}/1.0/group/:unique_name/devices' des = '' %}
{% include params.html title='Path Parameters' params='unique_name' type = 'string' des='unique name which the group will be moved to' option='required' %}
{% include params.html title='Body Parameters' params='eui' type = 'string' des='device EUI' option='required' %}
### response
```ruby
{
  "code": "0",
  "data": ""
}
```
