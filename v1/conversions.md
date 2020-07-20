# Conversions
[Conversions](https://www.comm100.com/livechat/features/conversions.aspx) helps you to track how Live Chat drives customer conversions. This feature is available in **Enterprise** edition.


## Get List of Conversion Actions
Get a list of your conversion actions. Only agents with **"Manage Settings"** permission have access to this resource. 

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/conversions
```
### Response
| Property | Description
| --- | ---
| `id`| the id of the conversion action
| `isEnable` | whether the conversion action is enabled or not
| `name` | the name of the conversion action

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/conversions" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 1,
        "isEnable": true,
        "name": "Product Purchase"
    },
    {
        "id": 2,
        "isEnable": true,
        "name": ""
    }
]
```

## Mark API Conversion as Successful
Via this API, you can transmit conversion data to your Comm100 Live Chat account.

### Path
```bash
POST https://hosted.comm100.com/api/v1/livechat/mark_api_conversion_successful
```

### Parameter
| Property | Description
| --- | ---
| `conversion_name`| the name of the conversion
| `visitorId` | the identity string of visitor
| `value` | the value of this conversion

### Response
| Property | Description
| --- | ---
| `error_code` | `0`: ok;<br />`1`: the conversion name does not exist;<br />`2`: the visitorId does not exist;<br /> `3`: error adding conversion-related Data to system.
| `error_message` | error message

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/mark_api_conversion_successful" \
    -X POST -d "conversion_name=sales_goal&visitorId=7273e957-02cb-4c03-a84c-44283fcfd47d&value=500" \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "error_code": 1,
    "error_message": "the conversion does not exist"
}
```
