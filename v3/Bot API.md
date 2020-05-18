  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 2.0 | v1 | Bot Restful API | 2018-5-5 | Iguo | 
  | 3.0 | v2 | Bot3.0 Update | 2018-12-9 | Iguo |
  | 3.1 | v2 | Add Third-Party Bot | 2019-01-19 | Ares |
  | 3.2 | v2 | Add Agent Assist Restful API | 2019-03-22 | Davy |
  | 3.3 | v2 | Add Comm100 Own Bot Restful API | 2019-05-24 | Page |
  | 3.4 | v3 | update to v3 | 2019-09-29 | Davy |
  | 4.0 | v3 | xversion | 2019-10-21 | Davy |
  | 4.1 | v3 | voice bot | 2020-05-18 | [Page] |

# Summary
  - Chatbot
    - [chatbot subscription](#chatbot-subscription)
    - [chatbot language](#chatbot-language)
    - [bot](#bot)
       - [greetingMessageInChannel](#GreetingMessageInChannel)
         - [response](#Chatbot-response) 
       - [noAnswerMessageInChannel](#noAnswerMessageInChannel)
       - [messageAfterSeveralConsecutivePossibleAnswersInChannel](#messageAfterSeveralConsecutivePossibleAnswersInChannel)
    - [category](#category)
    - [intent](#intent)
       - [question](#question) 
       - [answerInChannel](#answer-in-channel) 
         - [response](#Chatbot-response)      
         - [authentication request](#authentication-request)
         - [location request](#Location-Request)
         - [form](#form) 
           - [field](#field)
         - [prompt](#prompt) 
    - [response](#Chatbot-response) 
       - [button](#button)
    - [session](#session)
    - [entity](#entity)
       - [entity keyword](#entity-keyword) 
    - [smart trigger](#smart-trigger)
       - [smart trigger condition](#smart-trigger-condition) 
       - [smart trigger action](#smart-trigger-action) 
    - [quick reply](#quick-reply)
       - [quick reply item](#quickreplyitem) 
    - [learning question](#learning-question) 
    - [prebuiltEntity](#PrebuiltEntity)
    - [operation](#operation) 
    - [image](#image)
    - [report](#report)
  - AgentAssist
    - [agent assist language](#agent-assist-language) 
    - [agent assist](#agent-assist)
    - [agent assist synonym](#agent-assist-synonym) 
    - [agent assist learning question](#agent-assist-learning-question) 
    - [agent assist suggestion](#agent-assist-suggestion)

  

# Chatbot Subscription
  - `GET /api/v3/chatbot/subscription` - [Get chatbot subscription](#get-chatbot-subscription)

## Related Object Json Format

### Chatbot Subscription Object
  Chatbot Subscription Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `isChatbotEnabled` | bool  | N/A | N/A | false | if chatbot has been enabled under this site |
  | `totalPurchasedMessageAmount` | integer | N/A | N/A | 0 | It is the maximum available amount of the chatbot messages in this month. |
  | `startDate` | Date | N/A | N/A | | the chatbot subscription start date |
  | `nextRenewDate` | Date | N/A | N/A | | next renew date |
  | `messageQuotaPerMonth` | integer | N/A | N/A | 0 | message quota per month |
  | `paymentPeriod` | string  | N/A | N/A | Monthly | enums: `monthly`,`quarterly`, `yearly` |
  | `monthlyPrice` | float  | N/A | N/A | 0 | monthly price |
  | `quarterlyPrice` | float  | N/A | N/A | 0 | quarterly price |
  | `yearlyPrice` | float  | N/A | N/A | 0 | yearly price |
  | `overageUnitPrice` | float  | N/A | N/A | 0 | overage unit price |
  | `overageMessageQuota` | integer  | N/A | N/A | 0 | overage message quota |
  | `chatbotUsages` | [ChatbotUsage](#Chatbot-Usage-Object)[]  | N/A | N/A | | an array of [ChatbotUsage](#Chatbot-Quota-Object) Objects  |


### Chatbot Usage Object
  Chatbot Usage Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  | `botId` | Guid  | | N/A | N/A | | id of the bot |
  | `usedMessageAmount` | double  | | N/A | N/A | 0 | amount of used bot messages |
  | `bot` | [Bot](#bot-Object)  | yes | N/A | N/A | | Available only when bot is included |

## Endpoints
### Get chatbot subscription

  `GET /api/v3/chatbot/subscription`

#### Parameters
  
Query string

  | Name  | Type | Required | Default | Description |
  | - | - | :-: | :-: | - | 
  | `include` | string | no  | |  Available value: `bot` |

#### Response
the response is: [Chatbot Subscription](#Chatbot-Subscription-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/chatbot/subscription?include=bot
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
   "isChatbotEnabled": true,
   "totalPurchasedMessageAmount": 100000,
   "startDate": "2019-11-11",
   "nextRenewDate": "2019-12-11",
   "messageQuotaPerMonth": 100000,
   "paymentPeriod": "Monthly",
   "monthlyPrice": 1200,
   "quarterlyPrice": 3600,
   "yearlyPrice": 14400,
   "overageUnitPrice": 600,
   "overageMessageQuota": 25000,
   "chatbotUsages":[
      {
        "botId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "usedMessageAmount":123,
        "bot": {  // include the bot
          "id":"f9928d68-92e6-4487-a2e8-8234fc9d1f48",
          "name": "Peely",
          "engineType": "chloe",
          "language": "en",
          ...
        }
      },
      ...    
    ]
}
```
  


#  Chatbot Language
  - `GET /api/v3/chatbot/languages` - [Get chatbot supported languages ](#get-chatbot-supported-languages)

## Language Related Objects Json Format
### Language Object
  Language is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `code` | string  | N/A | N/A | | code of the Language |
  | `name` | string  | N/A | N/A | | name of the Language |

## Endpoints
### Get chatbot supported languages

  `GET /api/v3/chatbot/languages`

#### Parameters
  
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - |  - | 
  | `engineType` | string | no  | dialogflow | Available value: `dialogflow`, `chloe` |


#### Response
the response is: list of [Language](#Language-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/chatbot/languages?engineType=chloe
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "code": "en",
    "name": "English"
  },
  {
    "code": "es",
    "name": "Spanish"
  },
  ...
]
```

# Bot
  + `GET /api/v3/chatbot/bots` - [Get all bots of a site](#get-all-bots-of-a-site)
  + `POST /api/v3/chatbot/bots` - [Create a new bot](#create-a-new-bot)
  + `PUT /api/v3/chatbot/bots/{id}` - [Update a bot](#update-a-bot)
  + `GET /api/v3/chatbot/bots/{id}` - [Get a bot by id](#get-a-bot-by-id)
  + `DELETE /api/v3/chatbot/bots/{id}` - [Remove a bot](#delete-a-bot-by-id)
  + `GET /api/v3/chatbot/bots/{id}:export` - [Export a bot](#export-a-bot)
  + `POST /api/v3/chatbot/bots/{id}:import` - [Import a bot](#import-a-bot)
  + `POST /api/v3/chatbot/bots/{id}:train` - [Train a bot](#train-a-bot)
  + `POST /api/v3/chatbot/bots/{id}:test`  - [Test a bot](#test-a-bot)

## Bot Related Object Json Format

### Bot Object
  Bot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  | `id` | Guid  | | yes | N/A | | id of the bot |
  | `name` | string  | | no | yes | | name of the bot |
  | `engineType` | string  | | yes | yes | dialogflow | type of the bot, enums contain `dialogflow`,`chloe`, `thirdParty` |
  | `language` | string  | | yes | yes | en | language code of the bot |  
  | `avatar` | [Image](#image-object)  | | no | no | | an [Image](#image-object) Object ,the avatar of bot |  
  | `isTrained` | bool  | | N/A | N/A | false | if the bot is trained |  
  | `greetingMessageInChannels` | [GreetingMessageInChannel](#GreetingMessageInChannel-object)[]  | yes | no | no | | Available only when greetingMessageInChannels are included | 
  | `noAnswerMessageInChannels` | [NoAnswerMessageInChannel](#NoAnswerMessageInChannel-Object)[]  | yes | no | no | | Available only when noAnswerMessageInChannels are included |  
  | `messageWhenNotHelpful` | string  | | no | no |  I'm sorry to hear that wasn't helpful 😞. If you'd like, I can connect you to a human for assistance.  | not helpful message |  
  | `ifIncludeContactAgentOptionWhenNotHelpful` | bool  | | no | no | true | is show agent link when not helpful from bot |  
  | `messageWhenProvidingPossibleAnswer` | string  | | no | no | Hmm... Do any of these topics match what you're looking for? | The defined message which is displayed before listing the possible answers |  
  | `consecutiveTimesOfPossibleAnswers` | integer  | | no | no | 3 |The number of times bot can provide possible answers consecutively before displaying the customized message |  
  | `messageAfterSeveralConsecutivePossibleAnswersInChannels` | [MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-Object)[]  | yes | no | no | Available only when messageAfterSeveralConsecutivePossibleAnswersInChannels are included |  
  | `messageAfterVisitorChooseToContactAgent` | string  | | no | no |  We are connecting you to a human agent. |  
  | `contactAgentButtonTextWhenOnline` | string  | | no | no | Chat with Human Agent | agent is online text|  
  | `contactAgentButtonTextWhenOffline` | string  | | no | no | Leave a Message | agent is offline text  |  
  | `formSubmitButtonText` | string  | | no | no | Submit | submit button text |  
  | `formCancelButtonText` | string  | | no | no | Cancel | cancel button text |  
  | `formConfirmButtonText` | string  | | no | no | Confirm | confirm button text |  
  | `highConfidenceScore` | integer  | | no | no | 40 | When visitors send a message, Bot will match it with all of your intents. If the top matching score(matching score ranges from 0 to 100) is higher than the High Confidence Answer Score, Bot will send the answer of the top score intent to visitors |  
  | `noAnswerScore` | integer | | no | no | 10 | When visitors send a message, Bot will match it with all of your intents. If the top macthing score(matching score ranges from 0 to 100) is between the High Confidence Answer Score and No Answer Score, Bot will send the answer of the top score intent as a possible answer to visitors; if the top matching score is lower than the No Answer Score, Bot will send the message configured for When Visitor Question Is Not Recognized. |
  | `lastUpdatedTime` | datetime  | | N/A | N/A | | This attribute stores the last updated time for a chatbot. Once the chatbot or any sub attribute of the chatbot is edited, this value will be changed to the current time |
  |`thirdPartyWebhook` | [Webhook](#Webhook-object) | | no | no | | [Webhook](#Webhook-object) object, Only available when engineType is `thirdParty`  | 
  | `enabledChannels` | string[]  | | no | no | | list of channel, eg: [`Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`]  |  

### GreetingMessageInChannel Object
GreetingMessageInChannel is represented as simple flat json objects with the following keys:

|Name| Type| Include | Read-only For Put |Mandatory For Post |Default | Description     | 
| - | - | :-: | :-: | :-: | :-: | - | 
|`id` | Guid  | | yes | N/A | | id of the current item.  | 
| `channel` | string  | | yes | yes | | eg:  `Default`, `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `Voice` |
|`responses`| [Response](#response-object)[] | | no | yes | | an array of [Response](#response-object) object. |


### NoAnswerMessageInChannel Object
NoAnswerMessageInChannel is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post | Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item.  | 
| `channel` | string  | yes | yes | | eg :  `Default`, `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
|`message` | string | no | yes | | text of the message  | 
|`ifIncludeContactAgentOption` | bool | no | yes | false | include Contact An Agent or not,Only available when the Channel is Live Chat, Facebook Messenger or Twitter Direct Message. | 


### MessageAfterSeveralConsecutivePossibleAnswersInChannel Object
MessageAfterSeveralConsecutivePossibleAnswersInChannel is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post | Default |Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item.  | 
| `channel` | string  | yes | yes | | eg :  `Default`, `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
|`message` | string | no | yes | | text of the message  | 
|`ifIncludeContactAgentOption` | bool | no | yes | false | include Contact An Agent or not,Only available when the Channel is Live Chat, Facebook Messenger or Twitter Direct Message. |

## Bot Endpoints
### Get all bots of a site

  `GET /api/v3/chatbot/bots`

#### Parameters
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `channel` | string | no  |  | filter by enabled channel |
  | `include` | string | no  | |  Available value: `greetingMessageInChannels`,`noAnswerMessageInChannels`, `messageAfterSeveralConsecutivePossibleAnswersInChannels` |


#### Response
the response is: list of [Bot](#bot-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Test Bot",
    "engineType": "chloe",
    "language": "en",      
    "avatar": {
      "name": "bot.png",
      "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
    },
    "messageWhenNotHelpful":"",
    "ifIncludeContactAgentOptionWhenNotHelpful":true,
    "messageWhenProvidingPossibleAnswer":"",
    "consecutiveTimesOfPossibleAnswers":3,
    "messageAfterVisitorChooseToContactAgent":"",
    "contactAgentButtonTextWhenOnline":"Contact an agent",
    "contactAgentButtonTextWhenOffline":"Leave a message",
    "formSubmitButtonText":"Submit",
    "formCancelButtonText":"Cancel",
    "formConfirmButtonText":"Confirm",
    "highConfidenceScore":40,
    "noAnswerScore":20,
    "isTrained": true,
    "lastUpdatedTime": "2019-11-19 12:12:30",    
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  },
  ...
]
```

### Create a new bot

  `POST /api/v3/chatbot/bots`

#### Parameters
Request body

  The request body contains data with the [Bot](#bot-object) structure

  example:
  ```json
  {
    "name": "New Test Bot",
    "engineType": "chloe",
    "language": "en",
    "avatar": {
      "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
      "name": "bot.png",
      "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
    },    
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  }
  ```

#### Response
the response is: [Bot](#bot-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name": "New Test Bot",
    "engineType": "chloe",
    "language": "en",  
    "avatar": {
      "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
      "name": "bot.png",
      "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
    },  
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/bots/casd8d68-92e6-4487-a2e8-8234fc9d1f48

  {
    "id": "casd8d68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "New Test Bot",
    "engineType": "chloe",
    "language": "en",
    "avatar": {
      "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
      "name": "bot.png",
      "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
    },
    "messageWhenNotHelpful":"",
    "ifIncludeContactAgentOptionWhenNotHelpful": false,
    "messageWhenProvidingPossibleAnswer":"",
    "consecutiveTimesOfPossibleAnswers": 3,
    "messageAfterVisitorChooseToContactAgent": "",
    "contactAgentButtonTextWhenOnline":"Contact an agent",
    "contactAgentButtonTextWhenOffline":"Leave a message",
    "formSubmitButtonText":"Submit",
    "formCancelButtonText":"Cancel",
    "formConfirmButtonText":"Confirm",
    "highConfidenceScore": 40,
    "noAnswerScore": 20,
    "lastUpdatedTime": "2019-11-19 12:12:30",    
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  }
```

### Update a bot

  `PUT /api/v3/chatbot/bots/{id}`

#### Parameters
Path Parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

Request Body

  The request body contains data with the [Bot](#bot-object) structure

  example:
  ```json
  {
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Test Bot",
    "engineType": "chloe",
    "language": "en",
    "greetingMessageInChannels": [
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",  //update
        "channel":"Default",
        "responses": [
          {
            "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6", //update
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ]
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48", //update
        "channel":"Live Chat",
        "responses": [
           {
            "type":"image", //Create
            "image":{
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            },
            "order": 1
          },
          {
            "id":"a4e8fc9d-92e6-4487-a2e8-92e68d6892e6",  //update
            "type":"video",
            "videoUrl":"https://yutoob.com/v/sdwada_sdawcv5qwe13",
            "order": 2
          }
        ]
      }
    ],
    ...
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  }
  ```
#### Response
the response is: [Bot](#bot-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Test Bot",
    "engineType": "chloe",
    "language": "en",
    "greetingMessageInChannels": [
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",  //update
        "channel":"Default",
        "responses": [
          {
            "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6", //update
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ]
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48", //update
        "channel":"Live Chat",
        "responses": [
           {
            "type":"image", //Create
            "image":{
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            },
            "order": 1
          },
          {
            "id":"a4e8fc9d-92e6-4487-a2e8-92e68d6892e6",  //update
            "type":"video",
            "videoUrl":"https://yutoob.com/v/sdwada_sdawcv5qwe13",
            "order": 2
          }
        ]
      }
    ],
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

  {
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Test Bot",
    "engineType": "chloe",
    "language": "en",
    "greetingMessageInChannels": [
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
        "channel":"Default",
        "responses": [
          {
            "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6",
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ]
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48", 
        "channel":"Live Chat",
        "responses": [
           {
            "id":"dawdscwd-92e6-4487-a2e8-92e68d6892e6", 
            "type":"image", 
            "image":{
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            },
            "order": 1
          },
          {
            "id":"a4e8fc9d-92e6-4487-a2e8-92e68d6892e6", 
            "type":"video",
            "videoUrl":"https://yutoob.com/v/sdwada_sdawcv5qwe13",
            "order": 2
          }
        ]
      }
    ],
    ...
    "enabledChannels": [
      "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  }
```

### Get a bot by id

  `GET /api/v3/chatbot/bots/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - |  - | 
  | `include` | string | no  | |  Available value: `greetingMessageInChannels`,`noAnswerMessageInChannels`, `messageAfterSeveralConsecutivePossibleAnswersInChannels`,`intent` |
  
#### Response
the response is: [Bot](#bot-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48?include=greetingMessageInChannel,intent
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
  "name": "Test Bot",
  "engineType": "chloe",
  "language": "en",
  "greetingMessageInChannels": [
    {
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "channel":"Default",
      "responses": [
        {
          "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"text",
          "textVariants":[
            "Hi, what can i do for you?", "hello, may i help you?"
          ],
          "order": 0
        }
        ...
      ]
    },
    {
      "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",
      "channel":"Live Chat",
      "responses": [
        {
          "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"htmlText",
          "htmlTextVariants":[
            "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
          ],
          "order": 0
        },
        {
          "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"button",
          "message":"What can i do for help?",
          "buttons":[
            {
              "id":"dww12345-92e6-4487-a2e8-92e68d6892e6",
              "text": "Get Order Status",
              "type": "webView",
              "url": "https://taobao.com",
              "openStyle": "full"
            },
            {
              "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
              "text": "Call Me",
              "type": "triggerAnIntent",
              "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
              "intent": {  //include intent
                "id":"dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
                "name": "Transfer to sales",
                "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
              }
            }        
          ],
          "order": 1
        } 
        ...
      ]
    },
    ...
  ],  
  ...  
  "lastUpdatedTime": "2019-11-19 12:12:30",    
  "enabledChannels": [
    "Live Chat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
  ]
}
```

### Delete a bot by id

  `DELETE /api/v3/chatbot/bots/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 204 No Content
```

### Export a bot

  `GET /api/v3/chatbot/bots/{id}:export`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

#### Response
the response is:

  - `fileUrl ` : the exported bot fileUrl, it is a xml file

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48:export
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "fileUrl": "https://bot.comm100.com/botapi/files/74e29172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```

### Import a bot

  `POST /api/v3/chatbot/bots/{id}:import`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

Request body
  - the file data to be imported.
    you can use [Export a bot](#export-a-bot) first to get the xml template

 example:
```json
//Request header
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx7Uz45AqRfHzbAoI
//Request body
------WebKitFormBoundaryx7Uz45AqRfHzbAoI
Content-Disposition: form-data; name="file"; filename="[my bot].xml"
Content-Type: text/xml
file binary data
------WebKitFormBoundaryx7Uz45AqRfHzbAoI--
```   

#### Response
the response is:
  - `operationId ` : it is a guid, uniquely identify the import operation, you can use [operation](#operation) API to poll the result 

#### Example
Using curl
```
curl -F 'file=@[my bot].xml' 
-X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48:import
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "operationId": "74e29172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```

### Train a bot

  `POST /api/v3/chatbot/bots/{id}:train`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

#### Response
the response is:
  - `operationId ` : it is a guid, uniquely identify the import operation, you can use [operation](#operation) API to poll the result 

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48:train
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "operationId": "9c2d9172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```

### Test a bot

  `POST /api/v3/chatbot/bots/{id}:test`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the bot |

Request body

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - |
  | `channel` | string  | yes | | eg: `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS` |
  | `question` | string | yes  |  | the question |

  example:
  ```json
  {
    "channel": "Live Chat",
    "question": "i want to buy nbn"
  }
  ```

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | yes | | type of the response,including `highConfidenceAnswer`、`possibleAnswer`、`noAnswer` |
  | `content` | object | yes |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer); when type is `possibleAnswer`,it represents [PossibleAnswer](#PossibleAnswer);when type is `noAnswer`,it represents [NoAnswer](#NoAnswer) |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel": "Live Chat",
    "question": "i want to buy nbn"
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48:test
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "type": "highConfidenceAnswer",
  "content": {
    "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
    "intentName": "buy nbn",
    "score": 89.25,
    "answer": {
      "channel": "Live Chat",
      "responses":[
        {
          "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"htmlText",
          "htmlTextVariants":[
            "<div>Hi, what can i do for you?</div>"
          ],
          "order": 0
        },
        {
          "id":"12e8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"image",
          "image":{
            "id": "1dw142323-92e6-4487-a2e8-92e68d6892e6",
            "name":"greeting.png",
            "url": "https://bot.comm100.com/botapi/images/greeting.png"
          },
          "order": 1
        }
      ]
    }
  }
}
```


# GreetingMessageInChannel  
  + `GET /api/v3/chatbot/bots/{botId}/greetingMessageInChannels` - [Get all GreetingMessageInChannels of the bot](#get-all-GreetingMessageInChannels-of-the-bot)
  + `POST /api/v3/chatbot/bots/{botId}/greetingMessageInChannels` - [Create a new GreetingMessageInChannel](#create-a-new-GreetingMessageInChannel)
  + `PUT /api/v3/chatbot/greetingMessageInChannels/{id}` - [Update a GreetingMessageInChannel](#update-a-GreetingMessageInChannel)
  + `DELETE /api/v3/chatbot/greetingMessageInChannels/{id}` - [Remove a GreetingMessageInChannel](#remove-a-GreetingMessageInChannel)
  + `GET /api/v3/chatbot/greetingMessageInChannels/{id}` - [Get a GreetingMessageInChannel by id](#get-a-GreetingMessageInChannel-by-id)

## GreetingMessageInChannel Endpoints
### Get all GreetingMessageInChannels of the bot

  `GET /api/v3/chatbot/bots/{botId}/greetingMessageInChannels`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Query string

  | Name  | Type | Required | Default  | Description |     
  | - | - | - | - | - |
  | `include` | string | no  | | Available value: `intent`  | 

#### Response
the response is: list of [GreetingMessageInChannel](#GreetingMessageInChannel-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/greetingMessageInChannels
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",  
    "responses": [
      {
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ]
  },
  ...
]
```

### Create a new GreetingMessageInChannel

  `POST /api/v3/chatbot/bots/{botId}/greetingMessageInChannels`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Request body 

  The request body contains data with the [GreetingMessageInChannel](#GreetingMessageInChannel-object) structure

  example:
  ```json  
  {
    "channel":"SMS",
    "responses": [
      {
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ]
  }
  ```

#### Response
the response is:
 [GreetingMessageInChannel](#GreetingMessageInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"SMS",
    "responses": [
      {
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ]
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/greetingMessageInChannels
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/greetingMessageInChannels/bs22qa68-92e6-4487-a2e8-8234fc9d1f48

{
  "id": "bs22qa68-92e6-4487-a2e8-8234fc9d1f48",
  "channel":"SMS",
  "responses": [
    {
      "type":"text",
      "textVariants":[
        "Hi, what can i do for you?", "hello, may i help you?"
      ],
      "order": 0
    }
  ]
}
```

### Update a GreetingMessageInChannel

  `PUT /api/v3/chatbot/greetingMessageInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the greetingMessageInChannel |

Request body 

  The request body contains data with the [GreetingMessageInChannel](#GreetingMessageInChannel-object) structure

  example:
  ```json  
  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "responses": [
      {
        "id": "92e68d68-92e6-4487-a2e8-92e68d6892e6",  //update
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      },
      {
        "type":"text",  // create
        "textVariants":[
          "this is a chatbot!", "i am a chatbot!"
        ],
        "order": 0
      }
    ]
  }
```
#### Response
the response is:
 [GreetingMessageInChannel](#GreetingMessageInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "responses": [
      {
        "id": "92e68d68-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      },
      {
        "type":"text",
        "textVariants":[
          "this is a chatbot!", "i am a chatbot!"
        ],
        "order": 0
      }
    ]
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/greetingMessageInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
  "channel":"SMS",
  "responses": [
    {
      "id": "92e68d68-92e6-4487-a2e8-92e68d6892e6",
      "type":"text",
      "textVariants":[
        "Hi, what can i do for you?", "hello, may i help you?"
      ],
      "order": 0
    },
    {
      "id": "dawd2ws21-92e6-4487-a2e8-92e68d6892e6",
      "type":"text",
      "textVariants":[
        "this is a chatbot!", "i am a chatbot!"
      ],
      "order": 0
    }
  ]
}
```

### Remove a GreetingMessageInChannel

  `DELETE /api/v3/chatbot/greetingMessageInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the greetingMessageInChannel |


#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/greetingMessageInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get a GreetingMessageInChannel by id

  `GET /api/v3/chatbot/greetingMessageInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the greetingMessageInChannel |

Query string

  | Name  | Type | Required | Default  | Description |     
  | - | - | - | - | - |
  | `include` | string | no  | | Available value: `intent`  | 

#### Response
the response is:
 [GreetingMessageInChannel](#GreetingMessageInChannel-object) Object

#### Example
Using curl
```
curl -X GET https://domain.comm100.com/api/v3/chatbot/greetingMessageInChannels/4487fc9d-92e6-4487-a2e8-92e68d6892e6?include=intent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "responses": [
      {
        "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      },
      {
        "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
        "type":"button",
        "message":"What can i do for help?",
        "buttons":[
          {
            "id":"dww12345-92e6-4487-a2e8-92e68d6892e6",
            "text": "Get Order Status",
            "type": "webView",
            "url": "https://taobao.com",
            "openStyle": "full"
          },
          {
            "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
            "text": "Call Me",
            "type": "triggerAnIntent",
            "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
            "intent": {  //include intent
              "id":"dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
              "name": "Transfer to sales",
              "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
            }
          }        
        ],
        "order": 1
      }    
    ]
  }
```

# NoAnswerMessageInChannel
  You need `Manage Bot` permission to manage bot NoAnswerMessageInChannels.
  - `NoAnswerMessageInChannels`
    + `GET /api/v3/chatbot/bots/{botId}/noAnswerMessageInChannels` - [Get all NoAnswerMessageInChannels of the bot](#get-all-NoAnswerMessageInChannels-of-the-bot)   
    + `POST /api/v3/chatbot/bots/{botId}/noAnswerMessageInChannels` - [Create a new NoAnswerMessageInChannel](#create-a-new-NoAnswerMessageInChannel)
    + `PUT /api/v3/chatbot/noAnswerMessageInChannels/{id}` - [Update a NoAnswerMessageInChannel](#update-a-NoAnswerMessageInChannel)
    + `DELETE /api/v3/chatbot/noAnswerMessageInChannels/{id}` - [Remove a NoAnswerMessageInChannel](#remove-a-NoAnswerMessageInChannel)
    + `GET /api/v3/chatbot/noAnswerMessageInChannels/{id}` - [Get a NoAnswerMessageInChannel by id](#get-a-NoAnswerMessageInChannel-by-id)

## NoAnswerMessageInChannel Endpoints
### Get all NoAnswerMessageInChannels of the bot

  `GET /api/v3/chatbot/bots/{botId}/noAnswerMessageInChannels`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot |

#### Response
the response is: list of [NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/noAnswerMessageInChannels
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "message": "sorry , i can not understand your question.",
    "ifIncludeContactAgentOption": false
  },
  {
    "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",
    "channel":"Live Chat",
    "message": "sorry , i can not understand your question.",
    "ifIncludeContactAgentOption": true
  }  
]
```

### Create a new NoAnswerMessageInChannel

  `POST /api/v3/chatbot/bots/{botId}/noAnswerMessageInChannels`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot |

Request body 

  The request body contains data with the [NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) structure

  example:
```json
  {
    "channel":"SMS",
    "message": "sorry , i can not understand.",
    "ifIncludeContactAgentOption": false
  }  
```

#### Response
the response is:
 [NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"SMS",
    "message": "sorry , i can not understand.",
    "ifIncludeContactAgentOption": false
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/noAnswerMessageInChannels
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/noAnswerMessageInChannels/bs22qa68-92e6-4487-a2e8-8234fc9d1f48

{
  "id": "bs22qa68-92e6-4487-a2e8-8234fc9d1f48",
  "channel":"SMS",
  "message": "sorry , i can not understand.",
  "ifIncludeContactAgentOption": false
}
```


### Update a NoAnswerMessageInChannel

  `PUT /api/v3/chatbot/noAnswerMessageInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the noAnswerMessageInChannel |

Request body 
  
  The request body contains data with the [NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) structure

  example:
  ```json
  {
    "id": "1bwfe21d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "message": "sorry , i can not help you.",
    "ifIncludeContactAgentOption": false
  }  
```

#### Response
the response is:
[NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "1bwfe21d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "message": "sorry , i can not help you.",
    "ifIncludeContactAgentOption": false
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/noAnswerMessageInChannels/1bwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "1bwfe21d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "message": "sorry , i can not help you.",
    "ifIncludeContactAgentOption": false
  } 
```

### Remove a NoAnswerMessageInChannel

  `DELETE /api/v3/chatbot/noAnswerMessageInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the noAnswerMessageInChannel |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/noAnswerMessageInChannels/1bwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get a NoAnswerMessageInChannel by id

  `GET /api/v3/chatbot/noAnswerMessageInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the noAnswerMessageInChannel |

#### Response
the response is:
[NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) Object

#### Example
Using curl
```
curl -X GET https://domain.comm100.com/api/v3/chatbot/noAnswerMessageInChannels/1bwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "1bwfe21d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "message": "sorry , i can not help you.",
    "ifIncludeContactAgentOption": false
  } 
```

# MessageAfterSeveralConsecutivePossibleAnswersInChannel
  You need `Manage Bot` permission to manage bot MessageAfterSeveralConsecutivePossibleAnswersInChannels.
  - `MessageAfterSeveralConsecutivePossibleAnswersInChannels`
    + `GET /api/v3/chatbot/bots/{botId}/messageAfterSeveralConsecutivePossibleAnswersInChannels` - [Get all MessageAfterSeveralConsecutivePossibleAnswersInChannels of the bot](#get-all-MessageAfterSeveralConsecutivePossibleAnswersInChannels-of-the-bot)
    + `POST /api/v3/chatbot/bots/{botId}/messageAfterSeveralConsecutivePossibleAnswersInChannels` - [Create a new MessageAfterSeveralConsecutivePossibleAnswersInChannel](#create-a-new-MessageAfterSeveralConsecutivePossibleAnswersInChannel)
    + `PUT /api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/{id}` - [Update a MessageAfterSeveralConsecutivePossibleAnswersInChannel](#update-a-MessageAfterSeveralConsecutivePossibleAnswersInChannel)
    + `DELETE /api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/{id}` - [Remove a MessageAfterSeveralConsecutivePossibleAnswersInChannel](#remove-a-MessageAfterSeveralConsecutivePossibleAnswersInChannel)
    + `GET /api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/{id}` - [Get a MessageAfterSeveralConsecutivePossibleAnswersInChannel by id](#get-a-MessageAfterSeveralConsecutivePossibleAnswersInChannel-by-id)

## MessageAfterSeveralConsecutivePossibleAnswersInChannel Endpoints
### Get all MessageAfterSeveralConsecutivePossibleAnswersInChannels of the bot

  `GET /api/v3/chatbot/bots/{botId}/messageAfterSeveralConsecutivePossibleAnswersInChannels`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot |

#### Response
the response is: list of [MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/messageAfterSeveralConsecutivePossibleAnswersInChannels
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  },
  {
    "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",
    "channel":"Live Chat",
    "message": "I think I'm not answering your question well. Please ask a different question or click on the button below to connect to an agent.",
    "ifIncludeContactAgentOption": true
  }
]
```

### Create a new MessageAfterSeveralConsecutivePossibleAnswersInChannel

  `POST /api/v3/chatbot/bots/{botId}/messageAfterSeveralConsecutivePossibleAnswersInChannels`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot |

Request body 
  
  The request body contains data with the [MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-object) structure

  example:
  ```json
  {
    "channel":"SMS",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }  
```

#### Response
the response is:
 [MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"SMS",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/messageAfterSeveralConsecutivePossibleAnswersInChannels
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/bs22qa68-92e6-4487-a2e8-8234fc9d1f48

  {
    "id": "bs22qa68-92e6-4487-a2e8-8234fc9d1f48",
    "channel":"SMS",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }
```

### Update a MessageAfterSeveralConsecutivePossibleAnswersInChannel

  `PUT /api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the MessageAfterSeveralConsecutivePossibleAnswersInChannel |

Request body 
   
  The request body contains data with the [MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-object) structure

  example:
  ```json
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }
```

#### Response
the response is:
[MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }
```

### Remove a MessageAfterSeveralConsecutivePossibleAnswersInChannel

  `DELETE /api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the MessageAfterSeveralConsecutivePossibleAnswersInChannel |


#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get a MessageAfterSeveralConsecutivePossibleAnswersInChannel by id

  `GET /api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the MessageAfterSeveralConsecutivePossibleAnswersInChannel |


#### Response
the response is:
[MessageAfterSeveralConsecutivePossibleAnswersInChannel](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-object) Object

#### Example
Using curl
```
curl -X GET https://domain.comm100.com/api/v3/chatbot/messageAfterSeveralConsecutivePossibleAnswersInChannels/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "message": "I think I'm not answering your question well.",
    "ifIncludeContactAgentOption": false
  }
```

# Category
  You need `Manage Bot` permission to manage bot category and customize the settings for a bot category.
  - `Categories` - Category Manage
    + `GET /api/v3/chatbot/bots/{botId}/categories` - [Get all categories of the bot](#get-all-categories-of-the-bot)
    + `POST /api/v3/chatbot/bots/{botId}/categories` - [Create a new category](#create-a-new-category)
    + `PUT /api/v3/chatbot/categories/{id}` - [Update a category](#update-a-category)
    + `POST /api/v3/chatbot/categories/{id}:reassign` - [Reassign the sub-categories](#reassign-the-sub-categories)
    + `DELETE /api/v3/chatbot/categories/{id}` - [Remove a category](#remove-a-category)
    + `GET /api/v3/chatbot/categories/{id}` - [Get a category by id](#get-a-category-by-id)

## Category Related Object Json Format
### Category Object
  Category is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default |Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A | | id of the Category |
  | `name` | string  | no | yes | | name of the Category |
  | `parentId` | Guid  | no | yes |  | parent Id of the Category |

## Category Endpoints
### Get all categories of the bot

  `GET /api/v3/chatbot/bots/{botId}/categories`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot  |

#### Response
the response is: list of  [Category](#category-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/categories
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"/",
    "parentId": "00000000-0000-0000-0000-000000000000"    
  },
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"System",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  },
  ...
]
```
### Create a new category

  `POST /api/v3/chatbot/bots/{botId}/categories`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot  |

Request body

  The request body contains data with the [Category](#category-object) structure

  example:
```Json
  {
    "name":"Greeting",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  }
```

#### Response
the response is:
 [Category](#category-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name":"Greeting",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/categories
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/categories/b222qa68-92e6-4487-a2e8-8234fc9d1f48

{
  "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
  "name":"Greeting",
  "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
}
```


### Update a category

  `PUT /api/v3/chatbot/categories/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the category  |

Request body 
  
  The request body contains data with the [Category](#category-object) structure

  example:
```Json
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"System Rename",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  }
```

#### Response
the response is: [Category](#category-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"System Rename",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/categories/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"System Rename",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  }
```

### Reassign the sub categories
  Delete the category and then move all sub-categories and intents to the target category

  `POST /api/v3/chatbot/categories/{id}:reassign`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the category  |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - |  - |
  | `targetCategoryId` | Guid | yes  | |  the id of the target category |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X POST https://domain.comm100.com/api/v3/chatbot/categories/4487fc9d-92e6-4487-a2e8-92e68d6892e6:reassign?targetCategoryId=1487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```


### Remove a category
  Delete the category and all sub-categories and intents

  `DELETE /api/v3/chatbot/categories/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the category  |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/categories/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get a category by id

  `GET /api/v3/chatbot/categories/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the category  |

#### Response
the response is: [Category](#category-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/categories/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"System",
    "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"   
  }
```


# Intent
  +  `GET /api/v3/chatbot/bots/{botId}/intents` - [Get intents](#get-intents)
  +  `GET /api/v3/chatbot/bots/{botId}/intents:queryTopScore` - [Query top score intents](#query-top-score-intents)
  +  `POST /api/v3/chatbot/bots/{botId}/intents` - [Create a new intent](#create-a-new-intent)
  +  `PUT /api/v3/chatbot/intents/{id}` - [Update an intent](#update-an-intent)
  +  `GET /api/v3/chatbot/intents/{id}` - [Get an intent by id](#get-an-intent-by-id)
  +  `DELETE /api/v3/chatbot/intents/{id}` - [Remove an intent](#remove-an-intent)
  +  `POST /api/v3/chatbot/bots/{botId}/intents:import` - [Import intents](#import-intents)


## Intent Related Object Json Format
### Intent Object
Intent is represented as simple flat json objects with the following keys:

|Name| Type| Include | Read-only For Put |Mandatory For Post | Default | Description   |
| - | - |- | :-: | :-: | :-: | - | 
| `id` | Guid  |  | yes | N/A | | id of the intent |
| `name` | string  |  | no | yes | | name of the intent |
|`categoryId`| Guid |  | no | yes | | id of the intent category.|
|`category`| [Category](#category) |yes  | N/A | N/A | | Available only when category is included |
|`questions`| [Question](#question)[]|  | no |yes | |  |
|`answerInChannels`| [AnswerInChannel](#AnswerInChannel-object)[]|  | no |yes | |  |


### AnswerInChannel Object
AnswerInChannel is represented as simple flat json objects with the following keys:

|Name| Type| Include | Read-only For Put |Mandatory For Post | Default | Description   |
| - | - | :-: | :-: | :-:| :-: | - | 
| `id` | Guid  | | yes | N/A | | id of the intent |
| `channel` | string  | |  yes | yes | | eg :  `Default`, `Live Chat`, `Facebook Messenger`, `Twitter Direct Message`, `WeChat`, `WhatsApp`, `SMS`, `Voice` |
|`responses`| [Response](#response-object)[] | yes |  no | yes | | an array of [Response](#response-object) object.  |
|`informationCollectionType` | string |  | no | yes | none | enums :  `form`, `prompt`,`none`. | 
|`authenticationRequest`| [AuthenticationRequest](#AuthenticationRequest-Object)| yes |  no |no | |[AuthenticationRequest](#AuthenticationRequest-Object) object. |
|`locationRequest`| [LocationRequest](#LocationRequest-Object)| yes | no |no | | [LocationRequest](#LocationRequest-Object) object. |
| `form` | [Form](#Form-Object)  | yes | no | no |  |[Form](#Form-Object) object. |
| `prompts` | [Prompt](#Prompt-Object)[]  | yes | no | no | | an array of  [Prompt](#Prompt-Object) object. |


### AuthenticationRequest Object

  AuthenticationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A | | unique id |
  | `signInMessage` | string  | no | yes | | message of the sign in |
  | `signInButtonText` | string  | no | yes | | text of the sign in link |
  | `method` | string  | no | yes | sso | it is a Enum string: `sso`, `customVariable` |
  | `signInURL` | string  | no | no | | url of the sign in |
  | `customVariable` | string  | no | no | | custom variable |


### LocationRequest Object

  LocationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post | Default |Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A | | unique id |
  | `message` | string  | no | yes | Please share your location | message of Location Request |
  | `buttonText` | string  | no | yes | Send Location | text of Location Request button |  

### Prompt Object

  Prompt is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put |Mandatory For Post | Default | Description |    
  | - | - | :-: |:-: | :-: | :-: | - | 
  |`id` | Guid  | | yes | N/A | | id of the current item. |
  |`entityId` | Guid | | no | yes | | id of entity marked in one question. |
  |`entity` | [Entity](#entity-object) | yes | N/A  | N/A  | | Available only when entity is included |
  |`entityLabel` | string | | no | yes | | label to distinguish same entity marked on one question. |
  |`question` | string | | no | yes |  | |
  |`options` | string[] | | no | no | | an array of string |
  |`order` | integer | | no | yes |  | must greater than or equal 0, ascending sort |  

### Form Object
Form is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post | Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item. |
|`message` | string | no | yes |  | A separate message which is sent before the button is sent.|
|`title` | string | no | yes | | when a button is sent to visitor, clicking this button will open a form that contains information bot wants to collect from the visitor. the title refers to the title of that form, and it is also placed on the button as a name.|
|`isConfirmationRequired` | bool | no | yes | false | whether visitor needs to click confirm after filling out the information in a form.|
|`fields` | [Field](#field-object)[] | no | yes | | an array of [Field](#field-object) Object |

### Field Object
Field is represented as simple flat json objects with the following keys:

|Name| Type| Include | Read-only For Put |Mandatory For Post | Default | Description     | 
| - | - | :-: | :-: | :-: | :-: | - | 
|`id` | Guid  | | yes | N/A | | id of the current item. |
|`type` | string | | no | yes | text | enums: `text` ,`textArea`,`radioBox` ,`checkBox` ,`dropDownList` ,`checkBoxList`, type refers to the different kinds of fields which can be used in a form. |
|`name` | string | | no | yes | | a field’s name in a form. |
|`entityId` | Guid | | no | no | | id of entity marked in one question. |
|`entity` | [Entity](#entity-object) | yes | N/A  | N/A  | | Available only when entity is included |
|`entityLabel` | string | | no | no | | label to distinguish same entity marked on one question. |
|`isRequired` | bool | | no | yes | false | to mark whether a field in a form is required or not. |
|`isMasked` | bool | | no | yes | false | if this is true, visitor information will be masked with symbols in chat logs. |
|`options` | string[] | | no | no | | an array of of string when the fieldType is `radioBox` ,`dropDownList` ,`checkBoxList`|
|`order` | integer | | no | yes |  | must greater than or equal 0, ascending sort |

### FieldValue Object
FieldValue is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post | Default |  Description     |
| - | - | :-: | :-: | - |  - | 
|`name` | string |  N/A | N/A | | the name of a field in a form. |
|`value` | string | N/A | N/A | | the value of a field. |

### Response Object
Response is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post | Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item. |
|`type` | string | no | yes | | enums: `text` ,`htmlText` ,`button`,`quickReply` ,`image` ,`video` ,`webhook` ,`ivrMenu` ,`transferCall`. |
|`textVariants` | string[] | no | no | | an array of string ,only available when Type is `text`. |
|`speechVariants` | string[] | no | no | | an array of string ,only available when Type is `text` and channel is `Voice`. |
|`htmlTextVariants` | string[] | no | no | | an array of string ,only available when Type is `htmlText` |
|`image` | [Image](#image-object)  | no | no | | [Image](#image-object) object, only available when Type is `image`|
|`videoUrl` | string | no | no | | only available when Type is `video` |
|`message` | string | no | no | | only available when Type is `button` or `quickReply`. It stores the messages before Buttons or Quick Reply Items. |
|`quickReply` | [Quick Reply](#Quick-Reply-Object) | no | no | | [Quick Reply](#Quick-Reply-Object) object, only available when Type is `quickReply`|
|`buttons` | [Button](#button-object)[] | no | no | | an array of [Button](#button-object) object, only available when Type is `button`  | 
|`webhook` | [Webhook](#Webhook-object) | no | no | | [Webhook](#Webhook-object) object, only available when Type is `webhook`  | 
|`ivrMenu` | [IVRMenu](#IVRMenu-object) | no | no | | [IVRMenu](#IVRMenu-object) object, only available when Type is `ivrMenu`  | 
|`order` | integer | no | yes |  | must greater than or equal 0, the order of the response, ascending sort |

### Image Object
  Image is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post |  Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  |`id` | Guid  | yes | N/A | | id of the current item. |
  | `name` | string  | no | yes | | name of the image |
  | `url` | string  | no | yes | | url of the image | 

### Webhook Object
Webhook is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post |  Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item. |
|`url` | string | no | yes | | webhook request url  | 
|`headers` | Map | no | no | | webhook request header  | 

### IVRMenu Object
IVRMenu is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post |  Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item. |
|`Message` | string | no | yes | | The message sent to visitor before the options.This message will be transferred to voice and read to visitor  | 
|`InvalidInputActionRepeatTime` | Map | no | no | | How many times will this IVR Menu repeat if there is valid input   | 
|`InvalidInputActionIntentId` | Map | no | no | | The intent to go to when no valid input for several times.    | 
| `options` | [IVRMenuOption](#IVRMenuOption-object)[] | | no | yes |  | |

### IVRMenuOption Object
 IVRMenuOption is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include |  Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: |  :-: | - | 
  | `id` | Guid  | | yes | N/A | | id of option item |
  | `text` | string  | | no | yes | | Visitor can speak the text to choose this option.This text will not be read to visitors. |
  | `key` | string  | | no | yes | | 1, 2, 3, 4, 5, 6, 7, 8, 9, 0, *, #. Each key can only be used once in an IVR menu. Visitor can press the key to choose the option.  |
  | `intentId` | string  | | no | no | | The intent to go to when this option is chosen.  |
  | `intent` | [Intent](#intent-object) | yes | N/A | N/A | | Available only when intent is included  | 
  | `order` | integer | | no | yes |  | must greater than or equal 0,the order of the option item, ascending sort . |

### IVRMenu Response Object
IVRMenu Response is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put |Mandatory For Post |  Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item. |
|`Message` | string | no | yes | | The message sent to visitor before the options.This message will be transferred to voice and read to visitor  | 
|`speech` | string | no | no | | base64 string |

### Button Object
Button is represented as simple flat json objects with the following keys:

|Name| Type| Include | Read-only For Put |Mandatory For Post |  Default | Description     | 
| - | - | :-: | :-: | :-: | :-: | - | 
|`id` | Guid  | | yes | N/A | | id of the current item.  | 
|`text` | string | | no | yes | | text on button.  | 
|`type` | string | | no | yes | |enums: `triggerAnIntent`,`link` and `webView` | 
|`url` | string | | no | yes if type is `link` or `webView`| | url of the web page you want to open.  | 
|`intentId` | Guid | | no | yes if type is `triggerAnIntent` | | id of the intent   | 
|`intent` | [Intent](#intent-object) | yes | N/A  | N/A  | | Available only when intent is included |
|`openIn` | string | | no | yes if channel is `Live Chat` and type is `link` | | enums : `sideWindow`,`newWindow`,`currentWindow`, it represents the way that a page will be opened.  | 
|`openStyle` | string | | no | yes if channel is  `Live Chat` or `Facebook Messenger` and type is `webView` | full | enums: `compact`,`tall` and `full`,it represents the size of the webview that will be opened.  |
|`order` | integer | | no | yes |  | must greater than or equal 0, ascending sort |

### IntentScore Object

  IntentScore is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post  | Default | Description |    
  | - | - | :-: | :-: | - | - | 
  |`id` | Guid | N/A | N/A | | id of the intent  | 
  |`name` | string | N/A | N/A | | name of the intent |  
  | `score` | float  | N/A | N/A |  | the score of the intent matched, value is between 0.0 and 100.0 |

## Endpoints
### Get intents

  `GET /api/v3/chatbot/bots/{botId}/intents`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  |  | Available value: `category`, `questions`, `answerInChannels` |
  | `categoryId` | Guid | no  |  | id of the category, filter by category |
  | `keyword` | string | no  |  | keyword is used to search intents by intent name or question |

#### Response

the response is: list of  [Intent](#intent-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/intents?include=category
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json

[  
  {
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "category": {  // include category
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "name":"System",
      "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
    }    
  },  
  ...
]
```

### Query top score intents

  `GET /api/v3/chatbot/bots/{botId}/intents:queryTopScore`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `question` | string | yes  | |  |
  | `top` | integer | no  | 10 |  get top x intents, between 1 and 100   |

#### Response
the response is: list of  [IntentScore](#IntentScore-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/intents:queryTopScore?question=test question&top=3
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json

[  
  {
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"buy nbn",
    "score": 99.98,      
  },  
  ...
]
```

###  Get an intent by id

   `GET /api/v3/chatbot/intents/{id}`

#### Parameter
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  id of the intent  |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  |  | Available value: `category`, `entity`, `intent` |

#### Response

the response is: [Intent](#intent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6?include=category
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "category": {  // include category
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "name":"System",
      "parentId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
    },
    "questions":[
      {
        "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
        "content":"what about nbn",
        "selectedKeywords":[]
      },
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "content":"i want buy nbn",
        "selectedKeywords":[
          {
            "id":"8d6sfc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityLabel":"product",
            "startPosition":"11",
            "endPosition":"13"
          }
        ]
      }
    ],
    "answerInChannels":[
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "channel":"Default",
        "responses": [
          {
            "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6",
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ],
        "informationCollectionType" : "none"
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",
        "channel":"Live Chat",
        "responses": [
          {
            "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
            ],
            "order": 0
          },
          {
            "id":"sc38fc9d-92e6-4487-a2e8-92e68d6892e6",
            "type":"webhook",
            "webhook":{
              "id":"2dawdaww-92e6-4487-a2e8-92e68d6892e6",
              "url": "https://mysystem.com/botHandler/api",
              "headers": {
                "Authorization":"Basic YWRtaW46YWRtaW4="
              },              
            },
            "order": 1
          }
        ],
        "locationRequest": {
          "id":"aa38fc9d-92e6-4487-a2e8-92e68d6892e6",
          "message" : "Please share your location",
          "buttonText" : "share location"
        },
        "informationCollectionType" : "none",
        "authenticationRequest" : {
          "id":"bb38fc9d-92e6-4487-a2e8-92e68d6892e6",
          "signInMessage":"Please Login first",
          "signInButtonText":"Login",
          "method": "sso"
        },
      },
    ]
  }
```

### Create a new intent

  `POST /api/v3/chatbot/bots/{botId}/intents`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |   the unique id of the bot |

Request body
  
  The request body contains data with the [Intent](#intent-object) structure

  example:
```Json
  {
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questions":[
      {
        "content":"what about nbn",
        "selectedKeywords":[]
      },
      {
        "content":"i want buy nbn",
        "selectedKeywords":[
          {
            "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityLabel":"product",
            "startPosition":"11",
            "endPosition":"13"
          }
        ]
      }
    ],
    "answerInChannels":[
      {
        "channel":"Default",
        "responses": [
          {
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ],
        "informationCollectionType" : "none"
      },
      {
        "channel":"Live Chat",
        "responses": [
          {
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
            ],
            "order": 0
          }          
        ],
        "informationCollectionType" : "none"        
      },
    ]    
  }
```

#### Response
the response is: [Intent](#intent-object) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questions":[
      {
        "content":"what about nbn",
        "selectedKeywords":[]
      },
      {
        "content":"i want buy nbn",
        "selectedKeywords":[
          {
            "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityLabel":"product",
            "startPosition":"11",
            "endPosition":"13"
          }
        ]
      }
    ],
    "answerInChannels":[
      {
        "channel":"Default",
        "responses": [
          {
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ],
        "informationCollectionType" : "none"
      },
      {
        "channel":"Live Chat",
        "responses": [
          {
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
            ],
            "order": 0
          }          
        ],
        "informationCollectionType" : "none"        
      }
    ]    
  }' -X POST 
https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/intents
```
Response
```Json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/intents/sdaw341a-92e6-4487-a2e8-f9928d681f48

  {
    "id":"sdaw341a-92e6-4487-a2e8-f9928d681f48",
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6"      
  }
```


### Update an intent

  `PUT /api/v3/chatbot/intents/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  id of the intent |

Request body

The request body contains data with the [Intent](#intent-object) structure

  example:
```Json
  {
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questions":[
      {  //create
        "content":"what about nbn",
        "selectedKeywords":[]
      },
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",  //update
        "content":"i want buy nbn",
        "selectedKeywords":[
          {
            "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityLabel":"product",
            "startPosition":"11",
            "endPosition":"13"
          }
        ]
      }
    ],
    "answerInChannels":[
      {  //create
        "channel":"Default",  
        "responses": [
          {
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ],
        "informationCollectionType" : "none"
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",  //update
        "channel":"Live Chat",
        "responses": [
          {  
            "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6", //update
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
            ],
            "order": 0
          }          
        ],
        "informationCollectionType" : "none",
        "authenticationRequest" : {     //create
          "signInMessage":"Please Login first",
          "signInButtonText":"Login",
          "method": "sso"
        },
      },
    ]    
  }
```

#### Response
the response is: [Intent](#intent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questions":[
      {  
        "content":"what about nbn",
        "selectedKeywords":[]
      },
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",  
        "content":"i want buy nbn",
        "selectedKeywords":[
          {
            "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityLabel":"product",
            "startPosition":"11",
            "endPosition":"13"
          }
        ]
      }
    ],
    "answerInChannels":[
      {  
        "channel":"Default",  
        "responses": [
          {
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ],
        "informationCollectionType" : "none"
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",  
        "channel":"Live Chat",
        "responses": [
          {  
            "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6", 
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
            ],
            "order": 0
          }          
        ],
        "informationCollectionType" : "none",
        "authenticationRequest" : {
          "signInMessage":"Please Login first",
          "signInButtonText":"Login",
          "method": "sso"
        },
      },
    ]    
  }' -X PUT 
https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name":"buy nbn",
    "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questions":[
      { 
        "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "content":"what about nbn",
        "selectedKeywords":[]
      },
      {
        "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
        "content":"i want buy nbn",
        "selectedKeywords":[
          {
            "id":"adawsc9d-92e6-4487-a2e8-92e68d6892e6",
            "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
            "entityLabel":"product",
            "startPosition":"11",
            "endPosition":"13"
          }
        ]
      }
    ],
    "answerInChannels":[
      {  
        "id":"12qwec9d-92e6-4487-a2e8-92e68d6892e6",
        "channel":"Default",  
        "responses": [
          {
            "id":"jtfsec9d-92e6-4487-a2e8-92e68d6892e6",
            "type":"text",
            "textVariants":[
              "Hi, what can i do for you?", "hello, may i help you?"
            ],
            "order": 0
          }
        ],
        "informationCollectionType" : "none"
      },
      {
        "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48", 
        "channel":"Live Chat",
        "responses": [
          {  
            "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6", 
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
            ],
            "order": 0
          }          
        ],
        "informationCollectionType" : "none",
        "authenticationRequest" : {    
          "id":"vbd1ec9d-92e6-4487-a2e8-92e68d6892e6",
          "signInMessage":"Please Login first",
          "signInButtonText":"Login",
          "method": "sso"
        },
      },
    ]    
  }
```
### Remove an intent

  `DELETE /api/v3/chatbot/intents/{id}`

#### Parameter
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  id of the intent |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Import intents

  `POST /api/v3/chatbot/bots/{botId}/intents:import`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  botId |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `mode` | string | no  | add |  `add` or `replace`  | 

Note:
 - `mode`:
    + `add`: if an added intent name is different from an existing intent, it will be imported as a new intent. If an added intent has the same name as an existing one, the questions will be added under the corresponding intent, the answer will not be imported.
    + `replace`: all existing intents will be deleted and replaced with the newly added intents. 

Request body
  - the file data to be imported.
    you can [Download Templates](https://bot.comm100.com/botadmin/downloadfile.ashx?file=import Intents Template.xlsx) first

 example:
```json
//Request header
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx7Uz45AqRfHzbAoI
//Request body
------WebKitFormBoundaryx7Uz45AqRfHzbAoI
Content-Disposition: form-data; name="file"; filename="intents.xlsx"
Content-Type: application/vnd.ms-excel
file binary data
------WebKitFormBoundaryx7Uz45AqRfHzbAoI--
```   

#### Response
the response is:
  - `operationId ` : it is a guid, uniquely identify the import operation, you can use [operation](#operation) API to poll the result 

#### Example
Using curl
```
curl -F 'file=@intents.xlsx' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/intents:import?mode=replace
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "operationId": "74e29172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```


# Question
You need `Manage Bot` permission to manage Intent and customize the settings for an Intent Question.
  - `Questions` - Intent Question Manage
    +  `GET /api/v3/chatbot/intents/{intentId}/questions` - [Get questions of the intent](#get-questions-of-the-intent)
    +  `POST /api/v3/chatbot/intents/{intentId}/questions` - [Create a question for the intent](#create-a-question-for-the-intent)
    +  `PUT /api/v3/chatbot/questions/{id}` - [Update a question](#update-a-question)    
    +  `DELETE /api/v3/chatbot/questions/{id}` - [Remove a question](#remove-a-question)
    +  `GET /api/v3/chatbot/questions/{id}` - [Get a question by id](#get-a-question-by-id)
    +  `POST /api/v3/intents/{intentId}/questions:batchCreate` - [Batch add questions](#Batch-add-questions)

## Question Related Objects Json Format
### Question Object
Question is represented as simple flat json objects with the following keys:

|Name| Type| Read-only For Put | Mandatory For Post | Default | Description     | 
| - | - | :-: | :-: | :-: | - | 
|`id` | Guid  | yes | N/A | | id of the current item.|
|`content` | string  | no | yes | | visitor questions that trigger this intent. |
|`selectedKeywords` | [Question Selected Keyword](#Question-Selected-Keyword-Object)[]  | no | no | | an array of [Question Selected Keyword](#Question-Selected-Keyword-Object) that you want to mark in current question. |
|`order` | integer | no | yes |  | must greater than or equal 0, ascending sort |

### Question Selected Keyword Object
Question Selected Keyword is represented as simple flat json objects with the following keys:

|Name| Type| Include | Read-only For Put | Mandatory For Post | Default |Description     | 
| - | - | :-: | :-: | :-: | :-: | - | 
|`startPosition` | integer | | no | yes | 0 | strat index  of current question you marked. |
|`endPosition` | integer | | no | yes | 0 | end index  of current question you marked. |
|`entityId` | Guid | | no | yes | | id of entity marked in one question. |
|`entity` | [Entity](#entity-object) | yes | N/A  | N/A  | |  Available only when entity is included  |
|`entityLabel` | string | | no | yes | | label to distinguish same entity marked on one question. |

## Question Endpoints
### Get questions of the intent

  `GET /api/v3/chatbot/intents/{intentId}/questions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `intentId` | Guid | yes  |  intentId |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - |
  | `include` | string | no  | | Available value: `entity`  | 

#### Response
the response is: list of [Question](#question-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6/questions?include=entity
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    { 
      "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "content":"what about nbn",
      "selectedKeywords":[]
    },
    {
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
      "content":"i want buy nbn",
      "selectedKeywords":[
        {
          "id":"adawsc9d-92e6-4487-a2e8-92e68d6892e6",
          "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
          "entity": {  // include entity
            "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
            "name": "product"           
          },
          "entityLabel":"product",
          "startPosition":"11",
          "endPosition":"13"
        }
      ]
    }
  ]
```

### Create a question for the intent

  `POST /api/v3/chatbot/intents/{intentId}/questions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `intentId` | Guid | yes  |  intentId |

Request body 

  The request body contains data with the [Question](#question-object) structure

  example:
```Json 
  {
    "content":"what about nbn",
    "selectedKeywords":[]
  }
```

#### Response
the response is: [Question](#question-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "content":"what about nbn",
    "selectedKeywords":[]
  }' -X POST https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6/questions
```
Response
```Json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/questions/vvd7fc9d-92e6-4487-a2e8-92e68d6892e6

  {
    "id":"vvd7fc9d-92e6-4487-a2e8-92e68d6892e6", 
    "content":"what about nbn",
    "selectedKeywords":[]
  }
```

### Update a question

  `PUT /api/v3/chatbot/questions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the intent question id |

Request body 

  The request body contains data with the [Question](#question-object) structure

  example:
```Json 
    {
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
      "content":"i want buy a NBN?",
      "selectedKeywords":[
        {  // create
          "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1", 
          "entityLabel":"product",
          "startPosition":"13",
          "endPosition":"15"
        }
      ]
    }
```

#### Response
the response is: [Question](#question-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
      "content":"i want buy a NBN?",
      "selectedKeywords":[
        { 
          "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",          
          "entityLabel":"product",
          "startPosition":"13",
          "endPosition":"15"
        }
      ]
    }' -X PUT https://domain.comm100.com/api/v3/chatbot/questions/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
    "content":"i want buy a NBN?",
    "selectedKeywords":[
      {
        "id":"892e6c9d-92e6-4487-a2e8-92e68d6892e6", 
        "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",          
        "entityLabel":"product",
        "startPosition":"13",
        "endPosition":"15"
      }
    ]
  }
```

### Remove a question

  `DELETE /api/v3/chatbot/questions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the intent question id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/questions/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get a question by id

  `GET /api/v3/chatbot/questions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the intent question id |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `entity`  | 

#### Response
the response is: [Question](#question-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/questions/4487fc9d-92e6-4487-a2e8-92e68d6892e6?include=entity
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6", 
    "content":"i want buy nbn",
    "selectedKeywords":[
      {
        "id":"adawsc9d-92e6-4487-a2e8-92e68d6892e6",
        "entityId":"92e6fc9d-92e6-4487-a2e8-92e68d6892e1",
        "entity": {  // include entity
          "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "name": "product",          
        },
        "entityLabel":"product",
        "startPosition":"11",
        "endPosition":"13"
      }
    ]
  }  
```

### Batch add questions

  `POST /api/v3/chatbot/intents/{intentId}/questions:batchCreate` 

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `intentId` | Guid | yes  |  intentId |

Request body

The request body contains data with the list of [Question](#question-object) structure

  example:
```Json 
  [
    {
      "content":"what about nbn",
      "selectedKeywords":[]
    },
    {
      "content":"what is nbn",
      "selectedKeywords":[]
    },
  ]
```

#### Response
the response is: list of [Question](#question-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
    {
      "content":"what about nbn",
      "selectedKeywords":[]
    },
    {
      "content":"what is nbn",
      "selectedKeywords":[]
    },
  ]' -X POST https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6/questions:batchCreate
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"vvd7fc9d-92e6-4487-a2e8-92e68d6892e6", 
      "content":"what about nbn",
      "selectedKeywords":[]
    },
    {
      "id":"12dafc9d-92e6-4487-a2e8-92e68d6892e6", 
      "content":"what is nbn",
      "selectedKeywords":[]
    },
  ]  
```

# Answer in Channel
You need `Manage Bot` permission to manage Intent.
  - `Answer in Channel` - Intent Answer Manage
    +  `GET /api/v3/chatbot/intents/{intentId}/answerInChannels` - [Get AnswerInChannels of the intent](#get-answerInChannels-of-the-intent)
    +  `GET /api/v3/chatbot/answerInChannels/{id}` - [Get AnswerInChannel of the intent by id](#get-AnswerInChannel-of-the-intent-by-id)
    +  `POST /api/v3/chatbot/intents/{intentId}/answerInChannels` - [Create a AnswerInChannel for the intent](#create-a-AnswerInChannel-for-the-intent)
    +  `PUT /api/v3/chatbot/answerInChannels/{id}` - [Update an AnswerInChannel](#update-an-AnswerInChannel)    
    +  `DELETE /api/v3/chatbot/answerInChannels/{id}` - [Remove an AnswerInChannel](#remove-a-AnswerInChannel)

## AnswerInChannel Endpoints
### Get AnswerInChannels of the intent

  `GET /api/v3/chatbot/intents/{intentId}/answerInChannels`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `intentId` | Guid | yes  |  intentId |

#### Response
the response is: list of [AnswerInChannel](#AnswerInChannel-object) objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6/answerInChannels
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "channel":"Default",
      "informationCollectionType" : "none",
      "responses": [
        {
          "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"htmlText",
          "htmlTextVariants":[
            "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
          ],
          "order": 0
        },
      ]
    },
    {
      "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",
      "channel":"Live Chat",      
      "informationCollectionType" : "prompt",  
      "responses": [
        {
          "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"htmlText",
          "htmlTextVariants":[
            "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
          ],
          "order": 0
        },
        {
          "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
          "type":"button",
          "message":"What can i do for help?",
          "buttons":[            
            {
              "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
              "text": "Call Me",
              "type": "triggerAnIntent",
              "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",              
            }        
          ],
          "order": 1
        } 
      ],      
      "informationCollectionType" : "prompt",
      "prompts" : [
        {
          "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
          "entityId":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",         
          "entityLabel":"size",
          "question": "Pick a size",
          "options":["S", "L", "XL"],
        },
      ]    
    },
  ]
```

### Get AnswerInChannel of the intent by id

  `GET /api/v3/chatbot/answerInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the answerInChannel |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - |  - | 
  | `include` | string | no  | | Available value: `intent`, `entity`  | 

#### Response
the response is: [AnswerInChannel](#AnswerInChannel-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/answerInChannels/1487fc9d-92e6-4487-a2e8-92e68d6892e6?include=intent,entity
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  
  {
    "id":"8234fc9d-92e6-4487-a2e8-f9928d681f48",
    "channel":"Live Chat",
    "responses": [
      {
        "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
        "type":"htmlText",
        "htmlTextVariants":[
          "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
        ],
        "order": 0
      },
      {
        "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
        "type":"button",
        "message":"What can i do for help?",
        "buttons":[            
          {
            "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
            "text": "Call Me",
            "type": "triggerAnIntent",
            "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
            "intent": {  //include intent
              "id":"dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
              "name": "Transfer to sales",
              "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
            }
          }        
        ],
        "order": 1
      } 
    ],      
    "informationCollectionType" : "prompt",
    "prompts" : [
      {
        "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
        "entityId":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "entity":{  //include entity
          "id":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "name": "size"            
        },
        "entityLabel":"size",
        "question": "Pick a size",
        "options":["S", "L", "XL"],
      },
    ]
  }
```

### Create a AnswerInChannel for the intent

  `POST /api/v3/chatbot/intents/{intentId}/answerInChannels`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `intentId` | Guid | yes  |  intentId |

Request body 
  
  The request body contains data with the [AnswerInChannel](#AnswerInChannel-object)  structure

  example:
```Json 
  {
    "channel":"SMS",
    "responses": [
      {
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ],
    "informationCollectionType" : "none"
  }
```

#### Response
the response is: [AnswerInChannel](#AnswerInChannel-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"SMS",
    "responses": [
      {
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ],
    "informationCollectionType" : "none"
  }' -X POST https://domain.comm100.com/api/v3/chatbot/intents/1487fc9d-92e6-4487-a2e8-92e68d6892e6/answerInChannels
```
Response
```Json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/answerInChannels/4c21fc9d-92e6-4487-a2e8-92e68d6892e6
  
  {
    "id":"4c21fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"SMS",
    "responses": [
      {
        "id":"csa7fc9d-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ],
    "informationCollectionType" : "none"
  }
```

### Update an AnswerInChannel

  `PUT /api/v3/chatbot/answerInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the answerInChannel |

Request body 
  
  The request body contains data with the [AnswerInChannel](#AnswerInChannel-object) structure

  example:
```Json 
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "responses": [
      {  
        "type":"text",  //create
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ],
    "informationCollectionType" : "none"
  }
```

#### Response
the response is: [AnswerInChannel](#AnswerInChannel-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "responses": [
      {  
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ],
    "informationCollectionType" : "none"
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/answerInChannels/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  
  {
    "id":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "channel":"Default",
    "responses": [
      {
        "id":"92e6fc9d-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "textVariants":[
          "Hi, what can i do for you?", "hello, may i help you?"
        ],
        "order": 0
      }
    ],
    "informationCollectionType" : "none"
  }
```

### Remove an AnswerInChannel

  `DELETE /api/v3/chatbot/answerInChannels/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the answerInChannel |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/answerInChannels/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Authentication Request
You need `Manage Bot` permission to manage Intent and customize the settings for a Channel.
  - `Authentication Request` - Intent Answer Manage
    +  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/authenticationRequest` - [Get authenticationRequest of the answerInChannel](#get-authenticationRequest-of-the-answerInChannel)   
    +  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/authenticationRequest` - [Create a authenticationRequest for the answerInChannel](#create-a-authenticationRequest-for-the-answerInChannel)
    +  `PUT /api/v3/chatbot/authenticationRequests/{id}` - [Update a authenticationRequest](#update-a-authenticationRequest)    
    +  `DELETE /api/v3/chatbot/authenticationRequests/{id}` - [Remove a authenticationRequest by id](#remove-a-authenticationRequest-by-id)

## Authentication Request Endpoints
### Get AuthenticationRequest of the answerInChannel

  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/authenticationRequest`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

#### Response
the response is: [Authentication Request](#authenticationrequest-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/authenticationRequest
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"dawda111-92e6-4487-a2e8-92e68d6892e6",
    "signInMessage": "Please Login",
    "signInButtonText": "Login",
    "methord": "sso"  
  }
``` 

### Create a AuthenticationRequest for the answerInChannel

  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/authenticationRequest`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Request body 
  
The request body contains data with the [Authentication Request](#authenticationrequest-object) structure

example:
  ```json 
    {
      "signInMessage": "Please Login",
      "signInButtonText": "Login",
      "methord": "customVariable",
      "signInURL":"https://my-domian.com/login.php",
      "customVariable":"token"
    }
```

#### Response
the response is: [Authentication Request](#authenticationrequest-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "signInMessage": "Please Login",
      "signInButtonText": "Login",
      "methord": "customVariable",
      "signInURL":"https://my-domian.com/login.php",
      "customVariable":"token"
    }' -X POST https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/authenticationRequest
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/authenticationRequest

  {
    "id":"dawda111-92e6-4487-a2e8-92e68d6892e6",
    "signInMessage": "Please Login",
    "signInButtonText": "Login",
    "methord": "customVariable",
    "signInURL":"https://my-domian.com/login.php",
    "customVariable":"token"
  }
```  

### Update a AuthenticationRequest

  `PUT /api/v3/chatbot/authenticationRequests/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the authenticationRequest |

Request body 
  
The request body contains data with the [Authentication Request](#authenticationrequest-object) structure

example:
  ```json 
    {
      "id":"bbwfe21d-92e6-4487-a2e8-92e68d6892e6",
      "signInMessage": "Please Login",
      "signInButtonText": "Login",
      "methord": "customVariable",
      "signInURL":"https://my-domian.com/login.php",
      "customVariable":"token"
    }
```

#### Response
the response is: [Authentication Request](#authenticationrequest-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "id":"bbwfe21d-92e6-4487-a2e8-92e68d6892e6",
      "signInMessage": "Please Login",
      "signInButtonText": "Login",
      "methord": "customVariable",
      "signInURL":"https://my-domian.com/login.php",
      "customVariable":"token"
    }' -X PUT https://domain.comm100.com/api/v3/chatbot/authenticationRequests/bbwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"bbwfe21d-92e6-4487-a2e8-92e68d6892e6",
    "signInMessage": "Please Login",
    "signInButtonText": "Login",
    "methord": "customVariable",
    "signInURL":"https://my-domian.com/login.php",
    "customVariable":"token"
  }
``` 

### Remove a AuthenticationRequest by id

  `DELETE /api/v3/chatbot/authenticationRequests/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the authenticationRequest |

#### Response
HTTP/1.1 204 No Content


#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/authenticationRequests/bbwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```


# Location Request
You need `Manage Bot` permission to manage Intent and customize the settings for a Location Request.
  - `Location Request` - Intent Answer Manage
    +  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/locationRequest` - [Get LocationRequest of the answerInChannel](#get-LocationRequest-of-the-answerInChannel)
    +  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/locationRequest` - [Create a LocationRequest for the answerInChannel](#create-a-LocationRequest-for-the-answerInChannel)
    +  `PUT /api/v3/chatbot/locationRequests/{id}` - [Update a LocationRequest](#update-a-LocationRequest)    
    +  `DELETE /api/v3/chatbot/locationRequests/{id}` - [Remove a LocationRequest](#remove-a-LocationRequest-by-id)

## LocationRequest Endpoints
### Get LocationRequest of the answerInChannel

  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/locationRequest`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

#### Response
the response is: [Location Request](#LocationRequest-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/locationRequest
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please Share your location",
    "buttonText": "Share"
  }
``` 

### Create a LocationRequest for the answerInChannel

  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/locationRequest`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Request body 
  
The request body contains data with the [Location Request](#LocationRequest-object) structure

example:
  ```json 
    {
      "message": "Please Share your location",
      "buttonText": "Share"
    }
```

#### Response
the response is: [Location Request](#LocationRequest-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "message": "Please Share your location",
      "buttonText": "Share"
    }' -X POST https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/locationRequest
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/locationRequest


  {
    "id":"aawda111-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please Share your location",
    "buttonText": "Share"
  }
``` 


### Update a LocationRequest

  `PUT /api/v3/chatbot/locationRequests/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the locationRequest |

Request body 
  
  The request body contains data with the [Location Request](#LocationRequest-object) structure

example:
  ```json 
    {
      "id": "ccwfe21d-92e6-4487-a2e8-92e68d6892e6",
      "message": "Please Share your location",
      "buttonText": "Share"
    }
```

#### Response
the response is: [Location Request](#LocationRequest-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "id": "ccwfe21d-92e6-4487-a2e8-92e68d6892e6",
      "message": "Please Share your location",
      "buttonText": "Share"
    }' -X PUT https://domain.comm100.com/api/v3/chatbot/locationRequests/ccwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "ccwfe21d-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please Share your location",
    "buttonText": "Share"
  }
``` 

### Remove a LocationRequest by id

  `DELETE /api/v3/chatbot/locationRequests/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the locationRequest |

#### Response
HTTP/1.1 204 No Content


#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/locationRequests/ccwfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Form
You need `Manage Bot` permission to manage Intent and customize the settings for an intent answer form.
  - `Form` - Intent Answer Form Manage
    +  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/form` - [Get Form of the answerInChannel](#get-form-of-the-answerInChannel)
    +  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/form` - [Create a Form for the answerInChannel](#create-a-Form-for-the-answerInChannel)
    +  `PUT /api/v3/chatbot/forms/{id}` - [Update a Form](#update-a-Form)    
    +  `DELETE /api/v3/chatbot/forms/{id}` - [Remove a Form by id](#remove-a-Form-by-id)

## Form Endpoints
### Get Form of the answerInChannel

  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/form`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  |  | Available value: `entity`  | 


#### Response
the response is: [Form](#form-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/form?include=entity
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "entity":{  //include entity
          "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "name": "city",          
        },
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ],
  }
``` 

### Create a Form for the answerInChannel

  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/form`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Request body   
    
  The request body contains data with the [Form](#form-object) structure

example:
  ```json 
  {
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "type":"text",
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",        
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ]
  }
```

#### Response
the response is: [Form](#form-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "type":"text",
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",        
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ]
  }' -X POST https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/form
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/form

  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "entity":{  //include entity
          "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "name": "city",          
        },
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ],
  }
```   


### Update a Form

  `PUT /api/v3/chatbot/forms/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the form |

Request body 
    
  The request body contains data with the [Form](#form-object) structure

example:
  ```json 
  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "type":"text",   //create
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",  //update
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",        
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ]
  }
```

#### Response
the response is: [Form](#form-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "type":"text",   //create
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",  //update
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",        
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ]
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/forms/ge2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "message": "Please fill the information first",
    "title": "Fill a Form",
    "isConfirmationRequired": true,
    "fields": [
      {
        "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
        "type":"text",
        "name":"email",
        "entityId":"",
        "entityLabel":"",
        "isRequired":true,
        "isMasked":true,
      },
      {
        "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
        "type":"dropDownList",
        "name":"city",
        "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",       
        "entityLabel":"city",
        "isRequired":true,
        "isMasked":true,
        "options":["beijing", "hangzhou"],
      }
    ],
  }
``` 

### Remove a Form by id

  `DELETE /api/v3/chatbot/forms/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the form |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/forms/ge2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Field
You need `Manage Bot` permission to manage Intent and customize the settings for an intent answer form fields.
  - `Form Fields` - Intent Answer Manage
    +  `GET /api/v3/chatbot/forms/{formId}/fields` - [Get all fields of the form](#get-all-fields-of-the-form)
    +  `GET /api/v3/chatbot/fields/{id}` - [Get a field by id](#Get-a-field-by-id)    
    +  `POST /api/v3/chatbot/forms/{formId}/fields` - [Create a new field of the form](#create-a-new-field-of-the-form)
    +  `PUT /api/v3/chatbot/fields/{id}` - [Update a field](#update-a-field)    
    +  `DELETE /api/v3/chatbot/fields/{id}` - [Remove a field](#remove-a-field)

## Field Endpoints
### Get all fields of the form

  `GET /api/v3/chatbot/forms/{formId}/fields`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `formId` | Guid | yes  |  the unique id of the form |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `include` | string | no  | | Available value: `entity`  | 


#### Response
the response is: an array of [Field](#Field-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/forms/ge2341sa-92e6-4487-a2e8-92e68d6892e6/fields?include=entity
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
      "type":"text",
      "name":"email",
      "entityId":"",
      "entityLabel":"",
      "isRequired":true,
      "isMasked":true,
    },
    {
      "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
      "type":"dropDownList",
      "name":"city",
      "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "entity":{  //include entity
        "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "name": "city",        
      },
      "entityLabel":"city",
      "isRequired":true,
      "isMasked":true,
      "options":["beijing", "hangzhou"],
    }
  ]
``` 

### Get a field by id

  `GET /api/v3/chatbot/fields/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the field |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - |  - | 
  | `include` | string | no  |  | Available value: `entity`  | 

#### Response
the response is: [Field](#Field-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/fields/gg2341sa-92e6-4487-a2e8-92e68d6892e6?include=entity
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
    "type":"dropDownList",
    "name":"city",
    "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
    "entity":{  //include entity
      "id":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "name": "city",      
    },
    "entityLabel":"city",
    "isRequired":true,
    "isMasked":true,
    "options":["beijing", "hangzhou"],
  }  
``` 

### Create a new field of the form

  `POST /api/v3/chatbot/forms/{formId}/fields`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `formId` | Guid | yes  |  the unique id of the form |

Request body 

The request body contains data with the [Field](#Field-object) structure

example:
  ```json 

{
  "type":"dropDownList",
  "name":"city",
  "entityId":"",        
  "entityLabel":"",
  "isRequired":true,
  "isMasked":true,
  "options":["beijing", "hangzhou"],
}
```

#### Response
the response is:  [Field](#Field-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
  "type":"dropDownList",
  "name":"city",
  "entityId":"",        
  "entityLabel":"",
  "isRequired":true,
  "isMasked":true,
  "options":["beijing", "hangzhou"],
}' -X POST https://domain.comm100.com/api/v3/chatbot/forms/ge2341sa-92e6-4487-a2e8-92e68d6892e6/fields
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/fields/dw2341sa-92e6-4487-a2e8-92e68d6892e6
  
  {
    "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
    "type":"dropDownList",
    "name":"city",
    "entityId":"",        
    "entityLabel":"",
    "isRequired":true,
    "isMasked":true,
    "options":["beijing", "hangzhou"],
  }
``` 

### Update a field

  `PUT /api/v3/chatbot/fields/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the field |

Request body 
  
  The request body contains data with the [Field](#Field-object) structure

example:
  ```json 

{
  "id": "gg2341sa-92e6-4487-a2e8-92e68d6892e6",
  "type":"dropDownList",
  "name":"city",
  "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",        
  "entityLabel":"city",
  "isRequired":true,
  "isMasked":true,
  "options":["beijing", "hangzhou", "changsha"],
}
```

#### Response
the response is: [Field](#Field-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
  "id": "gg2341sa-92e6-4487-a2e8-92e68d6892e6",
  "type":"dropDownList",
  "name":"city",
  "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",        
  "entityLabel":"city",
  "isRequired":true,
  "isMasked":true,
  "options":["beijing", "hangzhou", "changsha"],
}' -X PUT https://domain.comm100.com/api/v3/chatbot/fields/gg2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
    "type":"dropDownList",
    "name":"city",
    "entityId":"a2e8sc9d-92e6-4487-a2e8-92e68d6892e6",    
    "entityLabel":"city",
    "isRequired":true,
    "isMasked":true,
    "options":["beijing", "hangzhou", "changsha"],
  }  
``` 

### Remove a field

  `DELETE /api/v3/chatbot/fields/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the field |

#### Response
HTTP/1.1 204 No Content


#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/fields/gg2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```


# Prompt
You need `Manage Bot` permission to manage Intent and customize the settings for  intent answer prompts.
  - `Prompts` - Intent Answer Manage
    +  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/prompts` - [Get prompts of the answerInChannel](#get-prompts-of-the-answerInChannel)
    +  `GET /api/v3/chatbot/prompts/{id}` - [Get prompt of the intent by id](#get-prompts-of-the-answerInChannel-by-id)
    +  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/prompts` - [Create a prompt for the answerInChannel](#create-a-prompt-for-the-answerInChannel)
    +  `PUT /api/v3/chatbot/prompts/{id}` - [Update a prompt](#update-a-prompt)    
    +  `DELETE /api/v3/chatbot/prompts/{id}` - [Remove a prompt](#remove-a-prompt)

## Prompts Endpoints
### Get prompts of the answerInChannel

  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/prompts`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - |  - | 
  | `include` | string | no  | | Available value: `entity`  | 

#### Response
the response is: an array of [Prompt](#prompt-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/prompts?include=entity
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"dw2341sa-92e6-4487-a2e8-92e68d6892e6",
      "entityId":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "entity":{  //include entity
        "id":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "name": "size"        
      },
      "entityLabel":"size",
      "question": "Pick a size",
      "options":["S", "L", "XL"],
    },
    {
      "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
      "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "entity":{  //include entity
        "id":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "name": "sys-color",        
      },
      "entityLabel":"color",
      "question": "Pick a color",
      "options":["red", "blue", "white"],
    }
  ]
``` 


### Get prompt of the answerInChannel by id

  `GET /api/v3/chatbot/prompts/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the prompt |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - |
  | `include` | string | no  | |  Available value: `entity`  | 

#### Response
the response is: [Prompt](#prompt-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/prompts/gg2341sa-92e6-4487-a2e8-92e68d6892e6?include=entity
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
    "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
    "entity":{  //include entity
      "id":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "name": "sys-color",        
    },
    "entityLabel":"color",
    "question": "Pick a color",
    "options":["red", "blue", "white"],
  }
``` 

### Create a prompt for the answerInChannel

  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/prompts`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |


Request body   

The request body contains data with the [Prompt](#prompt-object) structure

example:
  ```json 
  {
    "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",    
    "entityLabel":"color",
    "question": "Pick a color",
    "options":["red", "blue", "white"],
  }
```

#### Response
the response is: [Prompt](#prompt-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",    
    "entityLabel":"color",
    "question": "Pick a color",
    "options":["red", "blue", "white"],
  }' -X POST https://domain.comm100.com/api/v3/chatbot/answerInChannels/ge2341sa-92e6-4487-a2e8-92e68d6892e6/prompts
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/prompts/gg2341sa-92e6-4487-a2e8-92e68d6892e6

    {
      "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",      
      "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6", 
      "entityLabel":"color",
      "question": "Pick a color",
      "options":["red", "blue", "white"]  
    }  
``` 


### Update a prompt

  `PUT /api/v3/chatbot/prompts/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the prompt |

Request body 

  The request body contains data with the [Prompt](#prompt-object) structure

example:
```json
  {
    "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
    "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
    "entityLabel":"color",
    "question": "What color",
    "options":[],
  }
``` 

#### Response
the response is: [Prompt](#prompt-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
    "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
    "entityLabel":"color",
    "question": "What color",
    "options":[],
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/prompts/gg2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
    "entityId":"aee8sc9d-92e6-4487-a2e8-92e68d6892e6",
    "entityLabel":"color",
    "question": "What color",
    "options":[],
  }
``` 

### Remove a prompt

  `DELETE /api/v3/chatbot/prompts/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the prompt |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/prompts/gg2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Chatbot Response
  +  `GET /api/v3/chatbot/greetingMessageInChannels/{greetingMessageInChannelId}/responses` - [Get all responses of the greetingMessageInChannel](#get-all-responses-of-the-greetingMessageInChannel)   
  +  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/responses` - [Get all responses of the answerInChannel](#get-all-responses-of-the-answerInChannel)   
  +  `GET /api/v3/chatbot/responses/{id}` - [Get a response by id](#get-a-response-by-id)
  +  `POST /api/v3/chatbot/greetingMessageInChannels/{greetingMessageInChannelId}/responses` - [Create a response for the greetingMessageInChannel](#create-a-response-for-the-greetingMessageInChannel)
  +  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/responses` - [Create a response for the answerInChannel](#create-a-response-for-the-answerInChannel)
  +  `PUT /api/v3/chatbot/responses/{id}` - [Update a response](#update-a-response)    
  +  `DELETE /api/v3/chatbot/responses/{id}` - [Remove a response](#remove-a-response)

## Response Endpoints
### Get all responses of the greetingMessageInChannel

  `GET /api/v3/chatbot/greetingMessageInChannels/{greetingMessageInChannelId}/responses`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `greetingMessageInChannelId` | Guid | yes  |  the id of the greetingMessageInChannel |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent`  | 

#### Response
the response is: list of [Response](#response-object) objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/greetingMessageInChannels/f9928d68-92e6-4487-a2e8-8234fc9d1f48/responses?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 0
    },
    {
      "id":"a4e8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"video",
      "videoUrl":"https://yutoob.com/v/sdwada_sdawcv5qwe13",
      "order": 1
    },
    {
      "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"button",
      "message":"What can i do for help?",
      "buttons":[
        {
          "id":"dww12345-92e6-4487-a2e8-92e68d6892e6",
          "text": "Get Order Status",
          "type": "webView",
          "url": "https://taobao.com",
          "openStyle": "full"
        },
        {
          "id":"dwa1234s4-92e6-4487-a2e8-92e68d6892e6",
          "text": "Get Order List",
          "type": "link",
          "url": "https://taobao.com",
          "openIn": "sideWindow"
        },
        {
          "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
          "text": "Call Me",
          "type": "triggerAnIntent",
          "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
          "intent": {  //include intent
            "id":"dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
            "name": "Transfer to sales",
            "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
          }
        }        
      ],
      "order": 2
    },      
    ...
  ]
```

### Get all responses of the answerInChannel

  `GET /api/v3/chatbot/answerInChannels/{answerInChannelId}/responses`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent`  | 

#### Response
the response is: an array of [Response](#response-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/answerInChannels/1487fc9d-92e6-4487-a2e8-92e68d6892e6/responses?include=intent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 0
    },
    {
      "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"button",
      "message":"What can i do for help?",
      "buttons":[            
        {
          "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
          "text": "Call Me",
          "type": "triggerAnIntent",
          "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
          "intent": {  //include intent
            "id":"dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
            "name": "Transfer to sales",
            "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
          }
        }        
      ],
      "order": 1
    },
    {
      "id":"sc38fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"webhook",
      "webhook":{
        "id":"2dawdaww-92e6-4487-a2e8-92e68d6892e6",
        "url": "https://mysystem.com/botHandler/api",
        "headers": {
          "Authorization":"Basic YWRtaW46YWRtaW4="
        },              
      },
      "order": 2
    }
  ]
```

### Get a response by id

  `GET /api/v3/chatbot/responses/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the response |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  |  | Available value: `intent`  | 

#### Response
the response is: [Response](#response-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/responses/daw8fc9d-92e6-4487-a2e8-92e68d6892e6?include=intent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"daw8fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type":"button",
    "message":"What can i do for help?",
    "buttons":[            
      {
        "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
        "text": "Call Me",
        "type": "triggerAnIntent",
        "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
        "intent": {  //include intent
          "id":"dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",
          "name": "Transfer to sales",
          "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
        }
      }        
    ],
    "order": 1
  }
```

### Create a response for the greetingMessageInChannel

  `POST /api/v3/chatbot/greetingMessageInChannels/{greetingMessageInChannelId}/responses`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `greetingMessageInChannelId` | Guid | yes  |  the id of the greetingMessageInChannel |


Request body

  The request body contains data with the [Response](#response-object) structure

  example:
  ```json  
    {
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 0
    }
```

#### Response
the response is: [Response](#response-object) object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 0
    }
' -X POST https://domain.comm100.com/api/v3/chatbot/greetingMessageInChannels/f9928d68-92e6-4487-a2e8-8234fc9d1f48/responses
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/responses/a2e8fc9d-92e6-4487-a2e8-92e68d6892e6

  {
    "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",      
    "type":"htmlText",
    "htmlTextVariants":[
      "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
    ],
    "order": 0
  }
```

### Create a response for the answerInChannel

  `POST /api/v3/chatbot/answerInChannels/{answerInChannelId}/responses`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `answerInChannelId` | Guid | yes  |  the unique id of the answerInChannel |

Request body

  The request body contains data with the [Response](#response-object) structure

  example:
  ```json  
    {
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 0
    }
```

#### Response
the response is: [Response](#response-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 0
    }' -X POST https://domain.comm100.com/api/v3/chatbot/answerInChannels/1487fc9d-92e6-4487-a2e8-92e68d6892e6/responses
```
Response
```Json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/responses/a2e8fc9d-92e6-4487-a2e8-92e68d6892e6

  {
    "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type":"htmlText",
    "htmlTextVariants":[
      "<div>Hi, what can i do for you?</div>", 
      "<div>hello, may i help you?</div>"
    ],
    "order": 0
  }
```

### Update a response

  `PUT /api/v3/chatbot/responses/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the id of the response |

Request body 
  
  The request body contains data with the [Response](#response-object) structure

example:
  ```json 
    {
      "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 2
    }
```
#### Response
the response is: [Response](#response-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
      "type":"htmlText",
      "htmlTextVariants":[
        "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
      ],
      "order": 2
    }' -X PUT https://domain.comm100.com/api/v3/chatbot/responses/a2e8fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type":"htmlText",
    "htmlTextVariants":[
      "<div>Hi, what can i do for you?</div>", "<div>hello, may i help you?</div>"
    ],
    "order": 2
  }
```

### Remove a response

  `DELETE /api/v3/chatbot/responses/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the response |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/responses/a2e8fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Button
You need `Manage Bot` permission to manage buttons in response.
  - `Buttons` - Buttons Manage
    +  `GET /api/v3/chatbot/responses/{responseId}/buttons` - [Get all buttons of the response](#get-all-buttons-of-the-response)
    +  `GET /api/v3/chatbot/buttons/{id}` - [Get a button by id](#Get-a-button-by-id)    
    +  `POST /api/v3/chatbot/responses/{responseId}/buttons` - [Create a new button of the response](#create-a-new-button-of-the-response)
    +  `PUT /api/v3/chatbot/buttons/{id}` - [Update a button](#update-a-button)    
    +  `DELETE /api/v3/chatbot/buttons/{id}` - [Remove a button](#remove-a-button)

## Button Endpoints
### Get all buttons of the response

  `GET /api/v3/chatbot/responses/{responseId}/buttons`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `responseId` | Guid | yes  |  the unique id of the response |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent`  | 

#### Response
the response is: an array of [Button](#button-object) objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/responses/1487fc9d-92e6-4487-a2e8-92e68d6892e6/buttons?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"dww12345-92e6-4487-a2e8-92e68d6892e6",
      "text": "Get Order Status",
      "type": "webView",
      "url": "https://taobao.com",
      "openStyle": "full"
    },    
    {
      "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
      "text": "Call Me",
      "type": "triggerAnIntent",
      "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",  
      "intent": { //include intent        
        "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "name":"buy nbn",
        "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",        
      }    
    }
  ]
```

### Get a button by id

  `GET /api/v3/chatbot/buttons/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the button |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent`  | 

#### Response
the response is: [Button](#button-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/buttons/ge2341sa-92e6-4487-a2e8-92e68d6892e6?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "text": "Call Me",
    "type": "triggerAnIntent",
    "intentId": "dawdlkiu7-92e6-4487-a2e8-92e68d6892e6",  
    "intent": { //include intent        
      "id":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "name":"buy nbn",
      "categoryId": "4487fc9d-92e6-4487-a2e8-92e68d6892e6"  
    }    
  }
```   
### Create a new button of the response

  `POST /api/v3/chatbot/responses/{responseId}/buttons`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `responseId` | Guid | yes  |  the unique id of the response |

Request body 
  
The request body contains data with the [Button](#button-object) structure

example:
  ```json 
    {
      "text": "Get Order Status",
      "type": "webView",
      "url": "https://taobao.com",
      "openStyle": "full"
    }
```

#### Response
the response is: an array of [Button](#button-object) objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "text": "Get Order Status",
      "type": "webView",
      "url": "https://taobao.com",
      "openStyle": "full"
    }' -X POST https://domain.comm100.com/api/v3/chatbot/responses/1487fc9d-92e6-4487-a2e8-92e68d6892e6/buttons
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/buttons/dww12345-92e6-4487-a2e8-92e68d6892e6

  {
    "id":"dww12345-92e6-4487-a2e8-92e68d6892e6",
    "text": "Get Order Status",
    "type": "webView",
    "url": "https://taobao.com",
    "openStyle": "full"
  }
```  

### Update a button

  `PUT /api/v3/chatbot/buttons/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the button |

Request body 

The request body contains data with the [Button](#button-object) structure

example:
  ```json 
  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "text": "Get Order Status",
    "type": "webView",
    "url": "https://taobao.com",
    "openStyle": "tall"    
  }
```

#### Response
the response is: [Button](#button-object) object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "text": "Get Order Status",
    "type": "webView",
    "url": "https://taobao.com",
    "openStyle": "tall"    
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/buttons/ge2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"ge2341sa-92e6-4487-a2e8-92e68d6892e6",
    "text": "Get Order Status",
    "type": "webView",
    "url": "https://taobao.com",
    "openStyle": "tall"    
  }
```  

### Remove a button

  `DELETE /api/v3/chatbot/buttons/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the button |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/buttons/ge2341sa-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Session
  - `POST /api/v3/chatbot/sessions/{sessionId}:greeting` - [chatbot greeting](#chatbot-greeting)
  - `POST /api/v3/chatbot/sessions/{sessionId}:detectIntent` - [Detect intent](#detect-intent)
  - `POST /api/v3/chatbot/sessions/{sessionId}:triggerAnIntent` - [Trigger an intent](#trigger-an-intent)
  - `POST /api/v3/chatbot/sessions/{sessionId}:submitForm` - [Submit Form](#Submit-Form)
  - `POST /api/v3/chatbot/sessions/{sessionId}:submitAuthentication` -  [Submit Authentication](#Submit-Authentication)
  - `POST /api/v3/chatbot/sessions/{sessionId}:submitLocation` - [Submit Location](#submit-location)
  - `POST /api/v3/chatbot/sessions/{sessionId}:rate` - [Rate the bot answer as helpful or not helpful](#rate-the-bot-answer-as-helpful-or-not-helpful)

## Related Object Json Format
### HighConfidenceAnswer

  HighConfidenceIntent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post  | Default | Description |    
  | - | - | :-: | :-: | - | - |
  | `intentId` | Guid  | N/A | N/A |  | id of the matched intent |
  | `intentName` | string  | N/A | N/A |  | name of the matched intent |
  | `score` | float  | N/A | N/A |  | the score of the intent matched, the value is beteween 0.0 and 100.0 |
  |`answer`| [AnswerInChannel](#AnswerInChannel-object) | N/A | N/A | | | N/A | N/A | | intent answer |


### PossibleAnswer

  PossibleAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post  | Default | Description |    
  | - | - | :-: | :-: | - | - | 
  | `messageWhenProvidingPossibleAnswer` | string  | N/A | N/A | | message of the possible response |
  | `intents` | [IntentScore](#IntentScore-object)[]  | N/A | N/A | | an array of [IntentScore](#IntentScore-object)   | 
  | `messageAfterSeveralConsecutivePossibleAnswers` | [MessageAfterSeveralConsecutivePossibleAnswers](#MessageAfterSeveralConsecutivePossibleAnswersInChannel-Object)  | N/A | N/A | |  |

### NoAnswer

  NoAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post  | Default | Description |    
  | - | - | :-: | :-: | - | - | 
  | `intentId` | Guid  | N/A | N/A |  | id of the matched intent |
  | `intentName` | string  | N/A | N/A |  | name of the matched intent |
  | `score` | float  | N/A | N/A |  | the score of the intent matched, the value is beteween 0.0 and 100.0 |
  |`answer`| [NoAnswerMessageInChannel](#NoAnswerMessageInChannel-object) | N/A | N/A | | |

## Endpoints

### Chatbot greeting
`POST /api/v3/chatbot/sessions/{sessionId}:greeting`

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
  | `botId` | Guid  | yes | | id of the bot |
  | `extra` | Map | no | | extra data, this data will be transferred to webhook. |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111"
    }
  }
```

#### Response
the response is:
 [GreetingMessageInChannel](#GreetingMessageInChannel-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111"
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:greeting
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "channel": "Facebook Messenger",
    "responses":[
      {
        "type":"htmlText",
        "htmlTextVariants":[
          "<div>Hi, what can i do for you?</div>"
        ],
      },
      {
        "type":"image",
        "image":{
          "id": "1dw142323-92e6-4487-a2e8-92e68d6892e6",
          "name":"greeting.png",
          "url": "https://bot.comm100.com/botapi/images/greeting.png"
        },
      }
    ]
  }
```

### Detect intent
`POST /api/v3/chatbot/sessions/{sessionId}:detectIntent`

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
  | `botId` | Guid  | yes | | id of the bot |
  | `question` | string  | yes | | visitor question |
  | `speech` | string  | yes | | when channel is `Voice`, visitor speech |
  | `extra` | Map | no | | extra data, this data will be transferred to webhook. example: you can assign authentication data or location data which your webhook will use |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "question":"i want to buy NBN",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111"
    }
  }
```

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `questionId` | Guid  | N/A | N/A |  | the unique id of the question |
  | `question` | string  | N/A | N/A |  | visitor question | 
  | `type` | string  | yes | | type of the response,including `highConfidenceAnswer`、`possibleAnswer`、`noAnswer`, `authenticationRequest` |
  | `smartTriggerActions` | [SmartTriggerAction](#smart-trigger-action-object)[] | no |  | an array of [SmartTriggerAction](#smart-trigger-action-object) objects. |
  | `content` | object | yes |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer); when type is `possibleAnswer`,it represents [PossibleAnswer](#PossibleAnswer);when type is `noAnswer`,it represents [NoAnswer](#NoAnswer); when type is `authenticationRequest`, it represents [AuthenticationRequest](#AuthenticationRequest-Object) |

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "question":"i want to buy NBN",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111"
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:detectIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "questionId": "89928d68-92e6-4487-a2e8-92e68d6892e6",
    "question":"i want to buy NBN",
    "type": "highConfidenceAnswer",
    "content": {
      "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
      "intentName": "buy nbn",
      "score": 89.25,
      "answer":{
        "channel": "Facebook Messenger",
        "responses":[
          {
            "type":"htmlText",
            "htmlTextVariants":[
              "<div>Hi, what can i do for you?</div>"
            ],
          },
          {
            "type":"image",
            "image":{
              "id": "1dw142323-92e6-4487-a2e8-92e68d6892e6",
              "name":"greeting.png",
              "url": "https://bot.comm100.com/botapi/images/greeting.png"
            },
          }
        ]
      } 
    }
  }
```

### Trigger an intent
`POST /api/v3/chatbot/sessions/{sessionId}:triggerAnIntent`

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
  | `botId` | Guid  | yes | | id of the bot |
  | `intentId` | Guid  | yes | | id of the intent triggered |
  | `extra` | Map | no | | extra data, this data will be transferred to webhook. example: you can assign authentication data or location data which your webhook will use |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111"
    }
  }
```

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | yes | | type of the response,including `highConfidenceAnswer`、`noAnswer` |
  | `smartTriggerActions` | [SmartTriggerAction](#smart-trigger-action-object)[] | no |  | an array of [SmartTriggerAction](#smart-trigger-action-object) objects. |
  | `content` | object | yes |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer); when type is `noAnswer`,it represents [NoAnswer](#NoAnswer) |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "intentId":"8d6892e6-92e6-4487-a2e8-92e68d6892e6",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111"
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:triggerAnIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "type": "highConfidenceAnswer",
    "content": {
    "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
    "intentName": "buy nbn",
      "score": 100,
      "answer":{
        "channel": "Facebook Messenger",
        "authenticationRequest":{
          "signInMessage": "Please Login",
          "signInButtonText": "Login",
          "methord": "sso"  
        }
      } 
    }
  }
```

### Submit Authentication
`POST /api/v3/chatbot/sessions/{sessionId}:submitAuthentication`

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
  | `botId` | Guid  | yes | | id of the bot |
  | `authentication` | string  | yes | | authentication data |
  | `extra` | Map | no | | extra data, this data will be transferred to webhook. example: you can assign authentication data or location data which your webhook will use |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "authentication": "vcw1fc9d-92e6-4487-a2e8-92e68d68dsww",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }
```

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | yes | | type of the response,including `highConfidenceAnswer`、`noAnswer` |  
  | `content` | object | yes |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer); when type is `noAnswer`,it represents [NoAnswer](#NoAnswer) |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "authentication": "vcw1fc9d-92e6-4487-a2e8-92e68d68dsww",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitAuthentication
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
{
  "type": "highConfidenceAnswer",
  "content": {
    "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
    "intentName": "buy nbn",
    "score": 100,
    "answer":{
      "channel": "Facebook Messenger",
      "locationRequest":{
        "message": "Please Share your location",
        "buttonText": "Share"
      }
    }     
  }
}
```

### Submit Location
`POST /api/v3/chatbot/sessions/{sessionId}:submitLocation`

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
  | `botId` | Guid  | yes | | id of the bot |
  | `location` | string  | yes | | the longitude and latitude of the location, eg: "39.900000,116.300000" |
  | `extra` | Map | no | | extra data, this data will be transferred to webhook. example: you can assign authentication data or location data which your webhook will use |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "location":"39.9000,116.3000",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }
```

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | yes | | type of the response,including `highConfidenceAnswer`、`noAnswer` |  
  | `content` | object | yes |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer); when type is `noAnswer`,it represents [NoAnswer](#NoAnswer) |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "location":"39.9000,116.3000",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitLocation
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
  "type": "highConfidenceAnswer",
  "content": {
    "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
    "intentName": "buy nbn",
    "score": 100,
    "answer":{
      "channel": "Facebook Messenger",
      "form":{
        "message": "Please fill the information first",
        "title": "Fill a Form",
        "isConfirmationRequired": true,
        "fields": [
          {
            "type":"text",
            "name":"email",
            "isRequired":true,
            "isMasked":true,
          },
          {
            "type":"dropDownList",
            "name":"city",
            "isRequired":true,
            "isMasked":true,
            "options":["beijing", "hangzhou"],
          }
        ],
      }
    }     
  }
}
```

### Submit Form
`POST /api/v3/chatbot/sessions/{sessionId}:submitForm`

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
  | `botId` | Guid  | yes | | id of the bot |
  |`formValues` | [FieldValue](#FieldValue-object)[] | yes | | an array of [FieldValue](#FieldValue-object) objects |
  | `extra` | Map | no | | extra data, this data will be transferred to webhook. example: you can assign authentication data or location data which your webhook will use |

example:
```Json 
  {
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
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
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }
```

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | yes | | type of the response,including `highConfidenceAnswer`、`noAnswer` |  
  | `content` | object | yes |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer); when type is `noAnswer`,it represents [NoAnswer](#NoAnswer) |


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Facebook Messenger",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
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
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitForm
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json
{
  "type": "highConfidenceAnswer",
  "content": {
    "intentId": "7534fdsca-92e6-4487-a2e8-92e68d6892e6",
    "intentName": "buy nbn",
    "score": 100,
    "answer":{
      "channel": "Facebook Messenger",
      "responses":[
        {
          "type":"htmlText",
          "htmlTextVariants":[
            "<div>Hi, what can i do for you?</div>"
          ],
        },
        {
          "type":"image",
          "image":{
            "id": "1dw142323-92e6-4487-a2e8-92e68d6892e6",
            "name":"greeting.png",
            "url": "https://bot.comm100.com/botapi/images/greeting.png"
          },
        }
      ]
    } 
  }  
}
```

### Rate the bot answer as helpful or not helpful

  `POST /api/v3/chatbot/sessions/{sessionId}:rate`

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
  | `botId` | Guid  | yes | | id of the bot |
  | `questionId` | Guid  | yes | | the id of the visitor question |
  | `type` | string  | yes  | | `helpful` or `notHelpful` |
  | `extra` | Map | no | | extra data which SmartTrigger used |

  example:
```Json 
  {
    "channel":"Live Chat",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questionId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "notHelpful",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }
```
#### Response
If bot was rated helpful, the response will be empty.

If bot is rated not helpful, the response body contains data with the following structure:

  | Name | Type | Required  | Default | Description |    
  | - | - | :-: | :-: | - | 
  |`messageWhenNotHelpful` | string | yes |  | text of the message  | 
  |`ifIncludeContactAgentOptionWhenNotHelpful` | bool | yes |  | include Contact An Agent or not . |  
  | `smartTriggerActionsWhenNotHelpful` | [SmartTriggerAction](#smart-trigger-action-object)[] | no | | if smart trigger conditions contain the condition `rate as not helpful is true` |

#### Example
- Rate the bot as not helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questionId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",    
    "type": "notHelpful",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/1487fc9d-92e6-4487-a2e8-92e68d6892e6:rate
```
  Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "messageWhenNotHelpful":"I am sorry that this doesn't answer your question. Please click on following button to connect to an agent.",
    "ifIncludeContactAgentOptionWhenNotHelpful": true,
    "smartTriggerActionsWhenNotHelpful":[
      {
        "type":"transfer", 
        "isEnabled": true,
        "targetType": "department",
        "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
      }
    ]
  }
```

- Rate the bot as helpful

  Using curl
```
curl -H "Content-Type: application/json" -d '{
    "channel":"Live Chat",
    "botId":"4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "questionId":"a2e8fc9d-92e6-4487-a2e8-92e68d6892e6",
    "type": "helpful",
    "extra": {
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
      "ip":"12.25.11.111",
    }
  }' -X POST https://domain.comm100.com/api/v3/chatbot/sessions/1487fc9d-92e6-4487-a2e8-92e68d6892e6:rate
```
  Response
```Json
HTTP/1.1 204 No Content
```

# Entity
  You need `Manage Bot` permission to manage bot Entity and customize the settings for a bot Entity.
  - `Entities` - Entity Manage
    + `GET /api/v3/chatbot/bots/{botId}/entities` - [Get entities by entity name/keyword/synonym](#get-entities-by-entity-name/keyword/synonym)
    + `POST /api/v3/chatbot/bots/{botId}/entities` - [Create a new entity](#create-a-new-entity)
    + `PUT /api/v3/chatbot/entities/{id}` - [Update an entity](#update-an-entity)
    + `DELETE /api/v3/chatbot/entities/{id}` - [Remove an entity](#remove-an-entity)
    + `GET /api/v3/chatbot/entities/{id}` - [Get an entity by id](#get-an-entity-by-id)
    + `POST /api/v3/chatbot/bots/{botId}/entities:import` - [Import entities](#import-entities)

## Entity Related Objects Json Format
### Entity Object
  Entity is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  | `id` | Guid  | | yes | N/A | | id of the Entity |
  | `name` | string  | | no | yes | | name of the Entity |
  | `keywords` | [EntityKeyword](#entitykeyword)[] | | no | yes |  |  |

### EntityKeyword
 EntityKeyword is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A |  | id of the entity keyword object |
  | `content` | string  | no | yes | | content |
  | `synonyms` | string[] | no | yes | | an array of string, synonyms list of keyword |


## Entity Endpoints
### Get entities by entity name/keyword/synonym

  `GET /api/v3/chatbot/bots/{botId}/entities`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |
  
Query string

  | Name  | Type | Required| Default  | Description |     
  | - | - | - | - | - | 
  | `keyword` | string | no  | |  search entity name or keyword or synonym by the keyword |
  | `include` | string | no  | | Available value: `keywords`  | 

#### Response
the response is: list of [Entity](#entity-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/entities?include=keywords
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {      
      "id":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",
      "name": "size",
      "keywords": [   //include keywords
        {
          "id":"11e8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "content":"small",
          "synonyms": ["Small", "S"]
        }
      ]          
    },
    {
      "id":"gg2341sa-92e6-4487-a2e8-92e68d6892e6",
      "name": "city",   
      "keywords": [   //include keywords
        {
          "id":"22e8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "content":"beijing",
          "synonyms": ["BEIJING"]
        },
        {
          "id":"22e8sc9d-92e6-4487-a2e8-92e68d6892e6",
          "content":"hangzhou",
          "synonyms": ["HANGZHOU"]
        }
      ]
    }
  ]
``` 

  
### Create a new entity

  `POST /api/v3/chatbot/bots/{botId}/entities`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Request body   

The request body contains data with the [Entity](#entity-object) structure

example:
  ```json 
  {
    "name": "product",
    "keywords": [
      {
        "content":"bot",
        "synonyms": ["BOT", "chatbot"]
      },
      {
        "content":"livechat",
        "synonyms": ["Live Chat", "chat"]
      }
    ]    
  }
```

#### Response
the response is:
 [Entity](#entity-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name": "product",
    "keywords": [
      {
        "content":"bot",
        "synonyms": ["BOT", "chatbot"]
      },
      {
        "content":"livechat",
        "synonyms": ["Live Chat", "chat"]
      }
    ]    
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/entities
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/entities/r2wfe21d-92e6-4487-a2e8-92e68d6892e6

  {
    "id": "r2wfe21d-92e6-4487-a2e8-92e68d6892e6",
    "name": "product" 
  }
``` 

### Update an entity

  `PUT /api/v3/chatbot/entities/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the entity |

Request body 

The request body contains data with the [Entity](#entity-object) structure

example:
  ```json 
  {
    "id": "r2wfe21d-92e6-4487-a2e8-92e68d6892e6",
    "name": "product",
    "keywords": [
      {
        "content":"bot",  //create
        "synonyms": ["BOT", "chatbot"]
      },
      {
        "id": "ffqfe21d-92e6-4487-a2e8-92e68d6892e6",  //update
        "content":"livechat",
        "synonyms": ["Live Chat", "chat"]
      }
    ]    
  }
```

#### Response
the response is: [Entity](#entity-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "r2wfe21d-92e6-4487-a2e8-92e68d6892e6",
    "name": "product",
    "keywords": [
      {
        "content":"bot",
        "synonyms": ["BOT", "chatbot"]
      },
      {
        "id": "ffqfe21d-92e6-4487-a2e8-92e68d6892e6", 
        "content":"livechat",
        "synonyms": ["Live Chat", "chat"]
      }
    ]    
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/entities/r2wfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "r2wfe21d-92e6-4487-a2e8-92e68d6892e6",
    "name": "product",
    "keywords": [
      {
        "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
        "content":"bot", 
        "synonyms": ["BOT", "chatbot"]
      },
      {
        "id": "ffqfe21d-92e6-4487-a2e8-92e68d6892e6",
        "content":"livechat",
        "synonyms": ["Live Chat", "chat"]
      }
    ]    
  }
``` 

### Remove an entity

  `DELETE /api/v3/chatbot/entities/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the entity |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/entities/aaa8sc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get an entity by id

  `GET /api/v3/chatbot/entities/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the entity |

#### Response
the response is: [Entity](#entity-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/entities/aaa8sc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {      
    "id":"aaa8sc9d-92e6-4487-a2e8-92e68d6892e6",
    "name": "size",
    "keywords": [
      {
        "id":"11e8sc9d-92e6-4487-a2e8-92e68d6892e6",
        "content":"small",
        "synonyms": ["Small", "S"]
      }
    ]    
  }
``` 

### Import entities

  `POST /api/v3/chatbot/bots/{botId}/entities:import`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |


Request body
  - the file data to be imported.
    you can [Download Templates](https://bot.comm100.com/botadmin/downloadfile.ashx?file=Import Entities Template.xlsx) first

 example:
```json
//Request header
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx7Uz45AqRfHzbAoI
//Request body
------WebKitFormBoundaryx7Uz45AqRfHzbAoI
Content-Disposition: form-data; name="file"; filename="entities.xlsx"
Content-Type: application/vnd.ms-excel
file binary data
------WebKitFormBoundaryx7Uz45AqRfHzbAoI--
```   

#### Response
the response is:
  - `operationId ` : it is a guid, uniquely identify the import operation, you can use [operation](#operation) API to poll the result 

#### Example
Using curl
```
curl -F 'file=@entities.xlsx' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/entities:import
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "operationId": "74e29172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```

# Entity Keyword
  You need `Manage Bot` permission to manage bot Entity Keywords.
  - `Entity Keywords` - Entity Keywords Manage
    + `GET /api/v3/chatbot/entities/{entityId}/entityKeywords` - [Get all keywords of the entity](#get-all-keywords-of-the-entity)
    + `POST /api/v3/chatbot/entities/{entityId}/entityKeywords` - [Create a new entity keyword](#create-a-new-entity-keyword)
    + `PUT /api/v3/chatbot/entityKeywords/{id}` - [Update an entity keyword](#update-an-entity-keyword)
    + `DELETE /api/v3/chatbot/entityKeywords/{id}` - [Remove an entity keyword](#remove-an-entity-keyword)
    + `GET /api/v3/chatbot/entityKeywords/{id}` - [Get an entity keyword by id](#get-an-entity-keyword-by-id)


## Entity Keyword Endpoints
### Get all keywords of the entity

  `GET /api/v3/chatbot/entities/{entityId}/entityKeywords`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `entityId` | Guid | yes  |  the unique id of the entity |

#### Response
the response is: list of [EntityKeyword](#entitykeyword) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/entities/s22fe21d-92e6-4487-a2e8-92e68d6892e6/entityKeywords
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
      "content":"bot", 
      "synonyms": ["BOT", "chatbot"]
    },
    {
      "id": "ffqfe21d-92e6-4487-a2e8-92e68d6892e6",
      "content":"livechat",
      "synonyms": ["Live Chat", "chat"]
    }
  ]      
``` 
  
### Create a new entity keyword

  `POST /api/v3/chatbot/entities/{entityId}/entityKeywords`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `entityId` | Guid | yes  |  the unique id of the entity |

Request body 

The request body contains data with the [EntityKeyword](#entitykeyword-object) structure

example:
  ```json 
  {
    "content":"ticket",
    "synonyms": ["email", "email ticket"]
  }
```

#### Response
the response is:
 [EntityKeyword](#entitykeyword-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "content":"ticket",
    "synonyms": ["email", "email ticket"]
  }' -X POST https://domain.comm100.com/api/v3/chatbot/entities/f9928d68-92e6-4487-a2e8-8234fc9d1f48/entityKeywords
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/entityKeywords/rd2fe21d-92e6-4487-a2e8-92e68d6892e6

  {
    "id": "rd2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "content":"ticket",
    "synonyms": ["email", "email ticket"]
  }
``` 

### Update an entity keyword

  `PUT /api/v3/chatbot/entityKeywords/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the entityKeyword |

Request body 

The request body contains data with the [EntityKeyword](#entitykeyword-object) structure

example:
  ```json 
  {
    "id": "rd2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "content":"ticket",
    "synonyms": ["email", "email ticket", "tickets"]
  }
```

#### Response
the response is: [EntityKeyword](#entitykeyword) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "rd2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "content":"ticket",
    "synonyms": ["email", "email ticket", "tickets"]
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/entityKeywords/rd2fe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "rd2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "content":"ticket",
    "synonyms": ["email", "email ticket", "tickets"]
  }     
``` 

### Remove an entity keyword

  `DELETE /api/v3/chatbot/entityKeywords/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the entityKeyword |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/entityKeywords/rd2fe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Get an entity keyword by id

  `GET /api/v3/chatbot/entityKeywords/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the entityKeyword |

#### Response
the response is: [EntityKeyword](#entitykeyword) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/entityKeywords/rd2fe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "rd2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "content":"ticket",
    "synonyms": ["email", "email ticket", "tickets"]
  }     
``` 

# Smart Trigger
  You need `Manage Bot` permission to manage Smart Triggers.
  - `Smart Triggers` - Smart Trigger Manage
    + `POST /api/v3/chatbot/bots/{botId}/smartTriggers` -[Create a new smart trigger](#create-a-new-smart-trigger)
    + `GET /api/v3/chatbot/bots/{botId}/smartTriggers` -[Get all smart triggers of the bot](#get-all-smart-triggers-of-the-bot)
    + `GET /api/v3/chatbot/smartTriggers/{id}`  -[Get a smart trigger by id](#get-a-smart-trigger-by-id)
    + `PUT /api/v3/chatbot/smartTriggers/{id}`  -[Update a smart trigger](#update-a-smart-trigger)
    + `DELETE /api/v3/chatbot/smartTriggers/{id}`  -[Remove a smart trigger](#remove-a-smart-trigger)
    + `POST /api/v3/chatbot/bots/{botId}/smartTriggers:sort`  -[Update the order of smart triggers](#Update-the-order-of-smart-triggers)

## Smart Trigger Related Object Json Format
### Smart Trigger

  Smart Trigger is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  | `id` | Guid | | yes | N/A | | id of the smart trigger. |
  | `name` | string | | no | yes | |name of smart trigger. |
  | `isEnabled` | bool | | no | no | false | If smartTriggers is enabled or not. the default value is false.|
  | `conditionExpressionType` | string | | no | no | | the relationship between condition.  enum: `all`,`any`,`logicalExpression`|
  | `logicalExpression` | string | | no | no | | it is an Expression that uses one or more conditions, example:(1 or 2) and 3  |
  | `conditions` |  [Smart Trigger Condition](#smart-trigger-condition-object)[] |  | no | no | |  |
  | `actions` | [Smart Trigger Action](#smart-trigger-action-object)[] |  | no | no | |  |
  | `order` | integer | | no | yes |  | must greater than or equal 0, the order of the smart trigger, ascending sort . |

 ### Smart Trigger Condition Object
  Condition is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | id of the smart trigger. |
  | `variable` | string | no | yes | | value of the Condition |
  | `expression` | string | no | yes |  | the rule of expression.enum:`equal`,`notEqual`,`contains`,`notContains`,`regularExpression`,`lessThan`,`moreThan` |
  | `value` | string | no | yes | | a string of condition matching value |
  | `order` | integer | no | yes |  |must greater than or equal 0,the order of the condition, ascending sort  |

###  Smart Trigger Action Object
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | id of the smart trigger. |
  | `type` | string | no | yes | | the type of the action. enum:[`sendNotification`,`autoMonitor`,`transferChat`,`changeAssignee`,`addToSegment`]|
  | `isEnabled` | bool | no | yes | false | if an action is enabled. |  
  | `agentOfflineMessage` | string | no | no | | agent offlineMessage prompt message |
  | `targetType` | string | no | yes | | the trigger action target type. enum: `department`, `agent`, `visitorSegment`. |
  | `selectedDepartments` | Guid[] | no | no | | a string array of  department id. |
  | `selectedAgents` | Guid[] | no | no | | a string  array of  agent id. |
  | `selectedVisitorSegments` | Guid[]  | no | no | | visitorSegment Id |

## Smart Trigger Endpoints  
### Get all smart triggers of the bot

  `GET /api/v3/chatbot/bots/{botId}/smartTriggers`
 
#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |
 
 Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - |  
  | `include` | string | no  |  | Available value: `conditions`, `actions` |

#### Response    
the response is: list of [Smart Trigger](#Smart-Trigger) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/smartTriggers
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
      "name":"Transfer to Sales", 
      "isEnabled": true,
      "conditionExpressionType": "all",
      "logicalExpression": "",      
      "order": 0,
    },
    {
      "id": "sadwdw12-92e6-4487-a2e8-92e68d6892e6",
      "name":"Transfer to Customer Service", 
      "isEnabled": true,
      "conditionExpressionType": "any",
      "logicalExpression": "",      
      "order": 1,
    }
  ]      
``` 
    
### Get a smart trigger by id

  `GET /api/v3/chatbot/smartTriggers/{id}`

#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTrigger |

#### Response
the response is: [Smart Trigger](#Smart-Trigger) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/smartTriggers/dawfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "name":"Transfer to Sales", 
    "isEnabled": true,
    "conditionExpressionType": "all",
    "logicalExpression": "",
    "conditions": [
      {
        "id": "33wfe21d-92e6-4487-a2e8-92e68d6892e6",
        "variable":"intent", 
        "expression": "equal",
        "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
        "order": 0,
      }
    ],
    "actions": [
      {
        "id": "22wfe21d-92e6-4487-a2e8-92e68d6892e6",
        "type":"transferChat", 
        "isEnabled": true,
        "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
        "targetType": "department",
        "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"]                       
      }
    ],
    "order": 0,
  }    
``` 
    
### Create a new smart trigger

  `POST /api/v3/chatbot/bots/{botId}/smartTriggers`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Request body 

The request body contains data with the [Smart Trigger](#Smart-Trigger) structure

example:
  ```json 
  {
    "name":"Transfer to Technical Support", 
    "isEnabled": true,
    "conditionExpressionType": "all",
    "logicalExpression": "",
    "conditions": [
      {
        "variable":"intent", 
        "expression": "equal",
        "value": "wwwfe21d-92e6-4487-a2e8-92e68d6892e6",
        "order": 0,
      }
    ],
    "actions": [
      {
        "type":"transferChat", 
        "isEnabled": true,
        "agentOfflineMessage": "No one on the Technical Support team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
        "targetType": "department",
        "selectedDepartments": ["cew3e21d-92e6-4487-a2e8-92e68d6892e6"]                
      }
    ],
    "order": 0,
  }
```

#### Response
the response is:
 [Smart Trigger](#Smart-Trigger) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name":"Transfer to Technical Support", 
    "isEnabled": true,
    "conditionExpressionType": "all",
    "logicalExpression": "",
    "conditions": [
      {
        "variable":"intent", 
        "expression": "equal",
        "value": "wwwfe21d-92e6-4487-a2e8-92e68d6892e6",
        "order": 0,
      }
    ],
    "actions": [
      {
        "type":"transferChat", 
        "isEnabled": true,
        "agentOfflineMessage": "No one on the Technical Support team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
        "targetType": "department",
        "selectedDepartments": ["cew3e21d-92e6-4487-a2e8-92e68d6892e6"]              
      }
    ],
    "order": 0,
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/smartTriggers
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/smartTriggers/de3fe21d-92e6-4487-a2e8-92e68d6892e6

  {
    "id":"de3fe21d-92e6-4487-a2e8-92e68d6892e6",
    "name":"Transfer to Technical Support", 
    "isEnabled": true,
    "conditionExpressionType": "all",
    "logicalExpression": "",    
    "order": 0,
  }
```

### Update a smart trigger

  `PUT /api/v3/chatbot/smartTriggers/{id}`
    
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTrigger |

Request body

The request body contains data with the [Smart Trigger](#Smart-Trigger) structure

example:
  ```json 
  {
    "id": "mm2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "name":"Transfer to Technical Support", 
    "isEnabled": true,
    "conditionExpressionType": "any",
    "logicalExpression": "",
    "conditions": [
      {
        "id":"sdwg124s-92e6-4487-a2e8-92e68d6892e6",  //update
        "variable":"intent", 
        "expression": "equal",
        "value": "wwwfe21d-92e6-4487-a2e8-92e68d6892e6",
        "order": 0,
      },
      {
        "variable":"visitor message",   //create
        "expression": "contains",
        "value": "support",
        "order": 1,
      },
    ],
    "actions": [
      {
        "id":"dasvbh1-92e6-4487-a2e8-92e68d6892e6",   //update
        "type":"transferChat", 
        "isEnabled": true,
        "agentOfflineMessage": "No one on the Technical Support team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
        "targetType": "department",
        "selectedDepartments": ["cew3e21d-92e6-4487-a2e8-92e68d6892e6"]              
      }
    ],
    "order": 0,
  }
```

#### Response
the response is: [Smart Trigger](#Smart-Trigger) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "mm2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "name":"Transfer to Technical Support", 
    "isEnabled": true,
    "conditionExpressionType": "any",
    "logicalExpression": "",
    "conditions": [
      {
        "id":"sdwg124s-92e6-4487-a2e8-92e68d6892e6",  //update
        "variable":"intent", 
        "expression": "equal",
        "value": "wwwfe21d-92e6-4487-a2e8-92e68d6892e6",
        "order": 0,
      },
      {
        "variable":"visitor message",   //create
        "expression": "contains",
        "value": "support",
        "order": 1,
      },
    ],
    "actions": [
      {
        "id":"dasvbh1-92e6-4487-a2e8-92e68d6892e6",   //update
        "type":"transferChat", 
        "isEnabled": true,
        "agentOfflineMessage": "No one on the Technical Support team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
        "targetType": "department",
        "selectedDepartments": ["cew3e21d-92e6-4487-a2e8-92e68d6892e6"]                
      }
    ],
    "order": 0,
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/smartTriggers/mm2fe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "mm2fe21d-92e6-4487-a2e8-92e68d6892e6",
    "name":"Transfer to Technical Support", 
    "isEnabled": true,
    "conditionExpressionType": "any",
    "logicalExpression": "",
    "conditions": [
      {
        "id":"sdwg124s-92e6-4487-a2e8-92e68d6892e6",  
        "variable":"intent", 
        "expression": "equal",
        "value": "wwwfe21d-92e6-4487-a2e8-92e68d6892e6",
        "order": 0,
      },
      {
        "id":"dawdwa1a-92e6-4487-a2e8-92e68d6892e6",
        "variable":"visitor message",   
        "expression": "contains",
        "value": "support",
        "order": 1,
      },
    ],
    "actions": [
      {
        "id":"dasvbh1-92e6-4487-a2e8-92e68d6892e6",
        "type":"transferChat", 
        "isEnabled": true,
        "agentOfflineMessage": "No one on the Technical Support team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
        "targetType": "department",
        "selectedDepartments": ["cew3e21d-92e6-4487-a2e8-92e68d6892e6"]                    
      }
    ],
    "order": 0,
  }    
```
    
### Remove a smart trigger
 
  `DELETE /api/v3/chatbot/smartTriggers/{id}`
  
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTrigger |
      
#### Response   
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/smartTriggers/aaa8sc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Update the order of smart triggers

  `POST /api/v3/chatbot/bots/{botId}/smartTriggers:sort`
    
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Request body 
 
The request body contains data with the list of the follow structure:

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - |
  | `id` | Guid | yes  |  | the unique id of the smartTrigger |
  | `order` | integer | yes  |  | the order of the smartTrigger |

  example:
  ```json
  [
    {
      "id": "74e29172-f383-4a2c-9c2d-fb91c3ecbb40",
      "order": 1
    },
    {
      "id": "9c2d9172-f383-4a2c-9c2d-fb91c3ecbb40",
      "order": 0
    }
  ]
  ```

#### Response      
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
    {
      "id": "74e29172-f383-4a2c-9c2d-fb91c3ecbb40",
      "order": 1
    },
    {
      "id": "9c2d9172-f383-4a2c-9c2d-fb91c3ecbb40",
      "order": 0
    }
  ]' -X POST https://domain.comm100.com/api/v3/chatbot/bots/aaa8sc9d-92e6-4487-a2e8-92e68d6892e6/smartTriggers:sort
```
Response
```json
HTTP/1.1 204 No Content
```


# Smart Trigger Condition
  You need `Manage Bot` permission to manage Smart Trigger Conditions.
  - `Smart Trigger Conditions` - Smart Trigger Conditions Manage
    + `POST /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerConditions` -[Create a new smart trigger condition](#create-a-new-smart-trigger-condition)
    + `GET /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerConditions` -[Get all smart triggers conditions](#get-all-smart-trigger-conditions)
    + `GET /api/v3/chatbot/smartTriggerConditions/{id}`  -[Get a smart trigger condition by id](#get-a-smart-trigger-condition-by-id)
    + `PUT /api/v3/chatbot/smartTriggerConditions/{id}`  -[Update a smart trigger condition](#update-a-smart-trigger-condition)
    + `DELETE /api/v3/chatbot/smartTriggerConditions/{id}`  -[Remove a smart trigger condition](#remove-a-smart-trigger-condition)

## Smart Trigger Condition Endpoints  
### Get all smart trigger conditions

  `GET /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerConditions`
 
#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `smartTriggerId` | Guid | yes  |  the unique id of the smartTrigger |

#### Response    
the response is: list of [Smart Trigger Condition](#smart-trigger-condition-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/smartTriggers/f9928d68-92e6-4487-a2e8-8234fc9d1f48/smartTriggerConditions
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
      "variable":"intent", 
      "expression": "equal",
      "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
      "order": 0,
    }
  ]    
``` 
    
### Get a smart trigger condition by id

  `GET /api/v3/chatbot/smartTriggerConditions/{id}`

#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTriggerCondition |

#### Response
the response is: [Smart Trigger Condition](#smart-trigger-condition-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/smartTriggerConditions/dawfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0,
  }     
``` 
    
### Create a new smart trigger condition

  `POST /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerConditions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `smartTriggerId` | Guid | yes  |  the unique id of the smartTrigger |

Request body

The request body contains data with the [Smart Trigger Condition](#smart-trigger-condition-object) structure

example:
  ```json 
  {
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0,
  }
```

#### Response
the response is: [Smart Trigger Condition](#smart-trigger-condition-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0,
  }' -X POST https://domain.comm100.com/api/v3/chatbot/smartTriggers/f9928d68-92e6-4487-a2e8-8234fc9d1f48/smartTriggerConditions
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/smartTriggerConditions/dawfe21d-92e6-4487-a2e8-92e68d6892e6

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0,
  }   
``` 

### Update a smart trigger condition

  `PUT /api/v3/chatbot/smartTriggerConditions/{id}`
    
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTriggerCondition |

Request body

The request body contains data with the [Smart Trigger Condition](#smart-trigger-condition-object) structure

example:
  ```json 
  {
    "id":"dawdjtr2-92e6-4487-a2e8-92e68d6892e6",
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0,
  }
```

#### Response
the response is: [Smart Trigger Condition](#smart-trigger-condition-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"dawdjtr2-92e6-4487-a2e8-92e68d6892e6",
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/smartTriggerConditions/dawdjtr2-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"dawdjtr2-92e6-4487-a2e8-92e68d6892e6",
    "variable":"intent", 
    "expression": "equal",
    "value": "vdfee21d-92e6-4487-a2e8-92e68d6892e6",
    "order": 0,
  }     
``` 
    
### Remove a smart trigger condition
 
  `DELETE /api/v3/chatbot/smartTriggerConditions/{id}`
  
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTriggerCondition |
      
#### Response   
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/smartTriggerConditions/dawdjtr2-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```
    
# Smart Trigger Action
  You need `Manage Bot` permission to manage Smart Trigger Actions.
  - `Smart Trigger Actions` - Smart Trigger Actions Manage
    + `POST /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerActions` -[Create a new smart trigger action](#create-a-new-smart-trigger-action)
    + `GET /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerActions` -[Get all smart triggers actions](#get-all-smart-trigger-actions)
    + `GET /api/v3/chatbot/smartTriggerActions/{id}`  -[Get a smart trigger action by id](#get-a-smart-trigger-action-by-id)
    + `PUT /api/v3/chatbot/smartTriggerActions/{id}`  -[Update a smart trigger action](#update-a-smart-trigger-action)
    + `DELETE /api/v3/chatbot/smartTriggerActions/{id}`  -[Remove a smart trigger action](#remove-a-smart-trigger-action)

## Smart Trigger Action Endpoints  
### Get all smart trigger actions

  `GET /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerActions`
 
#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `smartTriggerId` | Guid | yes  |  the unique id of the smartTrigger |

#### Response  
the response is: list of [Smart Trigger Action](#smart-trigger-action-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/smartTriggers/f9928d68-92e6-4487-a2e8-8234fc9d1f48/smartTriggerActions
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
      "type":"transferChat", 
      "isEnabled": true,
      "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
      "targetType": "department",
      "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
    }
  ]
```
    
### Get a smart trigger action by id

  `GET /api/v3/chatbot/smartTriggerActions/{id}`

#### Parameters 
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTriggerAction |

#### Response  
the response is: [Smart Trigger Action](#smart-trigger-action-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/smartTriggerActions/dawfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  
  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"],            
  }  
```
    
### Create a new smart trigger action

  `POST /api/v3/chatbot/smartTriggers/{smartTriggerId}/smartTriggerActions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `smartTriggerId` | Guid | yes  |  the unique id of the smartTrigger |

Request body 

The request body contains data with the [Smart Trigger Action](#smart-trigger-action-object) structure

example:
  ```json 
  {
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
  }
```

#### Response
the response is: [Smart Trigger Action](#smart-trigger-action-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
  }' -X POST https://domain.comm100.com/api/v3/chatbot/smartTriggers/f9928d68-92e6-4487-a2e8-8234fc9d1f48/smartTriggerActions
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/smartTriggerActions/dawfe21d-92e6-4487-a2e8-92e68d6892e6

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
  }   
``` 



### Update a smart trigger action

  `PUT /api/v3/chatbot/smartTriggerActions/{id}`
    
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTriggerAction |

Request body 

The request body contains data with the [Smart Trigger Action](#smart-trigger-action-object) structure

example:
  ```json 
  {
    "id":"jjtewsdw-92e6-4487-a2e8-92e68d6892e6",
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
  }
```

#### Response
the response is: [Smart Trigger Action](#smart-trigger-action-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"jjtewsdw-92e6-4487-a2e8-92e68d6892e6",
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"] 
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/smartTriggerActions/jjtewsdw-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  
  {
    "id":"jjtewsdw-92e6-4487-a2e8-92e68d6892e6",
    "type":"transferChat", 
    "isEnabled": true,
    "agentOfflineMessage": "No one on the Sales team is currently online. Please leave us a message and we'll get back to you as soon as possible.",
    "targetType": "department",
    "selectedDepartments": ["sadwe21d-92e6-4487-a2e8-92e68d6892e6"]       
  }  
```
    
### Remove a smart trigger action
 
  `DELETE /api/v3/chatbot/smartTriggerActions/{id}`
  
#### Parameters  
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the smartTriggerAction |
      
#### Response   
HTTP/1.1 204 No Content    

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/smartTriggerActions/jjtewsdw-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Quick Reply
  - `Quick Replies` - Quick Reply Manage
    + `GET /api/v3/chatbot/bots/{botId}/quickreplies` - [Get all quick replies of a bot](#get-all-quick-replies-of-a-bot)
    + `POST /api/v3/chatbot/bots/{botId}/quickreplies` - [Create a new quick reply](#create-a-new-quick-reply)
    + `GET /api/v3/chatbot/quickreplies/{id}` - [Get a quick reply](#get-a-quick-reply)
    + `PUT /api/v3/chatbot/quickreplies/{id}` - [Update a quick reply](#update-a-quick-reply)
    + `DELETE /api/v3/chatbot/quickreplies/{id}` - [Remove a quick reply](#remove-a-quick-reply)

## Quick Reply Json Format
### Quick Reply Object
  Quick Reply is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: |  :-: | :-: | - | 
  | `id` | Guid  | | yes | N/A | | id of the Quick Reply |
  | `type` | string  | | no | yes | | Available value, `custom` and `canned` |
  | `name` | string  | | no | yes | | name of the Quick Reply |
  | `items` | [QuickReplyItem](#QuickReplyItem-object)[] | | no | yes |  | |

### QuickReplyItem Object
 QuickReplyItem is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include |  Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: |  :-: | - | 
  | `id` | Guid  | | yes | N/A | | id of Quick Reply item |
  | `type` | string  | | no | yes | | enum value, `triggerAnIntent` and `contactAgent` |
  | `text` | string  | | no | yes | | Only available when Type is triggerAnIntent |
  | `intentId` | string  | | no | no | | when item type is triggerAnIntent, it is the id of the intent |
  |`intent` | [Intent](#intent-object) | yes | N/A | N/A | | Available only when intent is included  | 
  | `order` | integer | | no | yes |  | must greater than or equal 0,the order of the quick reply item, ascending sort . |

## Quick Reply Endpoints

### Get all quick replies of a bot

  `GET /api/v3/chatbot/bots/{botId}/quickreplies`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | -  | - | 
  | `type` | string | no  | | Available value: `custom`, `canned` |
  | `include` | string | no | |  Available value: `items`  |

#### Response
the response is: list of [QuickReply](#quick-reply-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/quickreplies
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
      "type":"canned", 
      "name": "Contact Agent"      
    },
    ...
  ]
```

### Create a new quick reply

  `POST /api/v3/chatbot/bots/{botId}/quickreplies`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Request body 

The request body contains data with the [QuickReply](#quick-reply-object) structure

example:
  ```json 
  {
    "type":"canned", 
    "name": "Contact Agent",
    "items":[  
      {
        "type": "triggerAnIntent",
        "text":"Sales",
        "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
        "order":0,
      },
      {
        "type": "triggerAnIntent",
        "text":"Tech Support",
        "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",      
        "order":1,
      },
    ]
  }
```

#### Response
the response is:
  [QuickReply](#quick-reply-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "type":"canned", 
    "name": "Contact Agent",
    "items":[  
      {
        "type": "triggerAnIntent",
        "text":"Sales",
        "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
        "order":0,
      },
      {
        "type": "triggerAnIntent",
        "text":"Tech Support",
        "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",      
        "order":1,
      },
    ]
  }' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/quickreplies
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/quickreplies/nm123dfe-92e6-4487-a2e8-92e68d6892e6

  {
    "id": "nm123dfe-92e6-4487-a2e8-92e68d6892e6",
    "type":"canned", 
    "name": "Contact Agent",    
  }
```


### Update a quick reply

  `PUT /api/v3/chatbot/quickreplies/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the quickreply |

Request body 

The request body contains data with the [QuickReply](#quick-reply-object) structure

example:
  ```json 
  {
    "id": "nm123dfe-92e6-4487-a2e8-92e68d6892e6",
    "type":"canned", 
    "name": "Contact Agent",
    "items":[  
      {
        "id": "mnnudaw1-92e6-4487-a2e8-92e68d6892e6",  //update
        "type": "triggerAnIntent",
        "text":"Sales",
        "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
        "order":0,
      },
      {
        "type": "triggerAnIntent",   //create
        "text":"Tech Support",
        "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",      
        "order":1,
      },
    ]
  }
```

#### Response
the response is: [QuickReply](#quick-reply-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "nm123dfe-92e6-4487-a2e8-92e68d6892e6",
    "type":"canned", 
    "name": "Contact Agent",
    "items":[  
      {
        "id": "mnnudaw1-92e6-4487-a2e8-92e68d6892e6",  //update
        "type": "triggerAnIntent",
        "text":"Sales",
        "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
        "order":0,
      },
      {
        "type": "triggerAnIntent",   //create
        "text":"Tech Support",
        "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",      
        "order":1,
      },
    ]
  }' -X PUT https://domain.comm100.com/api/v3/chatbot/quickreplies/nm123dfe-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "nm123dfe-92e6-4487-a2e8-92e68d6892e6",
    "type":"canned", 
    "name": "Contact Agent",
    "items":[  
      {
        "id": "mnnudaw1-92e6-4487-a2e8-92e68d6892e6", 
        "type": "triggerAnIntent",
        "text":"Sales",
        "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
        "order":0,
      },
      {
        "id": "vsdew132-92e6-4487-a2e8-92e68d6892e6", 
        "type": "triggerAnIntent",  
        "text":"Tech Support",
        "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",      
        "order":1,
      },
    ]
  }
```

### Get a quick reply

  `GET /api/v3/chatbot/quickreplies/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the quickreply |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent` |


#### Response
the response is: [QuickReply](#quick-reply-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/quickreplies/dawfe21d-92e6-4487-a2e8-92e68d6892e6?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "type":"canned", 
    "name": "Contact Agent",
    "items":[
      {
        "id": "sadwe21d-92e6-4487-a2e8-92e68d6892e6",
        "type": "triggerAnIntent",
        "text":"Sales",
        "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
        "intent":{  //include intent
          "id":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
          "name":"Transfer to Sales",
          "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
        },
        "order":0,
      },
      {
        "id": "sadwe21d-92e6-4487-a2e8-92e68d6892e6",
        "type": "triggerAnIntent",
        "text":"Tech Support",
        "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",
        "intent":{  //include intent
          "id":"345sdaws-92e6-4487-a2e8-92e68d6892e6",
          "name":"Transfer to Tech Support",
          "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
        },
        "order":1,
      },
    ]
  }
```

### Remove a quick reply

  `DELETE /api/v3/chatbot/quickreplies/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the quickreply |

#### Response
HTTP/1.1 204 No Content 

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/quickreplies/dawfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# QuickReplyItem 
  - `Quick Reply Items` - Quick Reply Items Manage
    + `GET /api/v3/chatbot/quickreplies/{quickreplyId}/quickreplyItems` - [Get all quick reply items of a bot](#get-all-quick-reply-items)
    + `POST /api/v3/chatbot/quickreplies/{quickreplyId}/quickreplyItems` - [Create a new quick reply item](#create-a-new-quick-reply-item)
    + `GET /api/v3/chatbot/quickreplyItems/{id}` - [Get a quick reply item](#get-a-quick-reply-item)
    + `PUT /api/v3/chatbot/quickreplyItems/{id}` - [Update a quick reply item](#update-a-quick-reply-item)
    + `DELETE /api/v3/chatbot/quickreplyItems/{id}` - [Remove a quick reply item](#remove-a-quick-reply-item)

## QuickReplyItem Endpoints

### Get all quick reply items

  `GET /api/v3/chatbot/quickreplies/{quickreplyId}/quickreplyItems`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `quickreplyId` | Guid | yes  |  the unique id of the quickreply |

Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  |  | Available value: `intent` |

#### Response
the response is: list of [QuickReplyItem](#QuickReplyItem-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/quickreplies/f9928d68-92e6-4487-a2e8-8234fc9d1f48/quickreplyItems?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [  
    {
      "id": "sadwe21d-92e6-4487-a2e8-92e68d6892e6",
      "type": "triggerAnIntent",
      "text":"Sales",
      "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
      "intent":{   //include intent
        "id":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
        "name":"Transfer to Sales",
        "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
      },
      "order":0,
    },
    {
      "id": "sadwe21d-92e6-4487-a2e8-92e68d6892e6",
      "type": "triggerAnIntent",
      "text":"Tech Support",
      "intentId":"345sdaws-92e6-4487-a2e8-92e68d6892e6",
      "intent":{   //include intent
        "id":"345sdaws-92e6-4487-a2e8-92e68d6892e6",
        "name":"Transfer to Tech Support",
        "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
      },
      "order":1,
    },
  ]
```

### Create a new quick reply item

  `POST /api/v3/chatbot/quickreplies/{quickreplyId}/quickreplyItems`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `quickreplyId` | Guid | yes  |  the unique id of the quickreply |

Request body 

The request body contains data with the [QuickReplyItem](#QuickReplyItem-object) structure

example:
  ```json 
  {
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
    "order":0,
  }
```

#### Response
the response is: [QuickReplyItem](#QuickReplyItem-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
    "order":0,
  }'
-X POST https://domain.comm100.com/api/v3/chatbot/quickreplies/f9928d68-92e6-4487-a2e8-8234fc9d1f48/quickreplyItems
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/quickreplyItems/sadwe21d-92e6-4487-a2e8-92e68d6892e6
   
  {
    "id": "sadwe21d-92e6-4487-a2e8-92e68d6892e6",
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",      
    "order":0,
  }
```


### Get a quick reply item

  `GET /api/v3/chatbot/quickreplyItems/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the quickreplyItem |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent` |

#### Response
the response is: [QuickReplyItem](#QuickReplyItem-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/quickreplyItems/sadwe21d-92e6-4487-a2e8-92e68d6892e6?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "sadwe21d-92e6-4487-a2e8-92e68d6892e6",
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
    "intent":{   //include intent
      "id":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
      "name":"Transfer to Sales",
      "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
    },
    "order":0,
  }
```
 
### Update a quick reply item

  `PUT /api/v3/chatbot/quickreplyItems/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the quickreplyItem |

Request body 

The request body contains data with the [QuickReplyItem](#QuickReplyItem-object) structure

example:
  ```json 
  {
    "id": "bgtyr122e-92e6-4487-a2e8-92e68d6892e6",
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
    "order":0,
  }
```

#### Response
the response is: [QuickReplyItem](#QuickReplyItem-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "bgtyr122e-92e6-4487-a2e8-92e68d6892e6",
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
    "order":0,
  }'
-X PUT https://domain.comm100.com/api/v3/chatbot/quickreplyItems/bgtyr122e-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "bgtyr122e-92e6-4487-a2e8-92e68d6892e6",
    "type": "triggerAnIntent",
    "text":"Sales",
    "intentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",       
    "order":0,
  }
```
### Remove a quick reply item

  `DELETE /api/v3/chatbot/quickreplyItems/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the quickreplyItem |

#### Response
HTTP/1.1 204 No Content 

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/quickreplyItems/bgtyr122e-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Learning Question

  + `GET /api/v3/chatbot/bots/{botId}/learningQuestions` - [Get all learning questions of a bot](#get-all-learning-questions-of-a-bot)
  + `DELETE /api/v3/chatbot/learningQuestions/{id}` - [Remove a learning question](#remove-a-learning-question)
  + `DELETE /api/v3/chatbot/learningQuestions` - [Batch Delete learning questions](#batch-delete-learning-questions)
  + `POST /api/v3/chatbot/bots/{botId}/learningQuestions:batchCreate` - [Batch add learning questions](#batch-add-learning-questions)
  + `GET /api/v3/chatbot/learningQuestions/{id}` - [Get a learning question by id](#get-a-learning-question-by-id)

## Learning Question Related Objects Json Format
### LearningQuestion
  LearningQuestion is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Include | Read-only For Put | Mandatory For Post | Default | Description     | 
  | - | - | :-: | :-: | :-: | :-: | - | 
  | `id` | string    | | N/A | N/A | | id of Learning Question |
  | `type` | string  |   | N/A | N/A | none | enum type. `notHelpful`, `possibleAnswer`, `noAnswer`, `none` |
  | `question` | string   |  | N/A | N/A | | questions asked by visitors |
  | `topScoreIntentId` | string  |   | N/A | N/A | | id of the intent |
  |`intent` | [Intent](#intent-object) | yes | N/A | N/A | | Available only when intent is included  | 
  | `topScore` | double   | |  N/A | N/A | 0 | match score between 0.0 and 100 |
  | `createdTime` | datetime   | |  N/A | N/A | | question asked time |

### LearningQuestionsResponse  
LearningQuestionsResponse is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Read-only For Put | Mandatory For Post | Default | Description     | 
  | - | - | :-: | :-: | :-: | - | 
  | `totalCount` | integer   | N/A | N/A | | total rows of Learning Questions |
  | `previousPage` | string | N/A | N/A | Url of the previous page. |
  | `nextPage` | string | N/A | N/A | Url of the next page. |
  | `list` | [LearningQuestion](#learningquestion)[] | N/A | N/A | | list of [LearningQuestion](#learningquestion) Object |

## Learning Question Endpoints
### Get all learning questions of a bot

  `GET /api/v3/chatbot/bots/{botId}/learningQuestions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Query string

  | Name  | Type | Required | Default  | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  | | Available value: `intent` |
  | `timeFrom` | string | yes  |  |  |
  | `timeTo` | string | yes  |  | |
  | `pageIndex` | integer | no  |  1 | page index |
  | `pageSize` | integer | no  | 10 | page size  |
  | `keyword` | string | no  | | search by keyword |
  | `minScore` | float | no  |  | search the data if topScore >= minScore |


#### Response

the response is: [LearningQuestionsResponse](#learningquestionsresponse) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/learningQuestions?include=intent&timeFrom=2019-11-12 00:00&timeTo=2019-11-13 00:00
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "totalCount": 100,
    "nextPage": "https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/learningQuestions?pageIndex=2&include=intent&timeFrom=2019-11-12 00:00&timeTo=2019-11-13 00:00",
    "previousPage": null,
    "list": [
      {
        "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
        "type":"noAnswer", 
        "question": "can io get nbn",
        "topScoreIntentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
        "intent":{   //include intent
          "id":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
          "name":"Fail",
          "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
        },
        "topScore": 45,
        "createdTime":"2019-11-12 15:21:09"
      },
      ...
    ]
  }  
```

### Remove a learning question

  `DELETE /api/v3/chatbot/learningQuestions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the learningQuestion |

#### Response
HTTP/1.1 204 No Content 

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/chatbot/learningQuestions/bgtyr122e-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Batch Delete learning questions

  `DELETE /api/v3/chatbot/learningQuestions`

#### Parameters

Request body 
  - an array of learningQuestions id

  example:
  ```json
  [
    "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "92e68d68-92e6-4487-a2e8-8234fc9d1f48",
    "44878d68-92e6-4487-a2e8-8234fc9d1f48"
  ]
  ```

#### Response
HTTP/1.1 204 No Content 

#### Example
Using curl
```
curl -d '[
    "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "92e68d68-92e6-4487-a2e8-8234fc9d1f48",
    "44878d68-92e6-4487-a2e8-8234fc9d1f48"
  ]' -X DELETE https://domain.comm100.com/api/v3/chatbot/learningQuestions
```
Response
```json
HTTP/1.1 204 No Content
```

### Batch add learning questions

  `POST /api/v3/chatbot/bots/{botId}/learningQuestions:batchCreate`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |

Request body 
  - an array of string

  example:
  ```json
  [
    "i want to do something",
    "buy asdw ",
    "test question"
  ]
  ```

#### Response
the response is:
  - `operationId ` : it is a guid, uniquely identify the import operation, you can use [operation](#operation) API to poll the result 

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
    "i want to do something",
    "buy asdw ",
    "test question"
  ]' -X POST https://domain.comm100.com/api/v3/chatbot/bots/f9928d68-92e6-4487-a2e8-8234fc9d1f48/learningQuestions:batchCreate
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "operationId": "74e29172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```

### Get a learning question by id

  `Get /api/v3/chatbot/learningQuestions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the learningQuestion |

Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - | 
  | `include` | string | no  |  | Available value: `intent` |

#### Response
the response is: [LearningQuestion](#learningquestion) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/learningQuestions/dawfe21d-92e6-4487-a2e8-92e68d6892e6?include=intent
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "type":"noAnswer", 
    "question": "can io get nbn",
    "topScoreIntentId":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
    "intent":{   //include intent
      "id":"dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
      "name":"Fail",
      "categoryId": "1q1dlkiu7-92e6-4487-a2e8-92e68d6892e6"
    },
    "topScore": 45,
    "createdTime":"2019-11-12 15:21:09"
  }
```

# PrebuiltEntity  
  - `PrebuiltEntity`
    + `GET /api/v3/chatbot/bots/{botId}/prebuiltEntities` - [Get all prebuiltEntities ](#get-all-prebuiltEntities)   

## PrebuiltEntity Related Objects Json Format
### PrebuiltEntity
  PrebuiltEntity is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | N/A | N/A | | id of the Entity |
  | `name` | string  | N/A | N/A | | name of the prebuilt entity |
  | `description` | string  | N/A | N/A | | description of the prebuilt entity |
  | `example` | string[]  | N/A | N/A | | examples of the prebuilt entity |


## PrebuiltEntity Endpoints
### Get all prebuiltEntities

  `GET /api/v3/chatbot/bots/{botId}/prebuiltEntities`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `botId` | Guid | yes  |  the unique id of the bot |
 
#### Response
the response is: list of [Prebuilt Entity](#prebuiltentity) Objects  

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/prebuiltEntities?language=en
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  [
    {
      "id":"sdawbgh1-92e6-4487-a2e8-92e68d6892e6",
      "name": "sys-date",
      "description":"Matches a date", 
      "example": ["tomorrow", "10/10/2019","Monday", "next Sunday"]   
    },
    ...
  ]  
```

# Operation  
  - `Operation` - Get the latest state of a long-running operation
    + `GET /api/v3/chatbot/operations/{id}` - [Get operation state by id](#get-operation-by-id)   

## Operation Related Objects Json Format
### OperationState
  OperationState is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post  | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `operationId` | string  | N/A | N/A | | operation id |
  | `status` | string  | N/A | N/A | Wait | enum values, `wait `,`succeeded `,`failed `,`processing ` |
  | `percent` | integer  | N/A | N/A | 0 | progress of the long-running operation  |
  | `errorMessage` | string  | N/A | N/A | | error message when operation status is Failed  |


## Endpoints
### Get operation by id

  `GET /api/v3/chatbot/operations/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the operation |

#### Response
the response is: [Operation State](#OperationState) Objects  

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/operations/dawdbgh1-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "operationId": "dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
    "status":"processing", 
    "percent": "25" ,
    "errorMessage":""     
  } 
```

# Image
+ `POST /api/v3/chatbot/images` - [upload an image](#upload-an-image)
+ `GET /api/v3/chatbot/images/{id}` - [get an image](#get-an-image)

## Endpoints  
### Upload an image

  `POST /api/v3/chatbot/images`

Note
```
Formats supported: GIF, JPG, JPEG, PNG or BMP
Max file size: 30MB
```

#### Parameters

Request body
  - the image data to be uploaded.
   
 example:
```json
//Request header
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryx7Uz45AqRfHzbAoI
//Request body
------WebKitFormBoundaryx7Uz45AqRfHzbAoI
Content-Disposition: form-data; name="file"; filename="test.png"
Content-Type: image/png
file binary data
------WebKitFormBoundaryx7Uz45AqRfHzbAoI--
```   

#### Response
the response is: [Image](#image-object) object

#### Example
Using curl
```
curl -F 'file=@test.png' -X POST https://domain.comm100.com/api/v3/chatbot/images
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/chatbot/images/dawdbgh1-92e6-4487-a2e8-92e68d6892e6

{
  "id": "dawdbgh1-92e6-4487-a2e8-92e68d6892e6",
  "name": "test.png",
  "url" : "https://bot.comm100.com/api/v3/chatbot/images/dawdbgh1-92e6-4487-a2e8-92e68d6892e6"
}
```

### Get an image

  `GET /api/v3/chatbot/images/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the image |

#### Response
the response is: the Image content

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/images/dawdbgh1-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 200 OK
Content-Length: 3262
Content-Type: image/jpeg

image file binary data

```

# Report
  + `GET /api/v3/chatbot/reports/chat` - [Chat report](#chat-report)
  + `GET /api/v3/chatbot/reports/answer` - [Answer report](#answer-report)
  + `GET /api/v3/chatbot/reports/highConfidenceAnswer` - [High confidence answer report](#high-confidence-answer-report)
  + `GET /api/v3/chatbot/reports/rating` - [Rating report](#rating-report)
  + `GET /api/v3/chatbot/reports/botAgent` - [Bot versus agent report](#bot-versus-agent-report)
  + `GET /api/v3/chatbot/reports/summary` - [Summary report](#summary-report)
  + `GET /api/v3/chatbot/reports/dailyDetails` - [ Daily details report](#daily-details-report)    
  + `GET /api/v3/chatbot/reports/intentUsageByCategory`  - [Intent Usage by category](#intent-usage-by-category)
  + `GET /api/v3/chatbot/reports/intentUsageByTime`  - [Intent Usage by time](#intent-usage-by-time)
  + `GET /api/v3/chatbot/reports:export`  - [Export report](#export-report)

## Report Related Object Json Format
### ChatReport
  ChatReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - |
  | `totalBotResolved` | integer  | 0 | |
  | `totalBotUnResolved` | integer | 0 | |
  | `totalBotTransferedAgent` | integer  |  0 | |
  | `totalBotTransferredOfflineMessage` | integer  |  0 | |
  | `totalAgentChatTime` | string  | | the string format is `day.hour:minute:second`  |
  | `totalBotChatTime` | string  | | the string format is `day.hour:minute:second` |
  | `dataList` | [ChatReportDetail](#chatreportdetail)[]  | |list of [ChatReportDetail](#chatreportdetail) Object  |

### ChatReportDetail
  ChatReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - |
  | `botResolved` | integer  |   0 | |
  | `botUnResolved` | integer  |  0 | |
  | `botTransferedAgent` | integer  |   0 | |
  | `botTransferredOfflineMessage` | integer  |   0 | |
  | `agentChatTime` | string  |  | the string format is `day.hour:minute:second` |
  | `botChatTime` | string  |  | the string format is `day.hour:minute:second` |
  | `time` | datetime  |  | statistical time |

### AnswerReport
  AnswerReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  | `percentOfHighConfidenceAnswers` | double  | 0 | percentage of high configdence answer |
  | `totalAnswers` | integer  | 0 | total answers count |
  | `totalHighConfidenceAnswers` | integer  | 0 | total high configdence answers count |
  | `totalNoAnswers` | integer  | 0 | total no answers count |
  | `totalPossibleAnswers` | integer  | 0 | total possible answers count |
  | `dataList` | [AnswerReportDetail](#answerreportdetail)[]  | | list of [AnswerReportDetail](#answerreportdetail) Object  |

### AnswerReportDetail
  AnswerReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  | `percentOfHighConfidenceAnswers` | double  | 0 | percentage of high configdence answer |
  | `answers` | integer  |  0 | total answers count |
  | `highConfidenceAnswers` | integer  |  0 | total high configdence answers count |
  | `noAnswers` | integer  |  0 |  total no answers count |
  | `possibleAnswers` | integer  |  0 | total possible answers count |
  | `time` | datetime  | | statistical time |

### HighConfidenceReport
  HighConfidenceReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  | `totalHelpful` | integer  | 0 | high configdence answers count |
  | `totalHighConfidence` | integer  |  0 |total answers count |
  | `totalNoRate` | integer  | 0 |total high configdence answers count |
  | `totalNotHelpful` | integer  |  0 | total no answers count |
  | `dataList` | [HighConfidenceReportDetail](#highconfidencereportdetail)[]  |  | list of [HighConfidenceReportDetail](#highconfidencereportdetail) Object  |

### HighConfidenceReportDetail
  HighConfidenceReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: | - | 
  | `helpful` | integer  |  0 |high configdence answers count |
  | `highConfidence` | integer  | 0 | total answers count |
  | `noRate` | integer  | 0 | total high configdence answers count |
  | `notHelpful` | integer  |  0 | total no answers count |
  | `time` | datetime  | | statistical time |

### RatingReport
  RatingReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `avgScore` | double  |  0 | average score |
  | `totalRatingTimes` | integer  |  0 |rating times |
  | `totalScore1Times` | integer  |  0 |the rating score is 1 times |
  | `totalScore2Times`  | integer  |  0 |the rating score is 2 times |
  | `totalScore3Times`  | integer  |  0 |the rating score is 3 times |
  | `totalScore4Times`  | integer  |  0 |the rating score is 4 times |
  | `totalScore5Times`  | integer  |  0 |the rating score is 5 times |
  | `dataList` | [RatingReportDetail](#ratingreportdetail)[]  | N/A | N/A | | list of [RatingReportDetail](#ratingreportdetail) Object  |

### RatingReportDetail
  RatingReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - |
  | `avgScore` | double  |  0 | average score |
  | `ratingTimes` | integer  |   0 |rating times |
  | `score1Times` | integer  |   0 |the rating score is 1 times |
  | `score2Times`  | integer  |  0 |the rating score is 2 times |
  | `score3Times`  | integer  |  0 |the rating score is 3 times |
  | `score4Times`  | integer  |  0 |the rating score is 4 times |
  | `score5Times`  | integer  |  0 |the rating score is 5 times |
  | `time` | datetime  | | statistical time |

### BotAgentReport
  BotAgentReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `avgScore` | double  | 0 |average score |
  | `avgTime` | double  | 0 | average time |
  | `chats` | integer  | 0 |chats |
  | `agent` | [BotAgentReportDetail](#botagentreportdetail)[]  | |list of [BotAgentReportDetail](#botagentreportdetail) Object  |
  | `bot` | [BotAgentReportDetail](#botagentreportdetail)[]  | | list of [BotAgentReportDetail](#botagentreportdetail) Object  |

### BotAgentReportDetail
  BotAgentReportBotDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - |
  | `avgScore` | double  | 0 | average score |
  | `avgTime` | double  |  0 | average time |
  | `chats` | integer  | 0 | chats |
  | `totalChatTime` | integer  |  | the string format is `day.hour:minute:second` |
  | `time` | datetime  |  | statistical time |

### SummaryReport
  dailyDetails is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: |  - | 
  | `averageRatingScore` | double  | 0 | average rating score |
  | `botOnlyChatCount` | integer  |  0 | number of chats that are between a visitor and bot, no agent included |
  | `botOnlyChatsTime` | integer  |  0 | time of chat that only involves bot and visitor, no agent |
  | `botAnswerCount` | integer  | 0 | number of answers provided by bot |
  | `chatsFromBotToAgentCount` | integer  |  0 | number of chats transferred from bot to agent |
  | `percentageOfBotOnlyChats` | double  |  0 | percentage of chats that are between a visitor and bot, no agent included |
  | `percentageOfHighConfidenceAnswers` | double  | 0 | percentage of high confidence answers |

### DailyReport
  DailyReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default |Description |    
  | - | - | :-: | - | 
  | `totalChatbotOnly` | integer  |  0 | total number of chats that are between a visitor and bot, no agent included |
  | `totalFromBotToAgent` | integer  |  0 | total number of chats transferred from bot to agent |
  | `totalPercentageOfBotOnlyChats` | double  |  0 | total percentage of chats that are between a visitor and bot, no agent involved |
  | `dataList` | [DailyDetailReport](#DailyDetailReport)[]  |  | list of [DailyDetailReport](#DailyDetailReport) Object  |

### DailyDetailReport
  Last7DaysDailyDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: |  - |
  | `chatbotOnly` | integer  |  0 | total number of chats that are between a visitor and bot, no agent included |
  | `fromBotToAgent` | integer  |  0 | total number of chats transferred from bot to agent |
  | `dailyChatsCount` | integer  |  0 | daily chats count |
  | `percentageOfBotOnlyChats` | double  |  0 | total percentage of chats that are between a visitor and bot, no agent involved |
  | `time` | datetime  |  | statistical time |

### IntentUsageByCategory
  IntentUsageByCategory is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default |  Description |    
  | - | - | :-: | - | 
  | `category` | string  |  | the category of the intent  |
  | `intentName` | string  |  | the intent name |
  | `count` | integer  |  0 |the count of use |


### IntentUsageByTime
  IntentUsageByTime is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | :-: | - | 
  | `total` | integer  | 0 |  |
  | `top3UsedIntents` | [IntentUsage](#intentusage)[]  | | list of [IntentUsage](#intentusage) Object  |
  | `dataList` | [IntentUsageDetailsByTime](#IntentUsageDetailsByTime)[]  | | list of [IntentUsageDetailsByTime](#IntentUsageDetailsByTime) Object  |

### IntentUsage
  IntentUsage is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | :-: |  - |
  | `intentName` | string  | | the intent name |
  | `count` | integer  |  0 |the count of use |

### IntentUsageDetailsByTime
  IntentUsageDetailsByTime is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default |Description |    
  | - | - | :-: |  - |
  | `time` | string  |  | statistical time |
  | `totalCount` | integer  |  0 | |
  | `mostTriggered` | integer  |  0 | the count of most triggered intent |
  | `secondMostTriggered` | integer  |  0 | the count of second most Triggered intent |
  | `thirdMostTriggered` | integer  |  0 |  the count of third most Triggered intent |

## Report Endpoints  
### Chat report

  `GET /api/v3/chatbot/reports/chat`

#### Parameters
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | |  query end time  | 
  | `filterType` | string  | no  | | Enum: `bot`, `campaign`,`channelAccount` |
  | `filterValue` | string | no  |  | value of the filter |
  | `displayBy` | string | no  |  day | Enum: `day`, `week`, `month` |
  | `channel` | string | no  | All Channels | eg: `All Channels`, `Live Chat` ... |

#### Response
the response is: [ChatReport](#chatreport) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/chat?channel=All Channels&timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&displayBy=day
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"totalBotResolved": 6,
	"totalBotUnResolved": 4,
	"totalBotTransferredAgent": 4,
	"totalBotTransferredOfflineMessage": 0,
	"totalAgentChatTime": "0.01:34:34",
	"totalBotChatTime": "0.00:58:24",
	"dataList": [{
      "time": "12/05/2019",
      "startTime": "2019-12-05 00:00:00",
      "endTime": "2019-12-06 00:00:00",
      "botResolved": 1,
      "botUnResolved": 2,
      "botTransferredAgent": 2,
      "botTransferredOfflineMessage": 0,
      "agentChatTime": "0.01:26:50",
      "botChatTime": "0.00:01:08"
    },
  ...
  ]
}
```

### Answer report

  `GET /api/v3/chatbot/reports/answer`

#### Parameters
Query string

  |Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | |  query end time  | 
  | `filterType` | string  | no  | | Enum: `bot`, `campaign`,`channelAccount` |
  | `filterValue` | string | no  |  | value of the filter |
  | `displayBy` | string | no  |  day | Enum: `day`, `week`, `month` |
  | `channel` | string | no  | All Channels | eg: `All Channels`, `Live Chat` ... |


#### Response
the response is: [AnswerReport](#answerreport) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/answer?channel=Twitter Direct Message&timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&displayBy=day
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"totalAnswers": 205,
	"totalHighConfidenceAnswers": 95,
	"totalPossibleAnswers": 15,
	"totalNoAnswers": 95,
	"percentOfHighConfidenceAnswers": 46.34,
	"dataList": [{
      "time": "12/05/2019",
      "startTime": "2019-12-05 00:00:00",
      "endTime": "2019-12-06 00:00:00",
      "answers": 90,
      "highConfidenceAnswers": 37,
      "possibleAnswers": 11,
      "noAnswers": 42,
      "percentOfHighConfidenceAnswers": 41.11
    },
  ...
  ]
}
```

### High confidence answer report

  `GET /api/v3/chatbot/reports/highConfidenceAnswer`

#### Parameters
Query string

  |Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | |  query end time  | 
  | `filterType` | string  | no  | | Enum: `bot`, `campaign` |
  | `filterValue` | string | no  |  | value of the filter |
  | `displayBy` | string | no  |  day | Enum: `day`, `week`, `month` |  


#### Response
the response is: [HighConfidenceReport](#highconfidencereport) Object
    
#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/highConfidenceAnswer?timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&displayBy=day
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"totalHighConfidence": 95,
	"totalHelpful": 0,
	"totalNotHelpful": 0,
	"totalNoRate": 95,
	"dataList": [
    {
      "time": "12/05/2019",
      "startTime": "2019-12-05 00:00:00",
      "endTime": "2019-12-06 00:00:00",
      "highConfidence": 37,
      "helpful": 0,
      "notHelpful": 0,
      "noRate": 37
    }, 
  ...
  ]
}
```

### Rating report

  `GET /api/v3/chatbot/reports/rating`

#### Parameters
Query string

 |Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | |  query end time  | 
  | `filterType` | string  | no  | | Enum: `bot`, `campaign` |
  | `filterValue` | string | no  |  | value of the filter |
  | `displayBy` | string | no  |  day | Enum: `day`, `week`, `month` |

#### Response
the response is: [RatingReport](#ratingreport) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/rating?timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&displayBy=day
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"totalRatingTimes": 0,
	"totalScore1Times": 0,
	"totalScore2Times": 0,
	"totalScore3Times": 0,
	"totalScore4Times": 0,
	"totalScore5Times": 0,
	"avgScore": 0.0,
	"dataList": [
    {
      "time": "12/05/2019",
      "startTime": "2019-12-05 00:00:00",
      "endTime": "2019-12-06 00:00:00",
      "ratingTimes": 0,
      "score5Times": 0,
      "score4Times": 0,
      "score3Times": 0,
      "score2Times": 0,
      "score1Times": 0,
      "avgScore": 0.0
    },
  ...
  ]
}
```

### Bot versus agent report

  `GET /api/v3/chatbot/reports/botAgent`

#### Parameters
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | | query end time  | 
  | `chatFilter` | string | no  | All Chats |  `All Chats` or `Exclude Chats from Bot to Agents` |
  
#### Response
the response is: [BotAgentReport](#botagentreport) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/botAgent?timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&chatFilter=All Chats
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"chats": 0,
	"avgTime": 0.0,
	"avgScore": 0.0,
	"agent": {
		"time": "11/06/2019",
		"startTime": "2019-11-06 00:00:00",
		"endTime": "2019-12-06 00:00:00",
		"chats": 0,
		"avgTime": 0.0,
		"avgScore": 0.0,
		"totalChatTime": "0.00:00:00"
	},
	"bot": {
		"time": "11/06/2019",
		"startTime": "2019-11-06 00:00:00",
		"endTime": "2019-12-06 00:00:00",
		"chats": 0,
		"avgTime": 0.0,
		"avgScore": 0.0,
		"totalChatTime": "0.00:00:00"
	}
}
```

### summary report

  `GET /api/v3/chatbot/reports/summary`

#### Parameters
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | | query end time  |  
  | `type` | string | no  | Live Chat | eg: `Messaging`, `Live Chat` |

#### Response
the response is: [SummaryReport](#summaryreport) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/summary?timeFrom=2019-11-30 00:00&timeTo=2019-12-06 00:00&type=Messaging
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"averageRatingScore": 0.0,
	"botOnlyChatCount": 6,
	"botOnlyChatsTime": 56.69,
	"botAnswerCount": 31,
	"chatsFromBotToAgentCount": 4,
	"percentageOfBotOnlyChats": 33.33,
	"percentageOfHighConfidenceAnswers": 19.35,
	"highConfidenceAnswerCount": 6.0
}
```

### daily details report

  `GET /api/v3/chatbot/reports/dailyDetails`

#### Parameters
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | | query end time  | 
  | `type` | string | no  | Live Chat | eg: `Messaging`, `Live Chat` |

#### Response
the response is: [DailyReport](#dailyreport) Object
  
#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/dailyDetails?timeFrom=2019-11-30 00:00&timeTo=2019-12-06 00:00&type=Live Chat
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"totalChatbotOnly": 6,
	"totalFromBotToAgent": 4,
	"totalPercentageOfBotOnlyChats": 33.33,
	"dataList": [
    {
      "time": "Dec 06",
      "startTime": "2019-12-06 00:00:00",
      "endTime": "2019-12-07 00:00:00",
      "chatBotOnly": 0,
      "fromBotToAgent": 0,
      "dailyChatsCount": 0,
      "percentageOfBotOnlyChats": 0.0
    }, 
  ...
  ]
}
```

### Intent usage by category

  `GET /api/v3/chatbot/reports/intentUsageByCategory`

#### Parameters
Query string

  |Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | |  query end time  | 
  | `filterType` | string  | yes  | bot | Enum: `bot`|
  | `filterValue` | string | yes  |  | id of the bot |
  | `channel` | string | no  | All Channels | eg: `All Channels`, `Live Chat` ... |


#### Response
the response is: list of [IntentUsageByCategory](#IntentUsageByCategory) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/intentUsageByCategory?channel=All Channels&filterType=bot&filterValue=bfa31cda-d0a5-40fc-a8a9-c7b7a12d5c18&timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
	"categoryName": "Smalltalk",
	"intentName": "I'm sorry",
	"count": 1
  }, {
    "categoryName": "System",
    "intentName": "Bot info",
    "count": 3
  }, {
    "categoryName": "/",
    "intentName": "a - test web view - frank",
    "count": 23
  }, 
...
]
```

### Intent usage by time

  `GET /api/v3/chatbot/reports/intentUsageByTime`

#### Parameters
Query string

  |Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  |  | query start time  |
  | `timeTo` | string | yes  | |  query end time  | 
  | `filterType` | string  | yes  | bot | Enum: `bot`|
  | `filterValue` | string | yes  |  | id of the bot |
  | `displayBy` | string | no  |  day | Enum: `day`, `week`, `month` |
  | `channel` | string | no  | All Channels | eg: `All Channels`, `Live Chat` ... |


#### Response
the response is: [IntentUsageByTime](#IntentUsageByTime) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/chatbot/reports/intentUsageByTime?channel=All Channels&filterType=bot&filterValue=bfa31cda-d0a5-40fc-a8a9-c7b7a12d5c18&timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&displayBy=day
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
	"total": 205,
	"top3UsedIntents": [{
		"intentName": "UNRECOGNIZED",
		"count": 89
	}, {
		"intentName": "a - test web view - frank",
		"count": 23
	}, {
		"intentName": "fsfsd",
		"count": 22
	}],
	"dataList": [
    {
      "time": "12/05/2019",
      "startTime": "2019-12-05 00:00:00",
      "endTime": "2019-12-06 00:00:00",
      "totalCount": 90,
      "mostTriggered": 37,
      "secondMostTriggered": 2,
      "thirdMostTriggered": 22
    },
  ...
  ]
}
```

### Export report

  `GET /api/v3/chatbot/reports:export `

#### Parameters
Query string

  | Name  | Type | Required | Default | Description |     
  | - | - | - | - | - |
  | `timeFrom` | string | yes  | | query start time  |
  | `timeTo` | string | yes  | | query end time  | 
  | `filterType` | string  | no  | | Enum: `bot`, `campaign` |
  | `filterValue` | string | no  | |  value of the filter |
  | `displayBy` | string | no  | day | Enum: `day`, `week`, `month` |  
  | `chatFilter` | string | no  | All Chats | `All Chats` or `Exclude Chats from Bot to Agents`, Only available when reportName is `botAgent` |
  | `channel` | string | no  | All Channels | eg: `All Channels`, `Live Chat` ... |
  | `reportName` | string | yes  | | Enum value: `chat`, `answer`, `highConfidenceAnswer`, `rating`, `botAgent`,  `intentUsageByCategory`, `intentUsageByTime` |


#### Response
the response is:

  - `fileUrl` -the excel report file full name

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/chatbot/bots/reports:export?channel=All Channels&filterType=bot&filterValue=bfa31cda-d0a5-40fc-a8a9-c7b7a12d5c18&timeFrom=2019-11-06 00:00&timeTo=2019-12-06 00:00&reportName=intentUsageByCategory
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "fileUrl": "https://bot.comm100.com/botapi/files/74e29172-f383-4a2c-9c2d-fb91c3ecbb40"
}
```


# Agent Assist Language

  + `GET /api/v3/agentAssist/languages` - [Get Agent Assist support languages ](#get-agent-assist-languages)

## Agent Assist Language Endpoints
### Get agent assist languages

  `GET /api/v3/agentAssist/languages`

#### Parameters
  
#### Response
the response is: list of [Language](#Language-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/agentAssist/languages
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "code": "en",
    "name": "English"
  },
  {
    "code": "es",
    "name": "Spanish"
  }
]
```

# Agent Assist
  + `GET /api/v3/agentAssist` - [Get setting of agent assist](#get-setting-of-a-agent-assist)
  + `POST /api/v3/agentAssist` - [Create a new setting for agent assist](#create-a-new-setting-for-agent-assist)
  + `PUT /api/v3/agentAssist` - [Update agent assist setting](#update-agent-assist-setting)

## Agent Assist Related Object Json Format

### AgentAssist

  AgentAssistSetting is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default |  Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A | | id of the agent assist |
  | `isEnabled` | bool  | no | yes | false | agent assist enable flag |
  | `language` | string  | no | yes | en | code of the Agent Assist supported language |
  | `ifIncludeCannedMessage` | bool  | no | yes | true | if canned message is included in agent assist’s suggestions source |
  | `ifIncludeKnowledgeBase` | bool  | no | yes | false | if knowledge base is included in agent assist’s suggestions source |
  | `ifIncludeChatbot` | bool  | no | yes | false | if chat bot is included in agent assist’s suggestions source |
  | `selectedKnowledgeBases` | Guid[]  | no | yes | | id of knowledge base array |
  | `selectedChatbots` | Guid[]  | no | yes | | id of ai bot array |
  | `highConfidenceScore` | integer  | no | yes | 60 | Agent Assist will display suggestions only when the score of the suggested item is higher than this value.  value is beteween 1 and 100  |
  | `maximumSuggestionNumber` | integer  | no | yes | 3 | the maximum number of suggestions Agent Assist can provide. available value: 1, 2, 3, 4, 5 |
  | `ifAddVisitorQuestionAsSimilarQuestion` | bool  | no | yes | true | for suggested canned messages or kb articles that agents chose to send, agent assist can automatically add such as similar questions to improve future performance. |
  | `textBeforeKBArticle` | string  | no | yes | Please refer to the knowledge base article | the message before a knowledge base article link |
  | `ifAddUnrecognizedQuestionsToLearning` | bool  | no | yes | false |Automatically add Unrecognized Visitor Questions to Agent Assist Learning Section |

## Agent Assist Endpoints  

### Get setting of a agent assist

  `GET /api/v3/agentAssist`

#### Parameters

#### Response
the response is: [AgentAssist](#agentassist) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/agentAssist
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id":"w124sad2-92e6-4487-a2e8-8234fc9d1f48",
  "isEnabled": true,
  "language":"en",
  "ifIncludeCannedMessage": true,
  "ifIncludeKnowledgeBase":false,
  "ifIncludeChatbot":true,
  "selectedKnowledgeBases":[],
  "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
  "highConfidenceScore":60,
  "maximumSuggestionNumber":5,
  "ifAddVisitorQuestionAsSimilarQuestion":true,
  "textBeforeKBArticle":"please refer this article:",
  "ifAddUnrecognizedQuestionsToLearning":false,
}
```

### Create a new setting for agent assist

  `POST /api/v3/agentAssist`

#### Parameters

Request body 

The request body contains data with the [AgentAssist](#agentassist) structure

example:
  ```json 
  {
    "isEnabled": true,
    "language":"en",
    "ifIncludeCannedMessage": true,
    "ifIncludeKnowledgeBase":false,
    "ifIncludeChatbot":true,
    "selectedKnowledgeBases":[],
    "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
    "highConfidenceScore":60,
    "maximumSuggestionNumber":5,
    "ifAddVisitorQuestionAsSimilarQuestion":true,
    "textBeforeKBArticle":"please refer this article:",
    "ifAddUnrecognizedQuestionsToLearning":false,
  }
```

#### Response
the response is: [AgentAssist](#agentassist);

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "isEnabled": true,
    "language":"en",
    "ifIncludeCannedMessage": true,
    "ifIncludeKnowledgeBase":false,
    "ifIncludeChatbot":true,
    "selectedKnowledgeBases":[],
    "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
    "highConfidenceScore":60,
    "maximumSuggestionNumber":5,
    "ifAddVisitorQuestionAsSimilarQuestion":true,
    "textBeforeKBArticle":"please refer this article:",
    "ifAddUnrecognizedQuestionsToLearning":false,
  }' -X POST https://domain.comm100.com/api/v3/agentAssist
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/agentAssist
  
  {
    "id":"w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "isEnabled": true,
    "language":"en",
    "ifIncludeCannedMessage": true,
    "ifIncludeKnowledgeBase":false,
    "ifIncludeChatbot":true,
    "selectedKnowledgeBases":[],
    "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
    "highConfidenceScore":60,
    "maximumSuggestionNumber":5,
    "ifAddVisitorQuestionAsSimilarQuestion":true,
    "textBeforeKBArticle":"please refer this article:",
    "ifAddUnrecognizedQuestionsToLearning":false,
  }
```

### Update agent assist setting

  `PUT /api/v3/agentAssist`

#### Parameters
Request body 

The request body contains data with the [AgentAssist](#agentassist) structure

example:
  ```json 
  {
    "id":"w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "isEnabled": false,
    "language":"en",
    "ifIncludeCannedMessage": true,
    "ifIncludeKnowledgeBase":false,
    "ifIncludeChatbot":true,
    "selectedKnowledgeBases":[],
    "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
    "highConfidenceScore":60,
    "maximumSuggestionNumber":5,
    "ifAddVisitorQuestionAsSimilarQuestion":true,
    "textBeforeKBArticle":"please refer this article:",
    "ifAddUnrecognizedQuestionsToLearning":false,
  }
```

#### Response
the response is: [AgentAssist](#agentassist);

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id":"w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "isEnabled": false,
    "language":"en",
    "ifIncludeCannedMessage": true,
    "ifIncludeKnowledgeBase":false,
    "ifIncludeChatbot":true,
    "selectedKnowledgeBases":[],
    "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
    "highConfidenceScore":60,
    "maximumSuggestionNumber":5,
    "ifAddVisitorQuestionAsSimilarQuestion":true,
    "textBeforeKBArticle":"please refer this article:",
    "ifAddUnrecognizedQuestionsToLearning":false,
  }' -X PUT https://domain.comm100.com/api/v3/agentAssist
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id":"w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "isEnabled": false,
    "language":"en",
    "ifIncludeCannedMessage": true,
    "ifIncludeKnowledgeBase":false,
    "ifIncludeChatbot":true,
    "selectedKnowledgeBases":[],
    "selectedChatbots":["f9928d68-92e6-4487-a2e8-8234fc9d1f48"],
    "highConfidenceScore":60,
    "maximumSuggestionNumber":5,
    "ifAddVisitorQuestionAsSimilarQuestion":true,
    "textBeforeKBArticle":"please refer this article:",
    "ifAddUnrecognizedQuestionsToLearning":false,
  }
```

# Agent Assist Synonym
  + `GET /api/v3/agentAssist/synonyms` - [Get all synonyms](#get-all-synonyms)
  + `GET /api/v3/agentAssist/synonyms/{id}` - [Get a synonym by id](#get-a-synonym-by-id)
  + `POST /api/v3/agentAssist/synonyms` - [Create a new synonym](#create-a-new-synonym)
  + `PUT /api/v3/agentAssist/synonyms/{id}` - [Update a synonym](#update-a-synonym)
  + `DELETE /api/v3/agentAssist/synonyms/{id}` - [Remove a synonym](#remove-a-synonym)

## Synonym Objects Json Format
### Synonym Object
  Synonym is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A | | id of the Synonym |
  | `content` | string  | no | yes | | content of the Synonym |
  | `synonyms` | string[]  | no | yes | | synonym of the Synonym |

## Agent Assist Synonym Endpoints
### Get all synonyms

  `GET /api/v3/agentAssist/synonyms`

#### Parameters

#### Response
the response is: list of [Synonym](#synonym-object) Objects
  
#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/agentAssist/synonyms
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

[
  {
    "id": "1xs4sad2-92e6-4487-a2e8-8234fc9d1f48",
    "content": "en",
    "synonyms": ["English"]
  },
  {
    "id": "",
    "content": "en",
    "synonyms": ["English"]
  }
]
```

### Get a synonym by id

  `GET /api/v3/agentAssist/synonyms/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the synonym |

#### Response
the response is: [Synonym](#synonym-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/agentAssist/synonyms/1xs4sad2-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

  {
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "content": "en",
    "synonyms": ["English"]
  }
```
  

### Create a new synonym

  `POST /api/v3/agentAssist/synonyms`

#### Parameters
Request body 

The request body contains data with the [Synonym](#synonym-object) structure

example:
  ```json 
  {
    "content": "en",
    "synonyms": ["English"]
  }
```

#### Response
the response is: [Synonym](#synonym-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "content": "en",
    "synonyms": "English"
  }' -X POST https://domain.comm100.com/api/v3/agentAssist/synonyms
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/agentAssist/synonyms/w124sad2-92e6-4487-a2e8-8234fc9d1f48

  {
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "content": "en",
    "synonyms": ["English"]
  }
```

### Update a synonym

  `PUT /api/v3/agentAssist/synonyms/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the synonym |

Request body 

The request body contains data with the [Synonym](#synonym-object) structure

example:
  ```json 
  {
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "content": "en",
    "synonyms": ["English"]
  }
```

#### Response
the response is: [Synonym](#synonym-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "content": "en",
    "synonyms": ["English"]
  }' -X PUT https://domain.comm100.com/api/v3/agentAssist/synonyms/w124sad2-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

  {
    "id": "w124sad2-92e6-4487-a2e8-8234fc9d1f48",
    "content": "en",
    "synonyms": ["English"]
  }
```

### Remove a synonym

  `DELETE /api/v3/agentAssist/synonyms/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the synonym |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/agentAssist/synonyms/w124sad2-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 204 No Content
```

# Agent Assist  learning Question

  + `GET api/v3/agentAssist/learningQuestions` - [Get agent assist learning questions by filters](#get-agent-assist-learning-questions-by-filters)
  + `GET api/v3/agentAssist/learningQuestions/{id}` - [Get an agent assist learning question by id](#get-an-agent-assist-learning-question-by-id)
  + `POST api/v3/agentAssist/learningQuestions` - [Create a new agent assist learning question](#create-a-new-agent-assist-learning-question)
  + `DELETE api/v3/agentAssist/learningQuestions/{id}` - [Remove an agent assist learning question](#remove-an-agent-assist-learning-question)
  + `POST api/v3/agentAssist/learningQuestions:batchCreate` - [Batch add agent assist learning questions](#batch-add-agent-assist-learning-questions)
  + `DELETE api/v3/agentAssist/learningQuestions` - [Batch delete agent assist learning questions](#batch-delete-agent-assist-learning-questions)


## Learning Object Json Format
### Agent Assist Learning Question
  Learning Question is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default |  Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | yes | N/A | | id of the Learning |
  | `type` | string  | no | yes | unidentified | enum value, `manual` and `unidentified` |
  | `question` | string  | no | yes | | questions for bot training |
  | `agentResponse` | string  | no | yes | | agents responses for bot training |
  | `suggestionType` | string  | no | yes | none | enum value, `cannedMessage`,`article`, `intent` and `none` |
  | `topScoreSuggestion` | object  | no | yes | | suggestion's content.<br/>when suggestionType is cannedMessage, it represents [CannedMessageContent](#canned-message-suggestion-content);<br/>when suggestionType is article ,it represents [KnowledgeBaseContent](#knowledge-base-suggestion-content);<br/>when suggestionType is intent, it represents [ChatbotSuggestionContent](#chatbot-suggestion-content). |
  | `score` | float  | no | yes | 0 | the score of the suggestion |
  | `createdTime` | datetime  | N/A | N/A | | |

### Canned Message Suggestion Content
  CannedMessageContent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | N/A | yes | |id of the Canned Message |
  | `title` | string  | N/A | yes | |title of the Canned Message |
  | `content` | string  | N/A | N/A | |the content of the Canned Message |

### Knowledge Base Suggestion Content
  KnowledgeBaseContent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post |Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | N/A | yes | |id of the Knowledge Base |
  | `articleId` | Guid  | N/A | yes | |articleId is the article of Knowledge Base |
  | `title` | string  | N/A | yes | |title of the article |
  | `content` | string  | N/A | N/A | |the content of the article |
  | `url` | string  | N/A | N/A | |the URL of the article |
  | `textBeforeKBArticle` | string  | N/A | N/A | | the message which usually works as guidance for visitors before a knowledge base article link |

### Chatbot Suggestion Content
  Chatbot Suggestion Content is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default |Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  | N/A | yes | |id of the Bot |
  | `intentId` | Guid  | N/A | yes | |id of the intent |
  | `intentName` | string  | N/A | yes | |name of the intent |
  | `content` | string  | N/A | N/A | |the content of the intent answers |


### AgentAssistLearningQuestionsResponse  
LearningQuestionsResponse is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Read-only For Put | Mandatory For Post | Default |Description     | 
  | - | - | :-: | :-: | :-: | - | 
  | `totalCount` | integer   | N/A | N/A | |total rows of Learning Questions |
  | `previousPage` | string | N/A | N/A | Url of the previous page. |
  | `nextPage` | string | N/A | N/A | Url of the next page. |
  | `list` | [AgentAssistLearningQuestion](#agent-assist-learning-question)[] | N/A | N/A | |list of [AgentAssistLearningQuestion](#agent-assist-learning-question) Object |

## Agent Assist Learning Question Endpoints
### Get agent assist learning questions by filters

  `GET api/v3/agentAssist/learningQuestions`

#### Parameters
Query string

  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - | 
  | `timeFrom` | string | yes  | |   |
  | `timeTo` | string | yes  | |  |  
  | `pageIndex` | integer | no  |  1 | page index |
  | `pageSize` | integer | no  | 10 | page size  |
  | `keyword` | string | no  | | search by keyword |
  | `minScore` | float | no  |  |search the data if score >= minScore |

#### Response
the response is: [AgentAssistLearningQuestionsResponse](#AgentAssistLearningQuestionsResponse) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/agentAssist/learningQuestions?timeFrom=2019-11-12 00:00&timeTo=2019-11-13 00:00
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "totalCount": 100,
    "nextPage": "https://domain.comm100.com/api/v3/agentAssist/learningQuestions?pageIndex=2&timeFrom=2019-11-12 00:00&timeTo=2019-11-13 00:00",
    "previousPage": null,
    "list": [
      {
        "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
        "type":"unidentified", 
        "question": "can i get nbn",
        "agentResponse": "",
        "suggestionType": "cannedMessage",
        "topScoreSuggestion":{
          "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
          "title": "NBN",
          "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
        },        
        "score": 45,
        "createdTime":"2019-11-12 15:21:09"
      },
      ...
    ]
  }  
```

### Create a new agent assist learning question

  `POST api/v3/agentAssist/learningQuestions`

####  Parameters
Request body

The request body contains data with the [AgentAssistLearningQuestion](#agent-assist-learning-question) structure

example:
  ```json
  {
    "type":"unidentified", 
    "question": "can i get nbn",
    "agentResponse": "yes, sure!",
    "suggestionType": "cannedMessage",
    "topScoreSuggestion":{
      "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
      "title": "NBN",
      "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
    },        
    "score": 45
  }
```

#### Response
the response is: [AgentAssistLearningQuestion](#agent-assist-learning-question) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "type":"unidentified", 
    "question": "can i get nbn",
    "agentResponse": "yes, sure!",
    "suggestionType": "cannedMessage",
    "topScoreSuggestion":{
      "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
      "title": "NBN",
      "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
    },        
    "score": 45
  }' -X POST https://domain.comm100.com/api/v3/agentAssist/learningQuestions
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/agentAssist/learningQuestions/dawfe21d-92e6-4487-a2e8-92e68d6892e6

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "type":"unidentified", 
    "question": "can i get nbn",
    "agentResponse": "yes, sure!",
    "suggestionType": "cannedMessage",
    "topScoreSuggestion":{
      "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
      "title": "NBN",
      "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
    },        
    "score": 45,
    "createdTime":"2019-11-26 15:21:09"
  } 
```

### Get an agent assist learning question by id
 
  `GET api/v3/agentAssist/learningQuestions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the learningQuestion |

#### Response
the response is: [AgentAssistLearningQuestion](#agent-assist-learning-question) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/agentAssist/learningQuestions/dawfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "id": "dawfe21d-92e6-4487-a2e8-92e68d6892e6",
    "type":"unidentified", 
    "question": "can i get nbn",
    "agentResponse": "",
    "suggestionType": "cannedMessage",
    "topScoreSuggestion":{
      "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
      "title": "NBN",
      "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
    },        
    "score": 45,
    "createdTime":"2019-11-12 15:21:09"
  } 
```

### Remove an agent assist learning question

  `DELETE api/v3/agentAssist/learningQuestions/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `id` | Guid | yes  |  the unique id of the learningQuestion |


#### Response
HTTP/1.1 204 No Content 

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/agentAssist/learningQuestions/dawfe21d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

### Batch add agent assist learning questions

  `POST api/v3/agentAssist/learningQuestions:batchCreate`

####  Parameters

Request body 

The request body contains data with the list of [AgentAssistLearningQuestion](#agent-assist-learning-question) structure

example:
  ```json
  [
    {
      "type":"unidentified", 
      "question": "can i get nbn",
      "agentResponse": "yes, sure!",
      "suggestionType": "cannedMessage",
      "topScoreSuggestion":{
        "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
        "title": "NBN",
        "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
      },        
      "score": 45
    }
  ]
```

#### Response
HTTP/1.1 204 No Content


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
    {
      "type":"unidentified", 
      "question": "can i get nbn",
      "agentResponse": "yes, sure!",
      "suggestionType": "cannedMessage",
      "topScoreSuggestion":{
        "id": "dawdwa-92e6-4487-a2e8-92e68d6892e6",
        "title": "NBN",
        "content": "NBN is powerful, you can access http://www.nbn.com/sales to get it"
      },        
      "score": 45
    }
  ]' -X POST https://domain.comm100.com/api/v3/agentAssist/learningQuestions:batchCreate
```
Response
```json
HTTP/1.1 204 No Content
```

### Batch delete agent assist learning questions

  `DELETE api/v3/agentAssist/learningQuestions`

#### Parameters

Request body 
  - an array of learningQuestions id

  example:
  ```json
  [
    "waw28d68-92e6-4487-a2e8-8234fc9d1f48",
    "92e68d68-92e6-4487-a2e8-8234fc9d1f48",
    "44878d68-92e6-4487-a2e8-8234fc9d1f48"
  ]
  ```

#### Response
HTTP/1.1 204 No Content 

#### Example
Using curl
```
curl -d '[
    "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "92e68d68-92e6-4487-a2e8-8234fc9d1f48",
    "44878d68-92e6-4487-a2e8-8234fc9d1f48"
  ]' -X DELETE https://domain.comm100.com/api/v3/agentAssist/learningQuestions
```
Response
```json
HTTP/1.1 204 No Content
```

# Agent Assist Suggestion
  + `POST /api/v3/agentAssist/questionSuggestions` -[Query question suggestions by agent assist](#query-question-suggestions-by-agent-assist)
  + `POST /api/v3/agentAssist/questionSuggestions:click` -[Question suggestions clicked by agent](#question-suggestions-clicked-by-agent)

## Agent Assist Suggestion Related Object Json Format

### Question
  Question is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | - | 
  | `id` | string  | N/A | yes |  | the unique id of the question |
  | `question` | string  | N/A | yes | | the question visitor asked. |
  | `campaignId` | Guid  | N/A | yes | | the campaign id |

### Suggestion

  Suggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `type` | string  | N/A | N/A | | enum value, `cannedMessage`,`article`, `intent` |
  | `content` | object  | N/A | N/A | |suggestion's content.<br/>when type is cannedMessage, it represents [CannedMessageContent](#canned-message-suggestion-content);<br/>when type is article ,it represents [KnowledgeBaseContent](#knowledge-base-suggestion-content);<br/>when type is intent, it represents [ChatbotSuggestionContent](#chatbot-suggestion-content). |
  | `score` | float  | N/A | N/A | 0 |the score of the suggestion |
 
### QuestionSuggestion

  QuestionSuggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | string  | N/A | N/A | | the unique id of the question |
  | `question` | string  | N/A | N/A | | the question visitor asked. |
  | `ifMatch` | bool  | N/A | N/A | false | if the suggestion score greater than highConfidenceScore then true, otherwise false |
  | `suggestions` | [Suggestion](#suggestion)[] | N/A | N/A | | array of [Suggestion](#suggestion) Object |

### ClickedQuestionSuggestion

  ClickedQuestionSuggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `question` | string  | N/A | N/A | | the question visitor asked. |
  | `clickedSuggestion` | [Suggestion](#suggestion) | N/A | N/A | | |

## Agent Assist Suggestion Endpoints
### Query question suggestions by agent assist

  `POST /api/v3/agentAssist/questionSuggestions`
 
#### Parameters

Request body

The request body contains data with the list of [Question](#question) structure

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
    "suggestions": []
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
          "intentId":"saw54s23-92e6-4487-a2e8-8234fc9d1f48",
          "intentName": "comm100 livechat",
          "content":""
        },
        "score": 88.5
      }
    ]
  }
]
```
### Question suggestions clicked by agent

  `POST /api/v3/agentAssist/questionSuggestions:click`
 
#### Parameters

Request body

The request body contains data with the [ClickedQuestionSuggestion](#ClickedQuestionSuggestion) structure

example:
  ```json
  {
    "question": "what is comm100 livechat about?",
    "clickedSuggestion": {
      "type": "intent",
      "content": {
        "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "intentId":"saw54s23-92e6-4487-a2e8-8234fc9d1f48",
        "intentName": "comm100 livechat",
        "content":""
      },
      "score": 88.5
    }    
  }
```
 
#### Response
HTTP/1.1 200 OK

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "question": "what is comm100 livechat about?",
    "clickedSuggestion": {
      "type": "intent",
      "content": {
        "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "intentId":"saw54s23-92e6-4487-a2e8-8234fc9d1f48",
        "intentName": "comm100 livechat",
        "content":""
      },
      "score": 88.5
    }    
  }' -X POST https://domain.comm100.com/api/v3/agentAssist/questionSuggestions:click
```
Response
```json
HTTP/1.1 200 OK

```
