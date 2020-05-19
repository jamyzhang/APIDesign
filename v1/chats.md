# Chats
What can you do with Chat?
Comm100 Live Chat API enables you to do the followings with the Chat resource:

| Method | Name | Path
| --- | --- | ---
| GET | [Get List of Chats](#get-list-of-chats) | /api/v1/livechat/chats
| GET | [Get a Single Chat](#get-a-single-chat) | /api/v1/livechat/chats/{id}


## Get List of Chats

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/chats
```

### Parameters
| Property | Description
| --- | ---
| `date_from` | optional, defaults to today. (format: `yyyy-MM-dd`)
| `date_to` | optional, defaults to today. (format: `yyyy-MM-dd`)
| `keyword` | optional, defaults to null
| `department` | optional, defaults to `0`, representing any department
| `operator` | optional, defaults to `0`, representing any operator
| `rating` | optional, defaults to `0`, representing any rating
| `page` | optional, page number, defaults to `1`. The number of the first page is `1`, not `0`.

### Response
| Property | Description
| --- | ---
| `chats` | chat array ([details of a chat](#details-of-a-chat))
| `pages` | the total number of pages
| `total` | the total number of chats

### Details of a Chat
| Property | Description
| --- | ---
| `id` | the id of the chat
| `name` | the name of the visitor
| `email` | the email of the visitor
| `company` | the company of the visitor
| `phone` | the phone of the visitor
| `product_service` | the product/service the visitor selected in the pre-chat window. Operators can also update the value while chatting with visitors.
| `department` | the department the visitor selected in the pre-chat window. Operators can also update the value while chatting with visitors.
| `operators` | the [operators](#details-of-a-operator) that participate in the chat, separated by comma
| `custom_fields` | the values of [custom fields](#details-of-a-custom-field) entered by visitors in the pre-chat window. Operators can also update the value(s) during chat in Visitor Monitor. 
| `custom_variable` | the information of [custom variables](#details-of-a-custom-variable) captured from the web page visitors viewed.
| `start_time` | the time when the chat started
| `waiting_time` | the amount of time a visitor has been waiting before his/her chat request was accepted
| `end_time` | the time when the chat ended
| `chat_transcript` | the content of the chat
| `attachment` | the files the agents send to the visitor or vice versa as well as the screenshots sent to the operator by the visitor through Comm100 Screen Capture. Attachment contains `name` and `uri`
| `note_attachment` | the files the agents send as the note attachment. Attachment contains `name` and `uri`
| `rating` | the rating on the agents submitted by the visitor
| `rating_comment` | the comment on agents' customer service submitted by the visitor
| `operator_comment` | the notes added for this chat by the agent
| `wrap_up` | the wrap-up information for this chat submitted by the agent 

### Details of a Custom Field
| Property | Description
| --- | ---
| `id` | the id of the custom field
| `name` | the name of the custom field
| `value` | the value of the custom field

### Details of a Custom Variable
| Property | Description
| --- | ---
| `name` | the name of the custom variable
| `value` | the value of the custom variable

### Details of a operator
| Property | Description
| --- | ---
| `id` | the id of the operator
| `display_name` | the name of the operator
| `email` | the email of the operator


### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/chats \
    ?date_from=2013-6-27&date_to=2013-9-27&keywords=comm100" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
{ 
    "chats": [
        { 
            "attachment": { 
                "name": "screen_capture.png",
                "uri": "http://hosted.comm100.com/livechatreport/download.ashx?siteId=10014&downloadtype=chatattachment&id=3679"
            },
            "chat_transcript": "Operator Henry - Comm100 has joined the chat.\n[19:16:06] Henry - Comm100: Hi Allon, this is Henry. How may I help you?\n....... ",
            "company": "comm100",
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
            "custom_variable": [
                { 
                    "name": "user_login",
                    "value": "facebook"
                },
                { 
                    "name": "have_sales",
                    "value": "yes"
                }
            ],
            "department": "livechat",
            "email": "allon@comm100.com",
            "end_time": "/Date(1358455857)/",
            "id": "7b1a47f5-6dd5-4d29-a14d-725effdad6bd",
            "name": "Allon",
            "operator_comment": "paid",
            "operators": "henry",
            "phone": "1-877-305-0464",
            "product_service": "livechat",
            "rating": "1",
            "rating_comment": "very good",
            "start_time": "/Date(1358453897)/",
            "waiting_time": "10s",
            "wrap_up": {
                "category": "Suggestion",
                "comment": "paid",
                "fields": [],
                "time": "/Date(1358456079)/"
            }
        }
        ...
    ],
    "pages": 3,
    "total": 27
}
```

## Get a Single Chat
Get a specific chat by id.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/chats/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id`| the id of the chat

### Response
The [detail](#details-of-a-chat) of the chat will be returned.

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/chats/7b1a47f5-6dd5-4d29-a14d-725effdad6bd" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
{
    "attachment": { 
        "name": "screen_capture.png",
        "uri": "http://hosted.comm100.com/livechatreport/download.ashx?siteId=10014&downloadtype=chatattachment&id=3679"
    },
    "chat_transcript": "Operator Henry - Comm100 has joined the chat.\n[19:16:06] Henry - Comm100: Hi Allon, this is Henry. How may I help you?\n....... ",
    "company": "comm100",
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
    "custom_variable": [
        { 
            "name": "user_login",
            "value": "facebook"
        },
        { 
            "name": "have_sales",
            "value": "yes"
        }
    ],
    "department": "livechat",
    "email": "allon@comm100.com",
    "end_time": "/Date(1358455857)/",
    "id": "7b1a47f5-6dd5-4d29-a14d-725effdad6bd",
    "name": "Allon",
    "operator_comment": "paid",
    "operators": "henry",
    "phone": "1-877-305-0464",
    "product_service": "livechat",
    "rating": "1",
    "rating_comment": "very good",
    "start_time": "/Date(1358453897)/",
    "waiting_time": "10s",
    "wrap_up": {
        "category": "Suggestion",
        "comment": "paid",
        "fields": [],
        "time": "/Date(1358456079)/"
    }
}
```
