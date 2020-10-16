
  | Change Version | API Version | Change Notes | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v3 | Chatbot Message Restful API | 2020-10-15 | Davy | 

# Summary
  - Chatbot Message RESTful API
    - [session](#session)

# Authentication
## API_key Authentication
For each method call, you must use your email and API_KEY.Authentication to the API is done via HTTP Basic Auth. Provide your email as the basic auth username and API_KEY as the password. You must authenticate for API requests.

# Session
  - `POST /api/v3/bot/sessions/{sessionId}:sendMessage` - [Send Message](#send-message)

## Related Object Json Format

### ChatbotMessage
ChatbotMessage is represented as simple flat json objects with the following keys:

|Name| Type    |Mandatory | Description     | 
| - | - | - | - | 
|`type` | string | yes |it is a enum value with options: text,image,video, quickreply, button.  | 
|`content` | object | yes |response's content.<br/>when type is text, it represents [TextResponse](#textresponse);<br/>when type is image ,it represents [ImageResponse](#imageresponse);<br/>when type is video, it represents [VideoResponse](#videoresponse);<br/>when type is quickreply, it represents [QuickReplyResponse](#quickreplyresponse);<br/>when type is button, it represents [ButtonResponse](#buttonresponse);<br/>|
|`disableChatInputArea` | bool | no | default value is `false` |

#### TextResponse
  TextResponse is represented as simple flat JSON objects with the following keys:

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `message` | string  | yes | message of the response |
  | [links](#link) | array of [link](#link)  | yes | links in the text |  

#### Link
  Link is represented as simple flat JSON objects with the following keys:

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `type` | enums | yes | it is an enum value with options: hyperlink and goToIntent |
  | `startPosition` | int | yes | start index of text which contains link info |
  | `endPosition` | int | yes | end index of text which contains link info |
  | `url` | string | no | url of the web resource,including web forms,articles,images,video,etc. When the type is hyperlink, it is mandatory, otherwise not |
  | `intentId` | string| no | id of the intent in the intent link. When the type is goToIntent, it is mandatory, otherwise not  |
  | `displayText` | string | no | display text of goToIntent link. When the type is goToIntent, it is mandatory, otherwise not |
  | `openIn` | enums | no | it is an enum value with options: currentWindow,sideWindow and newWindow. This field defined the way that webpage will be opened. When the type is goToIntent, it is mandatory, otherwise not |

#### ImageResponse
  ImageResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `description` | string  | yes | description of the image, it will be displayed as the alternative text of the image |
  | `url` | string  | yes | url of the image |

#### VideoResponse
  VideoResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `url` | string  | yes | url of the video |
  
#### QuickReplyResponse
  QuickReplyResponse is represented as simple flat JSON objects with the following keys:

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `message` | string  | yes | message of the response|
  | `items`| array of [QuickReplyItem](#quickreplyitem)  | yes | |  

#### QuickReplyItem
  QuickReplyItem is represented as simple flat JSON objects with the following keys: 

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `type` | string  | yes | it is an enum value with options: goToIntent, contactAgent and text|
  | `text`| string  | yes | text on quick reply |
  | `intentId`| string  | no  | id of the intent which current quickreply point to. When the type is goToIntent, it is mandatory, otherwise not |  

#### ButtonResponse
  ButtonResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `message` | string  | yes | message of the response|
  | `items`| array of [ButtonItem](#buttonItem)  | yes |  |  

#### ButtonItem
  ButtonItem is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `type` | string  | yes | it is an enum value with options: hyperlink,webview and goToIntent|
  | `text`| string  | yes | text on button |
  | `url` | string | no | url of the web resource,including web forms,articles,images,video,etc. When the type is hyperlink or webview, it is mandatory, otherwise not |
  | `intentId`| string  | no | id of the intent which current quickreply point to. When the type is goToIntent, it is mandatory, otherwise not |
  | `openIn` | enums | no | it is an enum value with options: currentWindow,sideWindow and newWindow. This field defined the way that webpage will be opened. When the type is hyperlink, it is mandatory, otherwise not |
  | `webviewOpenStyle` | enums | no | it is an enum value with options: compact, tall and full. This field defined the way that webview will be opened. When the type is webview, it is mandatory, otherwise not |


## Endpoints
### Send Message
`POST /api/v3/bot/sessions/{sessionId}:sendMessage`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat |

Request body

The request body contains data with the follow structure: 

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `botId` | int  | yes | | id of the chatbot|
  | `visitorId` | Guid  | yes | | id of the visitor  |
  | `messages` | [ChatbotMessage](#ChatbotMessage)[] | yes | | max 10 messages in the list and only 1 quickreply type message in the list  |


example:
```Json 
  {
    "botId": 257,
    "visitorId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "messages": [
        {
            "type": "text",
            "content": {
                "message": "this is a plain message"
            },
            "disableChatInputArea": true
        },
    ]
  }
```

#### Response
HTTP/1.1 204 No Content


#### Example
Using curl
```
curl -H "Authorization: Basic test@comm100.com:e07cce30b1b145e99049bf201f302239"
-H "Content-Type: application/json" -d '{
    "botId": 257,
    "visitorId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "messages": [
        {
            "type": "text",
            "content": {
                "message": "this is a plain message"
            },
            "disableChatInputArea": true
        },
    ]
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:sendMessage
```
Response
```Json
  HTTP/1.1 204 No Content
  Content-Type:  application/json
  
```

  #### ChatbotMessage List Sample Json
  ```json
   [
        {
            "type": "text",
            "content": {
                "message": "this is a plain message"
            },
            "disableChatInputArea": true
        },
        {
            "type": "text",
            "content": {
                "message": "this is a web link message",
                "link": [{
                    "type": "hypelink",// hypelink or goToIntent.
                    "startPosition": 10,
                    "endPosition": 17,
                    "ifPushPage": true,
                    "url": "www.test.com",
                    "openIn": "currentWindow"// currentWindow, sideWindow or newWindow.
                }]
            },
            "disableChatInputArea": true
        },
        {
            "type": "text",
            "content": {
                "message": "this is a go to intent message",
                "link": [{
                    "type": "goToIntent",
                    "startPosition": 10,
                    "endPosition": 17,
                    "intentId": "test-intent-id",
                    "displayText": "test-displayText"
                }]
            },
            "disableChatInputArea": true
        },
        {
            "type": "image",
            "content": {
                "description": "description of the image",
                "url": "www.test.com/test-image.jpg"
            },
            "disableChatInputArea": true
        },
        {
            "type": "video",
            "content": {
                "url": "www.test.com/test-video.jpg"
            },
            "disableChatInputArea": true
        },        
        {
            "type": "button",
            "content": {
                "message": "this is a button response",
                "items": [
                    {
                        "type": "goToIntent",// goToIntent, hyperlink or webview.
                        "text": "click to trigger test-intent-name",
                        "intentId": "test-intent-id"
                    },
                    {
                        "type": "hyperlink",
                        "text": "click to open this url in web page",
                        "url": "www.test.com",
                        "openIn": "currentWindow"
                    },
                    {
                        "type": "webview",
                        "text": "click to open this url in web view",
                        "url": "www.test.com",
                        "webviewOpenStyle": "full"
                    }
                ]
            },
            "disableChatInputArea": true
        }, {
            "type": "quickreply",
            "content": {
                "message": "this is a quick reply response",
                "items": [
                    {
                        "type": "goToIntent",// goToIntent, contactAgent or text.
                        "name": "click to trigger test-intent-name",
                        "intentId": "test-intent-id"
                    },
                    {
                        "type": "contactAgent",
                        "name": "click to contact agent"
                    }
                ]
            },
            "disableChatInputArea": true
        },
    ]
```
