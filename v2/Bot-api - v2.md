  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 2.0 | v1 | Bot Restful API | 2018-5-5 | Iguo | 
  | 3.0 | v2 | Bot3.0 Update | 2018-12-9 | Iguo |
  | 3.1 | v2 | Add Third-Party Bot | 2019-01-19 | Ares |
  | 3.2 | v2 | Add Agent Bot Restful API | 2019-03-22 | Davy |
  | 3.3 | v2 | Add Comm100 Own Bot Restful API | 2019-05-24 | Page |

# Summary

  | Object | Path |
  | - | - | 
  | [bot](#bot) | `/bot/bots` |
  | [intent](#intent) | `/bot/bots/{bot_id}/intents` |  
  | [entity](#entity) | `/bot/bots/{bot_id}/entities` |  
  | [category](#category) | `/bot/bots/{bot_id}/categories` |  
  | [smart trigger](#smart-trigger) | `/bot/bots/{bot_id}/smarttriggers` |  
  | [quick reply](#quick-reply) | `/bot/bots/{bot_id}/quickreplies` |  
  | [learning question](#learning-question) | `/bot/bots/{bot_id}/learningquestions` | 
  | [report](#report) | `/bot/bots/{bot_id}/reports` | 
  | [general](#general) | `/bot/` |
  | [agent bot setting](#agent-bot-setting) | `/agentBot/setting` |
  | [agent bot word weight](#agent-bot-word-weight) | `/agentBot/wordWeight` |  
  | [agent bot synonym](#agent-bot-synonym) | `/agentBot/synonyms` |  
  | [agent bot learning question](#agent-bot-learing-question) | `/agentBot/learningQuestions` |  
  | [agent bot suggestion](#agent-bot-suggestion) | `/agentBot/questionSuggestions:query` | 

## Bot
  You need `Manage Bot` permission to manage bot and customize the settings for a bot.
  - `Bots` - Bot Manage
    + `GET /api/v2/bot/bots` - [Get all bots of a site](#get-all-bots-of-a-site)
    + `POST /api/v2/bot/bots` - [Create a new bot](#create-a-new-bot)
    + `PUT /api/v2/bot/bots/{id}` - [Update a bot](#update-a-bot)
    + `GET /api/v2/bot/bots/{id}` - [Get a bot by id](#get-a-bot-by-id)
    + `DELETE /api/v2/bot/bots/{id}` - [Remove a bot](#remove-a-bot)
    + `POST /api/v2/bot/bots/{id}/export` - [Export a bot](#export-a-bot)
    + `POST /api/v2/bot/bots/{id}/import` - [Import a bot](#import-a-bot)
    + `POST /api/v2/bot/bots/{id}/train` - [Train a bot](#train-a-bot)
    + `GET /api/v2/bot/bots/{id}/availability`  - [Check if the bot is available](#check-if-the-bot-is-available)
    + `POST /api/v2/bot/bots/{id}/test`  - [Test a bot](#test-a-bot)
    + `POST /api/v2/bot/bots/{id}/sendMessage` - [Callback for webview, send message to visitor](#callback-for-webview,-send-message-to-visitor)
    + `POST /api/v2/bot/bots/{id}/queryIntent` - [chat with bot](#chat-with-bot)
    + `GET /api/v2/bot/bots/{id}/queryIntent:getTop10Score` - [chat with bot top 10 score](#chat-with-bot-top-10-score)

### Bot Related Object Json Format

#### QueryIntentParameter

  QueryIntentParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `channelType` | string  | no | yes | type of the channel,including `liveChat`、`faceBook` and `twitter` |
  | `operationType` | string  | no | yes | type of the operation,including `queryIntent`、`goToIntent`、`viaForm`、`signedIn`、`requestLocation` and `viaPrompts` |
  | `formValues` | [FormValues](#formValue) | no | no | an array of form value |
  | `sessionId` | string  | no | yes | sessionId of the chat |
  | `isHelpful` | boolean  | no | no | whether bot answer is helpful,`true` or `false` |
  | `question` | string  | no | yes | question of the chat |
  | `intentId` | integer  | no | yes | intentId of the bot |
  | `chatId` | integer  | no | yes | chatId of the chat |
  | `senderId` | integer  | no | no | senderId of the chat |
  | `senderType` | integer  | no | no | senderId of the chat |
  | `questionId` | string  | no | yes | questionId of the bot |
  | `campaignId` | integer  | no | yes | id of the campaign setting |
  | `visitorInfo` | [VisitorInfo](#visitorInfo)  | no | yes | visitor info object |

#### FormValue

  Form Value is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `label` | string  | no | yes | label of the formValue |
  | `value` | string  | no | yes | value of the formValue |

#### VisitorInfo

  Visitor info is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer | yes | no | id of the visitor |
  | `longitude` | float | no | no | longitude of the visitor location |
  | `latitude` | float | no | no | latitude of the visitor location |
  | `page_views` | integer | no | yes | count of the visited |
  | `browser` | string | no | yes | visitor use browser type |
  | `chats` | integer | no | yes | count of chat |
  | `city` | string | no | yes | the city of the visitor |
  | `company` | string | no | yes | the company of the visitor |
  | `country` | string | no | yes | the country of the visitor |
  | `current_browsing` | string | no | yes | page of the current browsing |
  | `custom_fields` | [CustomFields](#customfields) | no | yes | an array of custom fields |
  | `custom_variables` | [CustomVariables](#customvariables) | no | yes | an array of custom variables |
  | `department` | int | no | yes | department of the visitor |
  | `email` | string | no | yes | email of the visitor |
  | `first_visit_time` | string | no | yes | the time of first visit |
  | `flash_version` | string | no | yes | version of the flash |
  | `ip` | string | no | yes | ip of the visitor |
  | `keywords` | string | no | yes | search engine key |
  | `landing_page` | string | no | yes | the page of login |
  | `language` | string | no | yes | language |
  | `name` | string | no | yes | name of the visitor |
  | `operating_system` | string | no | yes | operating system of the visitor |
  | `phone` | string | no | yes | phone of the visitor |
  | `product_service` | string | no | yes | product service |
  | `referrer_url` | string | no | yes | referrer url |
  | `screen_resolution` | string | no | yes | screen resolution |
  | `search_engine` | string | no | yes | search engine |
  | `state` | string | no | yes | state of the visitor |
  | `status` | string | no | yes | status of the visitor |
  | `time_zone` | string | no | yes | time zone of the visitor |
  | `visit_time` | string | no | yes | time of the visitor |
  | `visits` | integer | no | yes | count of the visited |
  | `ssoId` | string | no | no | sso id |

#### CustomFields

  Custom fields is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the field |
  | `name` | string  | no | yes | name of the field |
  | `value` | string  | no | yes | value of the field |

#### CustomVariables

  Custom variables is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | string  | no | yes | name of the variable |
  | `value` | string  | no | yes | value of the variable |

#### QueryIntentResponse

  QueryIntentResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | yes | yes | type of the response,including `signIn`、`viaForm`、`viaPrompts`、`highConfidenceAnswer`、`possibleAnswer`、`noAnswer` and `requestLocation` |
  | `chatId` | integer  | yes | yes | chatId of the chat |
  | `question` | string | yes | no | question of the chat |
  | `siteId` | integer  | yes | yes | siteId of the bot |
  | `visitorId` | integer  | yes | yes | id of the visitor |
  | `senderType` | string  | yes | yes | type of the sender,including `agent` and `bot` |
  | `intentId` | integer  | yes | yes | id of the intent |
  | `questionId` | string  | yes | yes | id of the intent question |
  | `smartTriggerActions` | [SmartTriggerAction](#actionex)  | yes | yes | an array of smart trigger actions |
  | `content` | object | yes | yes | response's content. when type is signIn, it represents [SignInResponse](#signinresponse);when type is viaPrompts,it represents [ViaPromptsResponse](#viaprompts); when type is viaForm,it represents [ViaFormResponse](#viaform); when type is highConfidenceAnswer, it represents [HighConfidenceResponse](#highconfidenceresponse); when type is possibleAnswer,it represents [PossibleResponse](#possibleresponse);when type is noAnswer,it represents [NoAnswerResponse](#noanswerresponse);when type is requestLocation, it represents [RequestLocationResponse](#requestlocationresponse). |
  | `score` | float  | no | yes | the score of the intent matched |
  | `intentName` | string  | yes | yes | name of the intent |

#### HighConfidenceResponse

  High confidence response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `intentAnswers` | [Response](#query-intent-response-object)  | yes | yes | an array of intent answers |

#### SignInResponse

  Sign in response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `signInMessage` | string  | yes | yes | message of the sign in |
  | `signInLinkText` | string  | yes | yes | text of the sign in link |
  | `isSSO` | boolean  | yes | yes | is sso,`true` or `false` |
  | `signInURL` | string  | yes | yes | url of the sign in |
  | `customVariable` | string  | yes | yes | custom variable |
  | `openIn` | string  | yes | yes | it is a Enum string. with options `sideWindow`, `newWindow`, `currentWindow` |

#### ViaPrompts

  Via prompts is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `prompt` | string  | yes | yes | text of the prompt |
  | `options` | array  | yes | yes | an array of string quick reply |
 
#### ViaForm

  Via form is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `formMessage` | string  | yes | yes | name of the field |
  | `formTitle` | string  | yes | yes | name of the field |
  | `submitButtonText` | string  | yes | yes | submit button text |
  | `cancelButtonText` | string  | yes | yes | cancel button text |
  | `confirmButtonText` | string  | yes | yes | confirm button text |
  | `fields` | [Fields](#fields)  | yes | yes | an array of fields |

#### Fields

  Fields is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | string  | yes | yes | id of the field |
  | `value` | string  | yes | yes | name of the field |
  | `name` | string  | yes | yes | title of the field |
  | `type` | string  | yes | yes | type of the field,including `text`、`textArea`、`radio`、`checkBox`、`dropDownList`、`checkBoxList`、`attachment`、`rating`、`wrapUpCategory` and `wrapUpComment` |
  | `isRequired` | boolean  | yes | yes | is require, `true` or `false` |
  | `isMasked` | boolean  | yes | yes | is mask,`true` or `false` |
  | `options` | array  | yes | yes | an array of string entity collecion prompts |


#### IntentBase

  IntentBase is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | int  | yes | yes | an array of intents  |
  | `name` | string  | yes | yes | an array of intents  |
  | `score` | float  | yes | yes | an array of intents  |

#### PossibleResponse

  Possible response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `possibleResponsesMessage` | string  | yes | yes | message of the possible responses |
  | `intents` | array  | yes | yes | an array of [IntentBase](#IntentBase)   | 
  | `noAnswerResponse` | [NoAnswerResponse](#noAnswerResponse)  | yes | yes | an NoAnswerResponse object  |

#### NoAnswerResponse

  No answer response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `ifShowChatWithAgent` | boolean  | yes | yes | if shwo chat with agent,`true` or `false` |
  | `noResponseMessage` | string  | yes | yes | message of the no response |
  | `noResponseTextWhenAgentIsOnline` | string  | yes | yes | text of the no response when agent is on line |
  | `noResponseTextWhenAgentIsOffline` | string  | yes | yes | text of the no response when agent is off line |
  | `intent` | object  | yes | yes | object of [IntentBase](#IntentBase)   |

#### RequestLocationResponse

  Request location response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `requestVisitorLocationMessage` | string  | yes | yes | message of the request visitor location |
  | `askVisitorShareLocationText` | string  | yes | yes | text of the ask visitor share location |
  | `url` | string  | yes | yes | url |

#### TestBotResponse

  TestBotResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `intentId` | integer  | yes | yes | id of the intent |
  | `intentName` | string  | yes | yes | name of the intent |
  | `score` | float  | yes | yes | score of match intent |
  | `noAnswerScore` | float  | yes | yes | no answer score of the settings |
  | `type` | string  | yes | yes | type of the response,including `form`、`signIn`、`response` and `location` and `prompts` |
  | `answer` | object  | nyeso | yes | type of the answer,including [ViaPrompts](#viaprompts)、[ViaForm](#viaForm) 、list of [Response](#response-object)、[SignInResponse](#signinresponse) and [RequestLocationResponse](#requestlocationresponse) |

#### RateParameter

  RateParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `isHelpful` | boolean  | yes | yes | whether bot answer is helpful,`true` or `false` |
  | `questionId` | string  | yes | yes | questionId of the bot |
  | `chatId` | integer  | yes | yes | chatId of the chat |
  | `visitorInfo` | [VisitorInfo](#visitorinfo)  | yes | yes | visitor info object |

#### RateResponse

  RateParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `smartTriggerActions` | [SmartTriggerAction](#smarttriggeraction)  | yes | yes | an array of smart trigger actions |
  | `noAnswerResponse` | [NoAnswerResponse](#noAnswerResponse)  | yes | yes | an NoAnswerResponse object  |

#### CreateBot
  CreateBot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | string  | no | yes | name of the bot |
  | `engine` | string  | no | yes | type of the bot, enums contain comm100Bot, thirdPartyBot |
  | `language` | string  | no | yes when type is comm100Bot | language of the bot|
  | `webhookTargetUrl` | string  | no | yes when type is thirdPartyBot| Webhook target Url of the third-party bot | 

#### BotBasic
  Bot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the bot |
  | `name` | string  | no | yes | name of the bot |
  | `engine` | string  | yes | yes | type of the bot, enums contain comm100Bot, thirdPartyBot |
  | `language` | string  | no | yes when type is comm100Bot | language of the bot  |  
  | `avatarName` | string  | no | yes | avatar name of the bot |  
  | `avatarUrl` | string  | no | yes | avatar url of the bot |  
  | `isTrained` | bool  | yes | yes | if the bot is trained |  

#### Bot Object
  Bot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the bot |
  | `name` | string  | no | yes | name of the bot |
  | `engine` | string  | yes | yes | type of the bot, enums contain comm100Bot, thirdPartyBot |
  | `language` | string  | no | yes when type is comm100Bot | language of the bot |  
  | `avatarName` | string  | no | yes | avatar name of the bot |  
  | `avatarUrl` | string  | no | yes | avatar url of the bot |  
  | `isTrained` | bool  | yes | yes when type is comm100Bot | if the bot is trained |  
  | `greetingMessage` | object  | no | yes | list of [GreetingMessage](#greetingmessage) Object | 
  | `noResponseMessage` | string  | no | yes when type is comm100Bot | no response message |  
  | `isShowAgentLinkWhenNoResponse` | bool  | no | yes when type is comm100Bot | is show agent link when no response from bot |  
  | `notHelpfulMessage` | string  | no | yes when type is comm100Bot | not helpful message |  
  | `isShowAgentLinkWhenNotHelpful` | bool  | no | yes when type is comm100Bot | is show agent link when not helpful from bot |  
  | `possibleResponsesMessage` | string  | no | yes when type is comm100Bot | possible responses message |  
  | `possibleResponsesThreshold` | int  | no | yes when type is comm100Bot | possible responses threshold |  
  | `isShowAgentLinkWhenPossibleResponsesThreshold` | int  | no | yes when type is comm100Bot | is show agent link when possible responses threshold |  
  | `possibleResponsesExceedThresholdMessage` | string  | no | yes when type is comm100Bot | possible responses exceed threshold message |  
  | `agentIsOnlineText` | string  | no | yes when type is comm100Bot | agent is online text |  
  | `agentIsOfflineText` | string  | no | yes when type is comm100Bot | agent is offline text |  
  | `transferAgentMessage` | string  | no | yes when type is comm100Bot | transfer agent message |  
  | `leaveAMessageClickedMessage` | string  | no | yes when type is comm100Bot | leave a message button clicked message |  
  | `requestVisitorLocationMessage` | string  | no | yes when type is comm100Bot | request visitor location message |  
  | `locationButtonText` | string  | no | yes when type is comm100Bot | location button text |  
  | `submitButtonText` | string  | no | yes when type is comm100Bot | submit button text |  
  | `cancelButtonText` | string  | no | yes when type is comm100Bot | cancel button text |  
  | `confirmButtonText` | string  | no | yes when type is comm100Bot | confirm button text |  
  | `highConfidenceScore` | string  | no | yes when type is comm100Bot | high confidence score |  
  | `noAnswerScore` | string  | no | yes when type is comm100Bot | no answer score |  
 
#### Third-party Bot Object
  Third-party Bot is represented as simple flat JSON objects with the following keys:  
  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the bot |
  | `name` | string  | no | yes | name of the bot |
  | `engine` | string  | yes | yes | type of the bot, enums contain comm100Bot, thirdPartyBot |
  | `avatarName` | string  | no | yes | avatar name of the bot |  
  | `avatarUrl` | string  | no | yes | avatar url of the bot | 
  | `webhookTargetUrl` | string  | no | yes | Webhook target Url of the third-party bot | 
  | `greetingMessage` | object  | no | yes | list of [GreetingMessage](#greetingmessage) Object | 

#### Campaign
  Campaign is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Campaign |
  | `name` | string  | no | yes | name of the Campaign |
  | `url` | string  | no | yes | url of the Campaign |  

#### NameUrl
  NameUrl is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | string  | no | yes | name of the object |
  | `url` | string  | no | yes | url of the object |  

#### SendMessageParameter

  SendMessageParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `channelType` | string  | no | yes |enums contain default,livechat,facebook and twitter.|
  | `agentId` | integer  | no | yes | agentId of the chat |
  | `sessionId` | integer  | no | yes | sessionId of the chat |
  | `visitorId` | integer  | no | yes | visitorId of the chat |
  | `messages` | list of [Response](#response-object)  | no | yes | an array of responses  |

### Bot End Points
#### Get all bots of a site

  `GET /api/v2/bot/bots`

##### Parameters

query parameters

  - `siteId ` 

##### Response
the response is: list of [BotBasic](#botbasic) Objects

#### create a new bot

  `POST /api/v2/bot/bots`

##### Parameters
query parameters

  - `siteId ` 

request body parameters: [CreateBot](#createbot) Object

##### Response
when Bot type is comm100Bot, the response is: [Bot](#bot-object); when Bot type is thirdPartyBot,the response is: [Third-party Bot](#third-party-bot-object)

#### Update a bot

  `PUT /api/v2/bot/bots/{id}`

##### Parameters
path parameters

  - `id`
query parameters

 - `siteId ` 

request body parameters: [Bot](#bot-object) Object

##### Response
the response is: [Bot](#bot-object) Object

#### Get a bot by id

  `GET /api/v2/bot/bots/{id}`

##### Parameters
path parameters

  - `id`
query parameters

 - `siteId `
##### Response
when Bot type is comm100Bot, the response is: [Bot](#bot-object); when Bot type is thirdPartyBot,the response is: [Third-party Bot](#third-party-bot-object)

#### Remove a bot

  `DELETE /api/v2/bot/bots/{id}`

##### Parameters
path parameters

  - `id`
query parameters

 - `siteId `
##### Response
the response is: Http Status Code `200`

#### Export a bot

  `POST /api/v2/bot/bots/{id}/export`

##### Parameters
path parameters

  - `id`
query parameters

 - `siteId `
##### Response
the response is:

  - `fileName ` -the exported bot fileName, it is a xml file

#### Import a bot

  `POST /api/v2/bot/bots/{id}/import`

##### Parameters
path parameters

  - `id`

query parameters
  - `siteId `
  - `file` -the file to be imported. Server will get the file by Request.files["file"]

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` - it is a guid, uniquely identify the import operation

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

#### Train a bot

  `POST /api/v2/bot/bots/{id}/train`

##### Parameters
path parameters
  
  - `id`
query parameters

 - `siteId `
##### Response
the response is:

  - `operationId ` -the operation id of the train

#### Check if the bot is available

  `GET /api/v2/bot/bots/{id}/availability`

##### Parameters
  path parameters

  - `id`
query parameters

 - `siteId `
##### Response
the response is:

  `true` or `false`

#### Test a bot

  `POST /api/v2/bot/bots/{id}/test`

##### Parameters
path parameters

  - `id`

request body parameters
  - `siteId `
  - `question`  - test visitor question

##### Response
the response is: [TestBotResponse](#testbotresponse) Object 

#### Callback for webview, send message to visitor

  `POST /api/v2/bot/bots/{id}/sendMessage`

##### Parameters
path parameters

  - `id`

query parameters

  - `siteId`

request body parameters: [SendMessageParameter](#sendmessageparameter) Object 

##### Response
the response is: Http Status Code `200`

#### Chat with bot

  `POST /api/v2/bot/bots/{id}/queryIntent`

##### Parameters
path parameters

  - `id`-id of the bot
query parameters

 - `siteId `
request body parameters: [QueryIntentParameter](#queryintentparameter) Object 

##### Response
the response is: [QueryIntentResponse](#queryintentresponse) Object    

#### Chat with bot top 10 score

  `GET /api/v2/bot/bots/{id}/queryIntent:getTop10Score`

##### Parameters
path parameters

  - `id`-id of the bot
query parameters

 - `siteId `
 - `question `

##### Response
the response is: list of [IntentBase](#intentbase) Objects  

## Intent
You need `Manage Bot` permission to manage Intent and customize the settings for a Intent.
  - `Intents` - Intent Manage
  +  `POST /api/v2/bot/bots/{botId}/intents` - [Create a new intent](#create-a-new-intent)
  +  `GET /api/v2/bot/bots/{botId}/intents` - [Get intent(s) by category or by intent name/question](#get-intent(s)-by-category-or-by-intent-namequestion)
  +  `PUT /api/v2/bot/bots/{botId}/intents/{id}` - [Update an intent](#update-an-intent)
  +  `GET /api/v2/bot/bots/{botId}/intents/{id}` - [Get an intent](#get-an-intent)
  +  `DELETE /api/v2/bot/bots/{botId}/intents/{id}` - [Remove an intent](#remove-an-intent)
  +  `POST /api/v2/bot/bots/{botId}/intents/{id}/rating` - [Rate a bot answer as helpful or not helpful](#rate-a-bot-answer-as-helpful-or-not-helpful)
  +  `POST /api/v2/bot/bots/{botId}/intents/import` - [Import intents](#import-intents)
  +  `POST /api/v2/bot/bots/{botId}/intents/{id}:addQuestions` - [Update an intent only add questions](#update-an-intent-only-add-questions)

### Intent Related Ojbect Json Format
#### Intent Object
Intent is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description   |
| - | - | :-: | :-: | - | 
| `id` | integer  | yes | no | id of the intent |
| `name` | string  | no | yes | name of the intent |
|`categoryId`| integer | no | yes | id of the intent category.|
|`ifRequireDetailInfo` | bool | no | no | whether need visitor to provide more detail information.|
|`entityCollectionType` | string | no | yes if ifRequireDetailInfo is true | enums contain viaForm and viaPrompts,this represents the way you want to collect  visitor's information. there are two options: viaForm and viaPrompts.|
|`ifRequireLocation` | bool | no | no | whether need to collect visitor's location information.|
|`questions`| array| no |yes | an array of [Question](#question).|
|`entityCollectionForm`| object | no |yes if entityCollectionType is viaForm | an array of [EntityCollectionForm](#entitycollectionform).|
|`entityCollectionPrompts`| array| no |yes if entityCollectionType is viaPrompts | an array of [EntityCollectionPrompt](#entitycollectionprompt).|
|`answer`| object| no |yes | an item of [Answer](#answer).|

#### IntentBasic
IntentBasic is represented as simple flat json objects with the following keys: 

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
| `id` | integer  | yes | no | id of the intent |
| `name` | string  | no | yes | name of the intent |
|`category`| string | no | yes | name of the intent category.|
|`categoryId`| integer | no | yes | id of the intent category.|

#### AnswerSignInSettings
AnswerSignInSettings is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.|
|`signInMessage` | string  | no | yes |text sent to visitor before signin in button.|
|`signInLinkText` | string  | no | yes |text on signin button.|
|`isSSO` | string  | no | yes |whether is single sign on.|
|`signInURL` | string  | no | yes |url of the signin page.|
|`customVariable` | string  | no | yes |custom value sent to signin page.|
|`openIn` | string  | no | yes |enums contain sideWindow,newWindow,currentWindow,when channelType is livechat, it represents the way that a page will be opened.|

#### Question
Question is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.|
|`text` | string  | no | yes |question you can expect from users,that will trigger this intent. |
|`entityLabels` | array  | no | yes |an array of [EntityLabel](#entitylabel) that you want to mark on current question. |

#### EntityLabel
EntityLabel is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item. |
|`startPos` | integer | no | yes |strat index  of current question you marked. |
|`endPos` | integer | no | yes |end index  of current question you marked. |
|`entityId` | integer | no | yes |id of entity marked on one question. |
|`label` | string | no | yes |label to distinguish same entity marked on one question. |

#### EntityCollectionForm
EntityCollectionForm is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`formMessage` | string | yes | yes if entityCollectionType is viaForm | when entityCollectionType is viaForm, this is a message that will be sent before the button.|
|`formTitle` | string | yes | yes if entityCollectionType is viaForm | when entityCollectionType is viaForm,a button will be sent to visitor if bot need to collect detail information,visitor can click this button to open the form to fillout information. this is the text on this button,and also this is the title of that form.|
|`ifRequireConfirm` | bool | yes | yes | whether need visitor to confirm after collect all detail information that bot needed.|
|`formFields` | array | yes | no |an array of of [EntityCollectionFormField](#entitycollectionformfield) |

#### EntityCollectionFormField
EntityCollectionFormField is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item. |
|`fieldType` | string | no | yes |enums contain text ,textArea,radioBox ,checkBox ,dropDownList ,checkBoxList, this is the type of fields appear on the form. |
|`fieldName` | string | no | yes |this is the field's name appear on the form. |
|`entityId` | integer | no | yes |id of entity marked on one question. |
|`label` | string | no | yes |label to distinguish same entity marked on one question. |
|`isRequired` | bool | no | yes |it marks whether the field appear on the form is required or not. |
|`isMasked` | bool | no | yes |if this is true,visitor's information will replaced by anonymous symbol in chat logs. |
|`options` | array | no | no |an array of of string |

#### EntityCollectionPrompt
EntityCollectionPrompt is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description  |  
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item. |
|`entityId` | integer | no | yes |id of entity marked on one question. |
|`label` | string | no | yes |label to distinguish same entity marked on one question. |
|`questions` | array | no | yes |an array of string |
|`options` | array | no | no |an array of string |

#### TextResponse
TextResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description  |  
| - | - | :-: | :-: | - | 
|`texts` | array | no | yes |an array of list strings. |

#### UrlResponse
UrlResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`url` | string | no | yes |url of the video you choosed.  | 

#### ComplexResponse
ComplexResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |html text updated from old data.  | 

#### QuickReplyResponse
QuickReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |text sent before quickreplys.  | 
|`quickReplyId` | integer | no | yes |id of quickreply you choosed.  | 
|`agentOnlineText` | string | no | yes |text of agent on line.  | 
|`agentOfflineText` | string | no | yes |text of agent off line.  | 
|`quickReplyItems` | array | no | yes |quickreply item list.  | 

#### ComplexQuickReplyResponse
ComplexQuickReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |text sent before quickreplys.  | 
|`agentOnlineText` | string | no | yes |text of agent on line.  | 
|`agentOfflineText` | string | no | yes |text of agent off line.  | 
|`quickReplyItems` | array | no | yes |quickreply item list.  | 

#### ComplexQuickReplyItem 
|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`type` | string | no | yes |enum values, `goToIntent `,`contactAgent `  | 
|`name` | string | no | yes |name of quickreply item name.  | 
|`intentId` | integer | no | yes |id of quickreply you choosed.  | 


#### ButtonResponse
ButtonResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description   |   
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |text above buttons,this text will be sent before buttons.  | 
|`buttons` | array | no | yes |an array of [Button](#button).  | 
|`formValues` | array | no | yes |an array of [FormValue](#formvalue).  | 


#### Button
Button is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.  | 
|`text` | string | no | yes |text on button.  | 
|`type` | string | no | yes |enums contain goToIntent,link and webView,type of buttons  | 
|`linkUrl` | string | no | yes if buttonType is link or webView|url of the web page you want to open.  | 
|`intentId` | string | no | yes if buttonType is goToIntent | id of the intent you choosed.  | 
|`intentName` | string | yes | no | the name of the intent you choosed.  | 
|`openIn` | string | no | yes if channelType is livechat and buttonType is link or webView |enums contain sideWindow,newWindow,currentWindow, it represents the way that a page will be opened.  | 
|`openStyle` | string | no | yes if channelType is livechat or facebook and buttonType is webView |enums contain compact,tall and full,it represents the size of the webview that will be opened.  |

#### Answer
Answer is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`default`| object| no |no | an object of [AnswerSubItem](#answersubitem),but AnswerSubItem.response.type can not be image,video,webhook,complex.  | 
|`livechat`| object| no |no | an object of [AnswerSubItem](#answersubitem).  | 
|`facebook`| object| no |no | an object of [AnswerSubItem](#answersubitem),but AnswerSubItem.response.type can not be complex.  | 
|`twitter`| object| no |no | an object of [AnswerSubItem](#answersubitem),but AnswerSubItem.response.type can not be complex.  | 

#### GreetingMessage
GreetingMessage is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`default`| list of object | no |no | list of [Response](#response-object),but response.type can not be image,video,webhook,complex.  | 
|`livechat`| list of object | no |no | list of [Response](#response-object).  | 
|`facebook`| list of object | no |no | list of [Response](#response-object),but response.type can not be complex.  | 
|`twitter`| list of object | no |no | list of [Response](#response-object),but response.type can not be complex.  | 

#### AnswerSubItem
AnswerSubItem is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`responses`| list of object | no |no | an array of [Response](#response-object)  | 
|`ifNeedSignIn`| bool | no |yes | whether need sign in when bot response visitor's question     | 
|`signInSettings`| object | no |yes if isNeedSignInBeforeBotRespond is true | an item of [AnswerSignInSettings](#answersigninsettings)  | 

#### Response Object
Response is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.  | 
|`type` | string | yes | yes |enums contain text,image,video,webhook,button,quickReply,complex.  | 
|`content` | object | yes | yes |response's content. when type is text, it represents [TextResponse](#textresponse);when type is image ,it represents [ImageResponse](#nameurl);when type is video, it represents [VideoResponse](#urlresponse); when type is webhook,it represents [WebhookResponse](#urlresponse);when type is button,it represents [ButtonResponse](#buttonresponse);when type is quickReply, it represents [QuickReplyResponse](#quickreplyresponse);when type is complex,it represents   [ComplexResponse](#complexresponse).  | 

#### Query Intent Response Object
Response is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`type` | string | yes | yes |enums contain text,image,video,webhook,button,quickReply,complex.  | 
|`content` | object | yes | yes |response's content. when type is text, it represents string;when type is image ,it represents [ImageResponse](#nameurl);when type is video, it represents [VideoResponse](#urlresponse); when type is button,it represents [ButtonResponse](#buttonresponse);when type is quickReply, it represents [ComplexQuickReplyResponse](#complexquickreplyresponse);when type is complex,it represents   [ComplexResponse](#complexresponse).  | 


#### Create a new intent

  `POST /api/v2/bot/bots/{botId}/intents`

##### Parameters
  path parameters

  - `botId` - required , id of current bot

query parameters

- `siteId ` 
  - `learningQuestionId` - Comma-separated strings,id from visitor's  not matched  questions,optional

  request body parameters

  - `intent` - an item of [Intent](#intent-object),required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object),required

#### Update an intent

  `PUT /api/v2/bot/bots/{botId}/intents/{id}`

##### Parameters
  path parameters

  - `id`
  - `botId` - required , id of current bot

query parameters

- `siteId ` 
  - `learningQuestionId` - Comma-separated strings,id from visitor's  not matched  questions,optional

  request body parameter

  - `intent` - an item of [Intent](#intent-object),required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object)

#### Get intent(s) by category or by intent name/question

  `GET /api/v2/bot/bots/{botId}/intents`

##### Parameters

  path parameters
  - `botId` - id of current bot,required

query parameters

- `siteId ` 
  - `categoryId` -id of the category you want to explorer
  - `keyword` -name or question of the intent you want to explorer

##### Response
the response is:

  - `intentBasics` - an array of [IntentBasic](#intentbasic)

####  Get an intent

   `GET /api/v2/bot/bots/{botId}/intents/{id}`

##### Parameter
query parameters

- `siteId ` 

  path parameters
  - `botId` - id of current bot,required
  - `id` - id of the intent you want to get,required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object)

#### Remove an intent

  `DELETE /api/v2/bot/bots/{botId}/intents/{id}`

##### Parameter
query parameters

- `siteId ` 

path parameters

- `botId `
- `id`

##### Response
the response is: Http Status Code `200`

#### Rate a bot answer as helpful or not helpful

  `POST /api/v2/bot/bots/{botId}/intents/{id}/rating`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId`-id of the bot
  - `id`-id of the intent

request body parameters: [RateParameter](#rateparameter) Object 

##### Response
the response is: [RateResponse](#rateresponse) Object 

#### Import intents

  `POST /api/v2/bot/bots/{botId}/intents/import`

##### Parameters
path parameters

  - `botId` 
  - `mode` - enum values, `increment` or `overwrite`
 
query parameters

- `siteId ` 
  - `file` -the file to be imported. Server will get the file by Request.files["file"]

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` - it is a guid, uniquely identify the import operation

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `failUrl ` 
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

#### Update an intent only add questions

  `POST /api/v2/bot/bots/{botId}/intents/{id}:addQuestions` 

##### Parameters
  path parameters

  - `id`
  - `botId` - required , id of current bot

query parameters

- `siteId ` 
  - `learningQuestionId` - Comma-separated strings,id from visitor's  not matched  questions,optional

  request body parameter

  - `questions` - an array of string,required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object)

## Entity
  You need `Manage Bot` permission to manage bot Entity and customize the settings for a bot Entity.
  - `Entities` - Entity Manage
    + `GET /api/v2/bot/bots/{botId}/entities` - [Get entities by entity name/keyword/synonym](#get-entities-by-entity-name/keyword/synonym)
    + `POST /api/v2/bot/bots/{botId}/entities` - [Create a new entity](#create-a-new-entity)
    + `PUT /api/v2/bot/bots/{botId}/entities/{id}` - [Update an entity](#update-an-entity)
    + `DELETE /api/v2/bot/bots/{botId}/entities/{id}` - [Remove an entity](#remove-an-entity)
    + `GET /api/v2/bot/bots/{botId}/entities/{id}` - [Get an entity by id](#get-an-entity-by-id)
    + `POST /api/v2/bot/bots/{botId}/entities/import` - [Import entities](#import-entities)

### Entity Related Objects Json Format
#### EntityBasic
  EntityBasic is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Entity |
  | `name` | string  | no | yes | name of the Entity |
  | `displayName` | string  | no | yes | display name of the Entity |
  | `type` | string  | no | yes | type of the Entity, it is a enum value. `entity` or `systemEntity` |

#### Entity Object
  Entity is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Entity |
  | `name` | string  | no | yes | name of the Entity |
  | `displayName` | string  | no | yes | display name of the Entity |
  | `type` | string  | no | yes | type of the Entity, it is a enum value. `entity` or `systemEntity` |
  | `keywords` | list of [EntityKeyword](#entitykeyword) Objects   | no | yes | keyword and the synonyms list of the keyword |

#### EntityKeyword
 EntityKeyword is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the entity keyword object |
  | `keyword` | string  | no | yes | Keyword |
  | `synonyms` | list of string  | no | yes | synonyms list of keyword |


### Entity End Points
#### Get entities by entity name/keyword/synonym

  `GET /api/v2/bot/bots/{botId}/entities`

##### Parameters
path parameters

  - `botId` 
  
query parameters

- `siteId ` 
  - `keyword ` -entity name or keyword or synonym

##### Response
the response is: list of [EntityBasic](#entitybasic) Objects
  
#### Create a new entity

  `POST /api/v2/bot/bots/{botId}/entities`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

request body parameters: [Entity](#entity-object) Object

##### Response
the response is: [Entity](#entity-object) Object

#### Update an entity

  `PUT /api/v2/bot/bots/{botId}/entities/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `id`
  - `botId` 

request body parameters: [Entity](#entity-object) Object

##### Response
the response is: [Entity](#entity-object) Object

#### Remove an entity

  `DELETE /api/v2/bot/bots/{botId}/entities/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId `
  - `id ` 

##### Response
the response is: Http Status Code `200`

#### Get an entity by id

  `GET /api/v2/bot/bots/{botId}/entities/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 
  - `id `

##### Response
the response is: [Entity](#entity-object) Object

#### Import entities

  `POST /api/v2/bot/bots/{botId}/entities/import`

##### Parameters
path parameters

  - `botId` 

query parameters

- `siteId ` 
  - `file` -the file to be imported. Server will get the file by Request.files["file"]

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` - it is a guid, uniquely identify the import operation

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `failUrl ` 
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

## Category
  You need `Manage Bot` permission to manage bot category and customize the settings for a bot category.
  - `Categories` - Category Manage
    + `GET /api/v2/bot/bots/{botId}/categories` - [Get all categories of the bot](#get-all-categories-of-the-bot)
    + `POST /api/v2/bot/bots/{botId}/categories` - [Create a new category](#create-a-new-category)
    + `PUT /api/v2/bot/bots/{botId}/categories/{id}?move={1}` - [Update a category](#update-a-category)
    + `DELETE /api/v2/bot/bots/{botId}/categories/{id}` - [Remove a category](#remove-a-category)

### Category Related Object Json Format
#### Category
  Category is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Category |
  | `name` | string  | no | yes | name of the Category |
  | `parentId` | integer  | no | yes | parent Id of the Category |
  | `botId` | integer  | no | yes | bot id of the Category |

### Category End Points
#### Get all categories of the bot

  `GET /api/v2/bot/bots/{botId}/categories`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

##### Response
the response is: list of [Category](#category) Objects

#### Create a new category

  `POST /api/v2/bot/bots/{botId}/categories`

#####  Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

request body parameters: [Category](#category) Object

##### Response
the response is: [Category](#category) Object

#### Update a category

  `PUT /api/v2/bot/bots/{botId}/categories/{id}?move={1}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `id`
  - `botId` 

request parameters
  - `move` -true or false. true move the category as a sub-category of parentId and delete the category;false only update the categroy info.

request body parameters: [Category](#category) Object

##### Response
the response is: [Category](#category) Object

#### Remove a category

  `DELETE /api/v2/bot/bots/{botId}/categories/{id}`

##### Parameters
path parameters

  - `botId` 
  - `id ` 

##### Response
the response is: Http Status Code `200`

## Smart Trigger
  You need `Manage Bot` permission to manage Smart Triggers.
  - `Smart Triggers` - Smart Trigger Manage
    + `POST /api/v2/bot/bots/{botId}/smartTriggers` -[Create a new smart trigger](#create-a-new-smart-trigger)
    + `GET /api/v2/bot/bots/{botId}/smartTriggers` -[Get all smart triggers of the bot](#get-all-smart-triggers-of-the-bot)
    + `GET /api/v2/bot/bots/{botId}/smartTriggers/{id}`  -[Get a smart trigger by id](#get-a-smart-trigger-by-id)
    + `PUT /api/v2/bot/bots/{botId}/smartTriggers/{id}`  -[Update a smart trigger](#update-a-smart-trigger)
    + `DELETE /api/v2/bot/bots/{botId}/smartTriggers/{id}`  -[Remove a smart trigger](#remove-a-smart-trigger)
    + `PUT /api/v2/bot/bots/{botId}/smartTriggers/order`  -[Update the order of smart triggers](#Update-the-order-of-smart-triggers)

### Smart Trigger Related Ojbect Json Format
#### TriggerRule

  TriggerRule is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no |id of the smart trigger. |
  | `name` | string | no | yes |name of smart trigger. |
  | `isEnabled` | boolean | no | no |smartTriggers if is enabled. the default value is false.|
  | `conditions` | [Conditions](#conditions) | no | no |[Conditions](#conditions) object. |
  | `actions` | array | no | no |an array of [Action](#action) object. |

####  Conditions
  Conditions is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `when` | string | no | yes | the relationship between condition.  exp: [all,or,expression]|
  | `expression` | string | no | no |A formula to calculate exp:(1 or 2) and 3  |
  | `items` | array | no | no | an array of  [Condition](#condition) object. |

 #### Condition
  Condition is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `variable` | string | no | no | value of the Condition |
  | `expression` | string | no | yes |  the rule of expression.exp:[equal,notEqual,contains,notContains,regularExpression,lessThan,moreThan] |
  | `items` | array | no | yes | an string array of condition matching value |
 
####  Action
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `type` | string | no | yes | the type of the action. exp:[notification,monitor,transfer,changeAssignee,segment]|
  | `isEnabled` | boolean | no | yes | action if is enabled. |
  | `target` | [Target](#target) | no | no |  action target |
  | `agentOfflineMessage` | string | no | no | agent offlineMessage prompt message |

####  ActionEx
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `Action.type` | string | no | yes | the type of the action. exp:[notification,monitor,transfer,changeAssignee,segment]|
  | `Action.isEnabled` | boolean | no | yes | action if is enabled. |
  | `Action.target` | [Target](#target) | no | no |  action target |
  | `Action.agentOfflineMessage` | string | no | no | agent offlineMessage prompt message |
  | `agentOfflineText` | string | no | no | leave message button text when agent is offline |

####  Target
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `type` | string | no | no | The trigger action target type. exp:[department,agent] |
  | `departments` | array | no | no | an integer array of  department id. |
  | `agents` | array | no | no | an integer  array of  agent id. |
  | `visitorSegmentId` | integer  | no | no | visitor Segment Id |

  ####  Order
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | yes | The smarttrigger id  |
  | `position` | integer | no | yes |  The smarttrigger order number. |

### Smart Trigger End Points  
##### Get all smart triggers of the bot

  `GET /api/v2/bot/bots/{botId}/smartTriggers`
 
###### Parameters
query parameters

- `siteId ` 

 path parameters

 - `botId` 

####### Response    

 - Response: An array of  [TriggerRule](#triggerrule)  Object.
    
##### Get a smart trigger by id

  `GET /api/v2/bot/bots/{botId}/smartTriggers/{id}`

###### Parameters  
query parameters

- `siteId ` 

  path parameters

  - `botId` 
  - `id`

###### Response

  - Response:  [TriggerRule](#triggerrule) Object.
    
##### Create a new smart trigger

  `POST /api/v2/bot/bots/{botId}/smartTriggers`

###### Parameters
query parameters

- `siteId ` 

  path parameters

  - `botId` 

   request body parameters
  - [TriggerRule](#triggerrule) Object

###### Response

  the response is: [TriggerRule](#triggerrule) Object


##### Update a smart trigger

  `PUT /api/v2/bot/bots/{botId}/smartTriggers/{id}`
    
###### Parameters  
query parameters

- `siteId ` 

path parameters

  - `id`
  - `botId` 

 request body parameters
  - [TriggerRule](#triggerrule) Object

###### Response
      
  the response is [TriggerRule](#triggerrule) Object
    
##### Remove a smart trigger
 
  `DELETE /api/v2/bot/bots/{botId}/smartTrigger/{id}`
  
###### Parameters  
query parameters

- `siteId ` 

path parameters

  - `botId` 
  - `id`
      
###### Response   
the response is: Http Status Code `200`

##### Update the order of smart triggers

  `PUT /api/v2/bot/bots/{botId}/smartTriggers/order`
    
###### Parameters  
query parameters

- `siteId ` 

path parameters

  - `botId` 

 request body parameters
  - an array list of [Order](#Order) Object

###### Response
      
  the response is: Http Status Code `200`
    
##### Remove a smart trigger
## Quick Reply
  You need `Manage Bot` permission to manage Quick Reply and customize the settings for a Quick Reply.
  - `Quick Replies` - Quick Reply Manage
    + `GET /api/v2/bot/bots/{botId}/quickreplies` - [Get all quick replies of a bot](#get-all-quick-replies-of-a-bot)
    + `POST /api/v2/bot/bots/{botId}/quickreplies` - [Create a new quick reply](#create-a-new-quick-reply)
    + `GET /api/v2/bot/bots/{botId}/quickreplies/{id}` - [GET a quick reply](#get-a-quick-reply)
    + `PUT /api/v2/bot/bots/{botId}/quickreplies/{id}` - [Update a quick reply](#update-a-quick-reply)
    + `DELETE /api/v2/bot/bots/{botId}/quickreplies/{id}` - [Remove a quick reply](#remove-a-quick-reply)

### Quick Reply Json Format
#### Quick Reply Object
  Quick Reply is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Quick Reply |
  | `name` | string  | no | yes | name of the Quick Reply |
  | `items` | list of [Quick Reply Item](#Quick-Reply-Item) Objects   | no | no | the items of quick reply |

#### Quick Reply Item Object
 QuickReplyItem is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of Quick Reply item |
  | `type` | string  | no | yes | enum value, `goToIntent` and `contactAgent` |
  | `name` | string  | no | no | when item type is goToIntent, it is the name of the intent or it is empty string |
  | `intentId` | integer  | no | no | when item type is goToIntent, it is the id of the intent or it is 0 |

### Quick Reply End Points

#### Get all quick replies of a bot

  `GET /api/v2/bot/bots/{botId}/quickreplies`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId`

##### Response
the response is: list of [QuickReply](#quick-reply-object) Objects

#### Create a new quick reply

  `POST /api/v2/bot/bots/{botId}/quickreplies`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

request body parameters: [QuickReply](#quick-reply-object) Object

##### Response
the response is: [QuickReply](#quick-reply-object) Object

### Get a quick reply

  `PUT /api/v2/bot/bots/{botId}/quickreplies/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `id`
  - `botId` 

##### Response
the response is: [QuickReply](#quick-reply-object) Object

### Update a quick reply

  `GET /api/v2/bot/bots/{botId}/quickreplies/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `id`
  - `botId` 

request body parameters: [QuickReply](#quick-reply-object) Object

##### Response
the response is: [QuickReply](#quick-reply-object) Object

#### Remove a quick reply

  `DELETE /api/v2/bot/bots/{botId}/quickreplies/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 
  - `id ` 

##### Response
the response is: Http Status Code `200`

## Learning Question
  You need `Manage Bot` permission to manage Learning Question and customize the settings for a Learning Question.
  - `Learning Questions` - Learning Question Manage
    + `GET /api/v2/bot/bots/{botId}/learningQuestions` - [Get all learning questions of a bot](#get-all-learning-questions-of-a-bot)
    + `DELETE /api/v2/bot/bots/{botId}/learningQuestions/{id}` - [Remove a learning question](#remove-a-learning-question)
    + `POST /api/v2/bot/bots/{botId}/learningQuestions` - [Import learning questions](#import-learning-questions)
    + `GET /api/v2/bot/bots/{botId}/learningQuestions/operation` - [Get Operation Id](#get-operation-id)

### Learning Question Related Objects Json Format
#### LearningQuestion
  LearningQuestion is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Read-only    | Mandatory | Description     | 
  | - | - | :-: | :-: | - | 
  | `id` | integer   | yes | yes | id of Learning Question |
  | `botName` | string   | yes | yes | name of the bot |
  | `chatId` | int   | yes | yes | id of the chat |
  | `question` | string   | yes | yes | visitor asked question |
  | `intentId` | int   | yes | yes | id of the intent |
  | `intentName` | string   | yes | yes | name of the intent |
  | `score` | double   | yes | yes | match score between the visitor question and itent. |
  | `rateType` | string   | yes | yes | enum type. `helpfull`, `notHelpfull`, `none` |
  | `answerType` | string   | yes | yes | enum type. `highConfidenceAnswer`, `possibleAnswer`, `noAnswer`, `none` |
  | `questionAskedTime` | datetime   | yes | yes | question asked time |

#### LearningQuestionsResponse  
LearningQuestionsResponse is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Read-only    | Mandatory | Description     | 
  | - | - | :-: | :-: | - | 
  | `rowsCount` | integer   | yes | yes | total rows of Learning Questions |
  | `data` | list object   | no | yes | list of [LearningQuestion](#learningquestion) Object |

### Learning Question End Points
#### Get all learning questions of a bot

  `GET /api/v2/bot/bots/{botId}/learningQuestions`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

query parameters

  - `timeFrom ` -query start time.
  - `timeTo ` -query end time.
  - `timezone ` -
  - `page ` -
  - `pageSize ` -
  - `keywords ` -
  - `minScore ` - 

##### Response

the response is: [LearningQuestionsResponse](#learningquestionsresponse) Objects

#### Remove a learning question

  `DELETE /api/v2/bot/bots/{botId}/learningQuestions/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 
  - `id ` 

##### Response
the response is: Http Status Code `200`

#### Import learning questions

  `POST /api/v2/bot/bots/{botId}/learningQuestions`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

request body parameters
- an array list of string

##### Response
the response is:

  - `status ` -the value is `Wait `
  - `operationId ` - it is a guid, uniquely identify the import operation
  - `percent ` - it is a integer, progress of the import operation

#### Get Operation Id

  `GET /api/v2/bot/bots/{botId}/learningQuestions/operation`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `botId` 

query parameters

##### Response

the response is: operationId - it is a guid, uniquely identify the import operation

## report
  - `Reports` - Bot Manage
    + `GET /api/v2/bot/reports/chat` - [Chat report](#chat-report)
    + `GET /api/v2/bot/reports/answer` - [Answer report](#answer-report)
    + `GET /api/v2/bot/reports/highConfidenceAnswer` - [High confidence answer report](#high-confidence-answer-report)
    + `GET /api/v2/bot/reports/rating` - [Rating report](#rating-report)
    + `GET /api/v2/bot/reports/botAgent` - [Bot versus agent report](#bot-versus-agent-report)
    + `GET /api/v2/bot/reports/last7DaysSummary` - [Last 7 days summary report](#last-7-days-summary-report)
    + `GET /api/v2/bot/reports/7DaysDaily` - [Last 7 days daily report](#last-7-days-daily-report)
    + `GET /api/v2/bot/reports/export`  - [Export report by report type](#export-report-by-report-type)
    + `GET /api/v2/bot/reports/intentUsageByCategory`  - [Intent Usage by category](#intent-usage-by-category)
    + `GET /api/v2/bot/reports/intentUsageByTime`  - [Intent Usage by time](#intent-usage-by-time)

### Report Related Object Json Format
#### ReportParameters
  ReportParameters is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `siteId` | integer  | yes | yes | query site id |
  | `filterType` | string  | yes | yes | Enum type,  `site`, `campaign`, `bot`, `facebookPage`, `twitterAccount`, `chatFilterType` |
  | `filterValue` | string  | yes | yes | value of the filter, when filterType is `chatFilterType` then filterValue must is `All Chats` or `Exclude Chats from Bot to Agents` |
  | `timeFrom` | datetime  | yes | yes | query start time |
  | `timeTo` | datetime  | yes | yes | query end time |
  | `timeZone` | string  | yes | yes | ±hh:mm, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time |
  | `displayBy` | string  | yes | yes | query type, it is a Enum. `day`, `week`, `month`. |
  | `dimensionType` | string  | yes | yes | Enum type,  `byTime`,`allChannel`,`livechatChannel`,`facebookChannel`, `twitterChannel`. |

#### ChatReport
  ChatReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `totalBotResolved` | int  | yes | yes |  |
  | `totalBotUnResolved` | int  | yes | yes |  |
  | `totalBotTransferedAgent` | int  | yes | yes |  |
  | `totalBotTransferredOfflineMessage` | int  | yes | yes |  |
  | `totalAgentChatTime` | string  | yes | yes | the string format is `day.hour:minute:second`  |
  | `totalBotChatTime` | string  | yes | yes | the string format is `day.hour:minute:second` |
  | `dataList` | object  | yes | yes | list of [ChatReportDetail](#chatreportdetail) Object  |

#### ChatReportDetail
  ChatReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `botResolved` | int  | yes | yes |  |
  | `botUnResolved` | int  | yes | yes |  |
  | `botTransferedAgent` | int  | yes | yes |  |
  | `botTransferredOfflineMessage` | int  | yes | yes |  |
  | `agentChatTime` | string  | yes | yes | the string format is `day.hour:minute:second` |
  | `botChatTime` | string  | yes | yes | the string format is `day.hour:minute:second` |
  | `time` | datetime  | yes | yes | statistical time |

#### AnswerReport
  AnswerReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `percentOfHighConfidenceAnswers` | double  | yes | yes | percentage of high configdence answer |
  | `totalAnswers` | int  | yes | yes | total answers count |
  | `totalHighConfidenceAnswers` | int  | yes | yes | total high configdence answers count |
  | `totalNoAnswers` | int  | yes | yes | total no answers count |
  | `totalPossibleAnswers` | int  | yes | yes | total possible answers count |
  | `dataList` | object  | yes | yes | list of [AnswerReportDetail](#answerreportdetail) Object  |

#### AnswerReportDetail
  AnswerReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `percentOfHighConfidenceAnswers` | double  | yes | yes | percentage of high configdence answer |
  | `answers` | int  | yes | yes | total answers count |
  | `highConfidenceAnswers` | int  | yes | yes | total high configdence answers count |
  | `noAnswers` | int  | yes | yes | total no answers count |
  | `possibleAnswers` | int  | yes | yes | total possible answers count |
  | `time` | datetime  | yes | yes | statistical time |

#### HighConfidenceReport
  HighConfidenceReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `totalHelpful` | int  | yes | yes | high configdence answers count |
  | `totalHighConfidence` | int  | yes | yes | total answers count |
  | `totalNoRate` | int  | yes | yes | total high configdence answers count |
  | `totalNotHelpful` | int  | yes | yes | total no answers count |
  | `dataList` | object  | yes | yes | list of [HighConfidenceReportDetail](#highconfidencereportdetail) Object  |

#### HighConfidenceReportDetail
  HighConfidenceReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `helpful` | int  | yes | yes | high configdence answers count |
  | `highConfidence` | int  | yes | yes | total answers count |
  | `noRate` | int  | yes | yes | total high configdence answers count |
  | `notHelpful` | int  | yes | yes | total no answers count |
  | `time` | datetime  | yes | yes | statistical time |

#### RatingReport
  RatingReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | double  | yes | yes | average score |
  | `totalRatingTimes` | int  | yes | yes | rating times |
  | `totalScore1Times` | int  | yes | yes | the rating score is 1 times |
  | `totalScore2Times`  | int  | yes | yes | the rating score is 2 times |
  | `totalScore3Times`  | int  | yes | yes | the rating score is 3 times |
  | `totalScore4Times`  | int  | yes | yes | the rating score is 4 times |
  | `totalScore5Times`  | int  | yes | yes | the rating score is 5 times |
  | `dataList` | object  | yes | yes | list of [RatingReportDetail](#ratingreportdetail) Object  |

#### RatingReportDetail
  RatingReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | double  | yes | yes | average score |
  | `ratingTimes` | int  | yes | yes | rating times |
  | `score1Times` | int  | yes | yes | the rating score is 1 times |
  | `score2Times`  | int  | yes | yes | the rating score is 2 times |
  | `score3Times`  | int  | yes | yes | the rating score is 3 times |
  | `score4Times`  | int  | yes | yes | the rating score is 4 times |
  | `score5Times`  | int  | yes | yes | the rating score is 5 times |
  | `time` | datetime  | yes | yes | statistical time |

#### BotAgentReport
  BotAgentReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | double  | yes | yes | average score |
  | `avgTime` | double  | yes | yes | average time |
  | `chats` | int  | yes | yes | chats |
  | `agent` | object  | yes | yes | list of [BotAgentReportDetail](#botagentreportdetail) Object  |
  | `bot` | object  | yes | yes | list of [BotAgentReportDetail](#botagentreportdetail) Object  |

#### BotAgentReportDetail
  BotAgentReportBotDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | double  | yes | yes | average score |
  | `avgTime` | double  | yes | yes | average time |
  | `chats` | int  | yes | yes | chats |
  | `totalChatTime` | int  | yes | yes | the string format is `day.hour:minute:second` |
  | `time` | datetime  | yes | yes | statistical time |

#### Last7DaysSummaryReport
  Last7DaysSummaryReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `averageRatingScore` | double  | yes | yes | average rating score |
  | `botOnlyChatCount` | int  | yes | yes | bot only chats count |
  | `botOnlyChatsTime` | int  | yes | yes | bot only chats time |
  | `botAnswerCount` | int  | yes | yes | bot answers count |
  | `chatsFromBotToAgentCount` | int  | yes | yes | transferred from bot to agent chats count |
  | `percentageOfBotOnlyChats` | double  | yes | yes | helpful answers count |
  | `percentageOfHighConfidenceAnswers` | double  | yes | yes | percentage of high confidence answers |

#### Last7DaysDailyReport
  Last7DaysDaily is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `totalChatbotOnly` | int  | yes | yes | total bot only chats count |
  | `totalFromBotToAgent` | int  | yes | yes | total transferred from bot to agent chats count |
  | `totalPercentageOfBotOnlyChats` | double  | yes | yes | total percentage of bot only chats |
  | `dataList` | object  | yes | yes | list of [Last7DaysDailyReportDetail](#last7daysdailyreportdetail) Object  |

#### Last7DaysDailyReportDetail
  Last7DaysDailyDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `chatbotOnly` | int  | yes | yes | total bot only chats count |
  | `fromBotToAgent` | int  | yes | yes | total transferred from bot to agent chats count |
  | `dailyChatsCount` | int  | yes | yes | daily chats count |
  | `percentageOfBotOnlyChats` | double  | yes | yes | total percentage of bot only chats |
  | `time` | datetime  | yes | yes | statistical time |

#### IntentUsageByCategory
  IntentUsageByCategory is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `category` | string  | yes | yes | the category of the intent  |
  | `intentName` | string  | yes | yes | the intent name |
  | `count` | int  | yes | yes | the count of use |


#### IntentUsageByTime
  IntentUsageByTime is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `total` | int  | yes | yes |  |
  | `top3UsedIntents` | object  | yes | yes | list of [IntentUsage](#intentusage) Object  |
  | `dataList` | object  | yes | yes | list of [IntentUsageDetailsByTime](#IntentUsageDetailsByTime) Object  |

#### IntentUsage
  IntentUsage is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `intentName` | string  | yes | yes | the intent name |
  | `count` | int  | yes | yes | the count of use |

#### IntentUsageDetailsByTime
  IntentUsageDetailsByTime is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `time` | string  | yes | yes | statistical time |
  | `totalCount` | int  | yes | yes |  |
  | `mostTriggered` | int  | yes | yes | the count of most triggered intent |
  | `secondMostTriggered` | int  | yes | yes | the count of second most Triggered intent |
  | `thirdMostTriggered` | int  | yes | yes | the count of third most Triggered intent |

### Report End Points  
#### Chat report

  `GET /api/v2/bot/reports/chat`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [ChatReport](#chatreport) Object

#### Answer report

  `GET /api/v2/bot/reports/answer`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [AnswerReport](#answerreport) Object

#### High confidence answer report

  `GET /api/v2/bot/reports/highConfidenceAnswer`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [HighConfidenceReport](#highconfidencereport) Object
    
#### Rating report

  `GET /api/v2/bot/reports/rating`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [RatingReport](#ratingreport) Object
    
#### Bot versus agent report

  `GET /api/v2/bot/reports/botAgent`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [BotAgentReport](#botagentreport) Object
    
#### Last 7 days summary report

  `GET /api/v2/bot/reports/last7DaysSummary`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [Last7DaysSummaryReport](#last7dayssummaryreport) Object
    
#### Last 7 days daily report

  `GET /api/v2/bot/reports/last7DaysDaily`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [Last7DaysDailyReport](#last7daysdailyreport) Object
    
#### Export report by report type

  `GET /api/v2/bot/reports/export `

##### Parameters
query parameters

  - `siteId ` 
  - [ReportParameters](#reportparameters) Object
  - `reportType ` -Enum value: `chat`, `response`, `highConfidenceResponse`, `rating`, `botAgent`, `last7DaysDaily`, `intentUsageByCategory`, `intentUsageByTime`
  
##### Response
the response is:

  - `fileName` -the excel report file full name

#### Intent usage by category

  `GET /api/v2/bot/reports/intentUsageByCategory`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [IntentUsageByCategory](#IntentUsageByCategory) Object

#### Intent usage by time

  `GET /api/v2/bot/reports/intentUsageByTime`

##### Parameters
query parameters

- `siteId ` 
- [ReportParameters](#reportparameters) Object

##### Response
the response is: [IntentUsageByTime](#IntentUsageByTime) Object

## General
  You need `Manage Bot` permission to manage General settings.
  - `General` 
    + `POST /api/v2/bot/file` - [Upload file temporarily, the file will be deleted in 3 hours](#upload-file-temporarily-and-the-file-will-be-deleted-in-3-hours)
    + `POST /api/v2/bot/image`  - [Upload image](#upload-image)
    + `POST /api/v2/bot/newBotRequest` - [Request to create a new bot](#request-to-create-a-new-bot)
    + `GET /api/v2/bot/botEnabled` - [Get if the site is enabled bot](#get-if-the-site-is-enabled-bot)
    + `GET /api/v2/bot/defaultAvatar` - [Get the default avatar of bot](#get-the-default-avatar-of-bot)
    + `GET /api/v2/bot/quota` - [Get used quotas and quota balance of a site](#get-used-quotas-and-quota-balance-of-a-site)
    + `GET /api/v2/bot/languages` - [Get all supported languages](#get-all-supported-languages)
    + `GET /api/v2/bot/operations/{id}` - [Get the operations such as import or train status](#get-the-operations-such-as-import-or-train-status)
    + `GET /api/v2/bot/prebuiltEntities` - [Get all Prebuilt Entities of a language](#get-all-prebuilt-entities-of-a-language)
    + `GET /api/v2/bot/settings` - [Get settings](#get-settings)

#### PrebuiltEntity
  PrebuiltEntity is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | integer  | yes | yes | name of the prebuilt entity |
  | `displayName` | integer  | yes | yes | display name of the prebuilt entity |
  | `description` | integer  | yes | yes | description of the prebuilt entity |
  | `example` | integer  | yes | yes |example of the prebuilt entity |

### General Related Object Json Format
#### NewBotRequest
  NewBotRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the New Bot Request |
  | `name` | string  | no | yes | name of the applier |
  | `email` | string  | no | yes | email of the applier |
  | `botName` | string  | no | yes | bot Name of the Requested bot |
  | `language` | string  | no | yes | bot language of the Requested bot |

#### MonthlyQuota
  MonthlyQuota is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `balance` | integer  | yes | yes | the current month quota balance of the site |
  | `comm100BotUsed` | integer  | yes | yes | the current month used quotas by comm100 bot of the site |
  | `thirdPartyBotUsed` | integer  | yes | yes | the current month used quotas by third-party bot of the site |

#### Language Object
  Language is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `code` | string  | yes | yes | the code of the Language |
  | `name` | string  | yes | yes | the name of the Language |

### General End Points
#### Upload file temporarily and the file will be deleted in 3 hours

  `POST /api/v2/bot/file`

##### Parameters

query parameters

  - `siteId ` 

request body parameters

  - `file ` -the file content. it is a list

##### Response
the response is:

  - `fileName` -the uploaded file full name

#### Upload image

  `POST /api/v2/bot/image`

##### Parameters
query parameters

- `siteId ` 

request body parameters

  - `file ` -the file content. it is a list

##### Response
the response is: [NameUrl](#nameurl) Object

#### Request to create a new bot

  `POST /api/v2/bot/newBotRequest`

##### Parameters
query parameters

  - `siteId ` 

request body parameters: [NewBotRequest](#newbotrequest) Object

#### Get if the site is enabled bot

  `GET /api/v2/bot/botEnabled`

##### Parameters
query parameters

  - `siteId ` 

##### Response
the response is: 
  `true` or `false`

#### Get the default avatar of bot

  `GET /api/v2/bot/defaultAvatar`

##### Parameters
query parameters

- `siteId ` 

##### Response
the response is:  [NameUrl](#nameurl) Object

#### Get used quotas and quota balance of a site

  `GET /api/v2/bot/quota`

##### Parameters
query parameters

  - `siteId ` 

##### Response
the response is: [MonthlyQuota](#monthlyquota) Object
    
#### Get all supported languages

  `GET /api/v2/bot/languages`

##### Parameters
no parameter

##### Response
the response is: list of [Language](#language-object) Objects

#### Get the operations such as import or train status

  `GET /api/v2/bot/operations/{id}`

##### Parameters
query parameters

- `siteId ` 

path parameters

  - `id`

##### Response
the response is:

when the status is `Wait `: Waiting for the task to begin

  - `status ` -enum values, `Wait `,`Succeeded `,`Failed `,`Processing `
  - `operationId `
  - `percent ` - it is a integer, progress of the import operation

when the status is `Processing `:

  - `status ` -enum values, `Wait `,`Succeeded `,`Failed `,`Processing `
  - `operationId `
  - `percent ` - it is a integer, progress of the import operation 

when the status is `Failed `:

  - `status ` -enum values, `Wait `,`Succeeded `,`Failed `,`Processing `
  - `failUrl ` 
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Wait `,`Succeeded `,`Failed `,`Processing `
  - `percent ` - it is a integer, progress of the import operation

#### Get all prebuilt entities of a language

  `GET /api/v2/bot/prebuiltEntities`

##### Parameters
query parameters

- `siteId ` 
- `languageCode`

##### Response
the response is: list of [Prebuilt Entity](#prebuiltentity) Objects    

##### Get settings
 
`GET /api/v2/bot/settings`
###### Parameters
 
query parameters

- `siteId ` 
- `languageCode` -string, the code of language.
- `type` -string, exp:smartTriggerOfflineMessage
 
####### Response
the response is:
- `message` -the message of settings

## Agent Bot Setting
  You need `Manage Agent Bot` permission to manage agent bot and customize the settings for a agent bot.
  - `Setting` - Agent Bot Setting
    + `GET /api/v2/agentBot/setting` - [Get setting of agent bot](#get-setting-of-a-agent-bot)
    + `POST /api/v2/agentBot/setting` - [Create a new setting for agent bot](#create-a-new-setting-for-agent-bot)
    + `PUT /api/v2/agentBot/setting` - [Update agent bot setting](#update-agent-bot-setting)

### Agent Bot Related Object Json Format

#### AgentBotSetting

  AgentBotSetting is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | no | yes | id of the agent bot |
  | `ifEnable` | boolean  | no | yes | agent bot enable flag |
  | `language` | string  | no | yes | type of the language,including `English`、`Simplified Chinese` |
  | `ifIncludeCannedMessage` | boolean  | no | no | suggestion source including canned message,`true` or `false` |
  | `ifIncludeKnowledgeBase` | boolean  | no | yes | suggestion source including knowledge base,`true` or `false` |
  | `ifIncludeAiChatBot` | boolean  | no | yes | suggestion source including ai bot,`true` or `false` |
  | `selectedKB` | array  | no | yes | id of knowledge base array |
  | `selectedAiChatBot` | integer  | no | no | id of ai bot array |
  | `highConfidenceScore` | integer  | no | no | display suggestions only when the score is higher than |
  | `maximumSuggestionNumber` | integer  | no | yes | display at most suggestions |
  | `ifAddSimilarQuestion` | boolean  | no | yes | visitor questions will not be added as similar questions when there are already more than 10 questions under a canned message or knowledge base article. |
  | `kbArticleMessage` | string  | no | yes | the message before knowledge base article link |
  | `ifAddUnrecognizedQuestions` | boolean  | no | yes | automatically add unrecognized visitor questions to Agent Assist Learning section |

#### Get setting of a agent bot

  `GET /api/v2/agentBot/setting`

##### Parameters

query parameters

  - No parameters

##### Response
the response is: [AgentBotSetting](#agentbotsetting) Object

#### Create a new setting for agent bot

  `POST /api/v2/agentBot/setting`

##### Parameters
query parameters

  - No parameters

request body parameters: [AgentBotSetting](#agentbotsetting) Object

##### Response
the response is: [AgentBotSetting](#agentbotsetting);

#### Update agent bot setting

  `PUT /api/v2/agentBot/setting`

##### Parameters
query parameters

 - No parameters 

request body parameters: [AgentBotSetting](#agentbotsetting) Object

##### Response
the response is: [AgentBotSetting](#agentbotsetting) Object


## Agent Bot Word Weight
You need `Manage Agent Bot` permission to manage Agent bot word weight.
  - `Word Weight` - Word Weight Manage
  +  `PUT /api/v2/agentBot/wordWeight` - [Update word weights by siteid](#update-agent-bot-word-weights)
  +  `GET /api/v2/agentBot/wordWeight` - [Get word weight by siteid](#get-word-weight-by-siteid)

### Word Weight Ojbect Json Format
#### Word Weight Object
Word Weight is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description   |
| - | - | :-: | :-: | - | 
| `word` | string  | no | yes | name of the Word weight |
|`weight`| integer | no | yes | weight of the Word weight.|

#### Update agent bot word weights

  `PUT /api/v2/agentBot/wordWeight`

##### Parameters
  path parameters

query parameters

- No parameters

  request body parameters

  - array of word weight [WrodWeight](#word-weight-object),required

##### Response
the response is:

  - Http Status Code `200`

#### Get word weight by siteid

  `GET /api/v2/agentBot/wordWeight`

##### Parameters

  path parameters

query parameters

- No parameters

##### Response
the response is:

  - array of word weight [WrodWeight](#word-weight-object),required

## Agent Bot Synonym
  - `Synonyms` - Synonyms Manage
    + `GET /api/v2/agentBot/synonyms` - [Get agent synonyms](#get-all-agent-synonyms)
    + `POST /api/v2/agentBot/synonyms` - [Create a new synonym](#create-a-new-synonym)
    + `PUT /api/v2/agentBot/synonyms/{id}` - [Update a synonym](#update-a-synonym)
    + `DELETE /api/v2/agentBot/synonyms/{id}` - [Remove a synonym](#remove-a-synonym)

### Synonym Objects Json Format
#### Synonym Object
  Synonym is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Synonym |
  | `keyword` | string  | no | yes | keyword of the Synonym |
  | `synonyms` | string  | no | yes | synonym of the Synonym |

#### Get all agent synonyms

  `GET /api/v2/agentBot/synonyms`

##### Parameters
path parameters
  
query parameters

- No parameters

##### Response
the response is: list of [Synonym](#synonym-object) Objects
  
#### Create a new synonym

  `POST /api/v2/agentBot/synonyms`

##### Parameters
query parameters

- No parameters

path parameters

request body parameters: [Synonym](#synonym-object) Object

##### Response
the response is: [Synonym](#synonym-object) Object

#### Update a synonym

  `PUT /api/v2/agentBot/synonyms/{id}`

##### Parameters
query parameters

- No parameters

path parameters

  - `id`

request body parameters: [Synonym](#synonym-object) Object

##### Response
the response is: [Synonym](#synonym-object) Object

#### Remove a synonym

  `DELETE /api/v2/agentBot/synonyms/{id}`

##### Parameters
query parameters

- No parameters

path parameters

  - `id ` 

##### Response
the response is: Http Status Code `200`

## Agent Bot Learing Question
  You need `Manage Agent Bot` permission to manage agent bot learning .
  - `Learning` - Learning Manage
    + `GET api/v2/agentBot/learningQuestions` - [Get learning questions by filters](#search-learning-questions-by-filters)
    + `POST api/v2/agentBot/learningQuestions` - [Create a new learning question](#create-a-new-learning-question)
    + `DELETE api/v2/agentBot/learningQuestions/{id}` - [Remove a learning question](#remove-a-learning-question)
    + `POST api/v2/agentBot/learningQuestions:batchCreate` - [Batch add learning questions](#batch-add-learning-questions)
    + `DELETE api/v2/agentBot/learningQuestions` - [Batch delete learning questions](#batch-delete-learning-questions)


### Learning Object Json Format
#### Agent Bot Learning Question
  Learning Question is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Learning |
  | `type` | string  | no | yes | enum value, `manual` and `unidentified` |
  | `question` | string  | no | yes | question of the Learning |
  | `agentResponse` | string  | no | yes | response of the Learning |
  | `suggestionType` | string  | no | yes | enum value, `cannedMessage`,`knowledgeBase` and `aiChatBot` |
  | `suggestionContent` | object  | no | yes | suggestion's content.<br/>when suggestion type is cannedMessage, it represents [CannedMessageContent](#canned-message-suggestion-content);<br/>when type is knowledgeBase ,it represents [KnowledgeBaseContent](#knowledge-base-suggestion-content);<br/>when type is aiChatBot, it represents [AiChatBotContent](#ai-chat-bot-suggestion-content). |
  | `score` | float  | no | yes | the score of the suggestion |

#### Canned Message Suggestion Content
  CannedMessageContent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Canned Message |
  | `title` | string  | no | yes | title of the Canned Message |
  | `content` | string  | no | yes | the content of the Canned Message |

#### Knowledge Base Suggestion Content
  KnowledgeBaseContent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the knowledge Base |
  | `articleId` | integer  | yes | no | articleId is the article of knowledge Base |
  | `title` | string  | no | yes | title of the article |

#### Ai Chat Bot Suggestion Content
  AiChatBotContent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Ai Bot |
  | `intentId` | integer  | yes | no | id of the intent |
  | `intentName` | string  | no | yes | name of the intent |

#### Search learning questions by filters

  `GET api/v2/agentBot/learningQuestions`

##### Parameters
query parameters
 
  - `timezone` 
  - `page` 
  - `pageSize` 
  - `dateRange`
  - `filterText` 
  - `minScore` 

##### Response
the response is: list of [Agent Bot Learning Question](#agent-bot-learning-question) Objects

#### Create a new learning question

  `POST api/v2/agentBot/learningQuestions`

#####  Parameters
query parameters

- `siteId `

path parameters

request body parameters: [Agent Bot Learning Question](#agent-bot-learning-question) Object

##### Response
the response is: [Agent Bot Learning Question](#agent-bot-learning-question) Object

#### Remove a learning question

  `DELETE api/v2/agentBot/learningQuestions/{id}`

##### Parameters

query parameters

- No parameters

path parameters

  - `id ` 

##### Response
the response is: Http Status Code `200`

#### Batch add learning questions

  `POST api/v2/agentBot/learningQuestions:batchCreate`

#####  Parameters
query parameters

- `siteId ` 

path parameters

request body parameters: list of [Agent Bot Learning Question](#agent-bot-learning-question) Object

##### Response
the response is: Http Status Code `200`

#### Batch delete learning questions

  `DELETE api/v2/agentBot/learningQuestions`

##### Parameters

query parameters

- No parameters

path parameters

request body parameters: list of the learning question id

##### Response
the response is: Http Status Code `200`

## Agent Bot Suggestion
  - `Agent Bot Suggestion` - Agent Bot Suggestion
    + `POST /api/v2/agentBot/questionSuggestions:query` -[Query question suggestions by agent bot](#query-question-suggestions-by-agent-bot)

### Agent Bot Suggestion Related Ojbect Json Format

#### Question
  Question is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | string  | no | yes | 
  | `question` | string  | no | yes | the question visitor asked. |

#### Suggestion

  Suggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `type` | string  | no | yes | enum value, `cannedMessage` ， `knowledgeBase`， `aiChatBot` |
  | `content` | object  | no | yes | suggestion's content.<br/>when type is cannedMessage, it represents [CannedMessageContent](#canned-message-suggestion-content);<br/>when type is knowledgeBase ,it represents [KnowledgeBaseContent](#knowledge-base-suggestion-content);<br/>when type is aiChatBot, it represents [AiChatBotContent](#ai-chat-bot-suggestion-content). |
  | `score` | float  | no | yes | the score of the suggestion |
 
#### QuestionSuggestion

  QuestionSuggestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | string  | no | yes | 
  | `question` | string  | no | yes | the question visitor asked. |
  | `ifMatch` | bool  | no | yes | if the suggestion score greater than highConfidenceScore then true, otherwise false |
  | `suggestions` | array | no | yes | array of [Suggestion](#suggestion) Object |

##### Query question suggestions by agent bot

  `POST /api/v2/agentBot/questionSuggestions:query`
 
###### Parameters
query parameters

- `siteId ` 

 path parameters

request body parameters

  - list of [Question](#question) Object

###### Response    

 - the response is: list of [QuestionSuggestion](#questionSuggestion) Object