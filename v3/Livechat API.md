# Live Chat Restful API

Comm100 Live Chat API allows you to pull the raw livechat data from Comm100 Live Chat into your own systems.

| Change Version | API Version | Change note | Change Date | Author |
| - | - | - | - | - |
| 1.0 | v3 |  | 2020-02-17 | Grubby,Michael,Davy |

# Summary

- Live Chat
  - [settings](#settings)
    - [auto distribution](#auto-distribution)
    - [translation excluded word](#translation-excluded-word)
    - [dynamic campaign](#dynamic-campaign)
    - [mobile push](#mobile-push)
  - [customer segment](#customer-segment)
  - [live chat agent](#live-chat-agent)
  - [live chat visitor](#live-chat-visitor)
  - [session](#session)  
  - [chat](#chat)
  - [offline message](#offline-message)  
  - [campaign](#campaign)
    - [installation code](#installation-code)
    - [chat button](#chat-button)
    - [chat window](#chat-window)
    - [pre-chat](#pre-chat)
      - [campaign form field](#campaign-form-field)
    - [post chat](#post-chat)
      - [campaign form field](#campaign-form-field)
    - [offline message](#offline-message)
      - [campaign form field](#campaign-form-field)
    - [invitation](#invitation)
      - [manual invitation](#manual-invitation)
      - [auto invitation](#auto-invitation)
    - [agent wrap-up](#agent-wrap-up)
      - [campaign form field](#campaign-form-field)
    - [language](#language)
    - [routing](#routing)
      - [custom rule](#custom-rule)
    - [chatbot integration](#chatbot-integration)
    - [KB integration](#kb-integration)
  - [campaign form field](#campaign-form-field)
  - [ban](#ban)  
  - [conversion action](#conversion-action)
  - [secure form](#secure-form)
    - [secure form field](#secure-form-field)
  - [custom variable](#custom-variable)  
  - [webhook](#webhook)

# Settings

- `GET /api/v3/livechat/settings` - [Get settings of a site](#get-settings-of-a-site)
- `PUT /api/v3/livechat/settings` - [Update settings of a site](#update-settings-of-a-site)

## Settings Related Objects Json Format

### Settings Object

Customer Segment is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `siteId` |integer  || yes | no || id of the site which the configuration belongs to.|
| `isMultipleCampaignEnabled` |boolean || no | yes || whether multiple campaigns are enabled or not in the site.|
|`isAutoDistributionEnabled` |boolean || no | yes || whether auto distribution is enabled or not in the site.|
| `isCustomAwayStatusEnabled` |boolean || no | yes || whether custom away status is enabled or not in the site.|
| `isDepartmentEnabled` |boolean || no|  yes || whether department is enabled or not in the site.|
| `isAutoTranslationEnabled` |boolean || no | yes || whether auto translation is enabled or not in the site.|
| `isAudioAndVideoChatEnabled` |boolean || no | yes ||whether audio&video chat is enabled or not in the site.|
| `iscustomerSegmentEnabled` |boolean || no | yes ||whether customer segment chat is enabled or not in the site.|
| `isVisitorSSOtEnabled` |boolean || no | yes||whether vistor SSO is enabled or not in the site.|
| `isCreditCardMaskingEnabled` |boolean || no | yes ||whether Credit card masking is enabled or not in the site.|
| `isCustomVariablesEnabled` |boolean || no | yes||whether custom variables are enabled or not in the site.|
| `isSalesforceEnabled` |boolean || no | yes ||whether Salesforce integration is enabled or not in the site.|
| `isZendeskEnabled` |boolean || no | yes ||whether Zendesk integration is enabled or not in the site.|
| `isGoogleAnalyticsEnabled` |boolean || no | yes || whether Google Analytics integration is enabled or not in the site.|
| `isGotoMeetingEnabled` |boolean || no | yes || whether GotoMeeting integration is enabled or not in the site.|
| `isJoinmeEnabled` |boolean || no | yes || whether Joinme integration is enabled or not in the site.|
| `isCobrowsingEnabled` |boolean || no | yes || whether Cobrowsing feature is enabled or not in the site.|

## Endpoint

### Get settings of a site

  `GET /api/v3/livechat/settings`

#### Parameter

    No parameters

#### Response

the response is [Settings](#settings-object) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/settings
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "siteId": 6000000,
  "isMultipleCampaignEnabled": true,
  "isAutoDistributionEnabled": false,
  "isCustomAwayStatusEnabled": true,
  "isDepartmentEnabled": false,
  "isAutoTranslationEnabled": true,
  "isAudioAndVideoChatEnabled": false,
  "iscustomerSegmentEnabled": true,
  "isVisitorSSOtEnabled": false,
  "isCreditCardMaskingEnabled": true,
  "isCustomVariablesEnabled": true,
  "isSalesforceEnabled": false,
  "isZendeskEnabled": true,
  "isGoogleAnalyticsEnabled": true,
  "isGotoMeetingEnabled": true,
  "isJoinmeEnabled": true,
  "isCobrowsingEnabled":true
}
```

### Update settings of a site

  `PUT /api/v3/livechat/settings`

#### Parameters

Request body

  The request body contains data with the [Settings](#settings-object) Object structure

example:

```Json
{
    "siteId": 6000000,
    "isMultipleCampaignEnabled": true,
    "isAutoDistributionEnabled": false,
    "isCustomAwayStatusEnabled": true,
    "isDepartmentEnabled": false,
    "isAutoTranslationEnabled": true,
    "isAudioAndVideoChatEnabled": false,
    "iscustomerSegmentEnabled": true,
    "isVisitorSSOtEnabled": false,
    "isCreditCardMaskingEnabled": true,
    "isCustomVariablesEnabled": true,
    "isSalesforceEnabled": false,
    "isZendeskEnabled": true,
    "isGoogleAnalyticsEnabled": true,
    "isGotoMeetingEnabled": true,
    "isJoinmeEnabled": true,
    "isCobrowsingEnabled":true
}
```

#### Response

the response is [Settings](#settings-object) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '{
    "siteId": 6000000,
    "isMultipleCampaignEnabled": true,
    "isAutoDistributionEnabled": false,
    "isCustomAwayStatusEnabled": true,
    "isDepartmentEnabled": false,
    "isAutoTranslationEnabled": true,
    "isAudioAndVideoChatEnabled": false,
    "iscustomerSegmentEnabled": true,
    "isVisitorSSOtEnabled": false,
    "isCreditCardMaskingEnabled": true,
    "isCustomVariablesEnabled": true,
    "isSalesforceEnabled": false,
    "isZendeskEnabled": true,
    "isGoogleAnalyticsEnabled": true,
    "isGotoMeetingEnabled": true,
    "isJoinmeEnabled": true,
    "isCobrowsingEnabled":true
}' -X PUT https://domain.comm100.com/api/v3/livechat/settings
```

Response
```Json
HTTP/1.1 200 OK
{
  "siteId": 6000000,
  "isMultipleCampaignEnabled": true,
  "isAutoDistributionEnabled": false,
  "isCustomAwayStatusEnabled": true,
  "isDepartmentEnabled": false,
  "isAutoTranslationEnabled": true,
  "isAudioAndVideoChatEnabled": false,
  "iscustomerSegmentEnabled": true,
  "isVisitorSSOtEnabled": false,
  "isCreditCardMaskingEnabled": true,
  "isCustomVariablesEnabled": true,
  "isSalesforceEnabled": false,
  "isZendeskEnabled": true,
  "isGoogleAnalyticsEnabled": true,
  "isGotoMeetingEnabled": true,
  "isJoinmeEnabled": true,
  "isCobrowsingEnabled":true
}
```

# Auto Distribution

- `GET /api/v3/livechat/autoDistribution` - [Get auto distribution](#get-auto-distribution)
- `PUT /api/v3/livechat/autoDistribution` - [Update auto distribution](#update-auto-distribution)

## Auto Distribution Related Objects Json Format

### Auto Distribution Object

  Auto Distribution is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `autoDistributionMethod` | string || no | no | method of auto distribution, including `load banlancing` , `round robin` and `capability weighted` |
| `isLastChattedAgentPreferred` | boolean || no | no | whether last-chatted agent is preferred or not |
| `isLimitMaxConcurrentChatsForAllAgents` | boolean || no | no | whether to set the same maximum number of chats for all agents |
| `maxConcurrentChatsForAllAgents` | integer || no | no | maximum number of chats for all agents |
| `ifAutoAcceptChatWhenHavingAudioVideoChat` | boolean || no | no| whether to allocate chats to agents who are having audio or video chats |
| `ifAgentCanManuallyAcceptChatsAfterReachingMaxChatsLimit` | boolean || no | no | whether to allow agent to manually accept chat after reaching max chats limit in agent console |
| `departmentAutoDistributions` | [Department Auto Distribution](#department-auto-distribution-object)[] || no | no | auto distribution configuration for per department |
| `agentAutoDistributions` | [Agent Auto Distribution](#agent-auto-distribution-object)[] || no | no | auto distribution configuration for per agent |

### Department Auto Distribution Object

Department Auto Distribution Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `departmentId` | Guid ||  yes| no|| id of department |
| `isLastChattedAgentPreferred` | boolean||  no| no|  | whether last-chatted agent is preferred or not |
| `backupDepartmentId` | Guid ||  no| no|| id of backup department |

### Agent Auto Distribution Object

Agent Auto Distribution Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `agentId` | integer ||  yes| no|| id of agent |
| `ifAutoAcceptChat` | boolean||  no| no|| if agent can auto accept chat|
| `maxConcurrentChats` | boolean ||  no| no|| maximum concurrent chats, available when Is Chat Auto Accepted is true.|

## Endpoint

### Get Auto Distribution

  `GET /api/v3/livechat/autoDistribution`

#### Parameters

    No parameters

#### Response

the response is: [Auto Distribution](#auto-distribution-object) Object.

#### Example

Using curl:

```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/autoDistribution
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "autoDistributionMethod": "load balancing",
  "isLastChattedAgentPreferred": true,
  "isLimitMaxConcurrentChatsForAllAgents":true,
  "maxConcurrentChatsForAllAgents": 3,
  "ifAutoAcceptChatWhenHavingAudioVideoChat": true,
  "ifAgentCanManuallyAcceptChatsAfterReachingMaxChatsLimit": true,
  "departmentAutoDistributions":[
    {
      "departmentId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "isLastChattedAgentPreferred":"true",
      "backupDepartmentId":"2487fc9d-92e6-4487-a2e8-92e68d6892a7"
    },
    ...
  ],
  "agentAutoDistributions":[
    {
      "agentId":5,
      "ifAutoAcceptChat":true,
      "maxConcurrentChats":10
    }
  ]
}
```

### Update Auto Distribution

  `PUT /api/v3/livechat/autoDistribution`

#### Parameters

Request body

  The request body contains data with the [Auto Distribution](#auto-distribution-object) Object structure

example:
```Json
{
  "autoDistributionMethod": "load balancing",
  "isLastChattedAgentPreferred": true,
  "isLimitMaxConcurrentChatsForAllAgents":true,
  "maxConcurrentChatsForAllAgents": 3,
  "ifAutoAcceptChatWhenHavingAudioVideoChat": true,
  "ifAgentCanManuallyAcceptChatsAfterReachingMaxChatsLimit": true,
  "departmentAutoDistributions":[
    {
      "departmentId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "isLastChattedAgentPreferred":"true",
      "backupDepartmentId":"2487fc9d-92e6-4487-a2e8-92e68d6892a7"
    },
    ...
  ],
  "agentAutoDistributions":[
    {
      "agentId":5,
      "ifAutoAcceptChat":true,
      "maxConcurrentChats":10
    },
    ...
  ]
}
```

#### Response

the response is: [Auto Distribution](#auto-distribution-object) object.

#### Example

Using curl:

```shell
curl -H "Content-Type: application/json" -d '{
  "autoDistributionMethod": "load balancing",
  "isLastChattedAgentPreferred": true,
  "isLimitMaxConcurrentChatsForAllAgents":true,
  "maxConcurrentChatsForAllAgents": 3,
  "ifAutoAcceptChatWhenHavingAudioVideoChat": true,
  "ifAgentCanManuallyAcceptChatsAfterReachingMaxChatsLimit": true,
  "departmentAutoDistributions":[
    {
      "departmentId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "isLastChattedAgentPreferred":"true",
      "backupDepartmentId":"2487fc9d-92e6-4487-a2e8-92e68d6892a7"
    },
    ...
  ],
  "agentAutoDistributions":[
    {
      "agentId":5,
      "ifAutoAcceptChat":true,
      "maxConcurrentChats":10
    },
    ...
  ]
}' -X PUT https://domain.comm100.com/api/v3/livechat/autoDistribution
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "autoDistributionMethod": "load balancing",
  "isLastChattedAgentPreferred": true,
  "isLimitMaxConcurrentChatsForAllAgents":true,
  "maxConcurrentChatsForAllAgents": 3,
  "ifAutoAcceptChatWhenHavingAudioVideoChat": true,
  "ifAgentCanManuallyAcceptChatsAfterReachingMaxChatsLimit": true,
  "departmentAutoDistributions":[
    {
      "departmentId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "isLastChattedAgentPreferred":"true",
      "backupDepartmentId":"2487fc9d-92e6-4487-a2e8-92e68d6892a7"
    },
    ...
  ],
  "agentAutoDistributions":[
    {
      "agentId":5,
      "ifAutoAcceptChat":true,
      "maxConcurrentChats":10
    }
  ]
}
```

# Translation Excluded Word

- `GET /api/v3/livechat/translationExcludedWords` - [Get a list of translation excluded word](#get-a-list-of-translation-excluded-word)
- `PUT /api/v3/livechat/translationExcludedWords` - [Update a translation excluded word](#update-a-translation-excluded-word)

## Translation Excluded Word Related Objects Json Format

### Translation Excluded Word Object

Translation Excluded Word is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only| Mandatory| Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `excludedWords` |string[]  || no | yes || content of translation excluded word.

## Endpoints

### Get a list of translation excluded word

  `GET /api/v3/livechat/translationExcludedWords`

#### Parameters

    No parameters

#### Response

an array of [Translation Excluded Word](#translation-excluded-word) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/translationExcludedWords
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "excludedWords":[
    "Hello",
    "Hi"
  ]
}
```

### Update a translation excluded word

  `PUT /api/v3/livechat/translationExcludedWords/{id}`

#### Parameters

Request body

  The request body contains data with the [Translation Excluded Word](#translation-excluded-word) object structure

example:
```Json
{
  "excludedWords":[
    "Hello",
    "Hi"
  ]
}
```
#### Response

the response is [Translation Excluded Word](#translation-excluded-word) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '{
  "excludedWords":[
    "Hello",
    "Hi"
  ]
}' -X PUT https://domain.comm100.com/api/v3/livechat/translationExcludedWords/5587fc9d-92e6-4487-a2e8-92e68d6892c4
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "excludedWords":[
    "Hello",
    "Hi"
  ]
}

```

### Delete a translation excluded word

  `Delete /api/v3/livechat/translationExcludedWords/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of translation excluded word   |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```shell
curl -H -X DELETE https://domain.comm100.com/api/v3/livechat/translationExcludedWord/5587fc9d-92e6-4487-a2e8-92e68d6892c4
```

Response
```json
HTTP/1.1 204 No Content
```

# Customer Segment

- `GET /api/v3/livechat/customerSegments` - [Get a list of customer segments](#get-list-of-customer-segments)
- `GET /api/v3/livechat/customerSegments/{id}` - [Get a customer segment by id](#get-a-cusomer-segment-by-id)
- `POST /api/v3/livechat/customerSegments` - [Create a customer segment](#create-a-customer-segment)
- `PUT /api/v3/livechat/customerSegments/{id}` - [Update a customer segment](#update-a-info-customer-segment)
- `DELETE /api/v3/livechat/customerSegments/{id}` - [Delete a customer segment](#delete-a-customer-segment)

## Customer Segment Related Objects Json Format

### Customer Segment Object

Customer Segment is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only| Mandatory| Default | Description |
  | - | - | - | :-: | :-: | :-: | - |
  | `id` |Guid  || yes | no || id of the customer segment.
  | `name` |string  || no | yes || name of the customer segment.
  | `color` |string  || no | no |'339FD9'| color of the customer segment
  | `isEnabled` |boolean  || no | no |false| whether the customer segment is enabled or not.
  | `order` |int  || no | no |maximum order + 1 | order of the customer segment.
  | `description` |string  || no | no || description of the customer segment.
  | `conditionMetType` |string  || no | no |all| met type of condtion , including `all`,`any`,`logicalExpression`.
  | `logicalExpression` |string  || no | no || the logical expression for conditions.
  | `conditions` |[Live Chat Condition](#conditions-json-format)[]  || no | yes || an array of [Live Chat Condition](#live-chat-condition-object) object. |
  | `alertTo`| [Alert To](#alert-to)  || no | no | |an array of agent id or department Id|

### Alert To Segment Object

Alert To is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only| Mandatory| Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `departmentIds` |int[]  || no | no|| an array of department id.|
| `agentIds` |Guid[]  || no | no || an array of agent id.|

### Live Chat Condition object

Live Chat Condition is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only| Mandatory| Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `field` |String  | no | yes || the name of visitor field.
  | `Operator` |String  | no | yes || type of operator, including `is`,`isNot`,`contains`,`doesNotContain`,`isMoreThan`, `isNotMoreThan`, `isLessThan`, `isNotLessThan`, `regularExpression`
  | `value` |String  | no | yes || the value of a visitor field .
  | `order` |int  | no | no|maximum order + 1| the order of visitor field.

## Endpoint

### Get list of Customer Segments

  `GET /api/v3/livechat/customerSegments`

#### Parameters

    No parameters

#### Response

  an array of [Customer Segment](#customer-segment-object) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET  https://domain.comm100.com/api/v3/livechat/customerSegments
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name": "livechat15293908029",
    "color": "339FD9",
    "isEnabled": false,
    "order": 1,
    "description": "",
    "conditionMetType": "all",
    "logicalExpression": "",
    "conditions": [
      {
        "field": "CurrentPageUrl",
        "operator": "include",
        "value": "live",
        "order": 1
      }
    ],
    "alertTo":{
       "agentIds":[4,5],
       "departmentIds":[]
     }
  },
    ...
]
```

### Get a customer segment by id

  `GET /api/v3/livechat/customerSegments/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of customer segment   |

#### Response

the response is: [customer segment](#customer-segment-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/customerSegments/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "livechat15293908029",
  "color": "339FD9",
  "isEnable": false,
  "order": 1,
  "description": "",
  "conditionMetType": "all",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ],
  "alertTo":{
       "agentIds":[4,5],
       "departmentIds":[]
  }
}
```

### Create a customer segment

  `POST /api/v3/livechat/customerSegments`

#### Parameters

Request body

  The request body contains data with the [customer segment](#customer-segment) structure

example:
```Json
{
  "name": "livechat15293908029",
  "color": "339FD9",
  "isEnable": false,
  "order": 1,
  "description": "",
  "conditionMetType": "all",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ],
  "alertTo":{
       "agentIds":[4,5],
       "departmentIds":[]
  }
}
```

#### Response

the response is: [customer segment](#customer-segment-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '{
  "name": "livechat15293908029",
  "color": "339FD9",
  "isEnable": false,
  "order": 1,
  "description": "",
  "conditionMetType": "all",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ],
  "alertTo":{
       "agentIds":[4,5],
       "departmentIds":[]
  }
}' -X POST https://domain.comm100.com/api/v3/livechat/customerSegments
```

Response
```Json
HTTP/1.1 201 Created
Location: https://domain.comm100.com/api/v3/livechat/customerSegments/1487fc9d-92e6-4487-a2e8-92e68d6892e6
Content-Type:  application/json
{
  "name": "livechat15293908029",
  "color": "339FD9",
  "isEnable": false,
  "order": 1,
  "description": "",
  "conditionMetType": "all",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ],
  "alertTo":{
       "agentIds":[4,5],
       "departmentIds":[]
  }
}
```

### Update a customer segment

  `PUT /api/v3/livechat/customerSegments/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of the customer segment  |

#### Response

the response is: [customer segment](#customer-segment-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '{
  "name": "livechat15293908029",
  "color": "339FD9",
  "isEnable": false,
  "order": 1,
  "description": "",
  "conditionMetType": "all",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ],
  "alertTo":{
       "agentIds":[4,5],
       "departmentIds":[]
  }
}' -X PUT https://domain.comm100.com/api/v3/livechat/customerSegments
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "livechat15293908029",
  "color": "339FD9",
  "isEnable": false,
  "order": 1,
  "description": "",
  "conditionMetType": "all",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ],
  "alertTo":{
    "agentIds":[4,5],
    "departmentIds":[]
  }
}
```

### Delete a customer segment

 `DELETE /api/v3/livechat/customerSegments/{id}`

#### Parameter

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of customer segment   |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```shell
curl -X DELETE  https://domain.comm100.com/api/v3/livechat/customerSegments/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```json
HTTP/1.1 204 No Content
```

# Dynamic Campaign

- `GET /api/v3/livechat/dynamicCampaign` - [Get dynamic campaign](#get-dynamic-campaign) include campaign
- `PUT /api/v3/livechat/dynamicCampaign` - [Update dynamic campaign](#update-dynamic-campaign)

## Dynamic Campaign Related Objects Json Format

### Dynamic Campaign Object

Dynamic Campaign is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `defaultCampaignId` |Guid || no | no || id of the default campaign.|
| `defaultCampaign` |[Campaign](#campaign-object)  |yes| no | no || the default [Campaign](#campaign-object).|
| `dynamicCampaignRules` | [Dynamic Campaign Rule](#dynamic-campaign-rule-object)[] || no | no || this list of [Dynamic Campaign Rule](#dynamic-campaign-rule-object).|

### Dynamic Campaign Rule Object

Dynamic Campaign Rule is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `name` |string || no | yes || name of the dynamic campaign rule.|
| `isEnabled` |boolean || no | yes ||if this rule is enabled.|
| `conditionMetType` |String || no | yes ||including `all`, `any` and `logicalExpression`.|
| `logicalExpression` |String || no | no ||the logical expression for conditions.|
| `targetCampaignId` |integer || no | yes||the id of target [Campaign](#campaign-object).|
| `targetCampaign` |[Campaign](#campaign-object) |yes| no | no ||the target [Campaign](#campaign-object) object.|
| `conditions` |[Live Chat Condition](#live-chat-condition-object)[] || no | no ||an array of [Live Chat Condition](#live-chat-condition-object) object. .|
| `order` |integer|| no | yes ||the order of this rule|

## Endpoint

### Get dynamic campaign

  `GET /api/v3/livechat/dynamicCampaign`

#### Parameter

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `campaign`|

#### Response

the response is: [Dynamic Campaign](#dynamic-campaign-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/dynamicCampaign?include=Campaign
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "defaultCampaignId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "defaultCampaign": {
    "name":"default campaign",
    "description":""
  },
  "dynamicCampaignRules":
  [
    {
      "name": "default rule",
      "isEnabled": true,
      "conditionMetType": "all",
      "logicalExpression": "",
      "targetCampaignId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "targetCampaign":{
        "name":"default campaign",
        "description":""
      },
      "conditions":
      [
        {
          "id":"5687fc9d-92e6-4487-a2e8-92e68d6892d8",
          "field": "CurrentPageUrl",
          "operator": "include",
          "value": "live",
          "order": 1
        }
      ],
      "order":1
    }
  ]
}
```

### update dynamic campaign

  `PUT /api/v3/livechat/dynamicCampaign`

#### Parameter

Request body

  The request body contains data with the [Dynamic Campaign](#dynamic-campaign-object) Object structure

example:
```Json
{
  "defaultCampaignId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "dynamicCampaignRules":
  [
    {
      "name": "default rule",
      "isEnabled": true,
      "conditionMetType": "all",
      "logicalExpression": "",
      "targetCampaignId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "conditions":
      [
        {
          "id":"5687fc9d-92e6-4487-a2e8-92e68d6892d8",
          "field": "CurrentPageUrl",
          "operator": "include",
          "value": "live",
          "order": 1
        }
      ],
      "order":1
    }
  ]
}
```

#### Response

the response is: [Dynamic Campaign](#dynamic-campaign-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '
{
  "defaultCampaignId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "dynamicCampaignRules":
  [
    {
      "name": "default rule",
      "isEnabled": true,
      "conditionMetType": "all",
      "logicalExpression": "",
      "targetCampaignId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "conditions":
      [
        {
          "id":"5687fc9d-92e6-4487-a2e8-92e68d6892d8",
          "field": "CurrentPageUrl",
          "operator": "include",
          "value": "live",
          "order": 1
        }
      ],
      "order":1
    }
  ]
}' -X PUT https://domain.comm100.com/api/v3/livechat/dynamicCampaign
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "defaultCampaignId": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "defaultCampaign": {
    "name":"default campaign",
    "description":""
  },
  "dynamicCampaignRules":[
    {
      "name": "default rule",
      "isEnabled": true,
      "conditionMetType": "all",
      "logicalExpression": "",
      "targetCampaignId":"1487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "targetCampaign":{
        "name":"default campaign",
        "description":""
      }
    }
  ],
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    }
  ]
}
```

# Mobile Push

- `GET /api/v3/livechat/mobilePush` - [Get mobile push](#get-mobile-push)
- `PUT /api/v3/livechat/mobilePush` - [Update mobile push](#update-mobile-push)

## Related Object Json Format

### Mobile Push JSON Format

Mobile Push is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory| Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `iosType` | string |  | no | yes  | |type of ios |
| `iosProductionCertificateFileName` | string |  | no | yes | | name of ios prodution certicate file|
| `iosProductionCertificateFileData` | string |  | no | yes  | | data of ios prodution certicate file|
| `iosProductionCertificatePassword` | string |  | no | yes  | | password of ios prodution certicate|
| `iosDevelopmentCertificateFileName` | string |  | no | yes  | | name of ios development certicate file|
| `iosDevelopmentCertificateFileData` | string |  | no | yes  | | data of ios development certicate file|
| `iosDevelopmentCertificatePassword` | string |  | no | yes  | | password of ios development certicate|
| `iosApnsPayloadFormat` | string |  | no | yes  | | format of ios Apns payload|
| `iosThirdPartyURL` | string |  | no | yes  | | ios third party URL|
| `iosThirdPartyRequestHeaders` | string |  | no | yes  | | ios third party request headers|
| `androidType` | string |  | no |yes  | |type of android |
| `androidGcmAPIKey` | string |  | no | yes  | |android gcm API key|
| `androidGcmExtraData` | string |  | no| yes  | |android gcm extra data |
| `androidThirdPartyURL` | string |  | no | yes  | |android third party URL |
| `androidThirdPartyRequestHeaders` | string |  | no | yes | | android third party request headers|
| `androidThirdPartyRequestBody` | string |  | no | yes  | |android Third Party Request Body |

## Endpoint

### Get mobile push

`GET /api/v3/livechat/mobilePush`

#### Parameters

    No parameters

#### Response

the response is: [Mobile Push](#moble-push-object) Object.

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/mobilePush
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "iosType": "APNS",
  "iosProductionCertificateFileName": "",
  "iosProductionCertificateFileData": "",
  "iosProductionCertificatePassword": "",
  "iosDevelopmentCertificateFileName": "",
  "iosDevelopmentCertificateFileData": "",
  "iosDevelopmentCertificatePassword": "",
  "iosApnsPayloadFormat": "",
  "iosThirdPartyURL": "",
  "iosThirdPartyRequestHeaders": "",
  "androidType": "",
  "androidGcmAPIKey": "",
  "androidGcmExtraData": "",
  "androidThirdPartyURL": "",
  "androidThirdPartyRequestHeaders": "",
  "androidThirdPartyRequestBody": ""
}
```

### update mobile push

`POST /api/v3/livechat/mobilePush`

#### Parameters

Request body

  The request body contains data with the [Dynamic Campaign](#dynamic-campaign-object) Object structure

example:
```Json
{
  "iosType": "APNS",
  "iosProductionCertificateFileName": "",
  "iosProductionCertificateFileData": "",
  "iosProductionCertificatePassword": "",
  "iosDevelopmentCertificateFileName": "",
  "iosDevelopmentCertificateFileData": "",
  "iosDevelopmentCertificatePassword": "",
  "iosApnsPayloadFormat": "",
  "iosThirdPartyURL": "",
  "iosThirdPartyRequestHeaders": "",
  "androidType": "",
  "androidGcmAPIKey": "",
  "androidGcmExtraData": "",
  "androidThirdPartyURL": "",
  "androidThirdPartyRequestHeaders": "",
  "androidThirdPartyRequestBody": ""
}
```

#### Response

the response is: [Mobile Push](#moble-push-object) Object.

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "iosType": "APNS",
  "iosProductionCertificateFileName": "",
  "iosProductionCertificateFileData": "",
  "iosProductionCertificatePassword": "",
  "iosDevelopmentCertificateFileName": "",
  "iosDevelopmentCertificateFileData": "",
  "iosDevelopmentCertificatePassword": "",
  "iosApnsPayloadFormat": "",
  "iosThirdPartyURL": "",
  "iosThirdPartyRequestHeaders": "",
  "androidType": "",
  "androidGcmAPIKey": "",
  "androidGcmExtraData": "",
  "androidThirdPartyURL": "",
  "androidThirdPartyRequestHeaders": "",
  "androidThirdPartyRequestBody": "",
}' -X PUT https://domain.comm100.com/api/v3/livechat/mobilePush
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "iosType": "APNS",
  "iosProductionCertificateFileName": "",
  "iosProductionCertificateFileData": "",
  "iosProductionCertificatePassword": "",
  "iosDevelopmentCertificateFileName": "",
  "iosDevelopmentCertificateFileData": "",
  "iosDevelopmentCertificatePassword": "",
  "iosApnsPayloadFormat": "",
  "iosThirdPartyURL": "",
  "iosThirdPartyRequestHeaders": "",
  "androidType": "",
  "androidGcmAPIKey": "",
  "androidGcmExtraData": "",
  "androidThirdPartyURL": "",
  "androidThirdPartyRequestHeaders": "",
  "androidThirdPartyRequestBody": "",
}
```

# Live Chat Agent

- `GET /api/v3/livechat/agents` - [Get list of live chat agents](#get-list-of-live-chat-agents)
- `GET /api/v3/livechat/agents/{id}` - [Get a live chat agent by id](#get-a-live-chat-agent-by-id)  
- `PUT /api/v3/livechat/agents/{id}` - [Update a live chat agent](#update-a-live-chat-agent)  
  
## Related Object Json Format

### Live Chat Agent Object

agent is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only| Mandatory| Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | Guid |  |  yes| N/A | | id of the live chat agent. |
| `status` | String |  | no | yes | | status of the agent, including `online`, `away`, `offline` and custom away status defined by site. |
| `ongoingChats` | integer|  | yes | no | | total number of ongoing chats the agent has. |

## Endpoints

### Get list of live chat agents

`GET /api/v3/livechat/agents`

#### Parameters

    No parameters

#### Response

the response an array of [Live Chat Agent](#live-chat-agent-object) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/agents
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "status": "online",
    "ongoingChats": 50
  },
  ...
]
```

### Get an live chat agent by id

`GET /api/v3/livechat/agents/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of live chat agent   |

#### Response

the response is [Live Chat Agent](#live-chat-agent-object) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/agents/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "status": "online",
  "ongoingChats": 50
}
```

### Update a live chat agent

`POST /api/v3/livechat/agents/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of live chat agent   |

Request body

  The request body contains data with the [Live Chat Agent](#live-chat-agent-object) Object structure

example:
```Json
{
  "status": "online"
}
```

#### Response

the response is [Live Chat Agent](#live-chat-agent-object) object

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '{
  "name": "Grubby",
  "status": "online",
  "ongoingChats": 50
}' -X PUT https://domain.comm100.com/api/v3/livechat/agents/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "status": "online"
}
```

# Live Chat Visitor

- `GET /api/v3/livechat/visitors` - [Get list of live chat visitors](#get-list-of-live-chat-visitors)
- `GET /api/v3/livechat/visitors/{id}` - [Get a live chat visitor by id](#get-a-live-chat-visitor-by-id)  
- `PUT /api/v3/livechat/visitors/{id}` - [Update visitor custom variable](#update-visitor-custom-variable)  

## Related Object JSON Format

### Live Chat Visitor Object

online visitor is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | Guid |  |  yes| N/A | | id of the visitor. |
| `name` | name |  |  yes| N/A | | name of the visitor. |
| `email` | string |  | yes | N/A | | email of the visitor.|
| `status` | String|  | yes | N/A | |status of the visitor . |
| `pageViews` | integer|  | yes | N/A | |the total number of web pages the visitor viewed on your website. |
| `browser` | string|  | yes | N/A | |the browser the visitor is using. |
| `chats` | integer|  | yes | N/A | |the total times of chats a visitor has made on your website from the first time to present. |
| `city` | string|  | yes | N/A | |the city of the visitor. |
| `country` | string|  | yes | N/A | |the country of the visitor. |
| `currentBrowsing` | string|  | yes | N/A | |the page the visitor is currently looking at. |
| `customFields` | [Custom Field](#custom-field-object)[]|  | yes | N/A | |the values of custom fields entered by visitors in the pre-chat window. Operators can also update the value(s) during chat in Visitor Monitor.|
| `customVariableResults` | [Custom Variable result](#custom-variable-result-object)[]|  | yes | N/A | |the information of custom variables captured from the web page visitors viewed.|
| `departmentId` | Guid|  | yes | N/A ||the department the visitor selected in the pre-chat window. Operators can also update their value while chatting with visitors.. |
| `firstVisitTime` | datetime|  | yes | N/A | |the time the visitor first visited a web page pasted with Comm100 Live Chat code.|
| `flashVersion` | string|  | yes | N/A | |the flash version of the browser the visitor is using.|
| `ip` | string|  | yes | N/A | |the IP of the visitor.|
| `searchKeywords` | string|  | yes | N/A | |the keywords the visitor used to search for your website.|
| `landingPage` | string|  | yes | N/A | |the title and URL of the first page of your website the visitor visited.|
| `language` | string|  | yes | N/A | |the language the visitor is using.|
| `operatingSystem` | string|  | yes | N/A | |the operating system of the visitor's device.|
| `phone` | string|  | yes | N/A | |the phone of the visitor.|
| `productService` | string|  | yes | N/A | |the product/service the visitor selected in the pre-chat window. Operators can also update their value while chatting with visitors.|
| `referrerUrl` | string|  | yes | N/A | |the URL of the page from which a visitor comes to your website.|
| `screenResolution` | string|  | yes | N/A | |the screen resolution of the visitor's device.|
| `searchEngine` | string|  | yes | N/A | |the search engine the visitor used to search for your website.|
| `state` | string|  | yes | N/A | |the state of the visitor.|
| `timeZone` | string|  | yes | N/A | |the time zone of the visitor.|
| `visitTime` | string|  | yes | N/A | |the starting time when this visitor visits your website this time.|
| `visits` | string|  | yes | N/A | |the total times of visits a visitor has made on your website from the first time to present|


### Custom Field Object

Custom Field is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | Guid |  |  yes| no | | id of the custom field.|
| `name` | string |  |  yes| no | | name of the custom field.|
| `value` | string |  |  yes| no | | value of the custom field.|

### Custom Variable Result Object

Custom variable result is represented as simple flat JSON objects with the following keys: 

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `name` | string |  |  yes| no | | name of the custom variable.|
| `value` | string |  |  no| no | | value of the custom variable.|
| `url` | string |  | no| no | | url of the custom variable.|

## Endpoints

### Get list of live chat visitors

`GET /api/v3/livechat/visitors`

#### Parameters


Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `onlyChattingVisitor` | boolean | no  | false |  if only return the chatting visitor. |

#### Response

the response is: array of [Live Chat Visitor](#live-chat-visitor-object) Object.

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/visitors?onlyChattingVisitor=false
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
[
    {
      "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
      "pageViews": 1,
      "browser": "Firefox 67.0",
      "chats": 0,
      "city": "Changsha",
      "company": "",
      "country": "China",
      "currentBrowsing": "https://domain.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
      "customFields": null,
      "customVariableResults": [
        {
          "name": "justfortestupdate",
          "value": "text",
          "url": "bbbbb"
        }
      ],
      "department": "",
      "email": "",
      "first_visit_time": "2019-06-11T03:05:42.537Z",
      "flash_version": "",
      "ip": "218.76.52.108",
      "searchKeywords": "",
      "landing_page": "https://domain.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
      "language": "zh-CN",
      "name": "218.76.52.108",
      "operating_system": "Windows 10",
      "phone": "",
      "product_service": "",
      "referrer_url": "",
      "screen_resolution": "1920x1080",
      "search_engine": "",
      "state": "Hunan",
      "status": 3,
      "time_zone": "GMT +08:00",
      "visit_time": "2019-06-12T07:41:40.486Z",
      "visits": 4
  },
  ...
]
```

### Get a live chat visitor by id

`GET /api/v3/livechat/visitors/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of live chat visitor|

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `onlyChattingVisitor` | boolean | no  | false |  if only return the chatting visitor. |

#### Response

the response is: array of [Live Chat Visitor](#live-chat-visitor-object) Object.

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d?onlyChattingVisitor=false
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
  "pageViews": 1,
  "browser": "Firefox 67.0",
  "chats": 0,
  "city": "Changsha",
  "company": "",
  "country": "China",
  "currentBrowsing": "https://domain.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
  "customFields": null,
  "customVariableResults": [
    {
      "name": "justfortestupdate",
      "value": "text",
      "url": "bbbbb"
    }
  ],
  "department": "",
  "email": "",
  "first_visit_time": "2019-06-11T03:05:42.537Z",
  "flash_version": "",
  "ip": "218.76.52.108",
  "searchKeywords": "",
  "landing_page": "https://domain.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
  "language": "zh-CN",
  "name": "218.76.52.108",
  "operating_system": "Windows 10",
  "phone": "",
  "product_service": "",
  "referrer_url": "",
  "screen_resolution": "1920x1080",
  "search_engine": "",
  "state": "Hunan",
  "status": 3,
  "time_zone": "GMT +08:00",
  "visit_time": "2019-06-12T07:41:40.486Z",
  "visits": 4
}
```

### Update visitor custom variable

`PUT /api/v3/livechat/visitors/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of online visitor|

#### Response

the response is: array of [Live Chat Visitor](#live-chat-visitor-object) Object.

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
      "customVariableResults": [
        {
          "name": "justfortestupdate",
          "value": "text",
          "url": "bbbbb"
        }
      ]
  }' -X PUT https://domain.comm100.com/api/v3/livechat/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
  "pageViews": 1,
  "browser": "Firefox 67.0",
  "chats": 0,
  "city": "Changsha",
  "company": "",
  "country": "China",
  "currentBrowsing": "https://domain.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
  "customFields": null,
  "customVariableResults": [
    {
      "name": "justfortestupdate",
      "value": "text",
      "url": "bbbbb"
    }
  ],
  "department": "",
  "email": "",
  "first_visit_time": "2019-06-11T03:05:42.537Z",
  "flash_version": "",
  "ip": "218.76.52.108",
  "searchKeywords": "",
  "landing_page": "https://domain.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
  "language": "zh-CN",
  "name": "218.76.52.108",
  "operating_system": "Windows 10",
  "phone": "",
  "product_service": "",
  "referrer_url": "",
  "screen_resolution": "1920x1080",
  "search_engine": "",
  "state": "Hunan",
  "status": 3,
  "time_zone": "GMT +08:00",
  "visit_time": "2019-06-12T07:41:40.486Z",
  "visits": 4
}
```

# Session

- `GET /api/v3/livechat/sessions/{id}` - [Get a session by id](#get-a-session-by-id) include visitor, contact

## Related Object Json Format
### Session JSON format

 Session is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | string |  | yes | no | | id of the session. |
| `startTime` | datetime | | no | no |  | time of this session start. |
| `ip` | string |  | no | no | |  |
| `referrerURL` | string |  | no | no | | The rest part of URL will be abandoned if the URL is too long. |
| `searchEngine` | string |  | no | no | |  |
| `keywords` | string |  | no | no | |  |
| `browser` | string | | no | no | |  |
| `flashVersion` | string |  | no | no | |  |
| `language` | string |  | no | no | |  |
| `screenResolution` | string |  | no | no | |  |
| `operatingSystem` | integer |  | no | no | |  |
| `timeZone` | string |  | no | no | |  |
| `landingPageURL` | string |  | no | no | |  |
| `landingPageTitle` | string | | no | no | |  |
| `visitorId` | Guid | | no | no | | the id of the visitor |
| `visitor` | [Visitor](#visitor) | yes | no | no | | Available only when visitor is included  |
| `contactId` | Guid | | no | no | | the id of the contact  |
| `contact` | [Contact](#contact) | yes | no | no | | Available only when contact is included  |

## Endpoint

### Get a session by id

  `Get /api/v3/livechat/sessions/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the ban  |

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `visitor`, `contact` |

#### Response

the response is: [Session](#session-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/sessions/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e?include=visitor
```
Response
```json  
{
    "id": "f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "startTime": "2020-02-20T13:12:20Z",
    "ip": "192.168.0.201",
    "referrerURL": "",
    "searchEngine": "",
    "keywords": "",
    "browser": "Firefox",
    "flashVersion": "10.0",
    "language": "en",
    "screenResolution": "1920X1680",
    "operatingSystem": "Windows 10",
    "timeZone": "",
    "landingPageURL": "",
    "landingPageTitle": "",
    "visitorId": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
    "visitor": {  //include visitor
        "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
        "email": "test@comm100.com",
        "name": "test comm100",
        ...
    }
}
```

# Chat

- `GET /api/v3/livechat/chats` - [Get all chats](#get-all-chats)
- `GET /api/v3/livechat/chats/{id}` - [Get a chat by id](#get-a-chat-by-id)
- `DELETE /api/v3/livechat/chats/{id}` - [Delete a chat](#delete-a-chat)
- `DELETE /api/v3/livechat/chats` - [Batch Delete chats](#Batch-delete-chats)

## Related Object Json Format

### Chat Object

 Chat is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | Guid |  | no | no | | id of the chat. |
| `agentIds` | integer[] |  | no | no | | Maximum four agents can join a chat. |
| `agents` | [Agent](#agent-object)[] | yes | no | no | | Chatbot is a type of agent. |
| `startTime` | datetime | | no | no | |  |
| `endTime` | datetime | | no | no | |  |
| `ifQueued` | boolean | | no | no | |  |
| `ifAudioChatHappened` | boolean | | no | no | false |  |
| `ifVideoChatHappened` | boolean | | no | no | false |  |
| `messages` | [Chat Message](#Chat-Message-object)[] | | no | no |  | |
| `status` | string | | no | no |  | Including `normal`, `refused` and `missed`. |
| `requestingPageTitle` | string | | no | no |  |  |
| `requestingPageURL` | string | | no | no |  | |
| `source` | string | | no | no |  | Including `chatButton`, `autoInvitation` and `manualInvitation`. |
| `autoInvitationId` | Guid | | no | no |  | |
| `autoInvitation` | [Auto Invitation](#auto-invitation-object) | yes | no | no |  |  |
| `preChat` | [Chat Pre-Chat](#Chat-Pre-Chat-object) | yes | no | no |  |  |
| `postChat` | [Chat Post Chat](#Chat-Post-Chat-object) | yes | no | no |  |  |
| `agentWrapUp` | [Chat Agent wrap-up](#Chat-agent-wrap-up-object) | yes | no | no |  |  |
| `customVariable` | [Chat Custom Variable](#Chat-Custom-Variable-object) | yes | no | no |  |  |
| `requestedTime` | datetime | | no | no | | The time when the chat is requested. |
| `offlineMessage` | [Offline Message](#Offline-Message-JSON-format) | yes | no | no |  | The Offline Message submitted after the Visitor switches from Waiting for Chat. |
| `avgResponseTime` | float | | no | no | |  |
| `visitorMessagesCount` | integer | | no | no | 0 | The number of messages sent by Visitors. |
| `agentMessagesCount` | integer | | no | no | 0 | The number of messages sent by Agents. |
| `campaignId` | Guid | | no | no |  |  |
| `campaign` | [Campaign](#campaign) | yes | no | no |  |  |
| `lastMessageSentBy` | string | | no | no |  | Including `visitor`, `agent`, `chatbot` and `system`.  |
| `customerSegments` | [Customer Segment](#customer-segment)[] | | no | no |  | |
| `sessionId` | Guid | | no | no |  | id of session |
| `session` | [Session](#session) | yes | no | no |  |  the related [Session](#session) object|

### Chat Message Object

  Chat Message Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `type` | string | no  | no | | Including `system`, `visitor`, `agent`, `chatbot` and `note`. |
| `senderName` | string | no  | no | |  |
| `sentTime` | datetime | no  | no | |  |
| `content` | string | no  | no | | |
| `translatedMessage` | string | no  | no | |  |
| `attachment` | byte[] | no | no | |  | The attachment file data |
| `attachmentName` | string | no | no | |  | The attachment file name |

### Chat Pre-Chat Object

  Pre-Chat Window Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `socialMediaSource` | string | no  | no | |  Including `none` and `facebook`. |
| `socialProfileURL` | string | no  | no | |  |
| `name` | string | no  | no   | |  |
| `email` | string | no  | no | | |
| `phone` | string | no  | no   | |  |
| `company` | string | no  | no | | |
| `productService` | string | no  | no   | |  |
| `ticketID` | string | no  | no | | |
| `fieldValues` | [Field Value](#field-value-json-format)[] | no | no | |  |  |

### Chat Post Chat  Object

  Chat Post Chat Window Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `ratingGrade` | string | no | no | | Including `noRating`, `level1` , `level2` , `level3` , `level4` and `level5`. |
| `ratingComment` | string | no | no | | |
| `ratingTime` | datetime | no  | no | |  |
| `fieldValues` | [Field Value](#field-value-json-format)[] | no | no | |  |  |

### Chat Agent Wrap-Up Object

  Agent Wrap-Up Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `categories` | string[] | no | no | |   |
| `comment` | string | no | no | |   |
| `lastUpdatedTime` | datetime | no | no | |   |
| `lastUpdatedByAgentId` | Guid | no | no | |  Id of the agent. |
| `fieldValues` | [Field Value](#field-value-json-format)[] | no | no | |  |  |

### Chat Custom Variable Object

  Agent Wrap-Up Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `fieldValues` | [Field Value](#field-value-json-format)[] | no | no | |  |  |

## Endpoint

### Get all chats

  `Get /api/v3/livechat/chats`

#### Parameters

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `department`,`agent`, `campaign`, `chatbot`, `autoInvitation`, `session`. |
| `requestedTime` | datetime | no  | today | The time range of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`. |
| `timeZone` | string | no  | UTC |  Time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as `±hh:mm`. |
| `pageIndex` | integer | no  | 1 | The page index of query. |
| `pageSize` | integer | no  | 50 | Page size.  |
| `departmentId` | guid | no  |  | |
| `categoryId` | guid | no  |  | |
| `visitorId` | guid | no  |  | |
| `agentId` | integer | no  |  | |
| `keywords` | string | no  |  | |
| `conditions` | string | no  |  |  The condition list of inquiring the chat `conditions[0][field]=email&conditions[0][operate]=contains&conditions[0]` |

#### Response

The response body contains data with the follow structure:

| Name | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `totalCount` | integer | no | no | Total count of the list. |
| `previousPage` | string | no | no | Url of the previous page. |
| `nextPage` | string | no | no | Url of the next page. |
| `chats` | [Chat](#Chat-Object)[] | no | no |  |

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/chats?include=campaign,autoInvitation,session
```
Response
```json  

{
    "totalCount": 28,
    "previousPage": "",
    "nextPage": "https://domain.comm100.com/api/v3/livechat/chats?include=campaign,autoInvitation,session&pageIndex=2",
    "list": [
        {
            "id": "2BCB61DA-FC7D-67D8-43A5-5EB453B63231",
            "agentIds": [5],
            "startTime": "2019-01-05T07:17:08.89",
            "endTime": "2019-01-05T07:27:08.89",
            "ifQueued": false,
            "ifAudioChatHappened": false,
            "ifVideoChatHappened": false,
            "messages": [{
              "type": "agent",
              "senderName": "agent",
              "sentTime": "2019-01-05T07:17:09.89",
              "content": "test",
              "translatedMessage": "test",
              "attachment": [file binary data],
              "attachmentName": "comm100SDK.css"
            },
            ...
            ],
            "status": "normal",
            "requestingPageTitle":"",
            "requestingPageURL":"",
            "source":"autoInvitation",
            "autoInvitationId": "d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
            "autoInvitation": {
                //include autoInvitation
                "id":"d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
                "name": "autoTest",
                ...
            },
            "preChat": {
              "socialMediaSource": "none",
              "socialProfileURL": "",
              "name": "test",
              "email": "test@test.com",
              "phone": "11111111111",
              "company": "test",
              "productService": "test",
              "ticketID": "532DFB20-2A1C-BFC6-EEB5-46CACFE72EC2",
              "fieldValues": []
            },
            "postChat": {
              "ratingGrade": "noRating",
              "ratingComment": "",
              "ratingTime": "2019-01-05T07:17:09.89",
              "fieldValues": []
            },
            "agentWrapUp": {
              "categorys": [],
              "comment": "test",
              "lastUpdatedTime": "2019-01-05T07:17:09.89",
              "lastUpdatedBy": "9C93FC96-887B-4FC7-08A2-636A42D78CBE",
              "fieldValues": []
            },
            "customVariable": {
              "fieldValues": []
            },
            "requestedTime": "2019-01-05T07:17:07.89",
            "lastMessageSentBy": "agent",
            "offlineMessage": null,
            "avgResponseTime": 1.2,
            "visitorMessagesCount": 11,
            "agentMessagesCount": 16,
            "campaignId":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
            "campaign": {
                //include campaign
                "id":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
                "name": "testCampaign",
                ...
            },
            "customerSegments": [],
            "sessionId": "f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
            "session": {
                //include session
                "id":"f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
                "startTime": "2020-02-20T13:12:20Z",
                "ip": "192.168.0.201",
                "referrerURL": "",
                "searchEngine": "",
                "keywords": "",
                "browser": "Firefox",
                ...
            },
            "fieldValues": []
        },
        ...
    ]
}
```

### Get a chat by id

  `Get /api/v3/livechat/chats/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the chat. |

#### Response

the response is: [Chat](#Chat-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/chats/2BCB61DA-FC7D-67D8-43A5-5EB453B63231?include=campaign,autoInvitation,session
```
Response
```json  

{
  "id": "2BCB61DA-FC7D-67D8-43A5-5EB453B63231",
  "agentIds": [5],
  "startTime": "2019-01-05T07:17:08.89",
  "endTime": "2019-01-05T07:27:08.89",
  "ifQueued": false,
  "ifAudioChatHappened": false,
  "ifVideoChatHappened": false,
  "messages": [{
    "type": "agent",
    "senderName": "agent",
    "sentTime": "2019-01-05T07:17:09.89",
    "content": "test",
    "translatedMessage": "test",
    "attachment": [file binary data],
    "attachmentName": "comm100SDK.css"
  },
  ...
  ],
  "status": "normal",
  "requestingPageTitle":"",
  "requestingPageURL":"",
  "source":"autoInvitation",
  "autoInvitationId": "d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
  "autoInvitation": {
    //include autoInvitation
    "id":"d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "name": "autoTest",
    ...
  },
  "preChat": {
    "socialMediaSource": "none",
    "socialProfileURL": "",
    "name": "test",
    "email": "test@test.com",
    "phone": "11111111111",
    "company": "test",
    "productService": "test",
    "ticketID": "532DFB20-2A1C-BFC6-EEB5-46CACFE72EC2",
    "fieldValues": []
  },
  "postChat": {
    "ratingGrade": "noRating",
    "ratingComment": "",
    "ratingTime": "2019-01-05T07:17:09.89",
    "fieldValues": []
  },
  "agentWrapUp": {
    "categorys": [],
    "comment": "test",
    "lastUpdatedTime": "2019-01-05T07:17:09.89",
    "lastUpdatedBy": "9C93FC96-887B-4FC7-08A2-636A42D78CBE",
    "fieldValues": []
  },
  "customVariable": {
    "fieldValues": []
  },
  "requestedTime": "2019-01-05T07:17:07.89",
  "lastMessageSentBy": "agent",
  "offlineMessage": null,
  "avgResponseTime": 1.2,
  "visitorMessagesCount": 11,
  "agentMessagesCount": 16,
  "campaignId":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
  "campaign": {
    //include campaign
    "id":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "name": "testCampaign",
    ...
  },
  "customerSegments": [],
  "sessionId": "f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
  "session": {
    //include session
    "id":"f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "startTime": "2020-02-20T13:12:20Z",
    "ip": "192.168.0.201",
    "referrerURL": "",
    "searchEngine": "",
    "keywords": "",
    "browser": "Firefox",
    ...
  },
  "fieldValues": []
}
```

### Delete a chat

  `DELETE /api/v3/livechat/chats/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the chat |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/chats/2BCB61DA-FC7D-67D8-43A5-5EB453B63231
```
Response
```json
HTTP/1.1 204 No Content
```

### Batch Delete chats

  `DELETE /api/v3/livechat/chats`

#### Parameters

Request body
- an array of offline chat id

example:
```json
[
  "2BCB61DA-FC7D-67D8-43A5-5EB453B63231",
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
    "2BCB61DA-FC7D-67D8-43A5-5EB453B63231",
    "92e68d68-92e6-4487-a2e8-8234fc9d1f48",
    "44878d68-92e6-4487-a2e8-8234fc9d1f48"
  ]' -X DELETE https://domain.comm100.com/api/v3/livechat/chats
curl -X DELETE https://domain.comm100.com/api/v3/livechat/chats
```
Response
```json
HTTP/1.1 204 No Content
```

# Offline Message

- `GET /api/v3/livechat/offlineMessages` - [Get a list of offline messages](#get-a-list-of-offline-messages)
- `GET /api/v3/livechat/offlineMessages/{id}` - [Get an offline message by id](#get-an-offline-message-by-id)
- `DELETE /api/v3/livechat/offlineMessages/{id}` - [Delete an offline message by id](#delete-an-offline-message-by-id)
- `DELETE /api/v3/livechat/offlineMessages` - [Batch delete offline messages](#batch-delete-offline-messages)

## Related Object Json Format

### Offline Message JSON format

 Offline Message is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | string |  | yes | no | | id of the offline message. |
| `createdTime` | datetime | | no | no | | time of this offline message submitted. |
| `name` | string | | no | no |  | name of the visitor |
| `email` | string | | no | no |  | email of the visitor |
| `phone` | string | | no | no |  | phone of the visitor |
| `company` | string | | no | no |  | company of the visitor |
| `departmentId` | Guid | | no | no |  | The Department which the Offline Message belongs to |
| `department` | [Department](#department) | yes | no | no |  | Available only when department is included |
| `agentId` | integer | | no | no |  | The Agent whom the Offline Message belongs to |
| `agent` | [Agent](#agent) | yes | no | no |  | Available only when agent is included |
| `ticketId` | integer | | no | no |  |  |
| `subject` | string | | no | no |  | the subject of this offline message|
| `message` | string | | no | no | | the content of this offline message |
| `requestingPageTitle` | string | | no | no |  |  |
| `requestingPageURL` | string | | no | no |  |  |
| `source` | string | | no | no |  | including `chatButton` and `autoInvitation` |
| `autoInvitationId` | Guid | | no | no |  | Available when source is `autoInvitation` |
| `autoInvitation` | [Auto Invitation](#auto-invitation) | yes | no | no |  | Available only when autoInvitation is included |
| `campaignId` | Guid | | no | no |  | id of the campaign |
| `campaign` | [Campaign](#campaign) | yes | no | no |  | Available only when campaign is included |
| `sessionId` | Guid | | no | no |  | id of the session |
| `session` | [Session](#session) | yes | no | no |  | Available only when session is included |
| `customerSegments` | [Customer Segment](#customer-segment)[] | | no | no |  | an array of [Customer Segment](#customer-segment) |
| `fieldValues` | [Field Value](#field-value-json-format)[] | | no | no |  | values of custom fields entered by visitors in the offline message window. An array of [Field Value](#field-value-json-format). |
| `attachment` | byte[] | | no | no |  | the attachment file data |
| `attachmentName` | string | | no | no |  | the attachment file name |

### Field Value JSON format

 Field Value is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `fieldName` | string |  | no | no | |  |
| `value` | string | | no | no | |  |
| `url` | string | | no | no |  |  |

## Endpoint

### Get a list of offline messages

  `Get /api/v3/livechat/offlineMessages`

#### Parameters
Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `department`,`agent`, `campaign`,`autoInvitation`, `session` |
| `timeFrom` | datetime | no  | today |  the beginning of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`|
| `timeTo` | datetime | no  | today |  the end of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`|
| `timeZone` | string | no  | UTC |  time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as ±hh:mm.|
| `campaignId` | guid | no  |  | id of the campaign which the offline message |
| `departmentId` | guid | no  |  | id of the department which the offline message belongs to |
| `agentId` | integer | no  |  | id of the agent that this offline message belongs to |
| `visitorSegmentId` | guid | no  |  | id of the visitor segment which the visitor belongs to |
| `keywords` | string | no  |  | search subject or message by keywords |
| `pageIndex` | integer | no  | 1 | the page index of query |
| `pageSize` | integer | no  | 50 | page size  |

#### Response
The response body contains data with the follow structure:

| Name | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `totalCount` | integer | no | no | total count of the list. |
| `previousPage` | string | no | no | Url of the previous page. |
| `nextPage` | string | no | no | Url of the next page. |
| `list` | [Offline Message](#offline-message-json-format)[] | no | no | an array of [Offline Message](#offline-message-json-format) |

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/offlineMessages?include=department,agent,campaign,autoInvitation,session
```
Response
```json  

{
    "totalCount": 28,
    "previousPage": "",
    "nextPage": "https://domain.comm100.com/api/v3/livechat/offlineMessages?include=department,agent,campaign,autoInvitation,session&pageIndex=2",
    "list": [
        {
            "id": "a2317d24-bec0-43e5-aaf5-2eae29ce948f",
            "createdTime": "2019-01-05T07:17:08.89",
            "name": "allon",
            "email": "allon@comm100.com",
            "phone":"",
            "company":"",
            "departmentId":"2a317d24-bec0-43e5-aaf5-2eae29ce948f",
            "department": {
                //include department
                "id":"2a317d24-bec0-43e5-aaf5-2eae29ce948f",
                "name": "Sales",
                ...
            },
            "ticketId":0,
            "subject": "cccccccc",
            "message": "",
            "requestingPageTitle":"",
            "requestingPageURL":"",
            "source":"autoInvitation",
            "autoInvitationId": "d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
            "autoInvitation": {
                //include autoInvitation
                "id":"d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
                "name": "autoTest",
                ...
            },
            "campaignId":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
            "campaign":{
                //include campaign
                "id":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
                "name": "testCampaign",
                ...
            },
            "sessionId":"f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
            "session":{
                //include session
                "id":"f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
                "startTime": "2020-02-20T13:12:20Z",
                "ip": "192.168.0.201",
                "referrerURL": "",
                "searchEngine": "",
                "keywords": "",
                "browser": "Firefox",
                ...
            },
            "fieldValues": [],
            "customerSegments": [],
            "attachment": [file binary data],
            "attachmentName": "comm100SDK.css"
        },
        ...
    ]
}
```

### Get an offline message by id

  `Get /api/v3/livechat/offlineMessages/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the offline message  |

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `department`,`agent`, `campaign`,`autoInvitation`, `session` |

#### Response

the response is: [Offline Message](#offline-message-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/offlineMessages/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e?include=department,agent,campaign,autoInvitation, session
```
Response
```json  
{
    "id": "a2317d24-bec0-43e5-aaf5-2eae29ce948f",
    "createdTime": "2019-01-05T07:17:08.89",
    "name": "allon",
    "email": "allon@comm100.com",
    "phone":"",
    "company":"",
    "agentId":5,
    "agent": {
        //include agent
        "id":5,
        "name": "Sales",
        ...
    },
    "ticketId":0,
    "subject": "cccccccc",
    "message": "",
    "requestingPageTitle":"",
    "requestingPageURL":"",
    "source":"autoInvitation",
    "autoInvitationId": "d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "autoInvitation": {
        //include autoInvitation
        "id":"d245dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
        "name": "autoTest",
        ...
    },
    "campaignId":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "campaign":{
        //include campaign
        "id":"2d45dadd-a7c3-4b7b-ba1c-bc9eaea34f8e",
        "name": "testCampaign",
        ...
    },
    "sessionId":"f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "session":{
        //include session
        "id":"f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
        "startTime": "2020-02-20T13:12:20Z",
        "ip": "192.168.0.201",
        "referrerURL": "",
        "searchEngine": "",
        "keywords": "",
        "browser": "Firefox",
        ...
    },
    "fieldValues": [],
    "customerSegments": [],
    "attachment": [file binary data],
    "attachmentName": "comm100SDK.css"
}
```

### Delete an offline message by id

  `DELETE /api/v3/livechat/offlineMessages/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the offline message  |


#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/offlineMessages/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e
```
Response
```json
HTTP/1.1 204 No Content
```

### Batch delete offline messages

  `DELETE /api/v3/livechat/offlineMessages`

#### Parameters

Request body 
  - an array of offline message id

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
  ]' -X DELETE https://domain.comm100.com/api/v3/livechat/offlineMessages
```
Response
```json
HTTP/1.1 204 No Content
```

# Campaign

- `GET /api/v3/livechat/campaigns` - [Get all campaigns in site](#get-all-campaigns-in-site)
- `GET /api/v3/livechat/campaigns/{id}` - [Get a campaign by id](#get-a-campaign-by-id)
- `POST /api/v3/livechat/campaigns` - [Create a new campaign](#create-a-new-campaign)
- `PUT /api/v3/livechat/campaigns/{id}` - [Update a campaign](#update-a-campaign)
- `DELETE /api/v3/livechat/campaigns/{id}` - [Delete a campaign](#delete-a-campaign)

## Related Object Json Format

### Campaign Object

  Campaign Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
|`id` | Guid | yes | no | | Id of the current item.  |
| `name` | string  | no | yes | `Default Plan` | |
| `description` | string  | no | no | | |
| `language` | string | no | no | `English` | The languages are defined in cPanel.  |

## Campaign Endpoints

### Get all Campaigns in site

  `GET /api/v3/livechat/campaigns`

#### Parameters

    No parameters

#### Response

the response is: list of [Campaign](#Campaign-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
    {
        "id": "CE76FDBC-B451-F4C9-FE00-89360F86E9F9",
        "name": "campaigns",
        "description": "campaigns",
        "language": "English"
    },
    ...
]
```

### Get a Campaign by id

  `GET /api/v3/livechat/campaigns/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Campaign](#Campaign-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "CE76FDBC-B451-F4C9-FE00-89360F86E9F9",
  "name": "campaigns",
  "description": "campaigns",
  "language": "English"
}
```

### Create a new Campaign

  `POST /api/v3/livechat/campaigns`

#### Parameters

Request Body

  The request body contains data with the [Campaign](#Campaign-Object) structure

example:
```Json
{
  "name": "campaigns11111",
  "description": "campaigns",
  "language": "English"
}
```

#### Response

the response is: [Campaign](#Campaign-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "campaigns11111",
  "description": "campaigns",
  "language": "English"
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585

{
  "id": "FAE531BE-8CAD-207D-57B9-493BBCC6E585",
  "name": "campaigns11111",
  "description": "campaigns",
  "language": "English"
}
```

### Update a Campaign

  `PUT /api/v3/livechat/campaigns/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign](#Campaign-Object) structure

example:
```Json
{
  "name": "campaigns2222",
  "description": "campaigns",
  "language": "English"
}
```

#### Response

the response is: [Campaign](#Campaign-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "campaigns2222",
  "description": "campaigns",
  "language": "English"
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "FAE531BE-8CAD-207D-57B9-493BBCC6E585",
  "name": "campaigns2222",
  "description": "campaigns",
  "language": "English"
}
```

### Delete a Campaign

  `DELETE /api/v3/livechat/campaigns/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the campaign |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Installation Code

- `GET /api/v3/livechat/campaigns/{campaignId}/installationCode` - [Get installation code of a campaign](#get-installation-code-of-a-campaign)

## Related Object Json Format

### Installation Code Object

  Installation Code Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `code` | string  | no | no | | |

## Installation Code Endpoints

### Get installation code of a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/installationCode`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Installation Code](#Installation-Code-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/installationCode
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "code": "<!--Begin Tester Code-->
    <div id=\"livechat-button-1\"></div>
      <script type=\"text/javascript\">
        var Comm100API=Comm100API||{};(function(t){function e(e){var a=document.createElement(\"script\"),c=document.getElementsByTagName(\"script\")[0];a.type=\"text/javascript\",a.async=!0,a.src=e+t.site_id,c.parentNode.insertBefore(a,c)}t.chat_buttons=t.chat_buttons||[],t.chat_buttons.push({code_plan:1,div_id:\"livechat-button-1\"}),t.site_id=[SiteId],t.main_code_plan=1,e(\"  
        https://domain.comm100.com/chatserver/livechat.ashx?siteId=\"),setTimeout(function(){t.loaded||e(\"  
        https://domain.comm100.com/chatserver/livechat.ashx?siteId=\")},5e3)})(Comm100API||{})
      </script>
    <!--End Tester Code-->"
}
```

# Chat Button

- `GET /api/v3/livechat/campaigns/{campaignId}/chatButton` - [Get settings of ChatButton for a campaign](#get-chat-button)
- `PUT /api/v3/livechat/campaigns/{campaignId}/chatButton` - [Update settings of ChatButton for a campaign](#update-chat-button)

## Related Object Json Format

### Chat Button Object

  Chat Button Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `type` | string | no | no | `adaptive` | Type of the button, including `adaptive`, `image` and `textLink`. |
| `isHideWhenOffline` | boolean | no | no | | Whether the chat button is visible when no agent is online. `true` means that button is invisible. |
| `isDomainRestrictionEnabled` | boolean | no | no | | Whether the domain restriction is enabled or not. |
| `allowedDomains` | string[] | no | no | | An array of `domains` or `urls`, on which the chat button is visible. |
| `adaptiveButtonColor` | string | no | no | | The theme color of the chat button, available when `type` is `adaptive`. |
| `adaptiveButtonIconType` | integer | no | no | | Type of the chat button icon, including `1`, `2` , `3` and `4`, available when `type` is `adaptive`. |
| `adaptiveButtonOnlineIcon` | string | no | no | | Image file key of the chat online button, available when `type` is `adaptive`. |
| `adaptiveButtonOfflineIcon` | string | no | no | | Image file key of the chat offline button, available when `type` is `adaptive`. |
| `isImageButtonFloating` | boolean | no | no | | Whether the image button is float or not, available when `type` is `image`. |
| `imageButtonPosition` | string | no | no | | Position of the image button, including `centered`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available when `type` is `image`. |
| `imageButtonPositionMode` | string | no | no | | Position mode of the image button, including `Basic` and `Advanced`, available when `type` is `image`. |
| `isImageButtonXOffsetByPixel` | boolean | no | no | | Available when `type` is `image`. |
| `imageButtonXOffset` | integer | no | no | |  If Is XOffset By Pixel is True, it represents the offset pixel value of the X coordinate. If Is XOffset By Pixel is False, it represents the offset percentage value of the X coordinate, available when `type` is `image`. |
| `isImageButtonYOffsetByPixel` | boolean | no | no | | Available when `type` is `image`. |
| `imageButtonYOffset` | integer | no | no | |  If Is YOffset By Pixel is True, it represents the offset pixel value of the Y coordinate. If Is YOffset By Pixel is False, it represents the offset percentage value of the Y coordinate, available when `type` is `image`. |
| `imageButtonImageSource` | string | no | no | |  Type of the image source, including `fromGallery` and `fromMyComputer` |
| `imageButtonOnlineImage` | string | no | no | | Image file key of online button, available when `type` is `image`. |
| `imageButtonOfflineImage` | string | no | no | | Image file key of offline button, available when `type` is `image`. |
| `imageButtonTypeOnMobile` | string | no | no | | The type of button on mobile device, including `text` and `image`. |
| `imageButtonColorOnMobile` | string | no | no | | |
| `imageButtonTextColorOnMobile` | string | no | no | | The theme color of chatbutton on mobile device. |
| `imageButtonOnlineImageOnMobile` | string | no | no | | The Image file key on mobile device when any agents is online. |
| `imageButtonOfflineImageOnMobile` | string | no | no | | The image file key on mobile device when no agent is online. |
| `imageButtonPositionOnMobile` | string | no | no | | Position of the chat button on mobile device, including `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle`, `RightMiddle`, `leftBottom` and `rightBottom`. |
| `textLinkButtonText` | string | no | no | | the content of the text link, available when `type` is `textLink`. |

## Chat Button Endpoints

### Get Chat Button

  `GET /api/v3/livechat/campaigns/{campaignId}/chatButton`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Chat Button](#Chat-Button-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/chatButton
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "type": "image",
  "isHideWhenOffline":  false,
  "isDomainRestrictionEnabled": false,
  "allowedDomains": [],
  "adaptiveButtonColor": "#329fd9",
  "adaptiveButtonIconType": 1,
  "adaptiveButtonOnlineIcon": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "adaptiveButtonOfflineIcon": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isImageButtonFloating": false,
  "imageButtonPosition": "centered",
  "imageButtonPositionMode": "Basic",
  "isImageButtonXOffsetByPixel": false,
  "imageButtonXOffset": 10,
  "isImageButtonYOffsetByPixel": false,
  "imageButtonYOffset": 10,
  "imageButtonImageSource": "fromMyComputer",
  "imageButtonOnlineImage": "08A3ACFE-FD5C-1B46-FA40-86DBA3E110FF",
  "imageButtonOfflineImage": "2EF5F854-A5CC-972F-1DC7-6DEA8B50F63A",
  "imageButtonTypeOnMobile": "image",
  "imageButtonColorOnMobile": "#329fd9",
  "imageButtonTextColorOnMobile": "#329fd9",
  "imageButtonOnlineImageOnMobile": "ED1CDD86-57D8-E479-0B39-45089E9A77E8",
  "imageButtonOfflineImageOnMobile": "BC5CAA90-C7BB-5BEA-9811-D72AD73F2047",
  "imageButtonPositionOnMobile": "bottomLeft",
  "textLinkButtonText": "tset"
}
```

### Update Chat Button

  `PUT /api/v3/livechat/campaigns/{campaignId}/chatButton`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Chat Button](#Chat-Button-Object) structure

example:
```Json
{
  "type": "image",
  "isHideWhenOffline":  false,
  "isDomainRestrictionEnabled": false,
  "allowedDomains": [],
  "adaptiveButtonColor": "#329fd9",
  "adaptiveButtonIconType": 1,
  "adaptiveButtonOnlineIcon": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "adaptiveButtonOfflineIcon": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isImageButtonFloating": false,
  "imageButtonPosition": "centered",
  "imageButtonPositionMode": "Basic",
  "isImageButtonXOffsetByPixel": false,
  "imageButtonXOffset": 10,
  "isImageButtonYOffsetByPixel": false,
  "imageButtonYOffset": 10,
  "imageButtonImageSource": "fromMyComputer",
  "imageButtonOnlineImage": "08A3ACFE-FD5C-1B46-FA40-86DBA3E110FF",
  "imageButtonOfflineImage": "2EF5F854-A5CC-972F-1DC7-6DEA8B50F63A",
  "imageButtonTypeOnMobile": "image",
  "imageButtonColorOnMobile": "#329fd9",
  "imageButtonTextColorOnMobile": "#329fd9",
  "imageButtonOnlineImageOnMobile": "ED1CDD86-57D8-E479-0B39-45089E9A77E8",
  "imageButtonOfflineImageOnMobile": "BC5CAA90-C7BB-5BEA-9811-D72AD73F2047",
  "imageButtonPositionOnMobile": "bottomLeft",
  "textLinkButtonText": "tset111111"
}
```

#### Response

the response is: [Chat Button](#Chat-Button-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "type": "image",
  "isHideWhenOffline":  false,
  "isDomainRestrictionEnabled": false,
  "allowedDomains": [],
  "adaptiveButtonColor": "#329fd9",
  "adaptiveButtonIconType": 1,
  "adaptiveButtonOnlineIcon": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "adaptiveButtonOfflineIcon": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isImageButtonFloating": false,
  "imageButtonPosition": "centered",
  "imageButtonPositionMode": "Basic",
  "isImageButtonXOffsetByPixel": false,
  "imageButtonXOffset": 10,
  "isImageButtonYOffsetByPixel": false,
  "imageButtonYOffset": 10,
  "imageButtonImageSource": "fromMyComputer",
  "imageButtonOnlineImage": "08A3ACFE-FD5C-1B46-FA40-86DBA3E110FF",
  "imageButtonOfflineImage": "2EF5F854-A5CC-972F-1DC7-6DEA8B50F63A",
  "imageButtonTypeOnMobile": "image",
  "imageButtonColorOnMobile": "#329fd9",
  "imageButtonTextColorOnMobile": "#329fd9",
  "imageButtonOnlineImageOnMobile": "ED1CDD86-57D8-E479-0B39-45089E9A77E8",
  "imageButtonOfflineImageOnMobile": "BC5CAA90-C7BB-5BEA-9811-D72AD73F2047",
  "imageButtonPositionOnMobile": "bottomLeft",
  "textLinkButtonText": "tset111111"
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/chatButton
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "type": "image",
  "isHideWhenOffline":  false,
  "isDomainRestrictionEnabled": false,
  "allowedDomains": [],
  "adaptiveButtonColor": "#329fd9",
  "adaptiveButtonIconType": 1,
  "adaptiveButtonOnlineIcon": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "adaptiveButtonOfflineIcon": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isImageButtonFloating": false,
  "imageButtonPosition": "centered",
  "imageButtonPositionMode": "Basic",
  "isImageButtonXOffsetByPixel": false,
  "imageButtonXOffset": 10,
  "isImageButtonYOffsetByPixel": false,
  "imageButtonYOffset": 10,
  "imageButtonImageSource": "fromMyComputer",
  "imageButtonOnlineImage": "08A3ACFE-FD5C-1B46-FA40-86DBA3E110FF",
  "imageButtonOfflineImage": "2EF5F854-A5CC-972F-1DC7-6DEA8B50F63A",
  "imageButtonTypeOnMobile": "image",
  "imageButtonColorOnMobile": "#329fd9",
  "imageButtonTextColorOnMobile": "#329fd9",
  "imageButtonOnlineImageOnMobile": "ED1CDD86-57D8-E479-0B39-45089E9A77E8",
  "imageButtonOfflineImageOnMobile": "BC5CAA90-C7BB-5BEA-9811-D72AD73F2047",
  "imageButtonPositionOnMobile": "bottomLeft",
  "textLinkButtonText": "tset111111"
}
```

# Chat Window

- `GET /api/v3/livechat/campaigns/{campaignId}/chatWindow` - [Get settings of ChatWindow for a campaign](#get-chat-window)
- `PUT /api/v3/livechat/campaigns/{campaignId}/chatWindow` - [Update settings of ChatWindow for a campaign](#update-chat-window)

## Related Object Json Format

### Chat Window Object

  Chat Window Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `width` | integer | no | no | | |
| `height` | integer | no | no | | |
| `style` | string | no | no | |  Style of the window's theme, including `classic`, `circle` and `bubble`. |
| `color` | string | no | no | |  Color of the window's theme. |
| `type` | string | no | no | | Type of the chat window, including `embedded` and `popup`. |
| `headerType` | string | no | no | |  Type of the header, including `agentInfo`, `bannerImage` and `avatarAndLogo` when `style` is `classic`. |
| `isAvatarDisplayed` | boolean | no | no | | Whether the avatar of the agent is visible or not, available when  `headerType` is `agentInfo` or `avatarAndLogo`. |
| `isTitleDisplayed` | boolean | no | no | | Whether the title of the agent is visible or not, available when `headerType` is `agentInfo`. |
| `isBioDisplayed` | boolean | no | no | | Whether the bio of the agent is visible or not, available when `headerType` is `agentInfo`. |
| `isLogoDisplayed` | boolean | no | no | | Whether the logo is visible or not, available when `headerType` is `avatarAndLogo`. |
| `logo` | string | no | no | | Image file key of the logo. |
| `bannerImage` | string | no | no | | Image file key of the banner, available when `headerType` is `bannerImage`. |
| `isAvatarDisplayedWithMessage` | boolean | no | no   | | Whether the avatar of the agent is visible or not in the message body, available when `style` is `classic`or `simple`. |
| `isBackgroundDisplayed` | boolean | no | no | |  Whether the texture and picture of the background is visible or not in the message body, available when `style` is `classic`or `simple`. |
| `backgroundTexture` | string | no | no | | Including `style1`, `style2`, `style3`, `style4` and `style5`. |
| `customCSS` | string | no | no | | |
| `isTranscriptDownloadAllowed` | boolean | no | no | | Whether the visitor can download the chat transcript. |
| `isTranscriptPrintAllowed` | boolean | no | no | | Whether the visitor can print the chat transcript. |
| `isTranscriptSentToVisitors` | boolean | no | no | | Whether the transcript send to visitor. |
| `isTranscriptSentFromCurrentAgentEmail` | boolean | no | no | | Available when `isTranscriptDownloadAllowed` is true. |
| `fromEmailName` | string | no | no | |  The from name for sending transcript email, available when `isTranscriptSentFromCurrentAgentEmail` is true. |
| `fromEmailAddress` | string | no | no | |  The subject address for sending transcript email, available when `isTranscriptSentFromCurrentAgentEmail` is true. |
| `isSMTPServerCustomized` | boolean | no | no | | Whether use custome SMTP server. |
| `customSMTPServer` | [Custom SMTP Server](#Custom-SMTP-Server-Object) | no | no | | |
| `isSwitchToOfflineMessageAllow` | boolean | no | no | | Allow visitors to switch to Offline Message Window while waiting for chat. |
| `isFileSendAllow` | boolean | no | no | | Whether the agent can send file or not. |
| `ifMarkUnreadMessage` | boolean | no | no | | |
| `isAudioChatEnabled` | boolean | no | no | | Whether the agent can use audio chat. |
| `isVideoChatEnabled` | boolean | no | no | | Whether the agent can use video chat. |
| `isBrowserPopupNotificationEnabled` | boolean | no | no | | It is available for private server sites. For shared server clients, the push notification is disabled by default. |
| `ifEndChatWhenVisitorIsInactive` | boolean | no | no | | Automatically end chats if visitors don't respond in period of time. |
| `minutesOfVisitorInactivity` | integer | no | no | | |
| `isTranscriptSentForArchiving` | boolean | no | no | | |
| `receivingEmailAddressesForArchivingTranscripts` | string | no | no | | |
| `emailSubjectForArchivingTranscripts` | string | no | no | | |
| `greetingMessage` | string | no | no | | |
| `isCustomJSEnabled:` | boolean | no | no | | |
| `customJS` | string | no | no | | |

### Custom SMTP Server Object

  Custom SMTP Server Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `fromName` | string | no | no | | |
| `fromEmail` | string | no | no | | |
| `mailServer` | string | no | no | | |
| `port` | integer | no | no | | |
| `encryptedType` | string | no | no | | Including `none`, `SSL` and `TLS`. |
| `IsAuthenticationRequired` | boolean | no | no | | |
| `username` | string | no | no | | |
| `password` | string | no | no | | Return empty when get. |

## Chat Window Endpoints

### Get Chat Window

  `GET /api/v3/livechat/campaigns/{campaignId}/chatWindow`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Chat Window](#Chat-Window-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/chatWindow
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "width": 10,
  "height": 10,
  "style": "classic",
  "color": "#329fd9",
  "type": "popup",
  "isAvatarDisplayed":  false,
  "isTitleDisplayed": false,
  "isBioDisplayed":  false,
  "isLogoDisplayed": false,
  "logo": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "bannerImage": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isAvatarDisplayedWithMessage":  false,
  "isBackgroundDisplayed": false,
  "backgroundTexture": "style1",
  "customCSS": "",
  "isTranscriptDownloadAllowed":  false,
  "isTranscriptPrintAllowed": false,
  "isTranscriptSentToVisitors":  false,
  "isTranscriptSentFromCurrentAgentEmail": false,
  "fromEmailName": "",
  "fromEmailAddress": "",
  "isSMTPServerCustomized": false,
  "customSMTPServer": {
    "fromName": "",
    "fromEmail": "",
    "mailServer": "",
    "port": 80,
    "encryptedType": "none",
    "IsAuthenticationRequired": false,
    "username": "",
    "password": "",
  },
  "isSwitchToOfflineMessageAllow":  false,
  "isFileSendAllow": false,
  "ifMarkUnreadMessage":  false,
  "isAudioChatEnabled": false,
  "isVideoChatEnabled":  false,
  "isBrowserPopupNotificationEnabled": false,
  "ifEndChatWhenVisitorIsInactive":  false,
  "minutesOfVisitorInactivity": 1,
  "isTranscriptSentForArchiving": false,
  "receivingEmailAddressesForArchivingTranscripts": "",
  "emailSubjectForArchivingTranscripts": "",
  "greetingMessage": "",
  "isCustomJSEnabled": false,
  "customJS": ""
}
```

### Update Chat Window

  `PUT /api/v3/livechat/campaigns/{campaignId}/chatWindow`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Chat Window](#Chat-Window-Object) structure

example:
```Json
{
  "width": 10,
  "height": 10,
  "style": "classic",
  "color": "#4f527d",
  "type": "popup",
  "isAvatarDisplayed":  false,
  "isTitleDisplayed": false,
  "isBioDisplayed":  false,
  "isLogoDisplayed": false,
  "logo": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "bannerImage": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isAvatarDisplayedWithMessage":  false,
  "isBackgroundDisplayed": false,
  "backgroundTexture": "style1",
  "customCSS": "",
  "isTranscriptDownloadAllowed":  false,
  "isTranscriptPrintAllowed": false,
  "isTranscriptSentToVisitors":  false,
  "isTranscriptSentFromCurrentAgentEmail": false,
  "fromEmailName": "",
  "fromEmailAddress": "",
  "isSMTPServerCustomized": false,
  "customSMTPServer": {
    "fromName": "",
    "fromEmail": "",
    "mailServer": "",
    "port": 80,
    "encryptedType": "none",
    "IsAuthenticationRequired": false,
    "username": "",
    "password": "",
  },
  "isSwitchToOfflineMessageAllow":  false,
  "isFileSendAllow": false,
  "ifMarkUnreadMessage":  false,
  "isAudioChatEnabled": false,
  "isVideoChatEnabled":  false,
  "isBrowserPopupNotificationEnabled": false,
  "ifEndChatWhenVisitorIsInactive":  false,
  "minutesOfVisitorInactivity": 1,
  "isTranscriptSentForArchiving": false,
  "receivingEmailAddressesForArchivingTranscripts": "",
  "emailSubjectForArchivingTranscripts": "",
  "greetingMessage": "",
  "isCustomJSEnabled": false,
  "customJS": ""
}
```

#### Response

the response is: [Chat Window](#Chat-Window-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "width": 10,
  "height": 10,
  "style": "classic",
  "color": "#4f527d",
  "type": "popup",
  "isAvatarDisplayed":  false,
  "isTitleDisplayed": false,
  "isBioDisplayed":  false,
  "isLogoDisplayed": false,
  "logo": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "bannerImage": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isAvatarDisplayedWithMessage":  false,
  "isBackgroundDisplayed": false,
  "backgroundTexture": "style1",
  "customCSS": "",
  "isTranscriptDownloadAllowed":  false,
  "isTranscriptPrintAllowed": false,
  "isTranscriptSentToVisitors":  false,
  "isTranscriptSentFromCurrentAgentEmail": false,
  "fromEmailName": "",
  "fromEmailAddress": "",
  "isSMTPServerCustomized": false,
  "customSMTPServer": {
    "fromName": "",
    "fromEmail": "",
    "mailServer": "",
    "port": 80,
    "encryptedType": "none",
    "IsAuthenticationRequired": false,
    "username": "",
    "password": "",
  },
  "isSwitchToOfflineMessageAllow":  false,
  "isFileSendAllow": false,
  "ifMarkUnreadMessage":  false,
  "isAudioChatEnabled": false,
  "isVideoChatEnabled":  false,
  "isBrowserPopupNotificationEnabled": false,
  "ifEndChatWhenVisitorIsInactive":  false,
  "minutesOfVisitorInactivity": 1,
  "isTranscriptSentForArchiving": false,
  "receivingEmailAddressesForArchivingTranscripts": "",
  "emailSubjectForArchivingTranscripts": "",
  "greetingMessage": "",
  "isCustomJSEnabled": false,
  "customJS": ""
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/chatWindow
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "width": 10,
  "height": 10,
  "style": "classic",
  "color": "#4f527d",
  "type": "popup",
  "isAvatarDisplayed":  false,
  "isTitleDisplayed": false,
  "isBioDisplayed":  false,
  "isLogoDisplayed": false,
  "logo": "6FABEE8F-F5DB-C1DB-FAD2-154692BB0715",
  "bannerImage": "0892A3D3-C934-21AB-7499-A44D77C4E2F7",
  "isAvatarDisplayedWithMessage":  false,
  "isBackgroundDisplayed": false,
  "backgroundTexture": "style1",
  "customCSS": "",
  "isTranscriptDownloadAllowed":  false,
  "isTranscriptPrintAllowed": false,
  "isTranscriptSentToVisitors":  false,
  "isTranscriptSentFromCurrentAgentEmail": false,
  "fromEmailName": "",
  "fromEmailAddress": "",
  "isSMTPServerCustomized": false,
  "customSMTPServer": {
    "fromName": "",
    "fromEmail": "",
    "mailServer": "",
    "port": 80,
    "encryptedType": "none",
    "IsAuthenticationRequired": false,
    "username": "",
    "password": "",
  },
  "isSwitchToOfflineMessageAllow":  false,
  "isFileSendAllow": false,
  "ifMarkUnreadMessage":  false,
  "isAudioChatEnabled": false,
  "isVideoChatEnabled":  false,
  "isBrowserPopupNotificationEnabled": false,
  "ifEndChatWhenVisitorIsInactive":  false,
  "minutesOfVisitorInactivity": 1,
  "isTranscriptSentForArchiving": false,
  "receivingEmailAddressesForArchivingTranscripts": "",
  "emailSubjectForArchivingTranscripts": "",
  "greetingMessage": "",
  "isCustomJSEnabled": false,
  "customJS": ""
}
```

# Pre-Chat

- `GET /api/v3/livechat/campaigns/{campaignId}/preChat` - [Get settings of Pre-Chat for a campaign](#get-Pre-Chat)
- `PUT /api/v3/livechat/campaigns/{campaignId}/preChat` - [Update settings of Pre-Chat for a campaign](#update-Pre-Chat)

## Related Object Json Format

### Pre-Chat Object

  Pre-Chat Window Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `isEnable` | boolean | no | no | | Whether the pre-chat is enabled or not. |
| `isTeamNameDisplayed` | boolean | no | no | | Whether the team name is visible or not in the header. |
| `teamName` | string | no | no | | The team name displayed in the header. |
| `isAgentAvatarDisplayed` | boolean | no | no   | | Whether the avatar of the agent is visible or not in the header. |
| `greetingMessage` | string | no | no | | |
| `socialMediaLogin` | string | no | no | |  Including `none` and `facebook`. |
| `fields` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | no | no | | These System Fields are prebuilt and can’t be deleted: `name`, `email`, `phone`, `company`, `product service`, `department`, `ticket id`.  |
| `isVisitorInfoRecorded` | boolean | no | no | true | If remember visitor info collected from pre-chat form. |
| `formFieldLayoutStyle` | string | no | no | | Including `leftOfInput` and `aboveInput`. Available for Post Chat and Offline Message forms.  |

## Pre-Chat Endpoints

### Get Pre-Chat

  `GET /api/v3/livechat/campaigns/{campaignId}/preChat`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Pre-Chat](#Pre-Chat-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/preChat
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable":  false,
  "isTeamNameDisplayed": false,
  "teamName":  "team",
  "isAgentAvatarDisplayed": false,
  "greetingMessage": "",
  "socialMediaLogin": "none",
  "fields":  [
    {
      "id": "5062B231-E0D6-AFD3-2E72-4D143792DC03",
      "field": {
        "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
        "isSystem": false,
        "name": "teset",
        "type": "textBox",
        "options": [{
          "value": "test",
          "order": 1,
        },
        ...
        ],
        "leftText": "",
        "rightText": "",
        "optionGroups": [{
          "name": "test",
          "order": 1,
          "options":[]
        },
        ...
        ],
      },
      "isVisible": false,
      "isRequired": false,
      "order": 1,
      "ratingGrades": [{
        "grade": 1,
        "label": "",
        "isVisible": false
      },
      ...
      ]
    },
    ...
  ],
  "isVisitorInfoRecorded": false,
  "formFieldLayoutStyle": "leftofInput"
}
```

### Update Pre-Chat

  `PUT /api/v3/livechat/campaigns/{campaignId}/preChat`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Pre-Chat](#Pre-Chat-Object) structure

example:
```Json
{
  "isEnable":  true,
  "isTeamNameDisplayed": false,
  "teamName":  "team",
  "isAgentAvatarDisplayed": false,
  "greetingMessage": "",
  "socialMediaLogin": "none",
  "fields":  [],
  "isVisitorInfoRecorded": false,
  "formFieldLayoutStyle": "leftofInput"
}
```

#### Response

the response is: [Pre-Chat](#Pre-Chat-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable":  true,
  "isTeamNameDisplayed": false,
  "teamName":  "team",
  "isAgentAvatarDisplayed": false,
  "greetingMessage": "",
  "socialMediaLogin": "none",
  "fields":  [],
  "isVisitorInfoRecorded": false,
  "formFieldLayoutStyle": "leftofInput"
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/preChat
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable":  true,
  "isTeamNameDisplayed": false,
  "teamName":  "team",
  "isAgentAvatarDisplayed": false,
  "greetingMessage": "",
  "socialMediaLogin": "none",
  "fields":  [],
  "isVisitorInfoRecorded": false,
  "formFieldLayoutStyle": "leftofInput"
}
```

# Post Chat

- `GET /api/v3/livechat/campaigns/{campaignId}/postChat` - [Get settings of PostChat for a campaign](#get-Post-Chat)
- `PUT /api/v3/livechat/campaigns/{campaignId}/postChat` - [Update settings of PostChat for a campaign](#update-Post-Chat)

## Related Object Json Format

### Post Chat  Object

  Post Chat Window Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `isEnable` | boolean | no | no | | Whether the pot chat is enabled or not. |
| `fields` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | no | no | | These System Fields are prebuilt and can’t be deleted: `rating`, `rating comment`.  |
| `greetingMessage` | string | no | no | | |

## Post Chat Endpoints

### Get Post Chat

  `GET /api/v3/livechat/campaigns/{campaignId}/postChat`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Post Chat](#Post-Chat-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/postChat
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable":  false,
  "fields":  [],
  "greetingMessage": ""
}
```

### Update Post Chat

  `PUT /api/v3/livechat/campaigns/{campaignId}/postChat`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Post Chat](#Post-Chat-Object) structure

example:
```Json
{
  "isEnable":  true,
  "fields":  [],
  "greetingMessage": ""
}
```

#### Response

the response is: [Post Chat](#Post-Chat-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable":  true,
  "fields":  [],
  "greetingMessage": ""
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/postChat
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable":  true,
  "fields":  [],
  "greetingMessage": ""
}
```

# Campaign Offline Message

- `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage` - [Get settings of OfflineMessage for a campaign](#get-Campaign-Offline-Message)
- `PUT /api/v3/livechat/campaigns/{campaignId}/offlineMessage` - [Update settings of OfflineMessage for a campaign](#update-Campaign-Offline-Message)

## Related Object Json Format

### Campaign Offline Message Object

  Offline Message Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `type` | string | no | no | | Including `systemOfflineMessageWindow` and `customOfflineMessagePage`. |
| `customOfflineMessagePageURL` | string | no | no | | Available when Type is `customOfflineMessagePage`. |
| `ifOpenCustomOfflineMessagePageInNewWindow` | boolean | no | no | | Available when Type is `customOfflineMessagePage`. |
| `greetingMessage` | string | no | no | | |
| `emailOfflineMessageTo` | string | no | no | | Including `allAgents` and `customEmailAddresses`, available when routing rule is disabled. |
| `customEmailAddresses` | string | no | no | |  Available when routing rule is disabled.  |
| `fields` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | no | no | | These System Fields are prebuilt and can’t be deleted: `name`, `email`, `phone`, `company`, `product service`, `department`, `ticket id`.  |

## Campaign Offline Message Endpoints

### Get Campaign Offline Message

  `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Campaign Offline Message](#Campaign-Offline-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/offlineMessage
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "type": "systemOfflineMessageWindow",
  "customOfflineMessagePageURL": "",
  "ifOpenCustomOfflineMessagePageInNewWindow":  false,
  "greetingMessage": "",
  "emailOfflineMessageTo": "allAgents",
  "customEmailAddresses": "",
  "fields":  []
}
```

### Update Campaign Offline Message

  `PUT /api/v3/livechat/campaigns/{campaignId}/offlineMessage`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Offline Message](#Campaign-Offline-Message-Object) structure

example:
```Json
{
  "type": "systemOfflineMessageWindow",
  "customOfflineMessagePageURL": "",
  "ifOpenCustomOfflineMessagePageInNewWindow":  false,
  "greetingMessage": "",
  "emailOfflineMessageTo": "allAgents",
  "customEmailAddresses": "",
  "fields":  []
}
```

#### Response

the response is: [Campaign Offline Message](#Campaign-Offline-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "type": "systemOfflineMessageWindow",
  "customOfflineMessagePageURL": "",
  "ifOpenCustomOfflineMessagePageInNewWindow":  false,
  "greetingMessage": "",
  "emailOfflineMessageTo": "allAgents",
  "customEmailAddresses": "",
  "fields":  []
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/offlineMessage
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "type": "systemOfflineMessageWindow",
  "customOfflineMessagePageURL": "",
  "ifOpenCustomOfflineMessagePageInNewWindow":  false,
  "greetingMessage": "",
  "emailOfflineMessageTo": "allAgents",
  "customEmailAddresses": "",
  "fields":  []
}
```

# Invitation

- `GET /api/v3/livechat/campaigns/{campaignId}/invitation` - [Get settings of invitation  for a campaign](#get-Invitation)
- `PUT /api/v3/livechat/campaigns/{campaignId}/invitation` - [Update settings of invitation  for a campaign](#update-Invitation)

## Related Object Json Format

### Invitation Object

  Invitation Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `id` | Guid | yes | no | | Id of the current item. |
| `style` | string | no | no | | Including `bubble`, `popup` and `chatWindow`. |
| `autoInvitations` | [Auto Invitation](#Auto-Invitation-Object)[] | no | no | | |
| `manualInvitations` | [Manual Invitation](#Manual-Invitation-Object)[] //不对吧,手动邀请只有一个| no | no | | |

### Manual Invitation Object

  Manual Invitation Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `manualInvitationPosition` | string | no | no | | Including `centerWithOverlay`, `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available When using `popup` Invitation Style.  |
| `manualInvitationImageType` | string | no | no | | Including`fromGallery` and `fromMyComputer`.  |
| `manualInvitationImage` | string | no | no | | Image file key of Invitation.  |
| `manualInvitationCloseAreaXOffset` | integer | no | no | | |
| `manualInvitationCloseAreaYOffset` | integer | no | no | | |
| `manualInvitationCloseAreaWidth` | integer | no | no | | |
| `manualInvitationCloseAreaHeight` | integer | no | no | | |
| `manualInvitationTextAreaXOffset` | integer | no | no | | |
| `manualInvitationTextAreaYOffset` | integer | no | no | | |
| `manualInvitationTextAreaWidth` | integer | no | no | | |
| `manualInvitationTextAreaHeight` | integer | no | no | | |
| `manualInvitationText` | string | no | no | | |
| `manualInvitationTextFont` | string | no | no | | Including `timesNewRoman`, `tahoma`, `verdana`, `arial`, `comicSansMs` and `courier`. |
| `manualInvitationTextSize` | string | no | no | | Including `XXSmall`, `XSmall`, `small`, `medium`, `large`, `XLarge` and `XXLarge`. |
| `isManualInvitationTextBold` | boolean | no | no | | |
| `isManualInvitationTextItalic` | boolean | no | no | | |
| `manualInvitationTextColor` | string | no | no | | |

### Auto Invitation Object

  Auto Invitation Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `id` | Guid | yes | no | | Id of the current item. |
| `name` | string | no | yes | | |
| `isEnable` | boolean | no | no | | Whether the auto invitation is enabled or not. |
| `isDisplayedOnceInOneSession` | boolean | no | no | | |
| `order` | integer | no | no | | |
| `imageType` | string | no | no | | Including`fromGallery` and `fromMyComputer`. |
| `closeAreaXOffset` | integer | no | no | | |
| `closeAreaYOffset` | integer | no | no | | |
| `closeAreaWidth` | integer | no | no | | |
| `closeAreaHeight` | integer | no | no | | |
| `textAreaXOffset` | integer | no | no | | |
| `textAreaYOffset` | integer | no | no | | |
| `textAreaWidth` | integer | no | no | | |
| `textAreaHeight` | integer | no | no | | |
| `text` | string | no | no | | |
| `textFont` | string | no | no | | Including `timesNewRoman`, `tahoma`, `verdana`, `arial`, `comicSansMs` and `courier`. |
| `textSize` | string | no | no | | Including `XXSmall`, `XSmall`, `small`, `medium`, `large`, `XLarge` and `XXLarge`. |
| `isTextBold` | boolean | no | no | | |
| `isTextItalic` | boolean | no | no | | |
| `textColor` | string | no | no | | |
| `position` | string | no | no | | Including `centerWithOverlay`, `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`.  |
| `conditionMetType` | string | no | no | | Including `all`, `any` and `logicalExpression`. |
| `logicalExpression` | string | no | no | | |
| `conditions` | [Live Chat Condition](#Live-Chat-Condition-Object)[] | no | no | | an array of [Live Chat Condition](#live-chat-condition-object) object. |

## Invitation Endpoints

### Get Invitation

  `GET /api/v3/livechat/campaigns/{campaignId}/invitation`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Invitation](#Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/invitation
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "style": "bubble",
  "manualInvitation": {
    "manualInvitationPosition": "centerWithOverlay",
    "manualInvitationImageType": "fromGallery",
    "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
    "manualInvitationCloseAreaXOffset": 10,
    "manualInvitationCloseAreaYOffset": 10,
    "manualInvitationCloseAreaWidth": 10,
    "manualInvitationCloseAreaHeight": 10,
    "manualInvitationTextAreaXOffset": 10,
    "manualInvitationTextAreaYOffset": 10,
    "manualInvitationTextAreaWidth": 10,
    "manualInvitationTextAreaHeight": 10,
    "manualInvitationText": "",
    "manualInvitationTextFont": "timesNewRoman",
    "manualInvitationTextSize": "XXSmall",
    "isManualInvitationTextBold": false,
    "isManualInvitationTextItalic": false,
    "manualInvitationTextColor": "#339FD9"
  },
  "autoInvitations": [{
    "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
    "name": "test",
    "isEnable": false,
    "isDisplayedOnceInOneSession": false,
    "order": 1,
    "imageType": "fromGallery",
    "closeAreaXOffset": 10,
    "closeAreaYOffset": 10,
    "closeAreaWidth": 10,
    "closeAreaHeight": 10,
    "textAreaXOffset": 10,
    "textAreaYOffset": 10,
    "textAreaWidth": 10,
    "textAreaHeight": 10,
    "text": "",
    "textFont": "timesNewRoman",
    "textSize": "XXSmall",
    "isTextBold": false,
    "isTextItalic": false,
    "textColor": "#339FD9",
    "position": "centerWithOverlay",
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  },
  ...
  ]
}
```

### Update Invitation

  `PUT /api/v3/livechat/campaigns/{campaignId}/invitation`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Invitation](#Invitation-Object) structure

example:
```Json
{
  "style": "bubble",
  "manualInvitation": {
    "manualInvitationPosition": "centerWithOverlay",
    "manualInvitationImageType": "fromGallery",
    "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
    "manualInvitationCloseAreaXOffset": 10,
    "manualInvitationCloseAreaYOffset": 10,
    "manualInvitationCloseAreaWidth": 10,
    "manualInvitationCloseAreaHeight": 10,
    "manualInvitationTextAreaXOffset": 10,
    "manualInvitationTextAreaYOffset": 10,
    "manualInvitationTextAreaWidth": 10,
    "manualInvitationTextAreaHeight": 10,
    "manualInvitationText": "",
    "manualInvitationTextFont": "timesNewRoman",
    "manualInvitationTextSize": "XXSmall",
    "isManualInvitationTextBold": false,
    "isManualInvitationTextItalic": false,
    "manualInvitationTextColor": "#339FD9"
  },
  "autoInvitations": [{
    "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
    "name": "test",
    "isEnable": false,
    "isDisplayedOnceInOneSession": false,
    "order": 1,
    "imageType": "fromGallery",
    "closeAreaXOffset": 10,
    "closeAreaYOffset": 10,
    "closeAreaWidth": 10,
    "closeAreaHeight": 10,
    "textAreaXOffset": 10,
    "textAreaYOffset": 10,
    "textAreaWidth": 10,
    "textAreaHeight": 10,
    "text": "",
    "textFont": "timesNewRoman",
    "textSize": "XXSmall",
    "isTextBold": false,
    "isTextItalic": false,
    "textColor": "#339FD9",
    "position": "centerWithOverlay",
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  }]
}
```

#### Response

the response is: [Invitation](#Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "style": "bubble",
  "manualInvitation": {
    "manualInvitationPosition": "centerWithOverlay",
    "manualInvitationImageType": "fromGallery",
    "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
    "manualInvitationCloseAreaXOffset": 10,
    "manualInvitationCloseAreaYOffset": 10,
    "manualInvitationCloseAreaWidth": 10,
    "manualInvitationCloseAreaHeight": 10,
    "manualInvitationTextAreaXOffset": 10,
    "manualInvitationTextAreaYOffset": 10,
    "manualInvitationTextAreaWidth": 10,
    "manualInvitationTextAreaHeight": 10,
    "manualInvitationText": "",
    "manualInvitationTextFont": "timesNewRoman",
    "manualInvitationTextSize": "XXSmall",
    "isManualInvitationTextBold": false,
    "isManualInvitationTextItalic": false,
    "manualInvitationTextColor": "#339FD9"
  },
  "autoInvitations": [{
    "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
    "name": "test",
    "isEnable": false,
    "isDisplayedOnceInOneSession": false,
    "order": 1,
    "imageType": "fromGallery",
    "closeAreaXOffset": 10,
    "closeAreaYOffset": 10,
    "closeAreaWidth": 10,
    "closeAreaHeight": 10,
    "textAreaXOffset": 10,
    "textAreaYOffset": 10,
    "textAreaWidth": 10,
    "textAreaHeight": 10,
    "text": "",
    "textFont": "timesNewRoman",
    "textSize": "XXSmall",
    "isTextBold": false,
    "isTextItalic": false,
    "textColor": "#339FD9",
    "position": "centerWithOverlay",
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  }]
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/invitation
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "style": "bubble",
  "manualInvitation": {
    "manualInvitationPosition": "centerWithOverlay",
    "manualInvitationImageType": "fromGallery",
    "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
    "manualInvitationCloseAreaXOffset": 10,
    "manualInvitationCloseAreaYOffset": 10,
    "manualInvitationCloseAreaWidth": 10,
    "manualInvitationCloseAreaHeight": 10,
    "manualInvitationTextAreaXOffset": 10,
    "manualInvitationTextAreaYOffset": 10,
    "manualInvitationTextAreaWidth": 10,
    "manualInvitationTextAreaHeight": 10,
    "manualInvitationText": "",
    "manualInvitationTextFont": "timesNewRoman",
    "manualInvitationTextSize": "XXSmall",
    "isManualInvitationTextBold": false,
    "isManualInvitationTextItalic": false,
    "manualInvitationTextColor": "#339FD9"
  },
  "autoInvitations": [{
    "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
    "name": "test",
    "isEnable": false,
    "isDisplayedOnceInOneSession": false,
    "order": 1,
    "imageType": "fromGallery",
    "closeAreaXOffset": 10,
    "closeAreaYOffset": 10,
    "closeAreaWidth": 10,
    "closeAreaHeight": 10,
    "textAreaXOffset": 10,
    "textAreaYOffset": 10,
    "textAreaWidth": 10,
    "textAreaHeight": 10,
    "text": "",
    "textFont": "timesNewRoman",
    "textSize": "XXSmall",
    "isTextBold": false,
    "isTextItalic": false,
    "textColor": "#339FD9",
    "position": "centerWithOverlay",
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  }]
}
```

# Manual Invitation

- `GET /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation` - [Get settings of manual invitation  for a campaign](#get-Manual-Invitation)
- `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation` - [Update settings of manual invitation  for a campaign](#update-Manual-Invitation)

## Related Object Json Format

### Manual Invitation Object

  Manual Invitation Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `manualInvitationPosition` | string | no | no | | Including `centerWithOverlay`, `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available When using `popup` Invitation Style.  |
| `manualInvitationImageType` | string | no | no | | Including`fromGallery` and `fromMyComputer`.  |
| `manualInvitationImage` | string | no | no | | Image file key of Invitation.  |
| `manualInvitationCloseAreaXOffset` | integer | no | no | | |
| `manualInvitationCloseAreaYOffset` | integer | no | no | | |
| `manualInvitationCloseAreaWidth` | integer | no | no | | |
| `manualInvitationCloseAreaHeight` | integer | no | no | | |
| `manualInvitationTextAreaXOffset` | integer | no | no | | |
| `manualInvitationTextAreaYOffset` | integer | no | no | | |
| `manualInvitationTextAreaWidth` | integer | no | no | | |
| `manualInvitationTextAreaHeight` | integer | no | no | | |
| `manualInvitationText` | string | no | no | | |
| `manualInvitationTextFont` | string | no | no | | Including `timesNewRoman`, `tahoma`, `verdana`, `arial`, `comicSansMs` and `courier`. |
| `manualInvitationTextSize` | string | no | no | | Including `XXSmall`, `XSmall`, `small`, `medium`, `large`, `XLarge` and `XXLarge`. |
| `isManualInvitationTextBold` | boolean | no | no | | |
| `isManualInvitationTextItalic` | boolean | no | no | | |
| `manualInvitationTextColor` | string | no | no | | |

## Manual Invitation Endpoints

### Get Manual Invitation

  `GET /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Manual Invitation](#Manual-Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/invitation/manualInvitation
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "manualInvitationPosition": "centerWithOverlay",
  "manualInvitationImageType": "fromGallery",
  "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
  "manualInvitationCloseAreaXOffset": 10,
  "manualInvitationCloseAreaYOffset": 10,
  "manualInvitationCloseAreaWidth": 10,
  "manualInvitationCloseAreaHeight": 10,
  "manualInvitationTextAreaXOffset": 10,
  "manualInvitationTextAreaYOffset": 10,
  "manualInvitationTextAreaWidth": 10,
  "manualInvitationTextAreaHeight": 10,
  "manualInvitationText": "",
  "manualInvitationTextFont": "timesNewRoman",
  "manualInvitationTextSize": "XXSmall",
  "isManualInvitationTextBold": false,
  "isManualInvitationTextItalic": false,
  "manualInvitationTextColor": "#339FD9"
}
```

### Update Manual Invitation

  `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Manual Invitation](#Manual-Invitation-Object) structure

#### Response

the response is: [Invitation](#Invitation-Object) Object

example:
```Json
{
  "manualInvitationPosition": "centerWithOverlay",
  "manualInvitationImageType": "fromGallery",
  "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
  "manualInvitationCloseAreaXOffset": 10,
  "manualInvitationCloseAreaYOffset": 10,
  "manualInvitationCloseAreaWidth": 10,
  "manualInvitationCloseAreaHeight": 10,
  "manualInvitationTextAreaXOffset": 10,
  "manualInvitationTextAreaYOffset": 10,
  "manualInvitationTextAreaWidth": 10,
  "manualInvitationTextAreaHeight": 10,
  "manualInvitationText": "",
  "manualInvitationTextFont": "timesNewRoman",
  "manualInvitationTextSize": "XXSmall",
  "isManualInvitationTextBold": false,
  "isManualInvitationTextItalic": false,
  "manualInvitationTextColor": "#339FD9"
}
```

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "manualInvitationPosition": "centerWithOverlay",
  "manualInvitationImageType": "fromGallery",
  "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
  "manualInvitationCloseAreaXOffset": 10,
  "manualInvitationCloseAreaYOffset": 10,
  "manualInvitationCloseAreaWidth": 10,
  "manualInvitationCloseAreaHeight": 10,
  "manualInvitationTextAreaXOffset": 10,
  "manualInvitationTextAreaYOffset": 10,
  "manualInvitationTextAreaWidth": 10,
  "manualInvitationTextAreaHeight": 10,
  "manualInvitationText": "",
  "manualInvitationTextFont": "timesNewRoman",
  "manualInvitationTextSize": "XXSmall",
  "isManualInvitationTextBold": false,
  "isManualInvitationTextItalic": false,
  "manualInvitationTextColor": "#339FD9"
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/invitation/manualInvitation
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "manualInvitationPosition": "centerWithOverlay",
  "manualInvitationImageType": "fromGallery",
  "manualInvitationImage": "A036254E-1DBD-C271-8A12-0ED667EF9C8A",
  "manualInvitationCloseAreaXOffset": 10,
  "manualInvitationCloseAreaYOffset": 10,
  "manualInvitationCloseAreaWidth": 10,
  "manualInvitationCloseAreaHeight": 10,
  "manualInvitationTextAreaXOffset": 10,
  "manualInvitationTextAreaYOffset": 10,
  "manualInvitationTextAreaWidth": 10,
  "manualInvitationTextAreaHeight": 10,
  "manualInvitationText": "",
  "manualInvitationTextFont": "timesNewRoman",
  "manualInvitationTextSize": "XXSmall",
  "isManualInvitationTextBold": false,
  "isManualInvitationTextItalic": false,
  "manualInvitationTextColor": "#339FD9"
}
```

# Auto Invitation

- `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations` - [Get all auto invitations in a campaign](#get-all-Auto-Invitations-in-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Get a auto invitation by id](#get-a-Auto-Invitation-by-id)
- `POST /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations` - [Create a new auto invitation](#create-a-new-Auto-Invitation)
- `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Update a auto invitation](#update-a-Auto-Invitation)
- `DELETE /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Delete a auto invitation](#delete-a-Auto-Invitation)

## Related Object Json Format

### Auto Invitation Object

  Auto Invitation Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `id` | Guid | yes | no | | Id of the current item. |
| `name` | string | no | yes | | |
| `isEnable` | boolean | no | no | | Whether the auto invitation is enabled or not. |
| `isDisplayedOnceInOneSession` | boolean | no | no | | |
| `order` | integer | no | no | | |
| `imageType` | string | no | no | | Including`fromGallery` and `fromMyComputer`. |
| `closeAreaXOffset` | integer | no | no | | |
| `closeAreaYOffset` | integer | no | no | | |
| `closeAreaWidth` | integer | no | no | | |
| `closeAreaHeight` | integer | no | no | | |
| `textAreaXOffset` | integer | no | no | | |
| `textAreaYOffset` | integer | no | no | | |
| `textAreaWidth` | integer | no | no | | |
| `textAreaHeight` | integer | no | no | | |
| `text` | string | no | no | | |
| `textFont` | string | no | no | | Including `timesNewRoman`, `tahoma`, `verdana`, `arial`, `comicSansMs` and `courier`. |
| `textSize` | string | no | no | | Including `XXSmall`, `XSmall`, `small`, `medium`, `large`, `XLarge` and `XXLarge`. |
| `isTextBold` | boolean | no | no | | |
| `isTextItalic` | boolean | no | no | | |
| `textColor` | string | no | no | | |
| `position` | string | no | no | | Including `centerWithOverlay`, `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`.  |
| `conditionMetType` | string | no | no | | Including `all`, `any` and `logicalExpression`. |
| `logicalExpression` | string | no | no | | |
| `conditions` | [Live Chat Condition](#Live-Chat-Condition-Object)[] | no | no | | |

## Auto Invitation Endpoints

### Get all Auto Invitations in a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Auto Invitation](#Auto-Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/invitation/autoInvitations
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
    "name": "test",
    "isEnable": false,
    "isDisplayedOnceInOneSession": false,
    "order": 1,
    "imageType": "fromGallery",
    "closeAreaXOffset": 10,
    "closeAreaYOffset": 10,
    "closeAreaWidth": 10,
    "closeAreaHeight": 10,
    "textAreaXOffset": 10,
    "textAreaYOffset": 10,
    "textAreaWidth": 10,
    "textAreaHeight": 10,
    "text": "",
    "textFont": "timesNewRoman",
    "textSize": "XXSmall",
    "isTextBold": false,
    "isTextItalic": false,
    "textColor": "#339FD9",
    "position": "centerWithOverlay",
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  },
  ...
  ]
```

### Get a Auto Invitation by id

  `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |
| `id` | Guid | yes  |  the unique Id of the auto invitation |

#### Response

the response is: [Auto Invitation](#Auto-Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/invitation/autoInvitations/8CAE01CB-F74D-254C-A42B-84C00546C31E
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
    "name": "test",
    "isEnable": false,
    "isDisplayedOnceInOneSession": false,
    "order": 1,
    "imageType": "fromGallery",
    "closeAreaXOffset": 10,
    "closeAreaYOffset": 10,
    "closeAreaWidth": 10,
    "closeAreaHeight": 10,
    "textAreaXOffset": 10,
    "textAreaYOffset": 10,
    "textAreaWidth": 10,
    "textAreaHeight": 10,
    "text": "",
    "textFont": "timesNewRoman",
    "textSize": "XXSmall",
    "isTextBold": false,
    "isTextItalic": false,
    "textColor": "#339FD9",
    "position": "centerWithOverlay",
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  },
  ...
  ]
```

### Create a new Auto Invitation

  `POST /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Auto Invitation](#Auto-Invitation-Object) structure

example:
```Json
{
  "name": "test",
  "isEnable": false,
  "isDisplayedOnceInOneSession": false,
  "order": 1,
  "imageType": "fromGallery",
  "closeAreaXOffset": 10,
  "closeAreaYOffset": 10,
  "closeAreaWidth": 10,
  "closeAreaHeight": 10,
  "textAreaXOffset": 10,
  "textAreaYOffset": 10,
  "textAreaWidth": 10,
  "textAreaHeight": 10,
  "text": "",
  "textFont": "timesNewRoman",
  "textSize": "XXSmall",
  "isTextBold": false,
  "isTextItalic": false,
  "textColor": "#339FD9",
  "position": "centerWithOverlay",
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

#### Response

the response is: [Auto Invitation](#Auto-Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "test",
  "isEnable": false,
  "isDisplayedOnceInOneSession": false,
  "order": 1,
  "imageType": "fromGallery",
  "closeAreaXOffset": 10,
  "closeAreaYOffset": 10,
  "closeAreaWidth": 10,
  "closeAreaHeight": 10,
  "textAreaXOffset": 10,
  "textAreaYOffset": 10,
  "textAreaWidth": 10,
  "textAreaHeight": 10,
  "text": "",
  "textFont": "timesNewRoman",
  "textSize": "XXSmall",
  "isTextBold": false,
  "isTextItalic": false,
  "textColor": "#339FD9",
  "position": "centerWithOverlay",
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/invitation/autoInvitations
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/invitation/autoInvitations/8CAE01CB-F74D-254C-A42B-84C00546C31E

{
  "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
  "name": "test",
  "isEnable": false,
  "isDisplayedOnceInOneSession": false,
  "order": 1,
  "imageType": "fromGallery",
  "closeAreaXOffset": 10,
  "closeAreaYOffset": 10,
  "closeAreaWidth": 10,
  "closeAreaHeight": 10,
  "textAreaXOffset": 10,
  "textAreaYOffset": 10,
  "textAreaWidth": 10,
  "textAreaHeight": 10,
  "text": "",
  "textFont": "timesNewRoman",
  "textSize": "XXSmall",
  "isTextBold": false,
  "isTextItalic": false,
  "textColor": "#339FD9",
  "position": "centerWithOverlay",
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

### Update a Auto Invitation

  `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |
| `id` | Guid | yes  |  the unique Id of the auto invitation |

Request Body

  The request body contains data with the [Auto Invitation](#Auto-Invitation-Object) structure

example:
```Json
{
  "name": "test",
  "isEnable": false,
  "isDisplayedOnceInOneSession": false,
  "order": 1,
  "imageType": "fromGallery",
  "closeAreaXOffset": 10,
  "closeAreaYOffset": 10,
  "closeAreaWidth": 10,
  "closeAreaHeight": 10,
  "textAreaXOffset": 10,
  "textAreaYOffset": 10,
  "textAreaWidth": 10,
  "textAreaHeight": 10,
  "text": "",
  "textFont": "timesNewRoman",
  "textSize": "XXSmall",
  "isTextBold": false,
  "isTextItalic": false,
  "textColor": "#339FD9",
  "position": "centerWithOverlay",
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

#### Response

the response is: [Auto Invitation](#Auto-Invitation-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "test11111",
  "isEnable": false,
  "isDisplayedOnceInOneSession": false,
  "order": 1,
  "imageType": "fromGallery",
  "closeAreaXOffset": 10,
  "closeAreaYOffset": 10,
  "closeAreaWidth": 10,
  "closeAreaHeight": 10,
  "textAreaXOffset": 10,
  "textAreaYOffset": 10,
  "textAreaWidth": 10,
  "textAreaHeight": 10,
  "text": "",
  "textFont": "timesNewRoman",
  "textSize": "XXSmall",
  "isTextBold": false,
  "isTextItalic": false,
  "textColor": "#339FD9",
  "position": "centerWithOverlay",
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/invitation/autoInvitations/8CAE01CB-F74D-254C-A42B-84C00546C31E
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "8CAE01CB-F74D-254C-A42B-84C00546C31E",
  "name": "test11111",
  "isEnable": false,
  "isDisplayedOnceInOneSession": false,
  "order": 1,
  "imageType": "fromGallery",
  "closeAreaXOffset": 10,
  "closeAreaYOffset": 10,
  "closeAreaWidth": 10,
  "closeAreaHeight": 10,
  "textAreaXOffset": 10,
  "textAreaYOffset": 10,
  "textAreaWidth": 10,
  "textAreaHeight": 10,
  "text": "",
  "textFont": "timesNewRoman",
  "textSize": "XXSmall",
  "isTextBold": false,
  "isTextItalic": false,
  "textColor": "#339FD9",
  "position": "centerWithOverlay",
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

### Delete a Auto Invitation

  `DELETE /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |
| `id` | Guid | yes  |  the unique Id of the auto invitation |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/invitation/autoInvitations/8CAE01CB-F74D-254C-A42B-84C00546C31E
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Agent Wrap-Up

- `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup` - [Get settings of agent wrap-Up  for a campaign](#get-Agent-Wrap-Up)
- `PUT /api/v3/livechat/campaigns/{campaignId}/agentWrapup` - [Update settings of agent wrap-Up  for a campaign](#update-Agent-Wrap-Up)

## Related Object Json Format

### Agent Wrap-Up Object

  Agent Wrap-Up Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `fields` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | no | no | | These System Fields are prebuilt and can’t be deleted: `agent wrap-up category`, `agent wrap-up comments`.  |

## Agent Wrap-Up Endpoints

### Get Agent Wrap-Up

  `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Agent Wrap-Up](#Agent-Wrap-Up-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/agentWrapup
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "fields":  []
}
```

### Update Agent Wrap-Up

  `PUT /api/v3/livechat/campaigns/{campaignId}/agentWrapup`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Agent Wrap-Up](#Agent-Wrap-Up-Object) structure

example:
```Json
{
  "fields":  [
    {
      "id": "5062B231-E0D6-AFD3-2E72-4D143792DC03",
      "field": {
        "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
        "isSystem": false,
        "name": "teset",
        "type": "textBox",
        "options": [{
          "value": "test",
          "order": 1,
        },
        ...
        ],
        "leftText": "",
        "rightText": "",
        "optionGroups": [{
          "name": "test",
          "order": 1,
          "options":[]
        },
        ...
        ],
      },
      "isVisible": false,
      "isRequired": false,
      "order": 1,
      "ratingGrades": [{
        "grade": 1,
        "label": "",
        "isVisible": false
      },
      ...
      ]
    },
    ...
  ]
}
```

#### Response

the response is: [Agent Wrap-Up](#Agent-Wrap-Up-Object) Object

#### Example


Using curl
```
curl -H "Content-Type: application/json" -d '{
  "fields":  []
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/agentWrapup
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "fields":  []
}
```

# Language

- `GET /api/v3/livechat/campaigns/{campaignId}/language` - [Get settings of language for a campaign](#get-Language)
- `PUT /api/v3/livechat/campaigns/{campaignId}/language` - [Update settings of language for a campaign](#update-Language)

## Related Object Json Format

### Language Object

  Language Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `defaultLanguage` | string | no | no | | The languages are defined in cPanel.  |
| `isCustomLanguageEnabled` | boolean | no | no | | |
| `isTextDirectionRightToLeft` | boolean | no | no | | |
| `customLanguageItems` | [Custom Language](#Custom-Language-Object)[] | no | no | | |

### Custom Language Object

  Custom Language Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `systemName` | string | no | no | | |
| `customText` | string | no | no | | |

## Language Endpoints

### Get Language

  `GET /api/v3/livechat/campaigns/{campaignId}/language`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Language](#Language-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/language
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "defaultLanguage": "",
  "isCustomLanguageEnabled": false,
  "isTextDirectionRightToLeft": false,
  "customLanguageItems": {
    "systemName": "chatwindow",
    "customText": "chatwindowcustom"
  }
}
```

### Update Language

  `PUT /api/v3/livechat/campaigns/{campaignId}/language`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Language](#Language-Object) structure

example:
```Json
{
  "defaultLanguage": "",
  "isCustomLanguageEnabled": false,
  "isTextDirectionRightToLeft": false,
  "customLanguageItems": {
    "systemName": "chatwindow",
    "customText": "chatwindowcustom"
  }
}
```

#### Response

the response is: [Language](#Language-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "defaultLanguage": "",
  "isCustomLanguageEnabled": false,
  "isTextDirectionRightToLeft": false,
  "customLanguageItems": {
    "systemName": "chatwindow",
    "customText": "chatwindowcustom"
  }
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/language
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "defaultLanguage": "",
  "isCustomLanguageEnabled": false,
  "isTextDirectionRightToLeft": false,
  "customLanguageItems": {
    "systemName": "chatwindow",
    "customText": "chatwindowcustom"
  }
}
```

# Routing

- `GET /api/v3/livechat/campaigns/{campaignId}/routing` - [Get settings of routing for a campaign](#get-Routing)
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing` - [Update settings of routing for a campaign](#update-Routing)

## Related Object Json Format

### Routing Object

  Routing Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `isEnable` | boolean |  | no | no |  false | Whether the routing rule is enabled or not. |
| `type` | string |  | no | no | | Including `simple` and `customRule`. |
| `routeTo` | string | | no | no | | Including `agent` and `department`. //agent 对应的链接呢. |
| `routeToId` | String | | no | no | | AgentId or DepartmentId. |
| `routeToAgent` | [Agent](#Agent-Object) | yes | no | no | |  |
| `routeToDepartment` | [Department](#Department-Object) //department 对应的链接在哪呢?| yes | no | no | |  |
| `priority` | string |  | no | no | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
| `percentageToBot` | integer |  | no | no | | |
| `customRules` | [Custom Rule](#Custom-Rule-Object)[] |  | no | no | | |
| `actionWhenNoRuleMatched` | string |  | no | no | | Including `routeToSite`, `routeToDepartment`, `routeToAgent` and `redirectToOfflineMessage`. |
| `routeToWhenNoRuleMatched` | string | | no | no | | Including `agent` and `department`. |
| `routeToIdWhenNoRuleMatched` | String | | no | no | | AgentId or DepartmentId. |
| `routeToAgentWhenNoRuleMatched` | [Agent](#Agent-Object) | yes | no | no | |  |
| `routeToDepartmentWhenNoRuleMatched` | [Department](#Department-Object) | yes | no | no | |  |
| `priorityWhenNoRuleMatched` | string |  | no | no | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
| `percentageToBotWhenNoRuleMatched` | integer |  | no | no | | |
| `emailsToReceiveOfflineMessage` | string |  | no | no | |  |

## Routing Endpoints

### Get Routing

  `GET /api/v3/livechat/campaigns/{campaignId}/routing`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Query string

| Name  | Type | Required  | Default | Description |
| - | - | - | - | - |
| `include` | string | no  |  | Available value: `agent`, `department` |

#### Response

the response is: [Routing](#Routing-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/routing?include=department
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable": false,
  "type": "simple",
  "routeTo": "agent",
  "routeToId": "5",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "customRules": [],
  "actionWhenNoRuleMatched": "routeToDepartment",
  "routeToWhenNoRuleMatched": "department",
  "routeToIdWhenNoRuleMatched": "EFF66BBD-1FAD-A04E-486A-B8B4269A6BB5",
  "routeToDepartmentWhenNoRuleMatched": { // include department
      "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priorityWhenNoRuleMatched": "lowest",
  "percentageToBotWhenNoRuleMatched": 10,
  "emailsToReceiveOfflineMessage": ""
}
```

### Update Routing

  `PUT /api/v3/livechat/campaigns/{campaignId}/routing`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Routing](#Routing-Object) structure

example:
```Json
{
  "isEnable": false,
  "type": "simple",
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "priority": "lowest",
  "percentageToBot": 10,
  "customRules": [],
  "actionWhenNoRuleMatched": "routeToDepartment",
  "routeToWhenNoRuleMatched": "department",
  "routeToIdWhenNoRuleMatched": "EFF66BBD-1FAD-A04E-486A-B8B4269A6BB5",
  "priorityWhenNoRuleMatched": "lowest",
  "percentageToBotWhenNoRuleMatched": 10,
  "emailsToReceiveOfflineMessage": ""
}
```

#### Response

the response is: [Routing](#Routing-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable": false,
  "type": "simple",
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "priority": "lowest",
  "percentageToBot": 10,
  "customRules": [],
  "actionWhenNoRuleMatched": "routeToDepartment",
  "routeToWhenNoRuleMatched": "department",
  "routeToIdWhenNoRuleMatched": "EFF66BBD-1FAD-A04E-486A-B8B4269A6BB5",
  "priorityWhenNoRuleMatched": "lowest",
  "percentageToBotWhenNoRuleMatched": 10,
  "emailsToReceiveOfflineMessage": ""
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/routing
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable": false,
  "type": "simple",
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "priority": "lowest",
  "percentageToBot": 10,
  "customRules": [],
  "actionWhenNoRuleMatched": "routeToDepartment",
  "routeToWhenNoRuleMatched": "department",
  "routeToIdWhenNoRuleMatched": "EFF66BBD-1FAD-A04E-486A-B8B4269A6BB5",
  "priorityWhenNoRuleMatched": "lowest",
  "percentageToBotWhenNoRuleMatched": 10,
  "emailsToReceiveOfflineMessage": ""
}
```

# Custom Rule

- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Get all custom rules](#get-all-Custom-Rules)
- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Get a custom rule by id](#get-a-Custom-Rule-by-id)
- `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Create a new custom rule](#create-a-new-Custom-Rule)
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Update a custom rule](#update-a-Custom-Rule)
- `DELETE /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Delete a custom rule](#delete-a-Custom-Rule)

## Related Object Json Format

### Custom Rule Object

  Custom Rule Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `id` | Guid | yes | | no | | Id of the current item. |
| `isEnable` | boolean | | no | no | | Whether the custom rule is enabled or not. |
| `name` | string | | no | no | | |
| `order` | integer | | no | no | | |
| `routeTo` | string | | no | no | | Including `agent` and `department`. |
| `routeToId` | String | | no | no | | AgentId or DepartmentId. |
| `routeToAgent` | [Agent](#Agent-Object) | yes | no | no | |  |
| `routeToDepartment` | [Department](#Department-Object) | yes | no | no | |  |
| `priority` | string | | no | no | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
| `percentageToBot` | integer | | no | no | | |
| `conditionMetType` | string | | no | no | | Including `all`, `any` and `logicalExpression`. |
| `logicalExpression` | string | | no | no | | |
| `conditions` | [Live Chat Condition](#Live-Chat-Condition-Object)[] | | no | no | |an array of [Live Chat Condition](#Live-Chat-Condition-Object) object.  |

### Live Chat Condition Object

  Live Chat Condition Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `field` | string | no | no | | |
| `operator` | integer | no | no | | Include `is`, `isNot`, `contains`, `doesnotcontain`, `isMoreThan`, `isNotMoreThan`, `isLessThan`, `isNotLessThan` and `regularExpression`. |
| `value` | string | no | no | | |
| `order` | integer | no | no | | |

## Routing Endpoints

### Get all Custom Rules

  `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Query string

| Name  | Type | Required  | Default | Description |
| - | - | - | - | - |
| `include` | string | no  |  | Available value: `agent`, `department` |

#### Response

the response is: [Custom Rule](#Custom-Rule-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/routing/customRules?include=department
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F",
    "isEnable": false,
    "name": "test",
    "order": 1,
    "routeTo": "agent",
    "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
    "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
    },
    "priority": "lowest",
    "percentageToBot": 10,
    "conditionMetType": "any",
    "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
  },
  ...
]
```

### Get a Custom Rule by id

  `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the custom rule |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Query string

| Name  | Type | Required  | Default | Description |
| - | - | - | - | - |
| `include` | string | no  |  | Available value: `agent`, `department` |

#### Response

the response is: [Custom Rule](#Custom-Rule-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/routing/customRules/02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F?include=department
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F",
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

### Create a new Custom Rule

  `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the custom rule |

Request Body

  The request body contains data with the [Custom Rule](#Custom-Rule-Object) structure

example:
```Json
{
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
}
```

#### Response

the response is: [Custom Rule](#Custom-Rule-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/routing/customRules
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/routing/customRules/02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F

{
  "id": "02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F",
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
    "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
    ...
    ]
}
```

### Update a Custom Rule

  `PUT /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the custom rule |
| `campaignId` | Guid | yes  |  the unique Id of the custom rule |

Request Body

  The request body contains data with the [Custom Rule](#Custom-Rule-Object) structure

example:
```Json
{
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

#### Response

the response is: [Custom Rule](#Custom-Rule-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/routing/customRules/02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F",
  "isEnable": false,
  "name": "test",
  "order": 1,
  "routeTo": "agent",
  "routeToId": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
  "routeToDepartment": { // include department
    "id": "1455D7CD-C510-77F8-44AF-6E75ACEECC3D",
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  ["4487fc9d-92e6-4487-a2e8-92e68d6892e6"]
  },
  "priority": "lowest",
  "percentageToBot": 10,
  "conditionMetType": "any",
  "logicalExpression": "",
  "conditions": [
    {
      "field": "CurrentPageUrl",
      "operator": "include",
      "value": "live",
      "order": 1
    },
  ...
  ]
}
```

### Delete a Custom Rule

  `DELETE /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the custom rule |
| `campaignId` | Guid | yes  |  the unique Id of the custom rule |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/routing/customRules/02F842BF-70DA-95D0-8F6A-0D3C6CDCBB9F
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Chatbot Integration

- `GET /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration` - [Get settings of Chatbot Integration for a campaign](#get-Chatbot-Integration)
- `PUT /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration` - [Update settings of Chatbot Integration for a campaign](#update-Chatbot-Integration)

## Related Object Json Format

### Chatbot Integration Object

  Chatbot Integration Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - |- | :-: | :-: | :-: | - |
| `isEnable` | boolean | | no | no | | Whether the chatbot integration is enabled or not. |
| `selectedChatbotId` | Guid | | no | no | | |
| `selectedChatbot` | [Bot](#Bot-Object) | yes | no | no | | |
| `isChatbotAllocatedWhenAgentOnline` | boolean | | no | no | | |
| `ifDistributeChatsToChatbotByQueueLength` | boolean | | no | no | | |
| `ifDistributeChatsToChatbotByPercentage` | boolean | | no | no | | |
| `queueLength` | integer | | no | no | | Allocate chats to Chatbot when the queue reaches the preset length. |
| `percentageToChatbot` | smallint | | no | no | | |
| `isChatbotAllocatedWhenAgentOffline` | boolean | | no | no | | |

## Chatbot Integration Endpoints

### Get Chatbot Integration

  `GET /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Query string

| Name  | Type | Required  | Default | Description |
| - | - | - | - | - |
| `include` | string | no  |  | Available value: `chatbot` |

#### Response

the response is: [Chatbot Integration](#Chatbot-Integration-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/chatbotIntegration?include=chatbot
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable": false,
  "selectedChatbotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
  "selectedChatbot": { // include chatbot
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
      "LiveChat", "Facebook Messenger", "Twitter Direct Message", "WeChat", "WhatsApp", "SMS"
    ]
  },
  "isChatbotAllocatedWhenAgentOnline": false,
  "ifDistributeChatsToChatbotByQueueLength": false,
  "ifDistributeChatsToChatbotByPercentage": false,
  "queueLength": 1,
  "percentageToChatbot": 1,
  "isChatbotAllocatedWhenAgentOffline": false
}
```

### Update Chatbot Integration

  `PUT /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Chatbot Integration](#Chatbot-Integration-Object) structure

example:
```Json
{
  "isEnable": true,
  "selectedChatbotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
  "isChatbotAllocatedWhenAgentOnline": false,
  "ifDistributeChatsToChatbotByQueueLength": false,
  "ifDistributeChatsToChatbotByPercentage": false,
  "queueLength": 1,
  "percentageToChatbot": 1,
  "isChatbotAllocatedWhenAgentOffline": false
}
```

#### Response

the response is: [Chatbot Integration](#Chatbot-Integration-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable": true,
  "selectedChatbotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
  "isChatbotAllocatedWhenAgentOnline": false,
  "ifDistributeChatsToChatbotByQueueLength": false,
  "ifDistributeChatsToChatbotByPercentage": false,
  "queueLength": 1,
  "percentageToChatbot": 1,
  "isChatbotAllocatedWhenAgentOffline": false
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/chatbotIntegration
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable": true,
  "selectedChatbotId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
  "isChatbotAllocatedWhenAgentOnline": false,
  "ifDistributeChatsToChatbotByQueueLength": false,
  "ifDistributeChatsToChatbotByPercentage": false,
  "queueLength": 1,
  "percentageToChatbot": 1,
  "isChatbotAllocatedWhenAgentOffline": false
}
```

# KB Integration

- `GET /api/v3/livechat/campaigns/{campaignId}/kbIntegration` - [Get settings of KB Integration for a campaign](#get-KB-Integration) include knowledgeBase
- `PUT /api/v3/livechat/campaigns/{campaignId}/kbIntegration` - [Update settings of KB Integration for a campaign](#update-KB-Integration)

## Related Object Json Format

### KB Integration Object

  KB Integration Object is represented as simple flat JSON objects with the following keys:

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `isEnable` | boolean | no | no | | Whether the KB integration is enabled or not. |
| `selectedKBId` | Guid | no | no | | |
| `isSearchAllowedBeforeChatting` | boolean | no | no | | |
| `greetingMessageBeforeChatting` | string | no | no | | |
| `isSearchAllowedBeforeOfflineMessage` | boolean | no | no | | |
| `greetingMessageBeforeOfflineMessage` | string | no | no | | |
| `articlesShowedInSearchResult` | integer | no | no | | |

## KB Integration Endpoints

### Get KB Integration

  `GET /api/v3/livechat/campaigns/{campaignId}/KBIntegration`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [KB Integration](#KB-Integration-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/KBIntegration
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable": false,
  "selectedKBId": "7213D14D-1EAD-6ED7-EA09-D834BAB9F092",
  "isSearchAllowedBeforeChatting": false,
  "greetingMessageBeforeChatting": "",
  "isSearchAllowedBeforeOfflineMessage": false,
  "greetingMessageBeforeOfflineMessage": "",
  "articlesShowedInSearchResult": 1
}
```

### Update KB Integration

  `PUT /api/v3/livechat/campaigns/{campaignId}/KBIntegration`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [KB Integration](#KB-Integration-Object) structure

example:
```Json
{
  "isEnable": true,
  "selectedKBId": "7213D14D-1EAD-6ED7-EA09-D834BAB9F092",
  "isSearchAllowedBeforeChatting": false,
  "greetingMessageBeforeChatting": "",
  "isSearchAllowedBeforeOfflineMessage": false,
  "greetingMessageBeforeOfflineMessage": "",
  "articlesShowedInSearchResult": 1
}
```

#### Response

the response is: [KB Integration](#KB-Integration-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "isEnable": true,
  "selectedKBId": "7213D14D-1EAD-6ED7-EA09-D834BAB9F092",
  "isSearchAllowedBeforeChatting": false,
  "greetingMessageBeforeChatting": "",
  "isSearchAllowedBeforeOfflineMessage": false,
  "greetingMessageBeforeOfflineMessage": "",
  "articlesShowedInSearchResult": 1
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/KBIntegration
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "isEnable": true,
  "selectedKBId": "7213D14D-1EAD-6ED7-EA09-D834BAB9F092",
  "isSearchAllowedBeforeChatting": false,
  "greetingMessageBeforeChatting": "",
  "isSearchAllowedBeforeOfflineMessage": false,
  "greetingMessageBeforeOfflineMessage": "",
  "articlesShowedInSearchResult": 1
}
```

# Campaign Form Field

- `GET /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Get all form fields of Pre-Chat for a campaign](#get-all-form-fields-of-Pre-Chat-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Create a new form field of Pre-Chat for a campaign](#create-a-new-form-fields-of-Pre-Chat-for-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Get all form fields of Post Chat for a campaign](#get-all-form-fields-of-Post-Chat-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Create a new form field of Post Chat for a campaign](#create-a-new-form-fields-of-Offline-Message-for-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Get all form fields of offline message for a campaign](#get-all-form-fields-of-Offline-Message-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Create a new form field of offline message for a campaign](#create-a-new-form-fields-of-Offline-Message-for-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Get all form fields of agent wrapup for a campaign](#get-all-form-fields-of-Agent-Wrap-up-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Create a new form field of agent wrapup for a campaign](#create-a-new-form-fields-of-Agent-Wrap-up-for-a-campaign)
- `GET /api/v3/livechat/campaignFormFields/{id}` - [Get a campaign form field by id](#get-a-campaign-form-field-by-id)
- `PUT /api/v3/livechat/campaignFormFields/{id}` - [Update a campaign form field](#update-a-campaign-form-field)
- `DELETE /api/v3/livechat/campaignFormFields/{id}` - [Delete a campaign form field](#delete-a-campaign-form-field)

## Related Object Json Format

### Campaign Form Field Object

  Campaign Form Field is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `id` | Guid | yes | no | | Id of the current item. |
| `field` | [Live Chat Field](#Live-Chat-Field-Object) | no | no | | |
| `isVisible` | boolean | no | no | | Whether the field is visible or not. |
| `isRequired` | boolean | no | no | | Whether the field is required or not when submitting the form |
| `order` | integer | no | no | | The order of the field. |
| `ratingGrades` | [Rating Grade](#Rating-Grade-Object)[] | no | no | | Always 5 grades. Available whey Type of Live Chat Field is Rating. |

### Rating Grade Object

  Rating Grade is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `grade` | integer | no | no | | |
| `label` | string | no | no | | |
| `isVisible` | boolean | no | no | | |

### Live Chat Field Object

  Live Chat Field is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `id` | Guid | yes | no | | Id of the current item. |
| `isSystem` | boolean | no | no | | whether the field is system or not. |
| `name` | string | no | no | | |
| `type` | string | no | no | | The [Live Chat Field Type](#Live-Chat-Field-Type) of the field. |
| `options` | [Live Chat Field Option](#Live-Chat-Field-Option-Object)[] | no | no | | Live Chat Field Option, available whey Type is `radioBox`, `dropdownList`, `checkboxList`. |
| `leftText` | string | no | no | | Available whey Type is NPS. |
| `rightText` | string | no | no | | Available whey Type is NPS. |
| `optionGroups` | [Live Chat Field Option Group](#Live-Chat-Field-Option-Group-Object)[] | no | no | | Live Chat Field Option Group, available whey Type is `checkboxListwithOptionGroups`. |

### Live Chat System Field

  Live Chat System Field is one key of the following keys:

| System Field | Type | Only Available Forms | Is Required |
| - | - | :-: | - |
| `name` | `textBox` | Name field, `Pre Chat Form` or `Offline Message Form` only. | no |
| `email` | `textBox` | Email field, `Pre Chat Form` or `Offline Message Form` only. | no |
| `phone` | `textBox` | Phone field, `Pre Chat Form` or `Offline Message Form` only. | no |
| `company` | `textBox` | Company field, `Pre Chat Form` or `Offline Message Form` only. | no |
| `product service` | `dropdownList` | Product and Service field, `Pre Chat Form` only. | no |
| `department` | `dropdownList` | Department field, `Pre Chat Form` or `Offline Message Form` only. | no |
| `ticket id` | `textBox` | Ticket field, `Pre Chat Form` or `Offline Message Form` only.  | no |
| `rating` | `rating` | Rating field, `Post Chat Form` only. | no |
| `rating comment` | `textArea` | Comments field, `Post Chat Form` only. | no |
| `subject` | `textBox` | Subject field, `Offline Message Form` only. | yes |
| `message` | `textArea` | Content field, `Offline Message Form` only. | no |
| `attachment` | `file` | Attachment field, `Offline Message Form` only. | no |
| `category` | `dropdownList` or `checkboxListwithOptionGroups`  | category field , `agent wrap-up` only | no |
| `wrap-up comment` | `textArea` | comment field , `agent wrap-up` only | no |

### Live Chat Field Type

  Live Chat Field Type is one key of the following keys:

| Name | Available Forms |
| - | :-: |
| `textBox` | `Pre-Chat`, `Post Chat`, `Offline Message`, `Agent Wrap-Up`   |
| `textArea` | `Pre-Chat`, `Post Chat`, `Offline Message`, `Agent Wrap-Up`   |
| `radioBox` | `Pre-Chat`, `Post Chat`, `Offline Message`, `Agent Wrap-Up`   |
| `checkbox` | `Pre-Chat`, `Post Chat`, `Offline Message`, `Agent Wrap-Up`   |
| `dropdownList` | `Pre-Chat`, `Post Chat`, `Offline Message`, `Agent Wrap-Up` |
| `checkboxList` | `Pre-Chat`, `Post Chat`, `Offline Message`, `Agent Wrap-Up` |
| `NPS` | `Post Chat`  |
| `file` | `Offline Message`   |
| `rating` | `Post Chat` |
| `checkboxListwithOptionGroups` | `Agent Wrap-Up`   |

### Live Chat Field Option Object

  Live Chat Field Option Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `value` | string | no | no | | |
| `order` | integer | no | no | | |

### Live Chat Field Option Group Object

  Live Chat Field Option Group Object is represented as simple flat JSON objects with the following keys:  

| Name | Type | Read-only | Mandatory | Default | Description |
| - | - | :-: | :-: | :-: | - |
| `name` | string | no | no | | |
| `order` | integer | no | no | | |
| `options` | [Live Chat Field Option](#Live-Chat-Field-Option-Object)[]  | no | no | | |

## Endpoints

### Get all form fields of Pre-Chat for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/preChat/campaignFormFields
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "5062B231-E0D6-AFD3-2E72-4D143792DC03",
    "field": {
      "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
      "isSystem": false,
      "name": "teset",
      "type": "textBox",
      "options": [{
        "value": "test",
        "order": 1,
      },
      ...
      ],
      "leftText": "",
      "rightText": "",
      "optionGroups": [{
        "name": "test",
        "order": 1,
        "options":[]
      },
      ...
      ],
    },
    "isVisible": false,
    "isRequired": false,
    "order": 1,
    "ratingGrades": [{
      "grade": 1,
      "label": "",
      "isVisible": false
    },
    ...
    ]
  },
  ...
]
```

### Create a new form fields of Pre-Chat for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

example:
```Json
{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/preChat/campaignFormFields
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaignFormFields/5062B231-E0D6-AFD3-2E72-4D143792DC03

{
  "id": "5062B231-E0D6-AFD3-2E72-4D143792DC03",
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

### Get all form fields of Post Chat for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/postChat/campaignFormFields
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "8FD2DBE6-4653-1705-F791-F2C648A11FC7",
    "field": {
      "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
      "isSystem": false,
      "name": "teset",
      "type": "textBox",
      "options": [{
        "value": "test",
        "order": 1,
      },
      ...
      ],
      "leftText": "",
      "rightText": "",
      "optionGroups": [{
        "name": "test",
        "order": 1,
        "options":[]
      },
      ...
      ],
    },
    "isVisible": false,
    "isRequired": false,
    "order": 1,
    "ratingGrades": [{
      "grade": 1,
      "label": "",
      "isVisible": false
    },
    ...
    ]
  },
  ...
]
```

### Create a new form fields of Post Chat for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

example:
```Json
{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/postChat/campaignFormFields
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaignFormFields/8FD2DBE6-4653-1705-F791-F2C648A11FC7

{
  "id": "8FD2DBE6-4653-1705-F791-F2C648A11FC7",
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

### Get all form fields of Offline Message for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/offlineMessage/campaignFormFields
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "6BE9D31D-C9C7-0B0B-BC84-89FC948C81BA",
    "field": {
      "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
      "isSystem": false,
      "name": "teset",
      "type": "textBox",
      "options": [{
        "value": "test",
        "order": 1,
      },
      ...
      ],
      "leftText": "",
      "rightText": "",
      "optionGroups": [{
        "name": "test",
        "order": 1,
        "options":[]
      },
      ...
      ],
    },
    "isVisible": false,
    "isRequired": false,
    "order": 1,
    "ratingGrades": [{
      "grade": 1,
      "label": "",
      "isVisible": false
    },
    ...
    ]
  },
  ...
]
```

### Create a new form fields of Offline Message for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

example:
```Json
{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/offlineMessage/campaignFormFields
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaignFormFields/6BE9D31D-C9C7-0B0B-BC84-89FC948C81BA

{
  "id": "6BE9D31D-C9C7-0B0B-BC84-89FC948C81BA",
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

### Get all form fields of Agent Wrap-up for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaigns/CE76FDBC-B451-F4C9-FE00-89360F86E9F9/agentWrapup/campaignFormFields
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "5994A98C-CF88-1B8E-2909-CA81E0C1B469",
    "field": {
      "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
      "isSystem": false,
      "name": "teset",
      "type": "textBox",
      "options": [{
        "value": "test",
        "order": 1,
      },
      ...
      ],
      "leftText": "",
      "rightText": "",
      "optionGroups": [{
        "name": "test",
        "order": 1,
        "options":[]
      },
      ...
      ],
    },
    "isVisible": false,
    "isRequired": false,
    "order": 1,
    "ratingGrades": [{
      "grade": 1,
      "label": "",
      "isVisible": false
    },
    ...
    ]
  },
  ...
]
```

### Create a new form fields of Agent Wrap-up for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

example:
```Json
{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585/agentWrapup/campaignFormFields
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/campaignFormFields/5994A98C-CF88-1B8E-2909-CA81E0C1B469

{
  "id": "5994A98C-CF88-1B8E-2909-CA81E0C1B469",
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

### Get a campaign form field by id

  `GET /api/v3/livechat/campaignFormFields/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the campaign form fields |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/campaignFormFields/A721F271-D59C-2724-23D4-F66418676DD3
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "A721F271-D59C-2724-23D4-F66418676DD3",
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

### Update a campaign form field

  `PUT /api/v3/livechat/campaignFormFields/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the campaign form fields |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

example:
```Json
{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaignFormFields/A721F271-D59C-2724-23D4-F66418676DD3
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "A721F271-D59C-2724-23D4-F66418676DD3",
  "field": {
    "id": "EC8E372B-8456-C902-CD73-E600FD45CFE6",
    "isSystem": false,
    "name": "teset",
    "type": "textBox",
    "options": [{
      "value": "test",
      "order": 1,
    },
    ...
    ],
    "leftText": "",
    "rightText": "",
    "optionGroups": [{
      "name": "test",
      "order": 1,
      "options":[]
    },
    ...
    ],
  },
  "isVisible": false,
  "isRequired": false,
  "order": 1,
  "ratingGrades": [{
    "grade": 1,
    "label": "",
    "isVisible": false
  },
  ...
  ]
}
```

### Delete a campaign form field

  `DELETE /api/v3/livechat/campaignFormFields/{id}`

#### Parameters

Path Parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique Id of the campaign form fields |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/campaignFormFields/A721F271-D59C-2724-23D4-F66418676DD3
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Ban

  You need `Manage Ban List` permission to manage ban list.

- `GET /api/v3/livechat/bans` - [Get a list of bans](#get-site-bans) include visitor, agent
- `GET /api/v3/livechat/bans/{id}` - [Get a ban by id](#get-a-ban) include visitor, agent
- `POST /api/v3/livechat/bans` - [Create a ban](#get-a-ban)
- `PUT /api/v3/livechat/bans/{id}` - [Update a ban](#update-a-ban)
- `DELETE /api/v3/livechat/bans/{id}` - [Delete a ban](#delete-a-ban)

## Related Object Json Format

### Ban JSON Format

  Ban is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `id` | string | | yes | no | | id of the ban. |
| `type` | string | | no | yes | |  type of ban, including `visitor` , `ip` and `ipRange` |
| `visitorId` | Guid | | no | no | | visitor's id of the ban if `type` is `visitor`  |
| `visitor` | [Visitor](#visitor) | yes | no | no | |  Available only when visitor is included  |
| `ip` | string  |  | no | yes | | ip address of the ban if `type` is `ip`, it can be a specific ip `192.168.8.113` |
| `ipRangeFrom` | string | | no | yes | | ip address of the ban if `type` is `ipRange` |
| `ipRangeTo` | string | | no | yes | | ip address of the ban if `type` is `ipRange` |
| `comment` | string | | no | no | | comment of the ban. |
| `lastUpdatedBy` | Guid | | no | no | | comment of the ban. |
| `lastUpdatedAgent` | [Agent](#agent) | yes | no | no | | Available only when agent is included  |

## Endpoint

### Get list of bans

  `GET /api/v3/livechat/bans`

#### Parameters

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `visitor`, `agent` |

#### Response
An array of [Ban](#ban-json-format)

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/bans?include=visitor,agent
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
        "type": "visitor",
        "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7",
        "visitor": {  //include visitor
            "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
            "email": "test@comm100.com",
            "name": "test comm100",
            ...
        },
        "comment": "",
        "lastUpdatedBy": "ae165aad-b561-145b-427c-ba89849ff3c7",
        "lastUpdatedAgent": {  //include agent
            "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
            "email": "test@comm100.com",
            "displayName": "test comm100",
            "firstName": "test",
            "lastName": "comm100",
            ...
        },
    },
    ...
]
```

### Get a single ban

  `GET /api/v3/livechat/bans/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the ban  |

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `visitor`, `agent` |

#### Response

the response is: [Ban](#ban-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/bans/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e?include=visitor,agent
```
Response
```json
{
    "id": "f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e",
    "type": "visitor",
    "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7",
    "visitor": {  //include visitor
        "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
        "email": "test@comm100.com",
        "name": "test comm100",
        ...
    },
    "comment": "",
    "lastUpdatedBy": "ae165aad-b561-145b-427c-ba89849ff3c7",
    "lastUpdatedAgent": {  //include agent
        "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
        "email": "test@comm100.com",
        "displayName": "test comm100",
        "firstName": "test",
        "lastName": "comm100",
        ...
    },
}
```

### Create a new ban

  `POST /api/v3/livechat/bans`

#### Parameters
Request body

  The request body contains data with the [Ban](#ban-json-format) structure

  example:
```Json
  {
    "type": "ip",
    "ip": "192.168.1.1",
    "comment": "block this ip"
  }
```

#### Response
the response is:
[Ban](#ban-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "type": "ip",
    "ip": "192.168.1.1",
    "comment": "block this ip"
  }' -X POST https://domain.comm100.com/api/v3/livechat/bans
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/bans/b222qa68-92e6-4487-a2e8-8234fc9d1f48

{
    "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "type": "ip",
    "ip": "192.168.1.1",
    "comment": "block this ip",
    "lastUpdatedBy": "ae165aad-b561-145b-427c-ba89849ff3c7"
}
```

### Update a ban

  `PUT /api/v3/livechat/bans/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the ban  |

Request body 

  The request body contains data with the [Ban](#ban-json-format) structure

  example:
```Json
  {
    "id": "27c48ac9-2553-4066-bf94-e30957aa390e",
    "type": "ip",
    "ip": "192.168.1.2",
    "comment": ""
  }
```

#### Response
the response is: [Ban](#ban-json-format) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "27c48ac9-2553-4066-bf94-e30957aa390e",
    "type": "ip",
    "ip": "192.168.1.2",
    "comment": ""
  }' -X PUT https://domain.comm100.com/api/v3/livechat/bans/27c48ac9-2553-4066-bf94-e30957aa390e
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
    "id": "27c48ac9-2553-4066-bf94-e30957aa390e",
    "type": "ip",
    "ipAddress": "192.168.1.2",
    "comment": "",
    "lastUpdatedBy": "ae165aad-b561-145b-427c-ba89849ff3c7"
}
```

### Delete a ban

  `DELETE /api/v3/livechat/bans/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the ban  |


#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/bans/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e
```
Response
```json
HTTP/1.1 204 No Content
```

# Conversion Action

  You need `Manage Settings` permission to manage conversion action.

- `GET /api/v3/livechat/conversionActions` - [Get a list of conversion actions](#get-site-campaigns) include agent
- `GET /api/v3/livechat/conversionActions/{id}` - [Get a conversion action by id](#get-a-campaign)  include agent
- `POST /api/v3/livechat/conversionActions` - [Create a conversion action](#get-a-campaign)
- `PUT /api/v3/livechat/conversionActions/{id}` - [Update a conversion action](#update-a-campaign)
- `POST /api/v3/livechat/conversionActions:achieved` - [Make api conversion succesful](#make-api-conversion-succesful)

## Related Object Json Format

### Conversion Action JSON Format

  Conversion Action is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `id` | string | | yes | no | | id of the conversion action. |
| `name` | string | | no | yes |  | name of the conversion action. |
| `isEnable` | boolean | | no | no | | whether the conversion action is enabled or not. |
| `type` | string | | no | no | | type of the conversion action, including `url`, `customVariable` and `api`. |
| `customVariableUsedToDetermineConversion` | string  | | no | no |  | the name of the custom variable, available when `type` is `customVariable`. |
| `operator` | string | | no | no | | including `is`, `beginsWith`, `contains`, `regularExpression`, `isLessThen`, `isMoreThen`, available when `type` is `customVariable` or `url`. |
| `value` | string | | no | no |  | match value of the conversion action, available when `type` is `customVariable` or `url`. |
| `isCaseSensitive` | boolean | | no | no | | whether the conversion action is case sensitive or not, available when `type` is `url`. |
| `isValueAssignedToConversion` | boolean | | no | no |  | whether a value is assigned for the conversion action or not. |
| `valueSource` | string | | no | no |  | including `inputAValue`, `getFromCustomVariable` |
| `assignedValueFromInputting` | string | | no | no |  | the value assigned for the conversion action |
| `assignedValueFromCustomVariable` | string | | no | no |  | the value comes from the custom variable |
| `chatAssociatedWithConversion` | string | | no | no |  | including `theFirstChat`, `theLastChat` |
| `isChatInLastCertainDaysConsidered` | boolean | | no | no |  |  |
| `chatInLastDays` | integer | | no | no |   | between 1 and 30 |
| `isChatWithAtLeastCertainVisitorMessagesConsidered` | boolean | | no | no | |  |
| `visitorMessagesAtLeast` | integer | | no | no | |   |
| `isVariableIncludedInTranscript` | boolean | | no | no |  |  |
| `appendFieldList` | string | | no | no |  |  |
| `createdTime` | datetime | | no | no |  |  |
| `createdBy` | integer | | no | no |  |  |
| `createdAgent` | [Agent](#agent) | yes | no | no | | Available only when agent is included  |
| `lastUpdatedTime` | datetime | | no | no |  | |
| `lastUpdatedBy` | integer | | no | no |  | |
| `lastUpdatedAgent` | [Agent](#agent) | yes | no | no |  | Available only when agent is included |

## Endpoint

### Get list of conversion actions

  `GET /api/v3/livechat/conversionActions`

#### Parameters

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value: `agent` |

#### Response
An array of [Conversion Action](#conversion-action-json-format)

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/conversionActions?include=agent
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "5728600f-0e75-432f-8638-db189f1e4e44",
        "name": "justfortest2",
        "isEnable": false,
        "type": "url",
        "customVariableUsedToDetermineConversion": "",
        "operator": "is",
        "value": "",
        "isCaseSensitive": false,
        "isValueAssignedToConversion": false,
        "valueSource": "inputAValue",
        "assignedValueFromInputting": "https://www.comm100.com",
        "assignedValueFromCustomVariable": "",
        "chatAssociatedWithConversion": "theFirstChat",
        "isChatInLastCertainDaysConsidered": false,
        "chatInLastDays": 3,
        "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
        "visitorMessagesAtLeast": 1,
        "isVariableIncludedInTranscript": false,
        "appendFieldList": "",
        "createdTime": "2020-02-20T13:12:20Z",
        "createdBy": 1,
        "createdAgent": {
            //include agent
            "id": 1,
            "email": "test@comm100.com",
            "displayName": "test comm100",
            "firstName": "test",
            "lastName": "comm100",
            ...
        },
        "lastUpdatedTime": "2020-02-20T13:12:20Z",
        "lastUpdatedBy": 1,
        "lastUpdatedAgent": {
            //include agent
            "id": 1,
            "email": "test@comm100.com",
            "displayName": "test comm100",
            "firstName": "test",
            "lastName": "comm100",
            ...
        }
    },
]
```

### Get a single conversion action

  `GET /api/v3/livechat/conversionActions/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the conversion action  |

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `include` | string | no  | |  Available value:  `agent` |

#### Response

the response is: [Conversion Action](#conversion-action-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/conversionActions/5728600f-0e75-432f-8638-db189f1e4e44?include=agent
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
    "id": "5728600f-0e75-432f-8638-db189f1e4e44",
    "name": "justfortest2",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": "",
    "createdTime": "2020-02-20T13:12:20Z",
    "createdBy": 1,
    "createdAgent": {
        //include agent
        "id": 1,
        "email": "test@comm100.com",
        "displayName": "test comm100",
        "firstName": "test",
        "lastName": "comm100",
        ...
    },
    "lastUpdatedTime": "2020-02-20T13:12:20Z",
    "lastUpdatedBy": 1,
    "lastUpdatedAgent": {
        //include agent
        "id": 1,
        "email": "test@comm100.com",
        "displayName": "test comm100",
        "firstName": "test",
        "lastName": "comm100",
        ...
    }
}
```

### Create a new conversion action

  `POST /api/v3/livechat/conversionActions`

#### Parameters
Request body

  The request body contains data with the [Conversion Action](#conversion-action-json-format) structure

  example:
```Json
{
    "name": "justfortest2",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": ""
}
```

#### Response
the response is:[Conversion Action](#conversion-action-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name": "justfortest2",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": ""
  }' -X POST https://domain.comm100.com/api/v3/livechat/conversionActions
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/conversionActions/b222qa68-92e6-4487-a2e8-8234fc9d1f48

{
    "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "justfortest2",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": "",
    "createdTime": "2020-02-20T13:12:20Z",
    "createdBy": 1,
    "lastUpdatedTime": "2020-02-20T13:12:20Z",
    "lastUpdatedBy": 1
}
```

### Update a conversion action

  `PUT /api/v3/livechat/conversionActions/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the conversion action  |

Request body 

  The request body contains data with the [Conversion Action](#conversion-action-json-format) structure

  example:
```Json
  {
    "id": "60a555fd-b5db-40ac-9043-57fcee181f78",
    "name": "justfortest",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": ""
  }
```

#### Response
the response is: [Conversion Action](#conversion-action-json-format) Object


#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "60a555fd-b5db-40ac-9043-57fcee181f78",
    "name": "justfortest",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": ""
  }' -X PUT https://domain.comm100.com/api/v3/livechat/conversionActions/60a555fd-b5db-40ac-9043-57fcee181f78
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
    "id": "60a555fd-b5db-40ac-9043-57fcee181f78",
    "name": "justfortest",
    "isEnable": false,
    "type": "url",
    "customVariableUsedToDetermineConversion": "",
    "operator": "is",
    "value": "",
    "isCaseSensitive": false,
    "isValueAssignedToConversion": false,
    "valueSource": "inputAValue",
    "assignedValueFromInputting": "https://www.comm100.com",
    "assignedValueFromCustomVariable": "",
    "chatAssociatedWithConversion": "theFirstChat",
    "isChatInLastCertainDaysConsidered": false,
    "chatInLastDays": 3,
    "isChatWithAtLeastCertainVisitorMessagesConsidered": false,
    "visitorMessagesAtLeast": 1,
    "isVariableIncludedInTranscript": false,
    "appendFieldList": "",
    "createdTime": "2020-02-20T13:12:20Z",
    "createdBy": 1,
    "lastUpdatedTime": "2020-02-20T14:12:20Z",
    "lastUpdatedBy": 1
}
```

### make api conversion succesful

  `POST /api/v3/livechat/conversionActions:achieved`

#### Parameters
Request body

The request body contains data with the follow structure:

| Name | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `conversion_name` | string | yes | |  name of the conversion action. |
| `visitorId` | string | yes |  | |
| `value` | string  | no |  |  the name of the custom variable, available when conversion action `type` is `customVariable`. |

example:
```Json 
  {
    "conversion_name" : "justfortestupdate", 
    "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7", "value": "test"
  }
```

#### Response
The response body contains data with the follow structure:

| Name | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `code` | string | no | no |  0: ok; 1: the conversion name does not exist; 2: the visitorId does not exist; 3: error adding conversion-related Data to system. |
| `message` | string | no | no | error message. |

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "conversion_name" : "justfortestupdate", 
    "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7", "value": "test"
  }' -X POST https://domain.comm100.com/api/v3/livechat/conversionActions:achieved
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "code": 0,
    "message": "ok",
}
```

# Secure Form

- `GET /api/v3/livechat/secureForms` - [Get a list of secureForms](#get-list-of-secure-forms)
- `GET /api/v3/livechat/secureForms/{id}` - [Get a secure form by id](#get-a-secure-form)
- `POST /api/v3/livechat/secureForms` - [Create a secure form](#get-a-secure-form)
- `PUT /api/v3/livechat/secureForms/{id}` - [Update a secure form](#update-a-secure-form)
- `DELETE /api/v3/livechat/secureForms/{id}` - [Delete a secure form](#delete-a-secure-form)

## Related Object Json Format
### Secure Form JSON Format

Secure Form is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `id` | string  | | yes | no | | id of the secure form. |
| `name` | string  | | no | yes | | name of the secure form. |
| `description` | string |  | no | no | |description of the secure form. |
| `fields` | [Secure Form Field](#secure-form-field-json-format)[] | | no | no | | an array of [Field](#field-json-format) |

## Endpoint
### Get list of secure forms

  `GET /api/v3/livechat/secureForms`

#### Parameters

    No parameters

#### Response
An array of [Secure Form](#secure-form-json-format)

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/secureForms
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "5721c1ac-f18b-43ed-9ff1-597acd9f48e2",
        "name": "justfortest",
        "description": "",
        "fields": [
            {
                "id": "24fc507d-55b8-4a9c-9bb1-684ee7ad3770",
                "name": "Card Number",
                "type": "cardNumber",
                "displayName": "Card Number",
                "isSystem": true,
                "isVisible": false,
                "isRequired": false,
                "order": 1
            },
            ...
        ]
    },
    ...
]
```

### Get a single secure form

  `GET /api/v3/livechat/secureForms/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the secure form  |

#### Response

the response is: [Secure Form](#secure-form-json-format) Object


#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/secureforms/5721c1ac-f18b-43ed-9ff1-597acd9f48e2
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
    "id": "5721c1ac-f18b-43ed-9ff1-597acd9f48e2",
    "name": "justfortest2",
    "description": "",
    "fields": [
        {
            "id": "24fc507d-55b8-4a9c-9bb1-684ee7ad3770",
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        ...
    ]
}
```

### Create a new secure form

  `POST /api/v3/livechat/secureForms`

#### Parameters
Request body

  The request body contains data with the [Secure Form](#secure-form-json-format) structure

  example:
```Json
  {
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        ...
    ]
  }
```

#### Response
the response is:
[Secure Form](#secure-form-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        ...
    ]
  }' -X POST https://domain.comm100.com/api/v3/livechat/secureForms
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/secureForms/b222qa68-92e6-4487-a2e8-8234fc9d1f48

{
    "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            "id": "1222qa68-92e6-4487-a2e8-8234fc9d1f48",
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        ...
    ]
}
```

### Update a secure form

  `PUT /api/v3/livechat/secureForms/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the secure form  |

Request body

  The request body contains data with the [Secure Form](#secure-form-json-format) structure

  example:
```Json
  {
    "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            //update
            "id": "1222qa68-92e6-4487-a2e8-8234fc9d1f48",
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        {
            //create
            "type":"dropDownList",
            "name":"city",
            "displayName": "City",
            "isRequired":true,
            "isSystem": false,
            "isVisible": true,
            "options":[
              {
                "value": "beijing",
                "order":0,
              },
              {
                "value": "hangzhou",
                "order":1,
              }],
            "order": 2
        }
    ]
  }
```

#### Response
the response is:
[Secure Form](#secure-form-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            //update
            "id": "1222qa68-92e6-4487-a2e8-8234fc9d1f48",
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        {
            //create
            "type":"dropDownList",
            "name":"city",
            "displayName": "City",
            "isRequired":true,
            "isSystem": false,
            "isVisible": true,
            "options":[
              {
                "value": "beijing",
                "order":0,
              },
              {
                "value": "hangzhou",
                "order":1,
              }],
            "order": 2
        }
    ]
  }' -X PUT https://domain.comm100.com/api/v3/livechat/secureForms/b222qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

  {
    "id": "b222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            "id": "1222qa68-92e6-4487-a2e8-8234fc9d1f48",
            "name": "Card Number",
            "displayName": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "order": 1
        },
        {
            "id": "vc21qa68-92e6-4487-a2e8-8234fc9d1f48",
            "type":"dropDownList",
            "name":"city",
            "displayName": "City",
            "isRequired":true,
            "isSystem": false,
            "isVisible": true,
            "options":[
              {
                "value": "beijing",
                "order":0,
              },
              {
                "value": "hangzhou",
                "order":1,
              }],
            "order": 2
        }
    ]
  }
```

### Remove a secure form

  `DELETE /api/v3/livechat/secureForms/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the secure form  |


#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/secureForms/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e
```
Response
```json
HTTP/1.1 204 No Content
```

# Secure Form Field

- `GET /api/v3/livechat/secureForms/{secureFormId}/secureFormFields` - [Get a list of secureFormFields](#get-list-of-secure-form-fields)
- `GET /api/v3/livechat/secureFormFields/{id}` - [Get a secure form field by id](#get-a-secure-form-field)
- `POST /api/v3/livechat/secureForms/{secureFormId}/secureFormFields` - [Create a secure form field](#ceate-a-secure-form-field)
- `PUT /api/v3/livechat/secureFormFields/{id}` - [Update a secure form field](#update-a-secure-form-field)
- `DELETE /api/v3/livechat/secureFormFields/{id}` - [Delete a secure form field](#delete-a-secure-form-field)

## Related Object Json Format
### Secure Form Field JSON Format

  Secure Form Field is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only | Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `id` | string | | yes | no | | id of the field |
| `name` | string | | no | yes | | name of the field |
| `displayName` | string | | no | yes | | name of the field |
| `type` | string | | no | yes | | including `text`, `textArea`, `radioBox`, `checkbox`, `dropdownList`, `checkboxList`, `datePicker` |
| `isSystem` | boolean | | yes | no | false | whether the field is system field or not. |
| `isVisible` | boolean | | no | no | false | whether the field is visible or not. |
| `isRequired` | boolean | | no | no | false | whether the field is required or not when submitting the form |
| `order` | integer | | no | no |1  | the order of the field. |
| `options` | string |  | no | no | | the options of the field. |

## Endpoint
### Get list of secure form fields

  `GET /api/v3/livechat/secureForms/{secureFormId}/secureFormFields`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `secureFormId` | Guid | yes  |  the id of the secure form  |


#### Response
An array of [Secure Form Field](#secure-form-field-json-format)

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/secureForms/5721c1ac-f18b-43ed-9ff1-597acd9f48e2/secureFormFields
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "1222qa68-92e6-4487-a2e8-8234fc9d1f48",
        "name": "Card Number",
        "displayName": "Card Number",
        "type": "cardNumber",
        "isSystem": true,
        "isVisible": false,
        "isRequired": false,
        "order": 1
    },
    {
        "id": "vc21qa68-92e6-4487-a2e8-8234fc9d1f48",
        "type":"dropDownList",
        "name":"city",
        "displayName": "City",
        "isRequired":true,
        "isSystem": false,
        "isVisible": true,
        "options":[
            {
            "value": "beijing",
            "order":0,
            },
            {
            "value": "hangzhou",
            "order":1,
            }],
        "order": 2
    }
]
```

### Get a single secure form field

  `GET /api/v3/livechat/secureFormFields/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the secure form field |

#### Response

the response is: [Secure Form Field](#secure-form-field-json-format) Object


#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/secureFormFields/vc21qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
    "id": "vc21qa68-92e6-4487-a2e8-8234fc9d1f48",
    "type":"dropDownList",
    "name":"city",
    "displayName": "City",
    "isRequired":true,
    "isSystem": false,
    "isVisible": true,
    "options":[
        {
        "value": "beijing",
        "order":0,
        },
        {
        "value": "hangzhou",
        "order":1,
        }],
    "order": 2
}
```

### Create a new secure form field

  `POST /api/v3/livechat/secureForms/{secureFormId}/secureFormFields`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `secureFormId` | Guid | yes  |  the id of the secure form  |

Request body

  The request body contains data with the [Secure Form Field](#secure-form-field-json-format) structure

  example:
```Json
  {
    "name": "Card Number",
    "displayName": "Card Number",
    "type": "cardNumber",
    "isSystem": true,
    "isVisible": false,
    "isRequired": false,
    "order": 1     
  }
```

#### Response
the response is:
[Secure Form Field](#secure-form-field-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "name": "Card Number",
    "displayName": "Card Number",
    "type": "cardNumber",
    "isSystem": true,
    "isVisible": false,
    "isRequired": false,
    "order": 1 
  }' -X POST https://domain.comm100.com/api/v3/livechat/secureForms/b222qa68-92e6-4487-a2e8-8234fc9d1f48/secureFormFields
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/secureFormFields/3222qa68-92e6-4487-a2e8-8234fc9d1f48

{
    "id": "3222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Card Number",
    "displayName": "Card Number",
    "type": "cardNumber",
    "isSystem": true,
    "isVisible": false,
    "isRequired": false,
    "order": 1
}
```

### Update a secure form field

  `PUT /api/v3/livechat/secureFormFields/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the secure form field  |

Request body

  The request body contains data with the [Secure Form Field](#secure-form-field-json-format) structure

  example:
```Json
  {
    "id": "3222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Card Number",
    "displayName": "Card Number",
    "type": "cardNumber",
    "isSystem": true,
    "isVisible": false,
    "isRequired": false,
    "order": 1
  }
```

#### Response
the response is:
[Secure Form Field](#secure-form-field-json-format) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "3222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Card Number",
    "displayName": "Card Number",
    "type": "cardNumber",
    "isSystem": true,
    "isVisible": false,
    "isRequired": false,
    "order": 1
  }' -X PUT https://domain.comm100.com/api/v3/livechat/secureFormFields/3222qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json

  {
    "id": "3222qa68-92e6-4487-a2e8-8234fc9d1f48",
    "name": "Card Number",
    "displayName": "Card Number",
    "type": "cardNumber",
    "isSystem": true,
    "isVisible": false,
    "isRequired": false,
    "order": 1
  }
```

### Remove a secure form field

  `DELETE /api/v3/livechat/secureFormFields/{id}`

#### Parameters
Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the id of the secure form field |


#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/livechat/secureFormFields/f2d45dad-a7c3-4b7b-ba1c-bc9eaea34f8e
```
Response
```json
HTTP/1.1 204 No Content
```

# Webhook

+ `GET /api/v3/livechat/webhooks` - [Get a list of webhooks](#get-a-list-of-webhooks)
+ `GET /api/v3/livechat/webhooks/{id}` - [Get a webhook by id](#get-a-webhook-by-id)
+ `POST /api/v3/livechat/webhooks` - [Create a webhook](#create-a-webhook)
+ `PUT /api/v3/livechat/webhooks/{id}` - [Update a webhook](#update-a-webhook) 
+ `DELETE /api/v3/livechat/webhooks/{id}` - [Delete a webhook](#delete-a-webhook)

## Webhook Related Objects Json Format

### Webhook Object

  Webhook is represented as simple flat JSON objects with the following keys:

| Name | Type | Include | Read-only| Mandatory| Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `id` | guid  || yes | no | | id of the webhook |
| `event` | string  || no | yes | | event of webhook, including `offlineMessageSubmitted`, , `agentStatusChanges`,`chatStarts`, `chatEnds`, `chatWrappedUp`, `chatRequested` and `chatTransferred`. |
| `targetUrl` | string  || no | yes | | target url of the webhook. |

## Endpoints

### Get a list of webhooks

  `GET /api/v3/livechat/webhooks`

#### Parameters

    No parameters

#### Response

the response is: An array of [Webhook](#webhook-object)

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/webhooks
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "event": "chatWrappedUp",
    "targetUrl": "http://www.google.com"
  },
  ...
]
```

### Get a webhook by id

  `GET /api/v3/livechat/webhooks/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of the webhook  |

#### Response

the response is: [Webhook](#webhook-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "event": "chatWrappedUp",
  "targetUrl": "http://www.aa.com"
}
```

### Create a webhook

  `POST /api/v3/livechat/webhooks`

#### Parameters

Request body

  The request body contains data with the [Webhook](#webhook-object) structure

example:
```Json
{
  "event": "chatWrappedUp",
  "targetUrl": "http://www.aa.com"
}
  
```

#### Response
the response is: [Webhook](#webhook-object) Object.

### Example

Using curl:

```shell
curl -H "Content-Type: application/json" -d '{
  "event": "chatWrappedUp",
  "targetUrl": "http://www.aa.com"
}' -X POST https://domain.comm100.com/api/v3/livechat/webhooks
```

Sample response:

```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "event": "chatWrappedUp",
  "targetUrl": "https://www.google.com"
}
```

### Update a webhook

  `PUT /api/v3/livechat/webhooks/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  the unique id of the webhook|

Request body

  The request body contains data with the [Webhook](#webhook-object) structure

example:
```Json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "event": "chatWrappedUp",
  "targetUrl": "https://www.google.com"
}
```

#### Response
the response is: [Webhook](#webhook-object) Object.

#### Example

Using curl:

```shell
curl -H "Content-Type: application/json" -d '{
  "event": "chatWrappedUp",
  "targetUrl": "http://www.aa.com"
}' -X PUSThttps://domain.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6"
  "event": "chatWrappedUp",
  "targetUrl": "http://www.google.com"
}
```

#### delete a webhook

  `DELETE /api/v3/livechat/webhooks/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of the webhook  |

#### Response
HTTP/1.1 204 No Content

#### Example

Using curl:

```shell
curl  -X DELETE  https://domain.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Custom Variable

- `GET /api/v3/livechat/customVariables` - [Get a list of custom variables](#get-a-list-of-custom-variables)
- `GET /api/v3/livechat/campacustomVariables/{id}` - [Get a custom variable by id](#get-a-custom-variable-by-id)
- `POST /api/v3/livechat/customVariables` - [Create a custom variable](#create-a-custom-variable)
- `PUT /api/v3/livechat/customVariables/{id}` - [Update a custom variable](#update-a-custom-variable)
- `DELETE /api/v3/livechat/customVariables/{id}` - [Delete a custom variable](#delete-a-custom-variable)

## Custom Variable Related Objects Json Format

### Custom Variable Object

Custom Variable is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read| Mandatory | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `id` | Guid  || yes | no || id of the custom variable. |
  | `name` | string  || no | yes || name of the custom variable |.
  | `type` | string  || no | yes || type of the custom variable., including `text`, `integer` and `decimal`. |
  | `value` | string  || no | no || value of the custom variable. |
  |`hyperlink` | string  || no | no ||  hyperlink of the custom variable. |

## Endpoints

### Get a list of Custom Variables

  `GET /api/v3/livechat/customVariables`

#### Parameters

    No parameters

#### Response

the response is: An array of [Custom Variable](#custom-variable-object) Object.

### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/customvariables
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
[
  {
    "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "name": "test",
    "type": "text",
    "value": "'lizz'",
    "hyperlink": "{!Visitor.IP}"
  },
  ...
]
```

### Get a custom variable by id

  `GET /api/v3/livechat/customVariables/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of the custom variable  |

#### Response

the response is: [Custom Variable](#custom-variable-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/livechat/customvariables/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
}
```

### Create a custom variable

  `POST /api/v3/livechat/customVariables`

#### Parameters

Request body

The request body contains data with the [Custom Variable](#custom-variable-object) structure

example:
```Json
{
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
}
```

#### Response

the response is: [Custom Variable](#custom-variable-object) Object.

#### Example

Using curl
```shell
curl -H "Content-Type: application/json" -d '"name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"' -X POST  https://domain.comm100.com/api/v3/livechat/customvariables
```

Response
```Json
HTTP/1.1 201 Created
Location: https://domain.comm100.com/api/v3/livechat/customvariables/1487fc9d-92e6-4487-a2e8-92e68d6892e6
Content-Type:  application/json

{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
}
```

### Update a Custom Variable

  `PUT /api/v3/livechat/customVariables/{id}`

#### Parameters

Path parameters
| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of the custom variable  |

Request body

The request body contains data with the [Custom Variable](#custom-variable-object) structure

example:
```Json
{
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
}
```

#### Response

the response is: [Custom Variable](#custom-variable-object) Object.

#### Example

Using curl:

Using curl
```shell
curl -H "Content-Type: application/json" -d '{
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
  }' -X PUT https://domain.comm100.com/api/v3/livechat/customvariables
```

Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
}
```

###  Delete a custom variable

  `DELETE /api/v3/livechat/customVariables/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
| `id` | Guid | yes  |  id of the custom variable  |

#### Response

HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -H -X DELETE https://domain.comm100.com/api/v3/livechat/customvariables/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```json
HTTP/1.1 204 No Content
```
</div>
