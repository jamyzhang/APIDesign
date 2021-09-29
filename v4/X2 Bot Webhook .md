

## X2 Bot Webhook

When using webhook action in bot intent answers, we will pass data to this webhook, You need process data within this webhook and give us a formatted response so that we can give an answer to visitor base on your response through live chat or other social channels.

  #### Request Data Format

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `eventType` | string | yes | it is a enum value with options: `questionAsked`, `intentClicked`,`locationShared`,`formSubmitted`,`chatJoined` |  
  | `question` | string | no | the question that Bot received from visitor.  |
  | `channel` | string  | | e.g.,  `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `chatId` | GUID | yes | id of the chat or ticket |
  | `ChatId` | GUID | yes | <font color=red><b>Deprecated</b></font>, use chatId instead |
  | `botId` | GUID | yes | id of the chat |
  | `BotId` | GUID | yes | <font color=red><b>Deprecated</b></font>, use botId instead |
  | `visitorId` | GUID | yes | id of the visitor |
  | `VisitorId` | GUID | yes | <font color=red><b><font color=red><b>Deprecated</b></font></b></font>, use visitorId instead |
  | `campaignId` | GUID | no | id of the campaign in comm100 live chat |
  | `visitorInfo` | [VisitorInfo](#visitorinfo) | no | the visitor information with pre-chat fields, custom variables |
  | `Visitor` | [VisitorInfo](#visitorinfo) | no | <font color=red><b>Deprecated</b></font>, use visitorInfo instead |
  | `intentName` | string | no | the name of the intent.  |
  | `intentId` | Guid | no | the intent id that Bot received from visitor click the intent link or intent button or quickreply.  |
  | `IntentId` | Guid | no | <font color=red><b>Deprecated</b></font>, use intentId instead |
  | `FormValues` | array of [Field Value](#field-value) | no | <font color=red><b>Deprecated</b></font>, use variables instead |
  | `variables` | object | no | The variable data that Bot collected |
  | `additionalPostBody` | object | no | additional data |
  
 #### Request Data Sample Json
  ```json
{
    "eventType": "questionAsked",
    "question": "qqqwwe",
    "channel": "Live Chat",
    "chatId": "1f6ed431-c742-cb32-ae67-db7703e67ec2",
    "ChatId": "1f6ed431-c742-cb32-ae67-db7703e67ec2",
    "botId": "8bf93242-a0d4-4019-bc8f-8954d8928faf",
    "BotId": "8bf93242-a0d4-4019-bc8f-8954d8928faf",
    "visitorId": "00000000-0000-0000-0000-000000000000",
    "VisitorId": "00000000-0000-0000-0000-000000000000",
    "campaignId": "00000000-0000-0000-0000-000000000000",
    "visitorInfo": {
        "visitorGuid": "00000000-0000-0000-0000-000000000000",
        "longitude": 0,
        "latitude": 0,
        "pageViews": 0,
        "chats": 0,
        "department": "00000000-0000-0000-0000-000000000000",
        "firstVisitTime": "0001-01-01T00:00:00Z",
        "status": 0,
        "visitTime": "0001-01-01T00:00:00Z",
        "visits": 0,
        "campaignId": "00000000-0000-0000-0000-000000000000",
        "customFields":[],
        "customVariables":[
            {
                "name":"host ",
                "value":"conditiondash.testing.comm100dev.io"
            },
            {
                "name":"sunny1",
                "value":"Value is sunny1"
            }
        ],
        "channelAccountId": "00000000-0000-0000-0000-000000000000"
    },
    "Visitor": {
        "visitorGuid": "00000000-0000-0000-0000-000000000000",
        "longitude": 0,
        "latitude": 0,
        "pageViews": 0,
        "chats": 0,
        "department": "00000000-0000-0000-0000-000000000000",
        "firstVisitTime": "0001-01-01T00:00:00Z",
        "status": 0,
        "visitTime": "0001-01-01T00:00:00Z",
        "visits": 0,
        "campaignId": "00000000-0000-0000-0000-000000000000",
        "customFields":[],
        "customVariables":[
            {
                "name":"host ",
                "value":"conditiondash.testing.comm100dev.io"
            },
            {
                "name":"sunny1",
                "value":"Value is sunny1"
            }
        ],
        "channelAccountId": "00000000-0000-0000-0000-000000000000"
    },
    "IntentId": "00000000-0000-0000-0000-000000000000",
    "intentId": "00000000-0000-0000-0000-000000000000",
    "intentName": "",
    "FormValues": [
        {
            "label": "pizza-thickness",
            "value": "thin crust"
        },
        {
            "label": "pizza-size",
            "value": "Large"
        },
        {
            "label": "sys-any",
            "value": "gift box"
        },
        {
            "label": "pizza-flavor",
            "value": "Cheese"
        }
    ],
    "variables": {
        "previousIntentId": "7737e334-ae46-4731-b103-b6f03b7b2911",
        "previousIntentName": "haha",
        "currentIntentName": "pizza order",
        "{!Variable.pizza-size}": "Large",
        "{!Variable.sys-any}": "gift box",
        "{!Variable.pizza-thickness}": "thin crust",
        "{!Variable.pizza-flavor}": "Cheese"
    },
    "additionalPostBody": {
        "additional body": "test bbbb"
    }
}
```


 

 #### Response Data Format

  Array of [Response](#response) 
  An asnwer is composed of one or more responses, regardless of their type. 

  Here is a sample of response json: [sample](#response-sample-json)

  
### Bot webhook Related Object Json Format

#### Response
Response is represented as simple flat json objects with the following keys:

|Name| Type    |Mandatory | Description     | 
| - | - | - | - | 
|`type` | string | yes |it is a enum value with options: text,image,video, quickreply, button  | 
|`content` | object | yes |response's content.<br/>when type is text, it represents [TextResponse](#textresponse);<br/>when type is image ,it represents [ImageResponse](#imageresponse);<br/>when type is video, it represents [VideoResponse](#videoresponse);<br/>when type is quickreply, it represents [QuickReplyResponse](#quickreplyresponse);<br/>when type is button, it represents [ButtonResponse](#buttonresponse);<br/>| 
|`disableChatInputArea` | bool | no | default value is `false` |
|`delayTime` | decimal | 1 | how many seconds delay to show  |

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
  | `type` | enums | yes | it is an enum value with options: hyperlink |
  | `startPosition` | int | yes | start index of text which contains link info |
  | `endPosition` | int | yes | end index of text which contains link info |
  | `url` | string | no | url of the web resource,including web forms,articles,images,video,etc. When the type is hyperlink, it is mandatory, otherwise not |  
  | `ifPushPage` | bool | no | auto open url in the side window |   
  | `openIn` | enums | no | it is an enum value with options: currentWindow,sideWindow and newWindow. This field defined the way that webpage will be opened. |

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
  | `url` | string  | yes | url of the YouTube video |
  
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
  | `intentId`| GUID  | no  | id of the intent which current quickreply point to. When the type is goToIntent, it is mandatory, otherwise not |  

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
  | `intentId`| GUID  | no | id of the intent which current quickreply point to. When the type is goToIntent, it is mandatory, otherwise not |
  | `openIn` | enums | no | it is an enum value with options: currentWindow,sideWindow and newWindow. This field defined the way that webpage will be opened. When the type is hyperlink, it is mandatory, otherwise not |
  | `webviewOpenStyle` | enums | no | it is an enum value with options: compact, tall and full. This field defined the way that webview will be opened. When the type is webview, it is mandatory, otherwise not |

#### Field Value

  Field Value is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `name` | string  | yes | name of the form field item |
  | `value` | string  | yes | value of the form field item |
  
#### VisitorInfo

  Visitor info is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `visitorGuid` | GUID | yes | id of the visitor |
  | `name` | string | yes | name of the visitor |
  | `language` | string | yes | language |
  | `email` | string | yes | email of the visitor |
  | `phone` | string | yes | phone of the visitor |
  | `longitude` | float | no | longitude of the visitor location |
  | `latitude` | float | no | latitude of the visitor location |
  | `country` | string | yes | the country of the visitor |
  | `state` | string | yes | state of the visitor |
  | `city` | string | yes | the city of the visitor |
  | `company` | string | yes | the company of the visitor |
  | `department` | int | yes | department of the visitor |
  | `browser` | string | yes | visitor use browser type |
  | `currentBrowsing` | string | yes | page of the current browsing |
  | `referrerUrl` | string | yes | referrer url |
  | `landingPage` | string | yes | the page of login |
  | `searchEngine` | string | yes | search engine |
  | `keywords` | string | yes | search engine key |
  | `operatingSystem` | string | yes | operating system of the visitor |
  | `ip` | string | yes | ip of the visitor |
  | `flashVersion` | string | yes | version of the flash |
  | `productService` | string | yes | product service |
  | `screenResolution` | string | yes | screen resolution |
  | `timeZone` | string | yes | time zone of the visitor |
  | `firstVisitTime` | string | yes | the time of first visit |
  | `visitTime` | string | yes | time of the visitor |
  | `visits` | integer | yes | count of the visited |
  | `chats` | integer | yes | count of chat |
  | `pageViews` | integer | yes | count of the visited |
  | `status` | string | yes | status of the visitor |
  | `customFields` | [CustomFields](#customfields) | yes | an array of custom fields |
  | `customVariables` | [CustomVariables](#customvariables) | yes | an array of custom variables |

#### CustomFields

  Custom fields is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `name` | string  | yes | name of the field |
  | `value` | string  | yes | value of the field |

#### CustomVariables

  Custom variables is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `name` | string  | yes | name of the variable |
  | `value` | string  | yes | value of the variable |

  #### Response Sample Json
  ```json
   [
        {
            "type": "text",
            "content": {
                "message": "this is a plain message"
            }
        },
        {
            "type": "text",
            "content": {
                "message": "this is a web link message",
                "link": [{
                    "type": "hypelink",
                    "startPosition": 10,
                    "endPosition": 17,
                    "ifPushPage": true,
                    "url": "www.test.com",
                    "openIn": "currentWindow"// currentWindow, sideWindow or newWindow.
                }]
            }
        },        
        {
            "type": "image",
            "content": {
                "description": "description of the image",
                "url": "www.test.com/test-image.jpg"
            }
        },
        {
            "type": "video",
            "content": {
                "url": "https://youtu.be/pAzpsNbJzVY"
            }
        },
        {
            "type": "quickreply",
            "content": {
                "message": "this is a quick reply response",
                "items": [
                    {
                        "type": "goToIntent",// goToIntent, contactAgent or text.
                        "text": "click to trigger test-intent-name",
                        "intentId": "d3f5b968-ad51-42af-b759-64c0afc40b84",
                    },
                    {
                        "type": "contactAgent",
                        "text": "click to contact agent"
                    }
                ]
            }
        },
        {
            "type": "button",
            "content": {
                "message": "this is a button response",
                "items": [
                    {
                        "type": "goToIntent",// goToIntent, hyperlink or webview.
                        "text": "click to trigger test-intent-name",
                        "intentId": "d3f5b968-ad51-42af-b759-64c0afc40b84",
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
            }
        }        
    ]
```
