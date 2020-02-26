# Live Chat Restful API

Comm100 Live Chat API allows you to pull the raw livechat data from Comm100 Live Chat into your own systems.

  | Change Version | API Version | Change note | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v3 |  | 2020-02-17 | Michael |

# Summary

- Live Chat
  - [live chat settings](#live-chat-settings)
    - [auto distribution](#auto-distribution)
    - [translation excluded word](#translation-excluded-word)
    - [dynamic campaign](#dynamic-campaign)
      - [dynamic campaign rule](#dynamic-campaign-rule)
    - [mobile push](#mobile-push)
  - [customer segment](#customer-segment)
  - [session](#session)  
  - [chat](#chat)
  - [offline message](#offline-message)  
  - [campaign](#campaign)
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

- `GET /api/v3/livechat/settings` - [Get settings of a site](#get-settings)
- `PUT /api/v3/livechat/settings` - [Update settings of a site](#update-settings)

## Settings Related Objects Json Format

### Setting Object

Customer Segment is represented as simple flat JSON objects with the following keys:  

| Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - | 
 | `siteId` |integer  || yes | N/A || id of the site which the configuration belongs to.
 | `isMultipleCampaignEnabled` |boolean || no | N/A || whether multiple campaigns are enabled or not in the site.
 | `isAutoDistributionEnabled` |boolean || no | N/A || whether auto distribution is enabled or not in the site.
 | `isCustomAwayStatusEnabled` |boolean || no | N/A || whether custom away status is enabled or not in the site.
 | `isDepartmentEnabled` |boolean || no  N/A || whether department is enabled or not in the site.
 | `isAutoTranslationEnabled` |boolbean || no | N/A || whether auto translation is enabled or not in the site.
 | `isAudioAndVideoChatEnabled` |boolbean || no | N/A ||whether audio&video chat is enabled or not in the site.
 | `iscustomerSegmentEnabled` |boolbean || no | N/A ||whether customer segment chat is enabled or not in the site.
 | `isVisitorSSOtEnabled` |boolbean || no | N/A ||whether vistor SSO is enabled or not in the site.
 | `isCreditCardMaskingEnabled` |boolbean || no | N/A ||whether Credit card masking is enabled or not in the site.
 | `isCustomVariablesEnabled` |boolbean || no | N/A ||whether custom variables are enabled or not in the site.
 | `isSalesforceEnabled` |boolbean || no | N/A ||whether Salesforce integration is enabled or not in the site.
 | `isZendeskEnabled` |boolbean || no | N/A ||whether Zendesk integration is enabled or not in the site.
 | `isGoogleAnalyticsEnabled` |boolbean || no | N/A || whether Google Analytics integration is enabled or not in the site.
 | `isGotoMeetingEnabled` |boolbean || no | N/A || whether GotoMeeting integration is enabled or not in the site.
 | `isJoinmeEnabled` |boolbean || no | N/A || whether Joinme integration is enabled or not in the site.

## Endpoint

### Get settings of a site

  `GET /api/v3/livechat/settings`

#### Parameter

    No parameters

#### Response

the response is [Settings](#settings-object) object

####  Example

Using curl
```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/livechatwebapi/api/v2/livechat/configs
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
    "isJoinmeEnabled": true
}
```

### Update settings of a site

  `PUT /api/v3/livechat/settings`

#### Parameters

    No parameters

#### Response

the response is [Settings](#settings-object) object

### Example

Using curl
```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X PUT -d "siteid=6000000&isenablesalesforce=true"  https://hosted.comm100.com/api/v3/livechat/settings
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
    "isJoinmeEnabled": true
}
```
  
# Auto Distribution

- `GET /api/v3/livechat/autoDistribution` - [Get auto distribution](#get-auto-distribution)  include department, agent
- `PUT /api/v3/livechat/autoDistribution` - [Update livechat auto distribution of a site](#update-site-info)

## Auto Distribution Related Objects Json Format

### Auto Distribution Object

  Auto Distribution is represented as simple flat JSON objects with the following keys:

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - |
  | `autoDistributionMethod` | string || no | N/A | method of auto distribution, including `load banlancing` , `round robin` and `capability weighted` |
  | `isLastChattedAgentPreferred` | boolean || no | N/A | whether last-chatted agent is preferred or not |
  | `isLimitMaxConcurrentChatsForAllAgents` | boolean || no | N/A | whether to set the same maximum number of chats for all agents |
  | `maxConcurrentChatsForAllAgents` | integer || no | N/A | maximum number of chats for all agents |
  | `ifAutoAcceptChatWhenHavingAudioVideoChat` | boolean || no | N/A| whether to allocate chats to agents who are having audio or video chats |
  | `ifAgentCanManuallyAcceptChatsAfterReachingMaxChatsLimit` | boolean || no | N/A | whether to allow agent to manually accept chat after reaching max chats limit in agent console |
  | `departmentAutoDistributions` | [Department Auto Distribution](#department-auto-distribution-object)[] || no | N/A | auto distribution configuration for per department |
  | `agentAutoDistributions` | [Agent Auto Distribution](#agent-auto-distribution-object)[] || no | N/A | auto distribution configuration for per agent |
  
### Department Auto Distribution Object

Department Auto Distribution Object is represented as simple flat JSON objects with the following keys:
| Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
| - | - | - | :-: | :-: | :-: | - |
| `departmentId` | Guid ||  no| yes|| id of department |
| `department` | [Department](#department-object) ||  N/A| N/A|| related department object |
| `isLastChattedAgentPreferred` | boolean||  no| no| yes | id of department |


### Agent Auto Distribution Object

### Endpoint

#### Get auto allocation configuration

  `GET /api/v2/livechat/autoAllocation`

- Parameters:

    No Parameters

- Response:

    [Auto Allocation](#auto-allocation-json-format)

### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/livechatwebapi/api/v2/livechat/autoallocation
```

Sample response:

```json
{
    "isEnable": true,
    "allocationRule": "load balancing",
    "isLastChattedPreferred": true,
    "isAllocateChatWhenAgentInAudioVideo": false,
    "isMaxChatForAllAgents": true,
    "maxChatForAllAgents": 3,
    "isAllowAgentManualAcceptChat": true
}
```

#### Update auto allocation configuration

  `PUT /api/v2/livechat/autoAllocation`

- Parameters:

    [Auto Allocation](#auto-allocation-json-format)

- Response:

    [Auto Allocation](#auto-allocation-json-format)

### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X PUT -d "isenable=false"  https://hosted.comm100.com/livechatwebapi/api/v2/livechat/autoallocation
```

Sample response:

```json
{
    "isEnable": false,
    "allocationRule": "load balancing",
    "isLastChattedPreferred": true,
    "isAllocateChatWhenAgentInAudioVideo": false,
    "isMaxChatForAllAgents": true,
    "maxChatForAllAgents": 3,
    "isAllowAgentManualAcceptChat": true
}
```


# Translation Excluded Word

- `GET /api/v3/livechat/translationExcludedWords` - [Get a list of translation excluded words](#get-site-info)
- `GET /api/v3/livechat/translationExcludedWords/{id}` - [Get a translation excluded word by id](#get-site-info)
- `POST /api/v3/livechat/translationExcludedWords` - [Create a translation excluded word](#get-site-info)
- `PUT /api/v3/livechat/translationExcludedWords/{id}` - [Update a translation excluded word](#update-site-info)
- `DELETE /api/v3/livechat/translationExcludedWords/{id}` - [Delete a translation excluded word](#delete-a-customer-segment)
  
# Customer Segment

- `GET /api/v3/livechat/customerSegments` - [Get a list of customer segments](#get-list-of-customer-segments)
- `GET /api/v3/livechat/customerSegments/{id}` - [Get a customer segment by id](#get-a-cusomer-segment-by-id)
- `POST /api/v3/livechat/customerSegments` - [Create a customer segment](#create-a-customer-segment)
- `PUT /api/v3/livechat/customerSegments/{id}` - [Update a customer segment](#update-a-info-customer-segment)
- `DELETE /api/v3/livechat/customerSegments/{id}` - [Delete a customer segment](#delete-a-customer-segment)

## Customer Segment Related Objects Json Format

### Customer Segment Object

Customer Segment is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - | 
  | `id` |Guid  || yes | N/A || id of the customer segment.
  | `name` |string  || no | yes || name of the customer segment.
  | `color` |string  || no | no |'339FD9'| color of the customer segment
  | `isEnable` |boolean  || no | no |false| whether the customer segment is enabled or not.
  | `order` |int  || no | yes |maximum order + 1 | order of the customer segment.
  | `description` |string  || no | no || description of the customer segment.
  | `condition met type` |string  || no | no |all| met type of condtion , including `all`,`any`,`logicalExpression`.
  | `logical expression` |string  || no | no || the logical expression for conditions.
  | `conditions` |[Live Chat Condition](#conditions-json-format)[]  || no | yes || an array of [Live Chat Condition](#conditions-json-format) object. |
  | `alertTo`?? | [Department](#department)[] or [Agent](#Agent)[]  || no | no | |

### Live Chat Condition object

Live Chat Condition is represented as simple flat JSON objects with the following keys:  
  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `field` |String  | no | yes || the name of visitor field.
  | `Operator` |String  | no | yes || type of operator, including `is`,`isNot`,`contains`,`doesNotContain`,`isMoreThan`, `isNotMoreThan`, `isLessThan`, `isNotLessThan`, `regularExpression`
  | `value` |String  | no | yes || the value of a visitor field .
  | `order` |String  | no | no|maximum order + 1| the order of visitor field.

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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/api/v3/livechat/customerSegments
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
            ]
        "alertTo":[]
    },
    ...
]
```

### Get a customer segment by id

  `GET /api/v3/livechat/customerSegments/{id}`

#### Parameters

    No parameters

#### Response

the response is: [customer segment](#customer-segment-object) Object.

#### Example

Using curl
```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/api/v3/livechat/customerSegments//1487fc9d-92e6-4487-a2e8-92e68d6892e6
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
  "alertTo":[]
}
```

### Create a customer segment

  `POST /api/v3/livechat/customerSegments`

#### Parameters

Request body
  
  The request body contains data with the [customer segment](#custimer-segment) structure

example:
```Json
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
  "alertTo":[]
}
```

#### Response

the response is: [customer segment](#customer-segment-object) Object.

#### Example

Using curl
```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X POST -d "name=justfortest"  https://hosted.comm100.com/livechatwebapi/api/v2/livechat/visitorsegmentations
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
  "alertTo":[]
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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X PUT -d "name=justfortestupdate"  https://hosted.comm100.com/api/v3/livechat/customerSegments/1487fc9d-92e6-4487-a2e8-92e68d6892e6
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
  "alertTo":[]
```

#### Delete a customer segment

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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X DELETE  https://hosted.comm100.com/api/v3/livechat/visitorsegmentations/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```json
HTTP/1.1 204 No Content
```

# Dynamic Campaign

- `GET /api/v3/livechat/dynamicCampaign` - [Get livechat dynamic campaign of a site](#get-site-info) include campaign
- `PUT /api/v3/livechat/dynamicCampaign` - [Update livechat dynamic campaign of a site](#update-site-info)

- `GET /api/v3/livechat/liveChatSettings/dynamicCampaign` - [Get livechat dynamic campaign of a site](#get-site-info) include campaign
- `PUT /api/v3/livechat/liveChatSettings/dynamicCampaign` - [Update livechat dynamic campaign of a site](#update-site-info)

# Mobile Push

- `GET /api/v3/livechat/mobilePush` - [Get livechat mobile push profile of a site](#get-site-info)
- `PUT /api/v3/livechat/mobilePush` - [Update livechat mobile push profile of a site](#update-site-info)

# Online Agent  

//修改ER
//todo

- `GET /api/v3/livechat/agents` - [Get a list of agents in livechat](#get-all-agents)
- `GET /api/v3/livechat/agents/{id}` - [Get an agent by id](#get-an-agent)  
- `PUT /api/v3/livechat/agents/{id}` - [Update an agent](#update-an-agent)  

# Agent Chat
//修改ER
- `GET /api/v3/livechat/agentChats` - [Get a list of agent chats](#get-site-campaigns)
- `GET /api/v3/livechat/agentChats/{id}` - [Get an agent chat by id](#get-a-campaign)  

# Online Visitor  

//修改ER
//todo

- `GET /api/v3/livechat/visitors` - [Get a list of visitors in livechat](#get-all-visitors)
- `GET /api/v3/livechat/visitors/{id}` - [Get a visitor by id](#get-a-visitor)  
- `POST /api/v3/livechat/visitors/{id}/customVariables` - [update a visitor's custom variables](#update-a-visitor-custom-variables)

# Session 

- `GET /api/v3/livechat/sessions/{id}` - [Get a session by id](#get-a-session-by-id) include visitor, contact

## Related Object Json Format
### Session JSON format

 Session is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `id` | string |  | N/A | N/A | | id of the session. |
  | `startTime` | datetime | | N/A | N/A |  | time of this session start. |
  | `ip` | string |  | N/A | N/A | |  |
  | `referrerURL` | string |  | N/A | N/A | | The rest part of URL will be abandoned if the URL is too long. |
  | `searchEngine` | string |  | N/A | N/A | |  |
  | `keywords` | string |  | N/A | N/A | |  |
  | `browser` | string | | N/A | N/A | |  |
  | `flashVersion` | string |  | N/A | N/A | |  |
  | `language` | string |  | N/A | N/A | |  |
  | `screenResolution` | string |  | N/A | N/A | |  |
  | `operatingSystem` | integer |  | N/A | N/A | |  |
  | `timeZone` | string |  | N/A | N/A | |  |
  | `landingPageURL` | string |  | N/A | N/A | |  |
  | `landingPageTitle` | string | | N/A | N/A | |  |
  | `visitorId` | Guid | | N/A | N/A | | the id of the visitor |
  | `visitor` | [Visitor](#visitor) | yes | N/A | N/A | | Available only when visitor is included  |
  | `contactId` | Guid | | N/A | N/A | | the id of the contact  |
  | `contact` | [Contact](#contact) | yes | N/A | N/A | | Available only when contact is included  |

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
//chat对象 sessionId
- `GET /api/v3/livechat/chats` - [Get a list of chats](#get-site-campaigns) include department,agent , chatbot, campaign,autoInvitation, session
- `GET /api/v3/livechat/chats/{id}` - [Get a chat by id](#get-a-campaign)  include department,agent , chatbot, campaign,autoInvitation
- `DELETE /api/v3/livechat/chats/{id}` - [Delete a chat by id](#get-a-campaign)
- `DELETE /api/v3/livechat/chats` - [Batch Delete chats](#get-a-campaign)

# Offline Message
- `GET /api/v3/livechat/offlineMessages` - [Get a list of offline messages](#get-a-list-of-offline-messages)  include department,agent, campaign,autoInvitation, session
- `GET /api/v3/livechat/offlineMessages/{id}` - [Get an offline message by id](#get-an-offline-message-by-id)  include department,agent, campaign,autoInvitation, session
- `DELETE /api/v3/livechat/offlineMessages/{id}` - [Delete an offline message by id](#delete-an-offline-message-by-id)
- `DELETE /api/v3/livechat/offlineMessages` - [Batch delete offline messages](#batch-delete-offline-messages)

## Related Object Json Format

### Offline Message JSON format

 Offline Message is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `id` | string |  | N/A | N/A | | id of the offline message. |
  | `createdTime` | datetime | | N/A | N/A | | time of this offline message submitted. |
  | `name` | string | | N/A | N/A |  | name of the visitor |
  | `email` | string | | N/A | N/A |  | email of the visitor |
  | `phone` | string | | N/A | N/A |  | phone of the visitor |
  | `company` | string | | N/A | N/A |  | company of the visitor |
  | `departmentId` | Guid | | N/A | N/A |  | The Department which the Offline Message belongs to |
  | `department` | [Department](#department) | yes | N/A | N/A |  | Available only when department is included |
  | `agentId` | Guid | | N/A | N/A |  | The Agent whom the Offline Message belongs to |
  | `agent` | [Agent](#agent) | yes | N/A | N/A |  | Available only when agent is included |
  | `ticketId` | integer | | N/A | N/A |  |  |
  | `subject` | string | | N/A | N/A |  | the subject of this offline message|
  | `message` | string | | N/A | N/A | | the content of this offline message |
  | `requestingPageTitle` | string | | N/A | N/A |  |  |
  | `requestingPageURL` | string | | N/A | N/A |  |  |
  | `source` | string | | N/A | N/A |  | including `chatButton` and `autoInvitation` |
  | `autoInvitationId` | Guid | | N/A | N/A |  | Available when source is `autoInvitation` |
  | `autoInvitation` | [Auto Invitation](#auto-invitation) | yes | N/A | N/A |  | Available only when autoInvitation is included |
  | `campaignId` | Guid | | N/A | N/A |  | id of the campaign |
  | `campaign` | [Campaign](#campaign) | yes | N/A | N/A |  | Available only when campaign is included |
  | `sessionId` | Guid | | N/A | N/A |  | id of the session |
  | `session` | [Session](#session) | yes | N/A | N/A |  | Available only when session is included |
  | `customerSegments` | [Customer Segment](#customer-segment)[] | | N/A | N/A |  | an array of [Customer Segment](#customer-segment) |
  | `fieldValues` | [Field Value](#field-value-json-format)[] | | N/A | N/A |  | values of custom fields entered by visitors in the offline message window. An array of [Field Value](#field-value-json-format). |
  | `attachment` | byte[] | | N/A | N/A |  | the attachment file data |
  | `attachmentName` | string | | N/A | N/A |  | the attachment file name |

### Field Value JSON format

 Field Value is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `fieldName` | string |  | N/A | N/A | |  |
  | `value` | string | | N/A | N/A | |  |
  | `url` | string | | N/A | N/A |  |  |

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
  | `agentId` | guid | no  |  | id of the agent that this offline message belongs to |
  | `visitorSegmentId` | guid | no  |  | id of the visitor segment which the visitor belongs to |
  | `keywords` | string | no  |  | search subject or message by keywords |
  | `pageIndex` | integer | no  | 1 | the page index of query |
  | `pageSize` | integer | no  | 50 | page size  |

#### Response
The response body contains data with the follow structure:

  | Name | Type | Required | Default | Description |    
  | - | - | :-: | :-: | - | 
  | `totalCount` | integer | N/A | N/A | total count of the list. |
  | `list` | [Offline Message](#offline-message-json-format)[] | N/A | N/A | an array of [Offline Message](#offline-message-json-format) |

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/livechat/offlineMessages?include=department,agent,campaign,autoInvitation, session
```
Response
```json  

{
    "totalCount": 28,
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
    "agentId":"2a317d24-bec0-43e5-aaf5-2eae29ce948f",
    "agent": {
        //include agent
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
- `POST /api/v3/livechat/campaigns` - [Create a campaign](#create-a-new-campaign)
- `PUT /api/v3/livechat/campaigns/{id}` - [Update a campaign](#update-a-campaign)
- `DELETE /api/v3/livechat/campaigns/{id}` - [Delete a campaign](#delete-a-campaign)

## Related Object Json Format

### Campaign Object

  Campaign Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | no | yes | `Default Plan` | |
  | `description` | string  | no | no | | |

## Campaign Endpoints

### Get all Campaigns in site

  `GET /api/v3/livechat/campaigns`

#### Parameters

  no parameters

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
        "description": "campaigns"
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
  "description": "campaigns"
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
  "description": "campaigns"
}
```

#### Response

the response is: [Campaign](#Campaign-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "campaigns11111",
  "description": "campaigns"
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
  "description": "campaigns"
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
  "description": "campaigns"
}
```

#### Response

the response is: [Campaign](#Campaign-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "campaigns2222",
  "description": "campaigns"
  }' -X PUT https://domain.comm100.com/api/v3/livechat/campaigns/FAE531BE-8CAD-207D-57B9-493BBCC6E585
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "FAE531BE-8CAD-207D-57B9-493BBCC6E585",
  "name": "campaigns2222",
  "description": "campaigns"
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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `code` | string  | N/A | N/A | | |

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
        https://hosted.comm100.com/chatserver/livechat.ashx?siteId=\"),setTimeout(function(){t.loaded||e(\"  
        https://hosted.comm100.com/chatserver/livechat.ashx?siteId=\")},5e3)})(Comm100API||{})
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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `type` | string | no | N/A | `adaptive` | Type of the button, including `adaptive`, `image` and `textLink`. |
  | `isHideWhenOffline` | boolean | no | N/A | | Whether the chat button is visible when no agent is online. `true` means that button is invisible. |
  | `isDomainRestrictionEnabled` | boolean | no | N/A | | Whether the domain restriction is enabled or not. |
  | `allowedDomains` | string[] | no | N/A | | An array of `domains` or `urls`, on which the chat button is visible. |
  | `adaptiveButtonColor` | string | no | N/A | | The theme color of the chat button, available when `type` is `adaptive`. |
  | `adaptiveButtonIconType` | integer | no | N/A | | Type of the chat button icon, including `1`, `2` , `3` and `4`, available when `type` is `adaptive`. |
  | `adaptiveButtonOnlineIcon` | string | no | N/A | | Image file key of the chat online button, available when `type` is `adaptive`. |
  | `adaptiveButtonOfflineIcon` | string | no | N/A | | Image file key of the chat offline button, available when `type` is `adaptive`. |
  | `isImageButtonFloating` | boolean | no | N/A | | Whether the image button is float or not, available when `type` is `image`. |
  | `imageButtonPosition` | string | no | N/A | | Position of the image button, including `centered`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available when `type` is `image`. |
  | `imageButtonPositionMode` | string | no | N/A | | Position mode of the image button, including `Basic` and `Advanced`, available when `type` is `image`. |
  | `isImageButtonXOffsetByPixel` | boolean | no | N/A | |                 available when `type` is `image`. |
  | `imageButtonXOffset` | integer | no | N/A | |  If Is XOffset By Pixel is True, it represents the offset pixel value of the X coordinate. If Is XOffset By Pixel is False, it represents the offset percentage value of the X coordinate, available when `type` is `image`. |
  | `isImageButtonYOffsetByPixel` | boolean | no | N/A | |                 available when `type` is `image`. |
  | `imageButtonYOffset` | integer | no | N/A | |  If Is YOffset By Pixel is True, it represents the offset pixel value of the Y coordinate. If Is YOffset By Pixel is False, it represents the offset percentage value of the Y coordinate, available when `type` is `image`. |
  | `imageButtonImageSource` | string | no | N/A | |  Type of the image source, including `fromGallery` and `fromMyComputer` |
  | `imageButtonOnlineImage` | string | no | N/A | | Image file key of online button, available when `type` is `image`. |
  | `imageButtonOfflineImage` | string | no | N/A | | Image file key of offline button, available when `type` is `image`. |
  | `imageButtonTypeOnMobile` | string | no | N/A | | The type of button on mobile device, including `text` and `image`. |
  | `imageButtonColorOnMobile` | string | no | N/A | | |
  | `imageButtonTextColorOnMobile` | string | no | N/A | | The theme color of chatbutton on mobile device. |
  | `imageButtonOnlineImageOnMobile` | string | no | N/A | | The Image file key on mobile device when any agents is online. |
  | `imageButtonOfflineImageOnMobile` | string | no | N/A | | The image file key on mobile device when no agent is online. |
  | `imageButtonPositionOnMobile` | string | no | N/A | | Position of the chat button on mobile device, including `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle`, `RightMiddle`, `leftBottom` and `rightBottom`. |
  | `textLinkButtonText` | string | no | N/A | | the content of the text link, available when `type` is `textLink`. |

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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `width` | integer | no | N/A | | |
  | `height` | integer | no | N/A | | |
  | `style` | string | no | N/A | |  Style of the window's theme, including `classic`, `circle` and `bubble`. |
  | `color` | string | no | N/A | |  Color of the window's theme. |
  | `type` | string | no | N/A | | Type of the chat window, including `embedded` and `popup`. |
  | `headerType` | string | no | N/A | |  Type of the header, including `agentInfo`, `bannerImage` and `avatarAndLogo` when `style` is `classic`. |
  | `isAvatarDisplayed` | boolean | no | N/A | | Whether the avatar of the agent is visible or not, available when  `headerType` is `agentInfo` or `avatarAndLogo`. |
  | `isTitleDisplayed` | boolean | no | N/A | | Whether the title of the agent is visible or not, available when `headerType` is `agentInfo`. |
  | `isBioDisplayed` | boolean | no | N/A | | Whether the bio of the agent is visible or not, available when `headerType` is `agentInfo`. |
  | `isLogoDisplayed` | boolean | no | N/A | | Whether the logo is visible or not, available when `headerType` is `avatarAndLogo`. |
  | `logo` | string | no | N/A | | Image file key of the logo. |
  | `bannerImage` | string | no | N/A | | Image file key of the banner, available when `headerType` is `bannerImage`. |
  | `isAvatarDisplayedWithMessage` | boolean | no | N/A   | | Whether the avatar of the agent is visible or not in the message body, available when `style` is `classic`or `simple`. |
  | `isBackgroundDisplayed` | boolean | no | N/A | |  Whether the texture and picture of the background is visible or not in the message body, available when `style` is `classic`or `simple`. |
  | `backgroundTexture` | string | no | N/A | | Including `style1`, `style2`, `style3`, `style4` and `style5`. |
  | `customCSSOfClassic` | string | no | N/A | |  The content of custom css when  `style` is `classic`. |
  | `customCSSOfCircle` | string | no | N/A | |  The content of custom css when  `style` is `circle`. |
  | `isTranscriptDownloadAllowed` | boolean | no | N/A | | Whether the visitor can download the chat transcript. |
  | `isTranscriptPrintAllowed` | boolean | no | N/A | | Whether the visitor can print the chat transcript. |
  | `isTranscriptSentToVisitors` | boolean | no | N/A | | Whether the transcript send to visitor. |
  | `isTranscriptSentFromCurrentAgentEmail` | boolean | no | N/A | | Available when `isTranscriptDownloadAllowed` is true. |
  | `fromEmailName` | string | no | N/A | |  The from name for sending transcript email, available when `isTranscriptSentFromCurrentAgentEmail` is true. |
  | `fromEmailAddress` | string | no | N/A | |  The subject address for sending transcript email, available when `isTranscriptSentFromCurrentAgentEmail` is true. |
  | `isSMTPServerCustomized` | boolean | no | N/A | | Whether use custome SMTP server. |
  | `customSMTPServer` | [Custom SMTP Server](#Custom-SMTP-Server-Object) | no | N/A | | |
  | `isSwitchToOfflineMessageAllow` | boolean | no | N/A | | Allow visitors to switch to Offline Message Window while waiting for chat. |
  | `isFileSendAllow` | boolean | no | N/A | | Whether the agent can send file or not. |
  | `ifMarkUnreadMessage` | boolean | no | N/A | | |
  | `isAudioChatEnabled` | boolean | no | N/A | | Whether the agent can use audio chat. |
  | `isVideoChatEnabled` | boolean | no | N/A | | Whether the agent can use video chat. |
  | `isBrowserPopupNotificationEnabled` | boolean | no | N/A | | It is available for private server sites. For shared server clients, the push notification is disabled by default. |
  | `ifEndChatWhenVisitorIsInactive` | boolean | no | N/A | | Automatically end chats if visitors don't respond in period of time. |
  | `minutesOfVisitorInactivity` | integer | no | N/A | | |
  | `isTranscriptSentForArchiving` | boolean | no | N/A | | |
  | `receivingEmailAddressesForArchivingTranscripts` | string | no | N/A | | |
  | `emailSubjectForArchivingTranscripts` | string | no | N/A | | |
  | `greetingMessage` | string | no | N/A | | |
  | `isCustomJSEnabled:` | boolean | no | N/A | | |
  | `customJS` | string | no | N/A | | |

### Custom SMTP Server Object

  Custom SMTP Server Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `fromName` | string | no | N/A | | |
  | `fromEmail` | string | no | N/A | | |
  | `mailServer` | string | no | N/A | | |
  | `port` | integer | no | N/A | | |
  | `encryptedType` | string | no | N/A | | Including `none`, `SSL` and `TLS`. |
  | `IsAuthenticationRequired` | boolean | no | N/A | | |
  | `username` | string | no | N/A | | |
  | `password` | string | no | N/A | | |

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
  "customCSSOfClassic": "",
  "customCSSOfCircle": "",
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
  "customCSSOfClassic": "",
  "customCSSOfCircle": "",
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
  "customCSSOfClassic": "",
  "customCSSOfCircle": "",
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
  "customCSSOfClassic": "",
  "customCSSOfCircle": "",
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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `isEnable` | boolean | no | yes | | Whether the pre-chat is enabled or not. |
  | `isTeamNameDisplayed` | boolean | no | no | | Whether the team name is visible or not in the header. |
  | `teamName` | string | no | no | | The team name displayed in the header. |
  | `isAgentAvatarDisplayed` | boolean | no | N/A   | | Whether the avatar of the agent is visible or not in the header. |
  | `greetingMessage` | string | no | no | | |
  | `socialMediaLogin` | string | no | no | |  Including `none` and `facebook`. |
  | `fields` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | no | no | | These System Fields are prebuilt and can’t be deleted: `name`, `email`, `phone`, `company`, `product service`, `department`, `ticket id`.  |
  | `isVisitorInfoRecorded` | boolean | no | no | true | If remember visitor info collected from pre-chat form. |
  | `formFieldLayoutStyle` | string | no | no | | Including `leftofInput` and `aboveInput`. Available for Post Chat and Offline Message forms.  |

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
  "fields":  [],
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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `isEnable` | boolean | no | N/A | | Whether the pot chat is enabled or not. |
  | `fields` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | no | N/A | | These System Fields are prebuilt and can’t be deleted: `rating`, `rating comment`.  |
  | `greetingMessage` | string | no | N/A | | |

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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
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

### Update Campaign Offline Message

  `PUT /api/v3/livechat/campaigns/{campaignId}/offlineMessage`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Offline Message](#Campaign-Offline-Message-Object) structure

#### Response

the response is: [Campaign Offline Message](#Campaign-Offline-Message-Object) Object

# Invitation

- `GET /api/v3/livechat/campaigns/{campaignId}/invitation` - [Get settings of invitation  for a campaign](#get-Invitation)
- `PUT /api/v3/livechat/campaigns/{campaignId}/invitation` - [Update settings of invitation  for a campaign](#update-Invitation)

## Related Object Json Format

### Invitation Object

  Invitation Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `style` | string | no | no | | Including `bubble`, `popup` and `chatWindow`. |
  | `autoInvitations` | [Auto Invitation](#Auto-Invitation-Object)[] | no | no | | |
  | `manualInvitations` | [Manual Invitation](#Manual-Invitation-Object)[] | no | no | | |

### Manual Invitation Object

  Manual Invitation Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
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

### Update Invitation

  `PUT /api/v3/livechat/campaigns/{campaignId}/invitation`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `style` | string | no | no | | Including `bubble`, `popup` and `chatWindow`. |

#### Response

the response is: [Invitation](#Invitation-Object) Object

# Manual Invitation

- `GET /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation` - [Get settings of manual invitation  for a campaign](#get-Manual-Invitation)
- `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation` - [Update settings of manual invitation  for a campaign](#update-Manual-Invitation)

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

# Auto Invitation

- `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations` - [Get a list of auto invitations](#get-all-Auto-Invitations-in-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Get an auto invitation by id](#get-a-Auto-Invitation-by-id)
- `POST /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations` - [Create an auto invitation](#create-a-new-Auto-Invitation)
- `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Update an auto invitation](#update-a-Auto-Invitation)
- `DELETE /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Delete an auto invitation](#delete-a-Auto-Invitation)

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

### Create a new Auto Invitation

  `POST /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Auto Invitation](#Auto-Invitation-Object) structure

#### Response

the response is: [Auto Invitation](#Auto-Invitation-Object) Object

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

#### Response

the response is: [Auto Invitation](#Auto-Invitation-Object) Object

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

# Agent Wrap-Up

- `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup` - [Get settings of agent wrap-Up  for a campaign](#get-Agent-Wrap-Up)
- `PUT /api/v3/livechat/campaigns/{campaignId}/agentWrapup` - [Update settings of agent wrap-Up  for a campaign](#update-Agent-Wrap-Up)

## Related Object Json Format

### Agent Wrap-Up Object

  Agent Wrap-Up Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
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

### Update Agent Wrap-Up

  `PUT /api/v3/livechat/campaigns/{campaignId}/agentWrapup`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Agent Wrap-Up](#Agent-Wrap-Up-Object) structure

#### Response

the response is: [Agent Wrap-Up](#Agent-Wrap-Up-Object) Object

# Language

- `GET /api/v3/livechat/campaigns/{campaignId}/language` - [Get settings of language for a campaign](#get-Language)
- `PUT /api/v3/livechat/campaigns/{campaignId}/language` - [Update settings of language for a campaign](#update-Language)

## Related Object Json Format

### Language Object

  Language Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `defaultLanguage` | string | no | no | | The languages are defined in cPanel.  |
  | `isCustomLanguageEnabled` | boolean | no | no | | |
  | `isTextDirectionRightToLeft` | boolean | no | no | | |
  | `customLanguageItems` | [Custom Language](#Custom-Language-Object)[] | no | no | | |

### Custom Language Object

  Custom Language Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
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

### Update Language

  `PUT /api/v3/livechat/campaigns/{campaignId}/language`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Language](#Language-Object) structure

#### Response

the response is: [Language](#Language-Object) Object

# Routing

- `GET /api/v3/livechat/campaigns/{campaignId}/routing` - [Get settings of routing for a campaign](#get-Routing)
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing` - [Update settings of routing for a campaign](#update-Routing)

## Related Object Json Format

### Routing Object

  Routing Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `isEnable` | boolean |  | no | no |  false | Whether the routing rule is enabled or not. |
  | `type` | string |  | no | no | | Including `simple` and `customRule`. |
  | `routeTo` | [Agent](#Agent-Object) or [Department](#Department-Object) | yes | no | no | |  |
  | `priority` | string |  | no | no | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `percentageToBot` | integer |  | no | no | | |
  | `customRules` | [Custom Rule](#Custom-Rule-Object)[] |  | no | no | | |
  | `actionWhenNoRuleMatched` | string |  | no | no | | Including `routeToSite`, `routeToDepartment`, `routeToAgent` and `redirectToOfflineMessage`. |
  | `routeToWhenNoRuleMatched` | [Agent](#Agent-Object) or [Department](#Department-Object) | yes | no | no | |  |
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

### Update Routing

  `PUT /api/v3/livechat/campaigns/{campaignId}/routing`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Routing](#Routing-Object) structure

#### Response

the response is: [Routing](#Routing-Object) Object

# Custom Rule

- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Get a list of custom rules](#get-all-Custom-Rules)
- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Get a custom rule by id](#get-a-Custom-Rule-by-id)
- `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Create a custom rule](#create-a-new-Custom-Rule)
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Update a custom rule](#update-a-Custom-Rule)
- `DELETE /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Delete a custom rule](#delete-a-Custom-Rule)

## Related Object Json Format

### Custom Rule Object

  Custom Rule Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `id` | Guid | yes | | no | | Id of the current item. |
  | `isEnable` | boolean | | no | no | | Whether the custom rule is enabled or not. |
  | `name` | string | | no | no | | |
  | `order` | integer | | no | no | | |
  | `routeTo` | [Agent](#Agent-Object) or [Department](#Department-Object) | yes | no | no | |  |
  | `priority` | string | | no | no | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `percentageToBot` | integer | | no | no | | |
  | `conditionMetType` | string | | no | no | | Including `all`, `any` and `logicalExpression`. |
  | `logicalExpression` | string | | no | no | | |
  | `conditions` | [Live Chat Condition](#Live-Chat-Condition-Object)[] | | no | no | | |

### Live Chat Condition Object

  Live Chat Condition Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
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

### Create a new Custom Rule

  `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the custom rule |

Request Body

  The request body contains data with the [Custom Rule](#Custom-Rule-Object) structure

#### Response

the response is: [Custom Rule](#Custom-Rule-Object) Object

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

#### Response

the response is: [Custom Rule](#Custom-Rule-Object) Object

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

# Chatbot Integration

- `GET /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration` - [Get settings of Chatbot Integration for a campaign](#get-Chatbot-Integration)
- `PUT /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration` - [Update settings of Chatbot Integration for a campaign](#update-Chatbot-Integration)

## Related Object Json Format

### Chatbot Integration Object

  Chatbot Integration Object is represented as simple flat JSON objects with the following keys:

  | Name | Type || Include Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `isEnable` | boolean | | no | no | | Whether the chatbot integration is enabled or not. |
  | `selectedChatbot` | [Chatbot](#Chatbot-Object) | yes | no | no | | |
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

### Update Chatbot Integration

  `PUT /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Chatbot Integration](#Chatbot-Integration-Object) structure

#### Response

the response is: [Chatbot Integration](#Chatbot-Integration-Object) Object

# KB Integration

- `GET /api/v3/livechat/campaigns/{campaignId}/kbIntegration` - [Get settings of KB Integration for a campaign](#get-KB-Integration) include knowledgeBase
- `PUT /api/v3/livechat/campaigns/{campaignId}/kbIntegration` - [Update settings of KB Integration for a campaign](#update-KB-Integration)

## Related Object Json Format

### KB Integration Object

  KB Integration Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `isEnable` | boolean | no | no | | Whether the KB integration is enabled or not. |
  | `selectedKB` | [KB](#KB-Object) | no | no | | |
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

### Update KB Integration

  `PUT /api/v3/livechat/campaigns/{campaignId}/KBIntegration`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [KB Integration](#KB-Integration-Object) structure

#### Response

the response is: [KB Integration](#KB-Integration-Object) Object

# Campaign Form Field

- `GET /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Get a list of form fields of Pre-Chat for a campaign](#get-all-form-fields-of-Pre-Chat-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Create a form field of Pre-Chat for a campaign](#create-a-new-form-fields-of-Pre-Chat-for-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Get a list of form fields of Post Chat for a campaign](#get-all-form-fields-of-Post-Chat-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Create a form field of Post Chat for a campaign](#create-a-new-form-fields-of-Offline-Message-for-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Get a list of form fields of offline message for a campaign](#get-all-form-fields-of-Offline-Message-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Create a form field of offline message for a campaign](#create-a-new-form-fields-of-Offline-Message-for-a-campaign)
- `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Get a list of form fields of agent wrapup for a campaign](#get-all-form-fields-of-Agent-Wrap-up-for-a-campaign)
- `POST /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Create a form field of agent wrapup for a campaign](#create-a-new-form-fields-of-Agent-Wrap-up-for-a-campaign)
- `GET /api/v3/livechat/campaignFormFields/{id}` - [Get a campaign form field by id](#get-a-form-fields-by-id)
- `PUT /api/v3/livechat/campaignFormFields/{id}` - [Update a campaign form field](#update-a-form-fields)
- `DELETE /api/v3/livechat/campaignFormFields/{id}` - [Delete a campaign form field](#delete-a-form-fields)

## Related Object Json Format

### Campaign Form Field Object

  Campaign Form Field is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `field` | [type](#Live-Chat-Field-Object) | no | no | | |
  | `isVisible` | boolean | no | no | | Whether the field is visible or not. |
  | `isRequired` | boolean | no | no | | Whether the field is required or not when submitting the form |
  | `order` | integer | no | no | | The order of the field. |
  | `ratingGrade` | [type](#Rating-Grade-Object) | no | no | | |

### Rating Grade Object

  Rating Grade is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | Id of the current item. |
  | `grade` | integer | no | no | | |
  | `label` | string | no | no | | |
  | `isVisible` | boolean | no | no | | |

### Live Chat Field Object

  Live Chat Field is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
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
  | - | :-: | - |
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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `value` | string | no | no | | |
  | `order` | integer | no | no | | |

### Live Chat Field Option Group Object

  Live Chat Field Option Group Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `name` | string | no | no | | |
  | `order` | integer | no | no | | |
  | `options` | [Live Chat Field Option](#Live-Chat-Field-Option-Object)[]  | no | no | | |

## KB Integration Endpoints

### Get all form fields of Pre-Chat for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Create a new form fields of Pre-Chat for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Get all form fields of Post Chat for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Create a new form fields of Post Chat for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Get all form fields of Offline Message for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Create a new form fields of Offline Message for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Get all form fields of Agent Wrap-up for a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Create a new form fields of Agent Wrap-up for a campaign

  `POST /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Get a form fields by id

  `GET /api/v3/livechat/campaignFormFields/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign form fields |

#### Response

the response is: list of [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Update a form fields

  `PUT /api/v3/livechat/campaignFormFields/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign form fields |

Request Body

  The request body contains data with the [Campaign Form Field](#Campaign-Form-Field-Object) structure

#### Response

the response is: [Campaign Form Field](#Campaign-Form-Field-Object) Object

### Delete a form fields

  `DELETE /api/v3/livechat/campaignFormFields/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign form fields |

#### Response

HTTP/1.1 204 No Content

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

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - | 
  | `id` | string | | yes | N/A | | id of the ban. |
  | `type` | string | | no | yes | |  type of ban, including `visitor` , `ip` and `ipRange` |
  | `visitorId` | Guid | | no | no | | visitor's id of the ban if `type` is `visitor`  |
  | `visitor` | [Visitor](#visitor) | yes | N/A | N/A | |  Available only when visitor is included  |
  | `ip` | string  |  | no | yes | | ip address of the ban if `type` is `ip`, it can be a specific ip `192.168.8.113` |
  | `ipRangeFrom` | string | | no | yes | | ip address of the ban if `type` is `ipRange` |
  | `ipRangeTo` | string | | no | yes | | ip address of the ban if `type` is `ipRange` |
  | `comment` | string | | no | no | | comment of the ban. |
  | `lastUpdatedBy` | Guid | | N/A | N/A | | comment of the ban. |
  | `lastUpdatedAgent` | [Agent](#agent) | yes | N/A | N/A | | Available only when agent is included  |

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

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
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
  | `createdTime` | datetime | | N/A | N/A |  |  |
  | `createdBy` | Guid | | N/A | N/A |  |  |
  | `createdAgent` | [Agent](#agent) | yes | N/A | N/A | | Available only when agent is included  |
  | `lastUpdatedTime` | datetime | | N/A | N/A |  | |
  | `lastUpdatedBy` | Guid | | N/A | N/A |  | |
  | `lastUpdatedAgent` | [Agent](#agent) | yes | N/A | N/A |  | Available only when agent is included |

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
        "createdBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
        "createdAgent": {
            //include agent
            "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
            "email": "test@comm100.com",
            "displayName": "test comm100",
            "firstName": "test",
            "lastName": "comm100",
            ...
        },
        "lastUpdatedTime": "2020-02-20T13:12:20Z",
        "lastUpdatedBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
        "lastUpdatedAgent": {
            //include agent
            "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
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
    "createdBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
    "createdAgent": {
        //include agent
        "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
        "email": "test@comm100.com",
        "displayName": "test comm100",
        "firstName": "test",
        "lastName": "comm100",
        ...
    },
    "lastUpdatedTime": "2020-02-20T13:12:20Z",
    "lastUpdatedBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
    "lastUpdatedAgent": {
        //include agent
        "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
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
    "createdBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
    "lastUpdatedTime": "2020-02-20T13:12:20Z",
    "lastUpdatedBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2"
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
    "createdBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
    "lastUpdatedTime": "2020-02-20T14:12:20Z",
    "lastUpdatedBy": "9F4709DB-C391-4896-94BA-3A17BE12D9E2"
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
  | `code` | string | N/A | N/A |  0: ok; 1: the conversion name does not exist; 2: the visitorId does not exist; 3: error adding conversion-related Data to system. |
  | `message` | string | N/A | N/A | error message. |

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

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - |
  | `id` | string  | | yes | N/A | | id of the secure form. |
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

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
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

 | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - | 
  | `id` | guid  || N/A | N/A | | id of the webhook |
  | `event` | string  || no | yes | | event of webhook, including `offlineMessageSubmitted`, `operatorEventNotification`, `chatStarted`, `chatEnded`, `chatWrappedUp`, `chatRequested` and `chatTransferred`. |
  | `name` | string  || no | yes | | target url of the webhook. |

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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/api/v3/livechat/webhooks
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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
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

### Create a new webhook

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

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X POST -d "event=chatwrappedup&targeturl=http://www.baidu.com"  https://hosted.comm100.com/api/v3/livechat/webhooks
```

Sample response:

```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://hosted.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
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

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X PUT -d "event=chatwrappedup&targeturl=http://www.google.com"  https://hosted.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
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

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X DELETE  https://hosted.comm100.com/api/v3/livechat/webhooks/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Custom Variable

- `GET /api/v3/livechat/customVariables` - [Get a list of custom variables](#get-a-list-of-custom-variables)
- `GET /api/v3/livechat/campacustomVariablesigns/{id}` - [Get a custom variable by id](#get-a-custom-variable-by-id)
- `POST /api/v3/livechat/customVariables` - [Create a custom variable](#create-a-custom-variable)
- `PUT /api/v3/livechat/customVariables/{id}` - [Update a custom variable](#update-a-custom-variable)
- `DELETE /api/v3/livechat/customVariables/{id}` - [Delete a custom variable](#delete-a-custom-variable)

## Custom Variable Related Objects Json Format

### Custom Variable Object

Custom Variable is represented as simple flat JSON objects with the following keys:  

 | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | - | :-: | :-: | :-: | - | 
  | `id` | Guid  || yes | N/A || id of the custom variable. |
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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/api/v3/livechat/customvariables
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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" https://hosted.comm100.com/api/v3/livechat/customvariables/1487fc9d-92e6-4487-a2e8-92e68d6892e6
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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X POST -d "name=justfortest&type=text&value=aaaaa"  https://hosted.comm100.com/api/v3/livechat/customvariables
```

Response
```Json
HTTP/1.1 201 Created
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
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "test",
  "type": "text",
  "value": "'lizz'",
  "hyperlink": "{!Visitor.IP}"
}
```

#### Response

the response is: [Custom Variable](#custom-variable-object) Object.

### Example

Sample request:

Using curl
```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X POST -d "name=justfortestupdate&type=text&value=bbbbb"  https://hosted.comm100.com/api/v3/livechat/customvariables
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

### delete a custom variable

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
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk-aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRbfmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1xUTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ" -X DELETE https://hosted.comm100.com/api/v3/livechat/customvariables/1487fc9d-92e6-4487-a2e8-92e68d6892e6
```

Response
```json
HTTP/1.1 204 No Content
```

</div>
