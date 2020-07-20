# Offline Messages
What can you do with Offline Message?
Comm100 Live Chat API enables you to do the followings with the Offline Message resource:

| Method | Name | Path
| --- | --- | ---
| GET | [Get List of Offline Messages](#get-list-of-offline-messages) | /api/v1/livechat/offline_messages
| GET | [Get a Single Offline Message](#get-a-single-offline-message) | /api/v1/livechat/offline_messages/{id}


## Get List of Offline Messages

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/offline_messages
```

### Parameters
| Property | Description
| --- | ---
| `date_from` | optional, defaults to today. (format: `yyyy-MM-dd`)
| `date_to` | optional, defaults to today. (format: `yyyy-MM-dd`)
| `keyword` | optional, defaults to null
| `department` | optional, defaults to `0`, representing any department
| `page` | optional, page number, defaults to `1`. The number of the first page is `1`, not `0`.

### Response
| Property | Description
| --- | ---
| `offline_messages` | offline message array ([details of an offline message](#details-of-an-offline-message))
| `pages` | the total number of pages
| `total` | the total number of offline messages

### Details of an Offline Message
| Property | Description
| --- | ---
| `id` | the id of the offline message
| `name` | the name of the visitor who submitted the offline message
| `email` | the email of the visitor who submitted the offline message
| `company` | the company of the visitor who submitted the offline message
| `phone` | the phone of the visitor who submitted the offline message
| `department` | the department the visitor selected in the offline message window
| `subject` | the subject of the offline message entered by the visitor
| `content` | the content of the offline message entered by the visitor
| `custom_fields` | the values of [custom fields](#details-of-a-custom-field) entered by visitors in the offline message
| `attachment` | the file the visitor attached to the offline message. 
| `time` | the time when the visitor submitted the offline message

### Details of a Custom Field
Custom fields contain the following properties:

| Property | Description
| --- | ---
| `id` | the id of the custom field
| `name` | the name of the custom field
| `value` | the value of the custom field

### Details of Attachment
Attachment contains the following properties:

| Property | Description
| --- | ---
| `name` | the name of the attachment
| `uri` | the uri of the attachment

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/offline_messages?date_from=2018-4-10 \
    &date_to=2018-4-30&keyword=comm100" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
{ 
    "offline_messages": [
        { 
            "attachment": { 
                "name": "screen_capture.png",
                "uri": "http://hosted.comm100.com/livechatreport/download.ashx?siteId=10014&downloadtype=MessageAttachment&id=3679"
            },
            "company": "comm100",
            "content": "I have an problem about Comm100 live chat. ",
            "custom_fields": [
                { 
                    "field_id": 5000001,
                    "name": "order_id",
                    "value": "1780064"
                },
                { 
                    "field_id": 5000002,
                    "name": "bill_amount",
                    "value": "500.00"
                }
            ],
            "department": "livechat",
            "email": "allon@comm100.com",
            "id": "a2317d24-bec0-43e5-aaf5-2eae29ce948f",
            "name": "Allon",
            "phone": "1-877-305-0464",
            "subject": "comm100 live chat",
            "time": "/Date(1358453897)/"
        },
        ...
    ],
    "pages": 1,
    "total": 7
}
```

## Get a Single Offline Message

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/offline_messages/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id`| the id of the offline message

### Response
The [details](#details-of-an-offline-message) of the offline message will be returned.

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/offline_messages/a2317d24-bec0-43e5-aaf5-2eae29ce948f" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
{ 
    "offline_messages": [
        { 
            "attachment": { 
                "name": "screen_capture.png",
                "uri": "http://hosted.comm100.com/livechatreport/download.ashx?siteId=10014&downloadtype=MessageAttachment&id=3679"
            },
            "company": "comm100",
            "content": "I have an problem about Comm100 live chat. ",
            "custom_fields": [
                { 
                    "field_id": 5000001,
                    "name": "order_id",
                    "value": "1780064"
                },
                { 
                    "field_id": 5000002,
                    "name": "bill_amount",
                    "value": "500.00"
                }
            ],
            "department": "livechat",
            "email": "allon@comm100.com",
            "id": "a2317d24-bec0-43e5-aaf5-2eae29ce948f",
            "name": "Allon",
            "phone": "1-877-305-0464",
            "subject": "comm100 live chat",
            "time": "/Date(1358453897)/"
        },
        ...
    ],
    "pages": 1,
    "total": 7
}
```