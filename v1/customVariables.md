# Custom Variables

### Custom Variable Properties

| Property | Description
| --- | ---
| `name` | the name of the custom variable
| `value` | the expression used to capture the information. The value of a custom variable can be the right hand side of a JavaScript Assignment Statement.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/custom_variables
```

### Response
Returns a list of [custom variables](#custom-variable-properties).


### Example
Sample request:
```bash
curl "https://hosted.comm100.com/livechatapi/custom_variables" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "name": "name",
        "value": "document.getElementById('facebook_name').value"
    },
    {
        "name": "email",
        "value": "facebook_email"
    }
]
```
