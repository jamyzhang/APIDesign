  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 3.0 | v3 | AutoCoding Update | 2020-07-29 | Davy |


# Summary
  - Chatbot
    - [session](#session)  
  - AgentAssist
    - [agent assist suggestion](#agent-assist-suggestion)


# Session
  - `POST /api/v3/bot/chatbots/{chatbotId}/sessions` - [Create session](#create-session)
  - `POST /api/v3/bot/sessions/{sessionId}:detectIntent` - [Detect intent](#detect-intent)
  - `POST /api/v3/bot/sessions/{sessionId}:triggerAnIntent` - [Trigger an intent](#trigger-an-intent)
  - `POST /api/v3/bot/sessions/{sessionId}:submitForm` - [Submit Form](#Submit-Form)
  - `POST /api/v3/bot/sessions/{sessionId}:submitAuthentication` -  [Submit Authentication](#Submit-Authentication)
  - `POST /api/v3/bot/sessions/{sessionId}:submitLocation` - [Submit Location](#submit-location)
  - `POST /api/v3/bot/sessions/{sessionId}:submitIVRKey` - [Submit IVRKey](#Submit-IVRKey)
  - `POST /api/v3/bot/sessions/{sessionId}:rate` - [Rate the bot answer as helpful or not helpful](#rate-the-bot-answer-as-helpful-or-not-helpful)

## Related Object Json Format

### ChatbotSession Object
  ChatbotSession Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  | `id` | Guid  | | sessionId |
  | `channel` | string  | | e.g.,  `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `IVR` |
  | `message` |  [ChatbotMessage](#ChatbotMessage-Object) Object |  |  |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  |   |  |

### ChatbotSessionContext Object
  ChatbotSessionContext Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description     | 
  | - | - | :-: | - |   
  | `chatbotId` | Guid  | | chatbotId |
  | `currentIntentId` | Guid  | |  |
  | `authentication` | string  | | authentication data |
  | `location` | string  | | the longitude and latitude of the location, e.g. "-39.900000,116.300000" |
  | `formValues` | [FieldValue](#FieldValue-object)[] |  | an array of [FieldValue](#FieldValue-object) objects |
  | `isFormSubmitted` | bool  | false |  |
  | `latestMessage` | [ChatbotMessage](#ChatbotMessage-Object) Object  | |  |
  | `customData` | Object  |   | Custom data |

### FieldValue Object
FieldValue is represented as simple flat json objects with the following keys:

|Name| Type|  Default |  Description     |
| - | - | :-: |  - | 
|`name` | string |  | the name of a field in a form. |
|`value` | string |  | the value of a field. |


### ChatbotMessage Object
  ChatbotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  | `id` | Guid  |  | the unique id of the response |
  | `visitorQuestion` | string  |  | text |
  | `type` | string  |  | type of the response,including `greetingMessage`、 `highConfidenceAnswer`、`possibleAnswer`、`noAnswer`,`notHelpfulMessage`, `locationRequest`,`formRequest`,`authenticationRequest`,`prompt` |
  | `content` | object |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer-object); when type is `possibleAnswer`,it represents [PossibleAnswer](#PossibleAnswer-object);when type is `noAnswer`,it represents [NoAnswer](#NoAnswer-object);when type is `greetingMessage`,it represents [GreetingMessage](#GreetingMessage-Object); when type is `authenticationRequest`, it represents [AuthenticationRequest](#AuthenticationRequest-Object);when type is `locationRequest`, it represents [LocationRequest](#LocationRequest-Object);when type is `formRequest`, it represents [FormRequest](#FormRequest-Object);when type is `prompt`, it represents [Prompt](#Prompt-Object);when type is `notHelpfulMessage`, it represents [NotHelpfulMessage](#NotHelpfulMessage-Object);|
  | `disableChatInputArea` | bool  | false | Only available when channel is  `Live Chat`. |
  | `smartTriggerActions` | [SmartTriggerAction](#smart-trigger-action-object)[] |  | an array of [SmartTriggerAction](#smart-trigger-action-object) objects. |


###  Smart Trigger Action Object
  Smart Trigger Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |
  | - | - | :-: | - |
  | `type` | string |  | the type of the action. enum:[`sendNotification`,`autoMonitor`,`transferChat`,`changeAssignee`,`addToSegment`]|
  | `isEnabled` | bool | false | if an action is enabled. |  
  | `agentOfflineMessage` | string | | agent offlineMessage prompt message |
  | `targetType` | string |  | the trigger action target type. enum: `department`, `agent`, `segment`. |
  | `selectedDepartments` | Guid[] |  | Only available when targetType is  `department`.  |
  | `selectedAgents` | Guid[] |  | Only available when targetType is  `agent`.  |
  | `segmentId` | Guid  |  | Only available when targetType is  `segment`. |


### GreetingMessage Object
  GreetingMessage is represented as simple flat json objects with the following keys:

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  |`responses`| [ChatbotResponse](#Chatbot-Response-Object)[] | | an array of [ChatbotResponse](#Chatbot-Response-Object) object. |

### HighConfidenceAnswer Object

  HighConfidenceAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - |  
  | `responses`| [ChatbotResponse](#Chatbot-Response-Object)[] |  | an array of [ChatbotResponse](#Chatbot-Response-Object) object. |
  | `intentId` | Guid  | | id of the matched intent |
  | `intentName` | string  |  | name of the matched intent |
  | `score` | float  |  | the score of the intent matched, the value is beteween 0.0 and 100.0 |

### PossibleAnswer Object

  PossibleAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - | 
  | `message` | string | | Text of the Possible Answer message | 
  | `audio` | string |  | base64 string, convert the message text to speech |  
  | `intents` | [IntentScore](#IntentScore-object)[]  || an array of [IntentScore](#IntentScore-object)   | 
  | `messageAfterSeveralConsecutivePossibleAnswers` | [MessageAfterSeveralConsecutivePossibleAnswers](#MessageAfterSeveralConsecutivePossibleAnswers-object)  || | 


### MessageAfterSeveralConsecutivePossibleAnswers Object

  MessageAfterSeveralConsecutivePossibleAnswers is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  |`message` | string |  | text of the message  |
  |`audio` | string |  | base64 string, convert the message text to speech | 
  | `ifIncludeContactAgentOption` | bool  |  |  |

### IntentScore Object

  IntentScore is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  |`id` | Guid || id of the intent  | 
  |`name` | string | | name of the intent |  
  | `score` | float  |  | the score of the intent matched, value is between 0.0 and 100.0 |

### NoAnswer Object

  NoAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  |`message` | string |  | text of the No Answer message  |
  |`audio` | string |  | base64 string, convert the message text to speech | 
  | `intentId` | Guid  |  | id of the matched intent |
  | `intentName` | string  |   | name of the matched intent |
  | `score` | float  | | the score of the intent matched, the value is beteween 0.0 and 100.0 |  
  | `ifIncludeContactAgentOption` | bool  |  |  |


### AuthenticationRequest Object

  AuthenticationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `signInMessage` | string  |  | message of the sign in |
  | `audio` | string |  | base64 string, convert the signInMessage text to speech |   
  | `signInButtonText` | string  |  | text of the sign in link |
  | `signInURL` | string  |  | url of the sign in |


### LocationRequest Object

  LocationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `message` | string  |  | message of the sign in |
  | `buttonText` | string  |  | text of the sign in link |


### Prompt Object

  Prompt is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  |`question` | string | | |
  | `audio` | string |  | base64 string, convert the signInMessage text to speech |   
  |`options` | string[] |  | an array of string |


### FormRequest Object
FormRequest is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string |   | A separate message which is sent before the button is sent.|
|`title` | string |  | when a button is sent to visitor, clicking this button will open a form that contains information bot wants to collect from the visitor. the title refers to the title of that form, and it is also placed on the button as a name.|
|`isConfirmationRequired` | bool |   | whether visitor needs to click confirm after filling out the information in a form.|
|`fields` | [Field](#field-object)[] | | an array of [Field](#field-object) Object |
|`submitButtonText` | string |   | |
|`cancelButtonText` | string |   | |
|`confirmButtonText` | string |   | |


### Field Object
Field is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`type` | string | | enums: `text` ,`textArea`,`radioBox` ,`checkBox` ,`dropDownList` ,`checkBoxList`,`email` type refers to the different kinds of fields which can be used in a form. |
|`name` | string |  | a field’s name in a form. |
|`defaultValue` | string | | a field’s value |
|`isRequired` | bool |  | to mark whether a field in a form is required or not. |
|`isMasked` | bool |  | if this is true, visitor information will be masked with symbols in chat logs. |
|`options` | string[] |  | an array of of string when the fieldType is `radioBox` ,`dropDownList` ,`checkBoxList`|
|`order` | integer |  | must greater than or equal 0, ascending sort |

### NotHelpfulMessage Object
NotHelpfulMessage is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string |  | text of the message  | 
|`ifIncludeContactAgentOption` | bool |  | include Contact An Agent or not . |  


### Chatbot Response Object
  Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`type` | string | | enums: `text` ,`htmlText` ,`button`,`quickReply` ,`image` ,`video` ,`ivrMenu` ,`transferCall` . |
  | `content` | object | | response's content. when type is `text` or `htmlText`, it represents [Text Response](#Text-Response-Object); when type is `image` ,it represents [ImageResponse](#ImageResponse-Object);when type is `video`, the content is the video url, it represents string; when type is `button`,it represents [ButtonResponse](#buttonresponse-object);when type is `quickReply`, it represents [QuickReplyResponse](#QuickReplyResponse); when type is `ivrMenu`, it represents [IVRMenu Response](#IVRMenu-Response-Object);when type is `transferCall`, it represents [TransferCall Response](#TransferCall-Response-Object); |
  |`disableChatInputArea` | bool | false | Only available when channel is  `Live Chat`. |
  |`delayTime` | decimal | 1 | how many seconds delay to show  |

#### Text Response Object
  Text Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`text` | string |  | string  |
  |`audio` | string | | base64 string, convert the text to speech |

### ImageResponse Object
  Image is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `name` | string  |  | name of the image |
  | `url` | string  | | url of the image | 


#### ButtonResponse Object
ButtonResponse is represented as simple flat json objects with the following keys:

|Name| Type|  Default | Description   |   
| - | - | :-: | - | 
|`message` | string |  |text above buttons,this text will be sent before buttons.  | 
|`buttons` | [Button](#button-Object)[] | |an array of [Button](#button-Object).  | 

#### Button Object
Button is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`buttonText` | string |  |text on button.  | 
|`type` | string |  |enums contain `triggerAnIntent`,`link` and `webView`,type of buttons  | 
|`linkUrl` | string |  |url of the web page you want to open.  | 
|`intentId` | Guid |  | id of the intent you choosed.  | 
|`openIn` | string |  |enums contain `sideWindow`,`newWindow`,`currentWindow`, it represents the way that a page will be opened.  | 
|`openStyle` | string | |enums contain `compact`,`tall` and `full`,it represents the size of the webview that will be opened.  |

#### QuickReplyResponse
QuickReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Default | Description     | 
| - | - | :-: | - | 
|`message` | string | |text sent before quickreplys.  |  
|`quickReplyItems` | [QuickReplyItem](#QuickReplyItem-object)[]  | |an array of [QuickReplyItem](#QuickReplyItem-Object).  | 

#### QuickReplyItem Object
|Name| Type   |Default | Description     | 
| - | - | :-: | - | 
|`type` | string |  |enum values, `triggerAnIntent`,`contactAnAgent`  | 
|`text` | string |  |text of quickreply item .  | 
|`intentId` | Guid |  |  Only available when type is  `triggerAnIntent`.  | 


#### IVRMenu Response Object
  IVRMenu Response is represented as simple flat json objects with the following keys:

  |Name| Type|  Default | Description     | 
  | - | - | :-: | - | 
  |`message` | string |  | The message sent to visitor before the options.This message will be transferred to IVR and read to visitor  |
  |`audio` | string |  | base64 string, convert the message text to speech  |  
  |`invalidInputActionRepeatTime` | integer |  | How many times will this IVR Menu repeat if there is invalid input   | 
  | `keys` | [IVRMenuKey](#IVRMenuKey-object)[]  |  | The valid keys for visitor to choose options. the key contains: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `0`, `*`, `#`. Each key can only be used once in an IVR menu. Visitor can press the key to choose the option.  |


#### IVRMenuKey Object
|Name| Type   |Default | Description     | 
| - | - | :-: | - | 
|`key` | string |  | The valid keys for visitor to choose options. the key contains: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `0`, `*`, `#`. Each key can only be used once in an IVR menu. Visitor can press the key to choose the option.  | 
|`text` | string |  |text of quickreply item .  | 
|`intentId` | Guid |  |    | 


#### TransferCall Response Object
  TransferCall Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`targetNumber` | string |  | phone number. |

## Endpoints

### Create session
`POST /api/v3/bot/chatbots/{chatbotId}/sessions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `chatbotId` | Guid | yes  |  the unique id of the bot |  

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `IVR` |
  | `id` | Guid | yes | |  id of the session, you must generate the unique sessionId  |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | no  |  |

example:
```Json 
  {
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {   
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {   
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/chatbots/a9928d68-92e6-4487-a2e8-8234fc9d1f48/sessions
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"greetingMessage",
      "content":{
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"text",
            "content": {
              "text":"You can ask any questions. If you want to know what I can help with, you can say Menu or Options",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          }
        ]
      }
    }    
  }
```

### Detect intent
`POST /api/v3/bot/sessions/{sessionId}:detectIntent`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `Voice` |
  | `textInput` | string  | no | | text |
  | `audioInput` | string  | no | | audio, when textInput have value then this is invalid. |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "textInput":"i want to buy NBN",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
  }
```
#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "textInput":"i want to buy NBN",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:detectIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"Facebook Messenger",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"i want to buy NBN",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
        "intentName": "buy nbn",
        "score": 89.25,
        "responses":[
          {
            "type":"htmlText",
            "content": {
              "text":"<div>Hi, what can i do for you?</div>",
            }
          },
          {
            "type":"image",
            "content": {
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            }
          }
        ]
      }
    }    
  }
```

### Trigger an intent
`POST /api/v3/bot/sessions/{sessionId}:triggerAnIntent`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `intentId` | Guid  | yes | | id of the intent triggered |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:triggerAnIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"Lost Card",
      "type":"authenticationRequest",
      "content":{
        "signInMessage": "Please Login",
        "signInButtonText": "Login",
        "signInURL": "https://domain.comm100.com/ssoidp/ssoLogin.aspx"  
      }
    }    
  }
```

### Submit Authentication
`POST /api/v3/bot/sessions/{sessionId}:submitAuthentication`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `Voice` |
  | `authentication` | string  | yes | | authentication data |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitAuthentication
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
{    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"locationRequest",
      "content":{
        "message": "Please share your location first.",
        "buttonText": "Share",
      }
    }    
  }
```

### Submit Location
`POST /api/v3/bot/sessions/{sessionId}:submitLocation`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `location` | string  | yes | | the longitude and latitude of the location, eg: "39.900000,116.300000" |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "location": "39.900000,116.300000",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "location": "39.900000,116.300000",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitLocation
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"formRequest",
      "content":{
        "message": "Please fill the information first",
        "title": "Fill a Form",
        "isConfirmationRequired": true,
        "fields": [
          {
            "type":"text",
            "name":"email",
            "defaultValue": "kart@yahoo.com",
            "isRequired":true,
            "isMasked":true,
          },
          {
            "type":"dropDownList",
            "name":"city",
            "isRequired":true,
            "isMasked":false,
            "options":["beijing", "hangzhou"],
          }
        ],
      }
    }    
  } 
```

### Submit Form
`POST /api/v3/bot/sessions/{sessionId}:submitForm`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  |`formValues` | [FieldValue](#FieldValue-object)[] | yes | | an array of [FieldValue](#FieldValue-object) objects |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"Live Chat",
    "formValues": [
      {
        "name":"email",
        "value":"kart@yahoo.com",
      },
      {
        "name":"city",
        "value":"beijing",
      },
    ],
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }  
```

#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "formValues": [
      {
        "name":"email",
        "value":"kart@yahoo.com",
      },
      {
        "name":"city",
        "value":"beijing",
      },
    ],
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitForm
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
{    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "authentication": "vcw1fc9d92e64487a2e892e68d68dsww",
      "location": "39.900000,116.300000",
      "formValues": [
        {
          "name":"email",
          "value":"kart@yahoo.com",
        },
        {
          "name":"city",
          "value":"beijing",
        },
      ],
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"i want to buy NBN",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
        "intentName": "buy nbn",
        "score": 89.25,
        "responses":[
          {
            "type":"htmlText",
            "content": "<div>this is your order list</div>"
          },
          {
            "type":"image",
            "content": {
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            }
          }
        ]
      }
    }    
  }
```

### Submit IVRKey
`POST /api/v3/bot/sessions/{sessionId}:submitIVRKey`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | eg:  `IVR` |
  | `key` | string  | yes | | the key of ivr menu |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

example:
```Json 
  {
    "channel":"IVR",
    "key":"#",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }  
```
#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"IVR",
    "key":"#",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitIVRKey
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "currentIntentId": "8d6892e6-92e6-4487-a2e8-92e68d6892e6",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"2",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
        "intentName": "buy nbn",
        "score": 89.25,  
        "responses":[
          {
            "type":"text",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"text",
            "content": {
              "text":"You can ask any questions. If you want to know what I can help with, you can say Menu or Options",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          }
        ]
      }
    }    
  }
```

### Rate the bot answer as helpful or not helpful

  `POST /api/v3/bot/sessions/{sessionId}:rate`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `sessionId` | Guid | yes  |  id of the chat or conversation |

Request body

The request body contains data with the follow structure:

  | Name | Type | Required  | Default | Description |    
  | - | - | :-: | :-: |  - | 
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `chatbotMessageId` | Guid  | yes | | the id of the [ChatbotMessage](#ChatbotMessage-object) |
  | `type` | string  | yes  | | `helpful` or `notHelpful` |
  | `context` | [ChatbotSessionContext](#ChatbotSessionContext-Object) Object  | yes  |  |

  example:
```Json 
  {
    "channel":"Live Chat",
    "chatbotMessageId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "notHelpful",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }
```
#### Response
the response is: [ChatbotSession](#ChatbotSession-Object) Object

#### Example
- Rate the bot as not helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "chatbotMessageId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "notHelpful",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:rate
```
  Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"notHelpfulMessage",
      "content":{
        "messageWhenNotHelpful":"I am sorry that this doesn't answer your question. Please click on following button to connect to an agent.",
        "ifIncludeContactAgentOptionWhenNotHelpful": true,
      },
      "smartTriggerActions":[
        {
          "type":"transfer", 
          "isEnabled": true,
          "targetType": "department",
          "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
        }
      ]
    }    
  }  
```

- Rate the bot as helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "chatbotMessageId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "helpful",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/1487fc9d-92e6-4487-a2e8-92e68d6892e6:rate
```
  Response
```Json
HTTP/1.1 200 OK
  Content-Type:  application/json
  {    
    "channel":"Live Chat",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {
      "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
      "customData": {
        "name":"Kart",
        "email":"kart@yahoo.com",
        "phone":"123-4355-212",
      }
    }       
  }
```


# Agent Assist Suggestion
  + `POST /api/v3/agentAssist/questionSuggestions` -[Query question suggestions by agent assist](#query-question-suggestions-by-agent-assist)

## Agent Assist Suggestion Related Object Json Format

### QuestionSuggestion

  QuestionSuggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |
  | - | - | :-: | - |
  | `id` | string  |  | the unique id of the question |
  | `question` | string  |  | the question visitor asked. |
  | `ifMatch` | bool  | false | if the suggestion score greater than highConfidenceScore then true, otherwise false |
  | `suggestions` | [Suggestion](#suggestion)[] |  | array of [Suggestion](#suggestion) Object |

### Suggestion

  Suggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |
  | - | - | :-: |  - |
  | `type` | string  |  | enum value, `publicCannedMessage`,`KBArticle`, `chatbotIntent` |
  | `content` | object  |  |suggestion's content.<br/>when type is publicCannedMessage, it represents [CannedMessageSuggestionContent](#canned-message-suggestion-content);<br/>when type is KBArticle ,it represents [KBArticleSuggestionContent](#kb-Article-suggestion-content);<br/>when type is chatbotIntent, it represents [ChatbotIntentSuggestionContent](#chatbot-Intent-suggestion-content). |
  | `score` | float  |  0 |the score of the suggestion |
 
### Canned Message Suggestion Content
  Canned Message Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `id` | Guid  |  |id of the Canned Message |
  | `name` | string  |  |title of the Canned Message |
  | `content` | string  |  |the content of the Canned Message |

### KB Article Suggestion Content
  KB Article Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: |  - | 
  | `id` | Guid  |  |id of the Knowledge Base article |
  | `title` | string  ||title of the article |
  | `content` | string  |  |the content of the article |
  | `url` | string  |  |the URL of the article |
  | `textBeforeKBArticle` | string  |  | the message which usually works as guidance for visitors before a knowledge base article link |

### Chatbot Intent Suggestion Content
  Chatbot Intent Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default |Description |    
  | - | - | :-: | - | 
  | `id` | Guid  |  |id of the intent |
  | `name` | string  |  |name of the intent |
  | `content` | string  |  |the content of the intent answers |


## Agent Assist Suggestion Endpoints
### Query question suggestions by agent assist

  `POST /api/v3/agentAssist/questionSuggestions`
 
#### Parameters

Request body

The request body contains data with the list of the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | string  | yes | | the unique id of the question  |
  | `question` | string  | yes | | the question visitor asked. |
  | `campaignId` | Guid | no | | the campaign id |


example:
  ```json
  [ 
    {
      "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "how to use livechat?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    },
    {
      "id": "fff4sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "what is comm100 livechat about?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    }
  ]
```
#### Response    

 - the response is: list of [QuestionSuggestion](#questionSuggestion) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[ 
    {
      "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "how to use livechat?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    },
    {
      "id": "fff4sad2-92e6-4487-a2e8-8234fc9d1f48",
      "question": "what is comm100 livechat about?",
      "campaignId": "w124sad2-92e6-4487-a2e8-8234fc9d1f48"
    }
  ]' -X POST https://domain.comm100.com/api/v3/agentAssist/questionSuggestions
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "question": "how to use livechat?",
    "ifMatch": false,
    "suggestions": [
      {
        "type": "intent",
        "content": {
          "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
          "name": "comm100 livechat",
          "content":""
        },
        "score": 10
      }
    ]
  },
  {
    "id": "fff4sad2-92e6-4487-a2e8-8234fc9d1f48",
    "question": "what is comm100 livechat about?",
    "ifMatch": true,
    "suggestions": [
      {
        "type": "intent",
        "content": {
          "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
          "name": "comm100 livechat",
          "content":""
        },
        "score": 88.5
      }
    ]
  }
]
```
