  | Change Version | API Version | Change Notes | Change Date | Author |
  | - | - | - | - | - |
  | 3.0 | v1 | Bot Restful API | 2020-5-20 | Page | 

# Summary
  - Chatbot
    - [session](#session)

# Session
  - `POST /api/v3/bot/chatbots/{chatbotId}/sessions` - [Create session](#create-session)
  - `POST /api/v3/bot/sessions/{sessionId}:detectIntent` - [Detect intent](#detect-intent)
  - `POST /api/v3/bot/sessions/{sessionId}:submitAuthentication` -  [Submit Authentication](#Submit-Authentication)
  - `POST /api/v3/bot/sessions/{sessionId}:submitIVRKey` - [Submit IVRKey](#Submit-IVRKey)

## Related Object Json Format

#### ChatbotSession Object
  ChatbotSession Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  | `id` | Guid  | | sessionId |
  | `chatbotId` | Guid  | | chatbotId |
  | `channel` | string  | | e.g., `IVR` |
  | `message` |  [ChatbotMessage](#ChatbotMessage-Object) Object |  | message |
  | `context` | Object  |   | this data will be transferred to webhook |

#### ChatbotMessage Object
  ChatbotMessage Object is represented as simple flat JSON objects with the following keys:  

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  | `id` | Guid  |  | the unique id of the response |
  | `visitorQuestion` | string  |  | text |
  | `type` | string  |  | type of the response,including `greetingMessage`、 `highConfidenceAnswer`、`possibleAnswer`、`noAnswer`, `authenticationRequest` |
  | `content` | object |  | response's content. when type is `highConfidenceAnswer`, it represents [HighConfidenceAnswer](#HighConfidenceAnswer-object); when type is `possibleAnswer`,it represents [PossibleAnswer](#PossibleAnswer-object);when type is `noAnswer`,it represents [NoAnswer](#NoAnswer-object);when type is `greetingMessage`,it represents [GreetingMessage](#GreetingMessage-Object); when type is `authenticationRequest`, it represents [AuthenticationRequest](#AuthenticationRequest-Object);|

#### HighConfidenceAnswer Object

  HighConfidenceAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - |
  | `intentId` | Guid  | | id of the matched intent |
  | `intentName` | string  |  | name of the matched intent |
  | `score` | float  |  | the score of the intent matched, the value is beteween 0.0 and 100.0 |
  |`responses`| [ChatbotResponse](#Chatbot-Response-Object)[] |  | an array of [ChatbotResponse](#Chatbot-Response-Object) object. |

#### PossibleAnswer Object

  PossibleAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Default | Description |    
  | - | - | - | - | 
  | `intents` | [IntentScore](#IntentScore-object)[]  || an array of [IntentScore](#IntentScore-object)   | 
  |`message` | string | | Text of the Possible Answer message | 
  |`audio` | string |  | base64 string, convert the message text to speech |  

#### NoAnswer Object

  NoAnswer is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  | `intentId` | Guid  |  | id of the matched intent |
  | `intentName` | string  |   | name of the matched intent |
  | `score` | float  | | the score of the intent matched, the value is beteween 0.0 and 100.0 |
  |`message` | string |  | text of the No Answer message  |
  |`audio` | string |  | base64 string, convert the message text to speech |   

#### GreetingMessage Object
  GreetingMessage is represented as simple flat json objects with the following keys:

  |Name| Type | Default | Description     | 
  | - | - | :-: | - | 
  |`responses`| [ChatbotResponse](#Chatbot-Response-Object)[] | | an array of [ChatbotResponse](#Chatbot-Response-Object) object. |

#### AuthenticationRequest Object

  AuthenticationRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type  | Default | Description |    
  | - | - | :-: | - | 
  | `signInMessage` | string  |  | message of the sign in |
  |`audio` | string |  | base64 string, convert the signInMessage text to speech |   

#### Chatbot Response Object
  Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`type` | string || enums: `audio` ,`ivrMenu` ,`transferCall` . |
  | `content` | object | | response's content. when type is `audio`, it represents [Audio Response](#Audio-Response-Object);when type is `ivrMenu`, it represents [IVRMenu Response](#IVRMenu-Response-Object);when type is `transferCall`, it represents [TransferCall Response](#TransferCall-Response-Object); |

#### Audio Response Object
  Audio Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`text` | string |  | string  |
  |`audio` | string | | base64 string, convert the text to speech |  

#### IVRMenu Response Object
  IVRMenu Response is represented as simple flat json objects with the following keys:

  |Name| Type|  Default | Description     | 
  | - | - | :-: | - | 
  |`message` | string |  | The message sent to visitor before the options.This message will be transferred to IVR and read to visitor  |
  |`audio` | string |  | base64 string, convert the message text to speech  |  
  |`invalidInputActionRepeatTime` | Map |  | How many times will this IVR Menu repeat if there is invalid input   | 
  | `keys` | string[]  |  | The valid keys for visitor to choose options. the key contains: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `0`, `*`, `#`. Each key can only be used once in an IVR menu. Visitor can press the key to choose the option.  |

#### TransferCall Response Object
  TransferCall Response is represented as simple flat json objects with the following keys:

  |Name| Type| Default | Description     | 
  | - | - | :-: | - | 
  |`targetNumber` | string |  | phone number. |

#### IntentScore Object

  IntentScore is represented as simple flat JSON objects with the following keys:  

  | Name | Type |  Default | Description |    
  | - | - | - | - | 
  |`id` | Guid || id of the intent  | 
  |`name` | string | | name of the intent |  
  | `score` | float  |  | the score of the intent matched, value is between 0.0 and 100.0 |

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
  | `channel` | string  | yes | | e.g., `IVR` |
  | `id` | Guid | yes | |  id of the session, you must generate the unique sessionId  |
  | `context` | Map | no | | context data, this data will be transferred to webhook.example: you can assign authentication data or location data which your webhook will use  |

example:
```Json 
  {
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
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
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
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
    "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    },
    "message":{
      "id":"d3f5b968-ad51-42af-b759-64c0afc40b84",
      "visitorQuestion":"",
      "type":"greetingMessage",
      "content":{
        "responses":[
          {
            "type":"audio",
            "content": {
              "text":"Hi, I'm Peely, I'm glad to help you.",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
          },
          {
            "type":"audio",
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

The request body contains data with the follow structure: [DetectIntentRequest]

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `channel` | string  | yes | | e.g., `IVR` |
  | `textInput` | string  | no | | text, `textInput` and `audioInput` one of them is required |
  | `audioInput` | string  | no | | audio, when textInput have value then this is invalid. `textInput` and `audioInput` one of them is required |
  | `context` | Map | no | | context data, this data will be transferred to webhook. example: you can assign authentication data which your webhook will use |


example:
```Json 
  {
    "channel":"IVR",
    "audioInput": "UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA...",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
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
    "audioInput": "UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA...",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:detectIntent
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    },
    "message":{
      "id":"0d9f08d1-3fa6-4ce7-8118-e38e42551516",
      "visitorQuestion":"hello",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "503d70df-9715-40d6-8ea7-37fef9b348ff",
        "intentName": "Greeting",
        "score": 100,
        "responses":[
          {
            "type":"audio",
            "content": {
              "text":"Hello. It's nice to meet you! What can I do for you today?",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
        }]
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
  | `channel` | string  | yes | | e.g., `IVR` |
  | `authentication` | string  | yes | | authentication data |
  | `context` | Map | no | | context data, this data will be transferred to webhook. example: you can assign authentication data which your webhook will use |


example:
```Json 
  {
    "channel":"IVR",
    "authentication": "UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
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
    "authentication": "UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA...",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    }
  }' -X POST https://domain.comm100.com/api/v3/bot/sessions/f9928d68-92e6-4487-a2e8-8234fc9d1f48:submitAuthentication
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {    
    "channel":"IVR",
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    },
    "message":{
      "id":"0d9f08d1-3fa6-4ce7-8118-e38e42551516",
      "visitorQuestion":"",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "503d70df-9715-40d6-8ea7-37fef9b348ff",
        "intentName": "Greeting",
        "score": 100,
        "responses":[
          {
            "type":"audio",
            "content": {
              "text":"Hello. It's nice to meet you! What can I do for you today?",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
        }]
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
  | `channel` | string  | yes | | e.g.,  `IVR` |
  | `key` | string  | yes | | the key the caller pressed |
  | `context` | Map | no | | context data, this data will be transferred to webhook. example: you can assign authentication data or location data which your webhook will use |

example:
```Json 
  {
    "channel":"IVR",
    "key": "1",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
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
    "key": "1",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
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
    "chatbotId": "a9928d68-92e6-4487-a2e8-8234fc9d1f48",
    "context": {      
      "name":"Kart",
      "email":"kart@yahoo.com",
      "phone":"123-4355-212",
    },
    "message":{
      "id":"0d9f08d1-3fa6-4ce7-8118-e38e42551516",
      "visitorQuestion":"1",
      "type":"highConfidenceAnswer",
      "content":{
        "intentId": "503d70df-9715-40d6-8ea7-37fef9b348ff",
        "intentName": "Greeting",
        "score": 100,
        "responses":[
          {
            "type":"audio",
            "content": {
              "text":"Hello. It's nice to meet you! What can I do for you today?",
              "audio":"UklGRrj2AQBXQVZFZm10IBAAAAABAAEAwF0AAIC7AAACABAAZGF0YZT2AQA..."
            }
        }]
      }
    }    
  }
```