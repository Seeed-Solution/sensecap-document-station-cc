## Prerequisite
You should have your SenseCAP account from SenseCAP sales, and make sure you can login the SenseCAP Web Portal [https://sensecap.seeed.cc](https://sensecap.seeed.cc).

## Get an Access Key

1. Login the SenseCAP Web Portal [https://sensecap.seeed.cc](https://sensecap.seeed.cc)
1. Navigate to "Organization/Security Credentials"
1. Click "Create access key"
1. Set down the Access ID and Access Key 

{% include image.html file="open_api/api_quickstart1.png" %}

## Get all the Deivice EUIs
In this quickstart, we will use curl to issue HTTP requests. The example below calls an API to retrieve all the device EUIs belonging to you.
```ruby
curl --user "<access_id>:<access_key>" \
     https://sensecap-openapi.seeed.cc/1.0/lists/devices/eui
```
You should replace <access_id> and <access_key> with the one you got before. The command will output like the following
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
