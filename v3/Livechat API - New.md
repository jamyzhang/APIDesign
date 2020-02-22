# Live Chat Restful API

Comm100 Live Chat API allows you to pull the raw livechat data from Comm100 Live Chat into your own systems.

<div>

  | Change Version | API Version | Change notes | Change Date | Author  |
  | -------------- | ----------- | ------------ | ----------- | ------- |
  | 1.0            | v3          |              | 2020-02-17  | Michael |

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
    - [custom variable](#custom-variable)  
    - [webhook](#webhook)      

# Live Chat Settings
You need `Manage Settings` permission to config for a site.
  + `GET /api/v3/livechat/settings` - [Get livechat settings of a site](#get-site-info)
  + `PUT /api/v3/livechat/settings` - [Update livechat settings of a site](#update-site-info)

# Auto Distribution
  + `GET /api/v3/livechat/autoDistribution` - [Get livechat auto distribution of a site](#get-site-info)  include department, agent
  + `PUT /api/v3/livechat/autoDistribution` - [Update livechat auto distribution of a site](#update-site-info)

 # Translation Excluded Word
  + `GET /api/v3/livechat/translationExcludedWords` - [Get a list of translation excluded words](#get-site-info)
  + `GET /api/v3/livechat/translationExcludedWords/{id}` - [Get a translation excluded word by id](#get-site-info)
  + `POST /api/v3/livechat/translationExcludedWords` - [Create a translation excluded word](#get-site-info)
  + `PUT /api/v3/livechat/translationExcludedWords/{id}` - [Update a translation excluded word](#update-site-info) 
  + `DELETE /api/v3/livechat/translationExcludedWords/{id}` - [Delete a translation excluded word](#delete-a-customer-segment) 
 

# Customer Segment
 + `GET /api/v3/livechat/customerSegments` - [Get a list of customer segments](#get-site-info)
 + `GET /api/v3/livechat/customerSegments/{id}` - [Get a customer segment by id](#get-site-info)
 + `POST /api/v3/livechat/customerSegments` - [Create a customer segment](#get-site-info)
 + `PUT /api/v3/livechat/customerSegments/{id}` - [Update a customer segment](#update-site-info) 
 + `DELETE /api/v3/livechat/customerSegments/{id}` - [Delete a customer segment](#delete-a-customer-segment) 

# Dynamic Campaign
  + `GET /api/v3/livechat/dynamicCampaign` - [Get livechat dynamic campaign of a site](#get-site-info) include campaign
  + `PUT /api/v3/livechat/dynamicCampaign` - [Update livechat dynamic campaign of a site](#update-site-info) 

+ `GET /api/v3/livechat/liveChatSettings/dynamicCampaign` - [Get livechat dynamic campaign of a site](#get-site-info) include campaign
+ `PUT /api/v3/livechat/liveChatSettings/dynamicCampaign` - [Update livechat dynamic campaign of a site](#update-site-info) 

# Mobile Push
  + `GET /api/v3/livechat/mobilePush` - [Get livechat mobile push profile of a site](#get-site-info)
  + `PUT /api/v3/livechat/mobilePush` - [Update livechat mobile push profile of a site](#update-site-info)

# Online Visitor  
//修改ER
//todo
  + `GET /api/v3/livechat/visitors` - [Get a list of visitors in livechat](#get-all-visitors)
  + `GET /api/v3/livechat/visitors/{id}` - [Get a visitor by id](#get-a-visitor)  
  + `POST /api/v3/livechat/visitors/{id}/customVariables:change` - [update a visitor's custom variables](#update-a-visitor-custom-variables)   

# Online Agent  
//修改ER
//todo
  + `GET /api/v3/livechat/agents` - [Get a list of agents in livechat](#get-all-agents)
  + `GET /api/v3/livechat/agents/{id}` - [Get an agent by id](#get-an-agent)  
  + `PUT /api/v3/livechat/agents/{id}` - [Update an agent](#update-an-agent)  


  ??Todo: api 和 include 如何设计， 感觉这个是多余的
  ??session object 不含 chat 和 offlinemessage
+ `GET /api/v3/livechat/sessions` - [Get a list of sessions](#get-site-campaigns) include visitor, contact
+ `GET /api/v3/livechat/sessions/{id}` - [Get a session by id](#get-a-campaign) include visitor, contact

# Chat

+ `GET /api/v3/livechat/chats` - [Get a list of chats](#get-site-campaigns) include department,agent , chatbot, campaign,autoInvitation
+ `GET /api/v3/livechat/sessions/{sessionId}/chats` - [Get a list of chats in a session](#get-site-campaigns)  include department,agent , chatbot, campaign,autoInvitation
+ `GET /api/v3/livechat/chats/{id}` - [Get a chat by id](#get-a-campaign)  include department,agent , chatbot, campaign,autoInvitation
+ `DELETE /api/v3/livechat/chats/{id}` - [Delete a chat by id](#get-a-campaign)
+ `DELETE /api/v3/livechat/chats` - [Batch Delete chats](#get-a-campaign)

# Offline Message

+ `GET /api/v3/livechat/offlineMessages` - [Get a list of offlineMessages](#get-site-campaigns)  include department,agent, campaign,autoInvitation
+ `GET /api/v3/livechat/sessions/{sessionId}/offlineMessages` - [Get a list of offlineMessages in a session](#get-site-campaigns)  include department,agent, campaign,autoInvitation
+ `GET /api/v3/livechat/offlineMessages/{id}` - [Get an offlineMessage by id](#get-a-campaign)  include department,agent, campaign,autoInvitation
+ `DELETE /api/v3/livechat/offlineMessages/{id}` - [Delete an offlineMessage by id](#get-a-campaign)
+ `DELETE /api/v3/livechat/offlineMessages` - [Batch Delete offlineMessages](#get-a-campaign)

# Campaign

+ `GET /api/v3/livechat/campaigns` - [Get a list of campaigns](#get-site-campaigns)
+ `GET /api/v3/livechat/campaigns/{id}` - [Get a campaign by id](#get-a-campaign)
+ `POST /api/v3/livechat/campaigns` - [Create a campaign](#get-a-campaign)
+ `PUT /api/v3/livechat/campaigns/{id}` - [Update a campaign](#update-a-campaign) 
+ `DELETE /api/v3/livechat/campaigns/{id}` - [Delete a campaign](#delete-a-campaign)

# Installation Code

+ `GET /api/v3/livechat/campaigns/{campaignId}/installationCode` - [Get installation code of a campaign](#get-site-info)

# Chat Button

+ `GET /api/v3/livechat/campaigns/{campaignId}/chatButton` - [Get settings of ChatButton for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/chatButton` - [Update settings of ChatButton for a campaign](#update-site-info)

# Chat Window

+ `GET /api/v3/livechat/campaigns/{campaignId}/chatWindow` - [Get settings of ChatWindow for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/chatWindow` - [Update settings of ChatWindow for a campaign](#update-site-info)

# Pre-Chat

+ `GET /api/v3/livechat/campaigns/{campaignId}/preChat` - [Get settings of Pre-Chat for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/preChat` - [Update settings of Pre-Chat for a campaign](#update-site-info)

# Post Chat

+ `GET /api/v3/livechat/campaigns/{campaignId}/postChat` - [Get settings of PostChat for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/postChat` - [Update settings of PostChat for a campaign](#update-site-info)

# Campaign Offline Message

+ `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage` - [Get settings of OfflineMessage for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/offlineMessage` - [Update settings of OfflineMessage for a campaign](#update-site-info)

# Invitation

+ `GET /api/v3/livechat/campaigns/{campaignId}/invitation ` - [Get settings of invitation  for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/invitation ` - [Update settings of invitation  for a campaign](#update-site-info)

# Manual Invitation

+ `GET /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation ` - [Get settings of manual invitation  for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/manualInvitation ` - [Update settings of manual invitation  for a campaign](#update-site-info)

# Auto Invitation

+ `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations` - [Get a list of auto invitations](#get-site-info)
+ `GET /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Get an auto invitation by id](#get-site-info)
+ `POST /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations` - [Create an auto invitation](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Update an auto invitation](#update-site-info) 
+ `DELETE /api/v3/livechat/campaigns/{campaignId}/invitation/autoInvitations/{id}` - [Delete an auto invitation](#delete-a-customer-segment)

# Agent Wrap-Up

+ `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup ` - [Get settings of agent wrap-Up  for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/agentWrapup ` - [Update settings of agent wrap-Up  for a campaign](#update-site-info)

# Language

+ `GET /api/v3/livechat/campaigns/{campaignId}/language ` - [Get settings of language for a campaign](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/language ` - [Update settings of language for a campaign](#update-site-info)

# Routing

+ `GET /api/v3/livechat/campaigns/{campaignId}/routing ` - [Get settings of routing for a campaign](#get-site-info) include department, agent
+ `PUT /api/v3/livechat/campaigns/{campaignId}/routing ` - [Update settings of routing for a campaign](#update-site-info)

# Custom Rule

+ `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Get a list of custom rules](#get-site-info) include department, agent
+ `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Get a custom rule by id](#get-site-info) include department, agent
+ `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Create a custom rule](#get-site-info)
+ `PUT /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Update a custom rule](#update-site-info) 
+ `DELETE /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Delete a custom rule](#delete-a-customer-segment)

# Chatbot Integration

+ `GET /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration ` - [Get settings of Chatbot Integration for a campaign](#get-site-info) include chatbot
+ `PUT /api/v3/livechat/campaigns/{campaignId}/chatbotIntegration ` - [Update settings of Chatbot Integration for a campaign](#update-site-info)

# KB Integration

+ `GET /api/v3/livechat/campaigns/{campaignId}/kbIntegration ` - [Get settings of KB Integration for a campaign](#get-site-info) include knowledgeBase
+ `PUT /api/v3/livechat/campaigns/{campaignId}/kbIntegration ` - [Update settings of KB Integration for a campaign](#update-site-info)

# Campaign Form Field

+ `GET /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Get a list of form fields of Pre-Chat for a campaign](#get-site-info)
+ `POST /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Create a form field of Pre-Chat for a campaign](#update-site-info)
+ `GET /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Get a list of form fields of Post Chat for a campaign](#get-site-info)
+ `POST /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Create a form field of Post Chat for a campaign](#update-site-info)
+ `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Get a list of form fields of offline message for a campaign](#get-site-info)
+ `POST /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Create a form field of offline message for a campaign](#update-site-info)
+ `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Get a list of form fields of agent wrapup for a campaign](#get-site-info)
+ `POST /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Create a form field of agent wrapup for a campaign](#update-site-info)
+ `GET /api/v3/livechat/campaignFormFields/{id}` - [Get a campaign form field by id](#get-a-campaign-form-field)
+ `PUT /api/v3/livechat/campaignFormFields/{id}` - [Update a campaign form field](#update-a-campaign-form-field) 
+ `DELETE /api/v3/livechat/campaignFormFields/{id}` - [Delete a campaign form field](#delete-a-campaign-form-field)

# Ban

+ `GET /api/v3/livechat/bans` - [Get a list of bans](#get-site-bans) include visitor, agent
+ `GET /api/v3/livechat/bans/{id}` - [Get a ban by id](#get-a-ban) include visitor, agent
+ `POST /api/v3/livechat/bans` - [Create a ban](#get-a-ban)
+ `PUT /api/v3/livechat/bans/{id}` - [Update a ban](#update-a-ban) 
+ `DELETE /api/v3/livechat/bans/{id}` - [Delete a ban](#delete-a-ban)

# Conversion Action

+ `GET /api/v3/livechat/conversionActions` - [Get a list of conversion actions](#get-site-campaigns) include customVariable, agent
+ `GET /api/v3/livechat/conversionActions/{id}` - [Get a conversion action by id](#get-a-campaign)  include customVariable, agent
+ `POST /api/v3/livechat/conversionActions` - [Create a conversion action](#get-a-campaign)
+ `PUT /api/v3/livechat/conversionActions/{id}` - [Update a conversion action](#update-a-campaign) 
+ `POST /api/v3/livechat/conversionActions:achieved`[Make api conversion succesful](#make-api-conversion-succesful) 

# Secure Form

+ `GET /api/v3/livechat/secureForms` - [Get a list of secureForms](#get-site-secure-forms)
+ `GET /api/v3/livechat/secureForms/{id}` - [Get a secure form by id](#get-a-secure-form)
+ `POST /api/v3/livechat/secureForms` - [Create a secure form](#get-a-secure-form)
+ `PUT /api/v3/livechat/secureForms/{id}` - [Update a secure form](#update-a-secure-form) 
+ `DELETE /api/v3/livechat/secureForms/{id}` - [Delete a secure form](#delete-a-secure-form)

# Custom Variable

+ `GET /api/v3/livechat/customVariables` - [Get a list of custom variables](#get-site-custom-variables)
+ `GET /api/v3/livechat/campacustomVariablesigns/{id}` - [Get a custom variable by id](#get-a-custom-variable)
+ `POST /api/v3/livechat/customVariables` - [Create a custom variable](#get-a-custom-variable)
+ `PUT /api/v3/livechat/customVariables/{id}` - [Update a custom variable](#update-a-custom-variable)
+ `DELETE /api/v3/livechat/customVariables/{id}` - [Delete a custom variable](#delete-a-custom-variable)

# Webhook

+ `GET /api/v3/livechat/webhooks` - [Get a list of webhooks](#get-a-list-of-webhooks)
+ `GET /api/v3/livechat/webhooks/{id}` - [Get a webhook by id](#get-a-webhook-by-id)
+ `POST /api/v3/livechat/webhooks` - [Create a webhook](#create-a-webhook)
+ `PUT /api/v3/livechat/webhooks/{id}` - [Update a webhook](#update-a-webhook) 
+ `DELETE /api/v3/livechat/webhooks/{id}` - [Delete a webhook](#delete-a-webhook)

## Webhook Related Objects Json Format

### Webhook Object

  Webhook is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | guid  | N/A | N/A | | id of the webhook |
  | `event` | string  | no | yes | | event of webhook, including `offlineMessageSubmitted`, `operatorEventNotification`, `chatStarted`, `chatEnded`, `chatWrappedUp`, `chatRequested` and `chatTransferred`. |
  | `name` | string  | no | yes | | target url of the webhook. |

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

#### Create a new webhook

  `POST /api/v3/livechat/webhooks`

#### Parameters

Request body
  
  The request body contains data with the [Webhook](#webhook-object) structure

example:
```Json
{
  "id": "1487fc9d-92e6-4487-a2e8-92e68d6892e6",
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

#### Update a webhook

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
</div>