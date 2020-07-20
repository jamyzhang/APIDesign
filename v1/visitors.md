# Visitors
What can you do with Visitor?
Comm100 Live Chat API enables you to do the followings with the Visitor resource:

| Method | Name | Path
| --- | --- | ---
| GET | [Get List of Visitors](#get-list-of-visitors) | /api/v1/livechat/visitors
| GET | [Get Chatting Visitors](#get-chatting-visitors) | /api/v1/livechat/visitors/chatting
| GET | [Get a Single Visitor](#get-a-single-visitor) | /api/v1/livechat/visitors/{id}
| PUT | [Update Custom Variables](#update-custom-variables) | /api/v1/livechat/visitors/{id}

## Get List of Visitors

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/visitors
```

### Response
Returns a list of visitors.

### Details of a Visitor
| Property | Description
| --- | ---
| `id` | the id of the visitor
| `name` | the name of the visitor
| `email` | the email of the visitor
| `status` | the [status](#visitor-status) of the visitor
| `phone` | the phone of the visitor
| `company` | the company of the visitor
| `first_visit_time` | the time the visitor first visited a web page pasted with Comm100 Live Chat code
| `visit_time` | the starting time when this visitor visits your website this time
| `city` | the city of the visitor
| `state` | the state of the visitor
| `country` | the country of the visitor
| `ip` | the ip of the visitor
| `language` | the language the visitor is using
| `screen_resolution` | the screen resolution of the visitor's device
| `time_zone` | the time zone of the visitor
| `flash_version` | the flash version of the browser the visitor is using
| `operating_system` | the operating system of the visitor's device
| `browser` | the browser the visitor is using
| `custom_fields` | the values of [custom fields](#details-of-a-custom-field) entered by visitors in the pre-chat window. Operators can also update the value(s) during chat in Visitor Monitor.
| `product_service` | the product/service the visitor selected in the pre-chat window. Operators can also update the value while chatting with visitors.
| `department` | the department the visitor selected in the pre-chat window. Operators can also update the value while chatting with visitors.
| `custom_variable` | the information of [custom variables](#details-of-a-custom-variable) captured from the web page visitors viewed.
| `current_browsing` | the page the visitor is currently looking at
| `visits` | the total times of visits a visitor has made on your website from the first time to present
| `chats` | the total times of chats a visitor has made on your website from the first time to present
| `referrer_url` | the URL of the page from which a visitor comes to your website
| `search_engine` | the search engine the visitor used to search for your website
| `keywords` | the keywords the visitor used to search for your website
| `landing_page` | the title and URL of the first page of your website the visitor visited
| `page_views` | the total number of web pages the visitor viewed on your website

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

### Visitor Status
| Enumeration Value | Description
| --- | ---
| `0` | waiting for chat
| `1` | voice chatting
| `2` | chatting
| `3` | pre-Chat
| `4` | manually Invited
| `5` | auto invited
| `6` | offline message
| `7` | refused by operator
| `8` | refused by visitor
| `9` | chat ended
| `10` | in site
| `11` | out of site

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/visitors" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    { 
        "browser": "Google Chrome 29.0.1547.76",
        "chats": 2,
        "city": "Vancouver",
        "company": "Comm100",
        "country": "Canada",
        "current_browsing": "http://www.comm100.com",
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
        "first_visit_time": "/Date(13584868423)/",
        "flash_version": "11.8.800.170",
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "ip": "192.168.8.1",
        "keywords": "comm100",
        "landing_page": "http://www.comm100.com/livechat",
        "language": "en_us",
        "name": "allon",
        "operating_system": "Windows 7",
        "page_views": 3,
        "phone": "12983782710",
        "product_service": "livechat",
        "referrer_url": "http://www.google.com/q=comm100",
        "screen_resolution": "1440*900",
        "search_engine": "Google",
        "state": "British Columbia",
        "status": 2,
        "time_zone": "UTC-08:00",
        "visit_time": "/Date(13584868542)/",
        "visits": 5
    },
    ...
]
```

## Get Chatting Visitors

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/visitors/chatting
```

### Response
A list of chatting visitors is returned. The details of every visitor is listed [here](#details-of-a-visitor).

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/visitors/chatting" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    { 
        "browser": "Google Chrome 29.0.1547.76",
        "chats": 2,
        "city": "Vancouver",
        "company": "Comm100",
        "country": "Canada",
        "current_browsing": "http://www.comm100.com",
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
        "first_visit_time": "/Date(13584868423)/",
        "flash_version": "11.8.800.170",
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "ip": "192.168.8.1",
        "keywords": "comm100",
        "landing_page": "http://www.comm100.com/livechat",
        "language": "en_us",
        "name": "allon",
        "operating_system": "Windows 7",
        "page_views": 3,
        "phone": "12983782710",
        "product_service": "livechat",
        "referrer_url": "http://www.google.com/q=comm100",
        "screen_resolution": "1440*900",
        "search_engine": "Google",
        "state": "British Columbia",
        "status": 2,
        "time_zone": "UTC-08:00",
        "visit_time": "/Date(13584868542)/",
        "visits": 5
    },
    ...
]
```

## Get a Single Visitor

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/visitors/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id`| the id of the visitor

### Response
The [details](#details-of-a-visitor) of the visitor will be returned.

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{ 
    "browser": "Google Chrome 29.0.1547.76",
    "chats": 2,
    "city": "Vancouver",
    "company": "Comm100",
    "country": "Canada",
    "current_browsing": "http://www.comm100.com",
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
    "first_visit_time": "/Date(13584868423)/",
    "flash_version": "11.8.800.170",
    "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
    "ip": "192.168.8.1",
    "keywords": "comm100",
    "landing_page": "http://www.comm100.com/livechat",
    "language": "en_us",
    "name": "allon",
    "operating_system": "Windows 7",
    "page_views": 3,
    "phone": "12983782710",
    "product_service": "livechat",
    "referrer_url": "http://www.google.com/q=comm100",
    "screen_resolution": "1440*900",
    "search_engine": "Google",
    "state": "British Columbia",
    "status": 1,
    "time_zone": "UTC-08:00",
    "visit_time": "/Date(13584868542)/",
    "visits": 5
}
```

## Update Custom Variables
Updates the value of the custom variables of a specific visitor.

### Path
```bash
PUT https://hosted.comm100.com/api/v1/livechat/visitors/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id` | the id of the visitor
| `name` | the name of the custom variable
| `value` | the value of the custom variable

### Response
The [details](#details-of-a-visitor) of the visitor is returned.

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d" \
    -X PUT -d [{"name":"user_login","value":"googleplus"},{"name":"have_sales","value":"no"}] \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "browser": "Google Chrome 29.0.1547.76",
    "chats": 2,
    "city": "Vancouver",
    "company": "Comm100",
    "country": "Canada",
    "current_browsing": "http://www.comm100.com",
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
            "value": "googleplus"
        },
        { 
            "name": "have_sales",
            "value": "no"
        }
    ],
    "department": "livechat",
    "email": "allon@comm100.com",
    "first_visit_time": "/Date(13584868423)/",
    "flash_version": "11.8.800.170",
    "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
    "ip": "192.168.8.1",
    "keywords": "comm100",
    "landing_page": "http://www.comm100.com/livechat",
    "language": "en_us",
    "name": "allon",
    "operating_system": "Windows 7",
    "page_views": 3,
    "phone": "12983782710",
    "product_service": "livechat",
    "referrer_url": "http://www.google.com/q=comm100",
    "screen_resolution": "1440*900",
    "search_engine": "Google",
    "state": "British Columbia",
    "status": 1,
    "time_zone": "UTC-08:00",
    "visit_time": "/Date(13584868542)/",
    "visits": 5
}
```