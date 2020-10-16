

## Third-Party Bot Webhook Event

 ### Chat Joined Event

When we received a response whose event type is chatJoined, we will pass this action to this webhook, You need process this action within this webhook and give us a formatted response so than we can give an answer to visitor base on your response through live chat.

  #### Request Data Format

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `event` | string | yes | it is a enum value with options: questionAsked / intentClicked / locationShared / formSubmitted / chatJoined |   
  | `chatId` | string | yes | id of the chat |
  | `campaignId` | int | yes | id of the campaign in comm100 live chat |
  | `visitorInfo` | [VisitorInfo](#visitorinfo) | yes | the visitor information with pre-chat fields, custom variables |
  
 #### Response Data Format

|Name| Type    |Mandatory | Description     | 
| - | - | - | - | 
|`answer` | array of [Response](#response) | yes | An asnwer is composed of one or more responses, regardless of their type.  | 

Here is a sample of response json: [sample](#response-sample-json)

### Question Asked Event

When visitor sent a message through live chat, we will pass this message and other information we defined to this webhook. 
You need process this message and information within this webhook using your own bot engine and give us a formatted 
response so that we can give visitor an answer base on your response through live chat. 

  #### Request Data Format

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `event` | string | yes | it is a enum value with options: questionAsked / intentClicked / locationShared / formSubmitted / chatJoined |   
  | `chatId` | string | yes | | id of the chat |
  | `campaignId` | int | yes | id of the campaign in comm100 live chat |
  | `question` | string | yes | the question that Bot received from visitor.  |
  | `visitorInfo` | [VisitorInfo](#visitorinfo) | yes | the visitor information with pre-chat fields, custom variables |

  #### Response Data Format

The same as Chat Joined Event
  
  ### Intent Clicked Event

If the answer we give to visitor contains link/button/quickreply which point to an intent, when visitor click this link/button/quickreply, we will pass this action to this webhook with intent id and other information we defined. You need process this action within this webhook and give us a formatted response so than we can give an answer to visitor base on your response through live chat.

  #### Request Data Format

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `event` | string | yes | it is a enum value with options: questionAsked / intentClicked / locationShared / formSubmitted / chatJoined |   
  | `chatId` | string | yes | | id of the chat |
  | `campaignId` | int | yes | id of the campaign in comm100 live chat |
  | `intentId` | string | yes | the intent that visitor clicked. |
  | `visitorInfo` | [VisitorInfo](#visitorinfo) | yes | the visitor information with pre-chat fields, custom variables |

  #### Response Data Format

The same as Chat Joined Event
  
  ### Location Shared Event

When we received a response whose event type is locationShared, we will display an webview for visitor to collect his/her location, when visitor shared his/her location to us, we will pass these information to this webhook and you can give us a response base on nformation we provided through this webhook.

  #### Request Data Format

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `event` | string | yes | it is a enum value with options: questionAsked / intentClicked / locationShared / formSubmitted / chatJoined |   
  | `chatId` | string | yes | | id of the chat |
  | `campaignId` | int | yes | id of the campaign in comm100 live chat |
  | `intentId` | string | yes |  the intent that required visitor location. |
  | `visitorInfo` | [VisitorInfo](#visitorinfo) | yes | the visitor information with pre-chat fields, custom variables and also the visitor location |
  
  #### Response Data Format

The same as Chat Joined Event
  
  ### Form Submitted Event

When we received a response whose event type is formSubmitted, we will display an webview for visitor to collect more information about him/her, when visitor filled out webview, we will pass these information to this webhook, and you can give us a response based on information we provided through this webhook.

  #### Request Data Format

  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `event` | string | yes | it is a enum value with options: questionAsked / intentClicked / locationShared / formSubmitted / chatJoined |   
  | `chatId` | string | yes | | id of the chat |
  | `campaignId` | int | yes | id of the campaign in comm100 live chat |
  | `formValues` | array of [Field Value](#form-value) | yes |  |
  | `visitorInfo` | [VisitorInfo](#visitorinfo) | yes | the visitor information with pre-chat fields, custom variables |
  
  #### Response Data Format

The same as Chat Joined Event
  
### Third-Party Bot webhook Related Object Json Format

#### Response
Response is represented as simple flat json objects with the following keys:

|Name| Type    |Mandatory | Description     | 
| - | - | - | - | 
|`type` | string | yes |it is a enum value with options: text,image,video, quickreply, button, location and form.  | 
|`content` | object | yes |response's content.<br/>when type is text, it represents [TextResponse](#textresponse);<br/>when type is image ,it represents [ImageResponse](#imageresponse);<br/>when type is video, it represents [VideoResponse](#videoresponse);<br/>when type is quickreply, it represents [QuickReplyResponse](#quickreplyresponse);<br/>when type is button, it represents [ButtonResponse](#buttonresponse);<br/>when type is location, it should be null;<br/>when type is form, it represents [CollectFormValueResponse](#collectformvalueresponse)| 

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


#### CollectFormValueResponse
  CollectFormValueResponse is represented as simple flat JSON objects with the following keys:  
  
  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `message` | string  | yes | message of the response which will be displayed above the button|
  | `text` | string  | yes | text on the button which can be clicked to open a webview to collection information|
  | `ifNeedConfirm` | bool  | yes | whether need the visitor to double confirm the form field values |
  | `fields` | array of [Field](#field)  | yes | fields displayed on webview|

#### Field

  Field is represented as simple flat JSON objects with the following keys:  
  
  | Name | Type | Mandatory | Description |    
  | - | - | - | - | 
  | `name` | string  | yes | name of the field|
  | `value` | string  | yes | value of the field item |
  | `type` | string  | yes | it is an enum value with options: text, textArea, radio, checkBox, dropDownList and checkBoxList |
  | `ifRequired` | bool  | yes | when it is true, visitor have to input a value in the field before submit |
  | `ifMasked` | bool  | yes | when it is true, information collected will replaced by * in chat log for security |
  | `options` | an array of string  | no | values displayed in the field when type is dropDownList, checkBoxList for visitor to choose. When the type is dropDownList or checkBoxList, it is mandatory, otherwise not |
 
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
  | `id` | integer | yes | id of the visitor |
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
  | `id` | integer  | yes | id of the field |
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
                    "type": "hypelink",// hypelink or goToIntent.
                    "startPosition": 10,
                    "endPosition": 17,
                    "ifPushPage": true,
                    "url": "www.test.com",
                    "openIn": "currentWindow"// currentWindow, sideWindow or newWindow.
                }]
            }
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
                "url": "www.test.com/test-video.jpg"
            }
        },
        {
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
            }
        },
        {
            "type": "location",
            "content": null
        },
        {
            "type": "form",
            "content": {
                "text": "book ticket",
                "message": "please fill the form below",
                "ifNeedConfirm": true,
                "fields": [
                    {
                        "type": "text",// text, textArea, radio, checkBox, dropDownList or checkBoxList
                        "name": "field-1",
                        "value": "field-value-1",
                        "ifRequired": true,
                        "ifMasked": true
                    },
                    {
                        "type": "dropDownList",
                        "name": "field-2",
                        "value": "field-value-2",
                        "ifRequired": true,
                        "ifMasked": true,
                        "options": [
                            "value": "field-1-value",
                            "value": "field-2-value",
                            "value": "field-3-value"
                        ]
                    }
                ]
            }
        }
    ]
```
