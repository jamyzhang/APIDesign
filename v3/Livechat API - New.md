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

# Live Chat Settings

You need `Manage Settings` permission to config for a site.

- `GET /api/v3/livechat/settings` - [Get livechat settings of a site](#get-site-info)
- `PUT /api/v3/livechat/settings` - [Update livechat settings of a site](#update-site-info)

# Auto Distribution

- `GET /api/v3/livechat/autoDistribution` - [Get livechat auto distribution of a site](#get-site-info)  include department, agent
- `PUT /api/v3/livechat/autoDistribution` - [Update livechat auto distribution of a site](#update-site-info)

# Translation Excluded Word

- `GET /api/v3/livechat/translationExcludedWords` - [Get a list of translation excluded words](#get-site-info)
- `GET /api/v3/livechat/translationExcludedWords/{id}` - [Get a translation excluded word by id](#get-site-info)
- `POST /api/v3/livechat/translationExcludedWords` - [Create a translation excluded word](#get-site-info)
- `PUT /api/v3/livechat/translationExcludedWords/{id}` - [Update a translation excluded word](#update-site-info)
- `DELETE /api/v3/livechat/translationExcludedWords/{id}` - [Delete a translation excluded word](#delete-a-customer-segment)

# Customer Segment

- `GET /api/v3/livechat/customerSegments` - [Get a list of customer segments](#get-site-info)
- `GET /api/v3/livechat/customerSegments/{id}` - [Get a customer segment by id](#get-site-info)
- `POST /api/v3/livechat/customerSegments` - [Create a customer segment](#get-site-info)
- `PUT /api/v3/livechat/customerSegments/{id}` - [Update a customer segment](#update-site-info)
- `DELETE /api/v3/livechat/customerSegments/{id}` - [Delete a customer segment](#delete-a-customer-segment)

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

- `GET /api/v3/livechat/agentChats` - [Get a list of agent chats](#get-site-campaigns)
- `GET /api/v3/livechat/agentChats/{id}` - [Get an agent chat by id](#get-a-campaign)  

# Online Visitor  

//修改ER
//todo

- `GET /api/v3/livechat/visitors` - [Get a list of visitors in livechat](#get-all-visitors)
- `GET /api/v3/livechat/visitors/{id}` - [Get a visitor by id](#get-a-visitor)  
- `POST /api/v3/livechat/visitors/{id}/customVariables:change` - [update a visitor's custom variables](#update-a-visitor-custom-variables)

# Session

  ??Todo: api 和 include 如何设计， 感觉这个是多余的
  ??session object 不含 chat 和 offlinemessage

- `GET /api/v3/livechat/sessions` - [Get a list of sessions](#get-site-campaigns) include visitor, contact
- `GET /api/v3/livechat/sessions/{id}` - [Get a session by id](#get-a-campaign) include visitor, contact

# Chat

- `GET /api/v3/livechat/chats` - [Get a list of chats](#get-site-campaigns) include department,agent , chatbot, campaign,autoInvitation
- `GET /api/v3/livechat/sessions/{sessionId}/chats` - [Get a list of chats in a session](#get-site-campaigns)  include department,agent , chatbot, campaign,autoInvitation
- `GET /api/v3/livechat/chats/{id}` - [Get a chat by id](#get-a-campaign)  include department,agent , chatbot, campaign,autoInvitation
- `DELETE /api/v3/livechat/chats/{id}` - [Delete a chat by id](#get-a-campaign)
- `DELETE /api/v3/livechat/chats` - [Batch Delete chats](#get-a-campaign)

# Offline Message

- `GET /api/v3/livechat/offlineMessages` - [Get a list of offlineMessages](#get-site-campaigns)  include department,agent, campaign,autoInvitation
- `GET /api/v3/livechat/sessions/{sessionId}/offlineMessages` - [Get a list of offlineMessages in a session](#get-site-campaigns)  include department,agent, campaign,autoInvitation
- `GET /api/v3/livechat/offlineMessages/{id}` - [Get an offlineMessage by id](#get-a-campaign)  include department,agent, campaign,autoInvitation
- `DELETE /api/v3/livechat/offlineMessages/{id}` - [Delete an offlineMessage by id](#get-a-campaign)
- `DELETE /api/v3/livechat/offlineMessages` - [Batch Delete offlineMessages](#get-a-campaign)

## Related Object Json Format

### Offline Message JSON format

 Offline Message is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |  
  | `id` | string  | yes | yes | id of the chat. |
  | `time` | datetime | yes | no | time of this offline message submitted. |
  | `ssoUserId` | string | yes | no | SSO id of visitor |
  | `name` | string | no | no | name of the visitor |
  | `email` | string | no | no | email of the visitor |
  | `department` | string | no | no | department of this offline message |
  | `agent` | string | no | no | agent of this offline message |
  | `content` | string | no | no | content of this offline message |
  | `fields` | array | no | no | values of custom fields entered by visitors in the offline message window. An array of [Custom Field Value](#custom-field-value-json-format). |
  | `customVariables` | array | no | no | information of custom variables captured from the web page visitors viewed. An array of [Custom Variable Value](#custom-variable-value-json-format). |
  | `attachment` | [Attachment](#attachment-json-foramt) | no | no | attachment submitted in the offline message |

## Endpoint

### Get messages list

  `Get /api/v3/livechat/offlineMessages`

- Parameters:
  - `timeFrom` - the beginning of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timeTo` - the end of the query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timezone` - time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as ±hh:mm.
  - `campaignId` - id of the campaign which the offline message
  - `departmentId` - id of the department which the offline message belongs to
  - `agentId` - id of the agent that this offline message belongs to
  - `visitorSegment` - id of the visitor segment which the visitor belongs to.
  - `keywords` - the key words of inquiring the  offline message.
  - `pageIndex` -the page index of query.

- Response
  - `total` -total count of the list.
  - `previousPage` -url of the previous page.
  - `nextPage` -url of the next page.
  - `offlineMessages` - an array of [Offline Message](#offline-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x GET https://hosted.comm100.com/api/v3/livechat/offlinemessages
```

Sample response:

```json
{
    "total": 28,
    "previousPage": "https://hosted.comm100.com/api/v2.0/livechat/offlinemessages",
    "nextPage": "https://hosted.comm100.com/api/v2.0/livechat/offlinemessages",
    "offlineMessages": [
        {
            "id": "a2317d24-bec0-43e5-aaf5-2eae29ce948f",
            "time": "2019-01-05T07:17:08.89",
            "ssoUserId": "",
            "name": "allon",
            "email": "allon@comm100.com",
            "department": "",
            "agent": "",
            "content": "cccccccc",
            "fields": [],
            "customVariables": [],
            "attachment": [
                {
                    "name": "comm100SDK.css",
                    "uri": "https://ent.comm100.com/api/v2.0/livechat/download?id=411&downloadtype=offlinemessage"
                }
            ]
        },
        ...
    ]
}
```

### Get a single messages

  `Get /api/v3/livechat/offlinemessages/{id}`

- Parameters:

    No parameter.

- Response:

    [Chat](#chat-json_format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x GET https://hosted.comm100.com/api/v3/livechat/offlinemessages/a2317d24-bec0-43e5-aaf5-2eae29ce948f
```

Sample response:

```json
{
    "id": "a2317d24-bec0-43e5-aaf5-2eae29ce948f",
    "time": "2019-01-05T07:17:08.89",
    "ssoUserId": "",
    "name": "allon",
    "email": "allon@comm100.com",
    "department": "",
    "agent": "",
    "content": "cccccccc",
    "fields": [],
    "customVariables": [],
    "attachment": [
        {
            "name": "comm100SDK.css",
            "uri": "https://ent.comm100.com/api/v2.0/livechat/download?id=411&downloadtype=offlinemessage"
        }
    ]
}
```

### Remove a messages

  `DELETE /api/v3/livechat/offlinemessages/{id}`

- Parameters

    No parameters.

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh7
    4BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw4mW
    LEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkoUYutNz4Wt3iC
    80BlfjLcPnYOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
    -X DELETE  https://hosted.comm100.com/api/v3/livechat/offlinemessages/a2317d24-bec0-43e5-aaf5-2eae29ce948f
```

Sample response:

```json
"Chat with id 'a2317d24-bec0-43e5-aaf5-2eae29ce948f' has been removed."
```

# Campaign

- `GET /api/v3/livechat/campaigns` - [Get a list of campaigns](#get-all-campaigns-in-site)
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
  | `name` | string  | N/A | yes | `Default Plan` | |
  | `description` | string  | N/A | N/A | | |

## Campaign Endpoints

### Get all Campaigns in site

  `GET /api/v3/livechat/campaigns`

#### Response

the response is: list of [Campaign](#Campaign-Object) Object

### Get a Campaign by id

  `GET /api/v3/livechat/campaigns/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: [Campaign](#Campaign-Object) Object

### Create a new Campaign

  `POST /api/v3/livechat/campaigns`

#### Parameters

Request Body

  The request body contains data with the [Campaign](#Campaign-Object) structure

#### Response

the response is: [Campaign](#Campaign-Object) Object

### Update a Campaign

  `PUT /api/v3/livechat/campaigns/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Campaign](#Campaign-Object) structure

#### Response

the response is: [Campaign](#Campaign-Object) Object

### Delete a Campaign

  `DELETE /api/v3/livechat/campaigns/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign |

#### Response

HTTP/1.1 204 No Content

# Installation Code

- `GET /api/v3/livechat/campaigns/{campaignId}/installationCode` - [Get installation code of a campaign](#get-installation-code-of-a-campaign)

## Installation Code Endpoints

### Get installation code of a campaign

  `GET /api/v3/livechat/campaigns/{campaignId}/installationCode`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

#### Response

the response is: installation code for the campaign

# Chat Button

- `GET /api/v3/livechat/campaigns/{campaignId}/chatButton` - [Get settings of ChatButton for a campaign](#get-chat-button)
- `PUT /api/v3/livechat/campaigns/{campaignId}/chatButton` - [Update settings of ChatButton for a campaign](#update-chat-button)

## Related Object Json Format

### Chat Button Object

  Chat Button Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `type` | string | N/A | yes | `adaptive` | Type of the button, including `adaptive`, `image` and `textLink`. |
  | `isHideWhenOffline` | boolean | N/A | N/A | | Whether the chat button is visible when no agent is online. `true` means that button is invisible. |
  | `isDomainRestrictionEnabled` | boolean | N/A | N/A | | Whether the domain restriction is enabled or not. |
  | `allowedDomains` | string | N/A | N/A | | An array of `domains` or `urls`, on which the chat button is visible. |
  | `adaptiveButtonColor` | string | N/A | N/A | | The theme color of the chat button, available when `type` is `adaptive`. |
  | `adaptiveButtonIconType` | integer | N/A | N/A | | Type of the chat button icon, including `1`, `2` , `3` and `4`, available when `type` is `adaptive`. |
  | `adaptiveButtonOnlineIcon` | [Image](#image-object) | N/A | N/A | | Image of the chat online button, available when `type` is `adaptive`. |
  | `adaptiveButtonOfflineIcon` | [Image](#image-object) | N/A | N/A | | Image of the chat offline button, available when `type` is `adaptive`. |
  | `isImageButtonFloating` | boolean | N/A | N/A | | Whether the image button is float or not, available when `type` is `image`. |
  | `imageButtonPosition` | string | N/A | N/A | | Position of the image button, including `centered`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available when `type` is `image`. |
  | `imageButtonPositionMode` | string | N/A | N/A | | Position mode of the image button, including `Basic` and `Advanced`, available when `type` is `image`. |
  | `isImageButtonXOffsetByPixel` | boolean | N/A | N/A | |                 available when `type` is `image`. |
  | `imageButtonXOffset` | integer | N/A | N/A | |  If Is XOffset By Pixel is True, it represents the offset pixel value of the X coordinate. If Is XOffset By Pixel is False, it represents the offset percentage value of the X coordinate, available when `type` is `image`. |
  | `isImageButtonYOffsetByPixel` | boolean | N/A | N/A | |                 available when `type` is `image`. |
  | `imageButtonYOffset` | integer | N/A | N/A | |  If Is YOffset By Pixel is True, it represents the offset pixel value of the Y coordinate. If Is YOffset By Pixel is False, it represents the offset percentage value of the Y coordinate, available when `type` is `image`. |
  | `imageButtonImageSource` | string | N/A | N/A | |  Type of the image source, including `fromGallery` and `fromMyComputer` |
  | `imageButtonOnlineImage` | [Image](#image-object) | N/A | N/A | | Image of online button, available when `type` is `image`. |
  | `imageButtonOfflineImage` | [Image](#image-object) | N/A | N/A | | Image of offline button, available when `type` is `image`. |
  | `imageButtonTypeOnMobile` | string | N/A | N/A | | The type of button on mobile device, including `text` and `image`, available when `type` is `image`. |
  | `imageButtonColorOnMobile` | string | N/A | N/A | | |
  | `imageButtonTextColorOnMobile` | string | N/A | N/A | | The theme color of chatbutton on mobile device. |
  | `imageButtonOnlineImageOnMobile` | [Image](#image-object) | N/A | N/A | | The Image on mobile device when any agents is online. |
  | `imageButtonOfflineImageOnMobile` | [Image](#image-object) | N/A | N/A | | The image on mobile device when no agent is online. |
  | `imageButtonPositionOnMobile` | string | N/A | N/A | | Position of the chat button on mobile device, including `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle`, `RightMiddle`, `leftBottom` and `rightBottom`. |
  | `imageButtonTypeOnMobile` | string | N/A | N/A | | the content of the text link, available when `type` is `textLink`. |

### Image Object

  Image is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put |Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid  | yes | N/A | | id of the current item. |
  | `name` | string  | no | yes | | name of the image |
  | `url` | string  | no | yes | | url of the image |

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

### Update Chat Button

  `PUT /api/v3/livechat/campaigns/{campaignId}/chatButton`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Chat Button](#Chat-Button-Object) structure

#### Response

the response is: [Chat Button](#Chat-Button-Object) Object

# Chat Window

- `GET /api/v3/livechat/campaigns/{campaignId}/chatWindow` - [Get settings of ChatWindow for a campaign](#get-chat-window)
- `PUT /api/v3/livechat/campaigns/{campaignId}/chatWindow` - [Update settings of ChatWindow for a campaign](#update-chat-window)

## Related Object Json Format

### Chat Window Object

  Chat Window Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `width` | integer | N/A | N/A | | |
  | `height` | integer | N/A | N/A | | |
  | `style` | string | N/A | yes | |  Style of the window's theme, including `classic`, `circle` and `bubble`. |
  | `color` | string | N/A | yes | |  Color of the window's theme. |
  | `type` | string | N/A | yes | | Type of the chat window, including `embedded` and `popup`. |
  | `headerType` | string | N/A | N/A | |  Type of the header, including `agentInfo`, `bannerImage` and `avatarAndLogo` when `style` is `classic`. |
  | `isAvatarDisplayed` | boolean | N/A | N/A | | Whether the avatar of the agent is visible or not, available when  `headerType` is `agentInfo` or `avatarAndLogo`. |
  | `isTitleDisplayed` | boolean | N/A | N/A | | Whether the title of the agent is visible or not, available when `headerType` is `agentInfo`. |
  | `isBioDisplayed` | boolean | N/A | N/A | | Whether the bio of the agent is visible or not, available when `headerType` is `agentInfo`. |
  | `isLogoDisplayed` | boolean | N/A | N/A | | Whether the logo is visible or not, available when `headerType` is `avatarAndLogo`. |
  | `logo` | [Image](#image-object) | N/A | N/A | | Image of the logo. |
  | `bannerImage` | [Image](#image-object) | N/A | N/A | | Image of the banner, available when `headerType` is `bannerImage`. |
  | `isAvatarDisplayedWithMessage` | boolean | N/A | N/A   | | Whether the avatar of the agent is visible or not in the message body, available when `style` is `classic`or `simple`. |
  | `isBackgroundDisplayed` | boolean | N/A | N/A | |  Whether the texture and picture of the background is visible or not in the message body, available when `style` is `classic`or `simple`. |
  | `backgroundTexture` | integer | N/A | N/A | | |
  | `customCSSOfClassic` | string | N/A | N/A | |  The content of custom css when  `style` is `classic`. |
  | `customCSSOfCircle` | string | N/A | N/A | |  The content of custom css when  `style` is `circle`. |
  | `isTranscriptDownloadAllowed` | boolean | N/A | N/A | | Whether the visitor can download the chat transcript. |
  | `isTranscriptPrintAllowed` | boolean | N/A | N/A | | Whether the visitor can print the chat transcript. |
  | `isTranscriptSentToVisitors` | boolean | N/A | N/A | | Whether the transcript send to visitor. |
  | `isTranscriptSentFromCurrentAgentEmail` | boolean | N/A | N/A | | Available when `isTranscriptDownloadAllowed` is true. |
  | `fromEmailName` | string | N/A | N/A | |  The from name for sending transcript email, available when `isTranscriptSentFromCurrentAgentEmail` is true. |
  | `fromEmailAddress` | string | N/A | N/A | |  The subject address for sending transcript email, available when `isTranscriptSentFromCurrentAgentEmail` is true. |
  | `isSMTPServerCustomized` | boolean | N/A | N/A | | Whether use custome SMTP server. |
  | `customSMTPServer.fromName` | string | N/A | N/A | | |
  | `customSMTPServer.fromEmail` | string | N/A | N/A | | |
  | `customSMTPServer.mailServer` | string | N/A | N/A | | |
  | `customSMTPServer.port` | integer | N/A | N/A | | |
  | `customSMTPServer.encryptedType` | string | N/A | N/A | | Including `none`, `SSL` and `TLS`.  |
  | `customSMTPServer.IsAuthenticationRequired` | boolean | N/A | N/A | | |
  | `customSMTPServer.username` | string | N/A | N/A | | |
  | `customSMTPServer.password` | string | N/A | N/A | | |
  | `isSwitchToOfflineMessageAllow` | boolean | N/A | N/A | | Allow visitors to switch to Offline Message Window while waiting for chat. |
  | `isFileSendAllow` | boolean | N/A | N/A | | Whether the agent can send file or not. |
  | `ifMarkUnreadMessage` | boolean | N/A | N/A | | |
  | `isAudioChatEnabled` | boolean | N/A | N/A | | Whether the agent can use audio chat. |
  | `isVideoChatEnabled` | boolean | N/A | N/A | | Whether the agent can use video chat. |
  | `isBrowserPopupNotificationEnabled` | boolean | N/A | N/A | | It is available for private server sites. For shared server clients, the push notification is disabled by default. |
  | `ifEndChatWhenVisitorIsInactive` | boolean | N/A | N/A | | Automatically end chats if visitors don't respond in period of time. |
  | `minutesOfVisitorInactivity` | integer | N/A | N/A | | |
  | `isTranscriptSentForArchiving` | boolean | N/A | N/A | | |
  | `receivingEmailAddressesForArchivingTranscripts` | string | N/A | N/A | | |
  | `emailSubjectForArchivingTranscripts` | string | N/A | N/A | | |
  | `greetingMessage` | string | N/A | N/A | | |
  | `isCustomJSEnabled:` | boolean | N/A | N/A | | |
  | `customJS` | string | N/A | N/A | | |

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

### Update Chat Window

  `PUT /api/v3/livechat/campaigns/{campaignId}/chatWindow`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Chat Window](#Chat-Window-Object) structure

#### Response

the response is: [Chat Window](#Chat-Window-Object) Object

# Pre-Chat

- `GET /api/v3/livechat/campaigns/{campaignId}/preChat` - [Get settings of Pre-Chat for a campaign](#get-Pre-Chat)
- `PUT /api/v3/livechat/campaigns/{campaignId}/preChat` - [Update settings of Pre-Chat for a campaign](#update-Pre-Chat)

## Related Object Json Format

### Pre-Chat Object

  Pre-Chat Window Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `isEnable` | boolean | N/A | yes | | Whether the pre-chat is enabled or not. |
  | `isTeamNameDisplayed` | boolean | N/A | N/A | | Whether the team name is visible or not in the header. |
  | `teamName` | string | N/A | N/A | | The team name displayed in the header. |
  | `isAgentAvatarDisplayed` | boolean | N/A | N/A   | | Whether the avatar of the agent is visible or not in the header. |
  | `greetingMessage` | string | N/A | N/A | | |
  | `socialMediaLogin` | string | N/A | N/A | |  Including `none` and `facebook`. |
  | `field` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | N/A | N/A | | These System Fields are prebuilt and can’t be deleted: `name`, `email`, `phone`, `company`, `product service`, `department`, `ticket id`.  |
  | `isVisitorInfoRecorded` | boolean | N/A | N/A | true | If remember visitor info collected from pre-chat form. |
  | `formFieldLayoutStyle` | string | N/A | N/A | | Including `leftofInput` and `aboveInput`. Available for Post Chat and Offline Message forms.  |

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

### Update Pre-Chat

  `PUT /api/v3/livechat/campaigns/{campaignId}/preChat`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Pre-Chat](#Pre-Chat-Object) structure

#### Response

the response is: [Pre-Chat](#Pre-Chat-Object) Object

# Post Chat

- `GET /api/v3/livechat/campaigns/{campaignId}/postChat` - [Get settings of PostChat for a campaign](#get-Post-Chat)
- `PUT /api/v3/livechat/campaigns/{campaignId}/postChat` - [Update settings of PostChat for a campaign](#update-Post-Chat)

## Related Object Json Format

### Post Chat  Object

  Post Chat Window Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `isEnable` | boolean | N/A | yes | | Whether the pot chat is enabled or not. |
  | `field` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | N/A | N/A | | These System Fields are prebuilt and can’t be deleted: `rating`, `rating comment`.  |
  | `greetingMessage` | string | N/A | N/A | | |

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

### Update Post Chat

  `PUT /api/v3/livechat/campaigns/{campaignId}/postChat`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `campaignId` | Guid | yes  |  the unique Id of the campaign |

Request Body

  The request body contains data with the [Post Chat](#Post-Chat-Object) structure

#### Response

the response is: [Post Chat](#Post-Chat-Object) Object

# Campaign Offline Message

- `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage` - [Get settings of OfflineMessage for a campaign](#get-Campaign-Offline-Message)
- `PUT /api/v3/livechat/campaigns/{campaignId}/offlineMessage` - [Update settings of OfflineMessage for a campaign](#update-Campaign-Offline-Message)

## Related Object Json Format

### Campaign Offline Message Object

  Offline Message Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `type` | string | N/A | N/A | | Including `systemOfflineMessageWindow` and `customOfflineMessagePage`. |
  | `customOfflineMessagePageURL` | string | N/A | N/A | | Available when Type is `customOfflineMessagePage`. |
  | `ifOpenCustomOfflineMessagePageInNewWindow` | boolean | N/A | N/A | | Available when Type is `customOfflineMessagePage`. |
  | `greetingMessage` | string | N/A | N/A | | |
  | `emailOfflineMessageTo` | string | N/A | N/A | | Including `allAgents` and `customEmailAddresses`, available when routing rule is disabled. |
  | `customEmailAddresses` | string | N/A | N/A | |  Available when routing rule is disabled.  |
  | `field` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | N/A | N/A | | These System Fields are prebuilt and can’t be deleted: `name`, `email`, `phone`, `company`, `product service`, `department`, `ticket id`.  |

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
  | `style` | string | N/A | N/A | | Including `bubble`, `popup` and `chatWindow`. |
  | `autoInvitation` | [Auto Invitation](#Auto-Invitation-Object)[] | N/A | N/A | | |
  | `manualInvitation` | [Manual Invitation](#Manual-Invitation-Object)[] | N/A | N/A | | |

### Manual Invitation Object

  Manual Invitation Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `manualInvitationPosition` | string | N/A | N/A | | Including `centerWithOverlay`, `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available When using `popup` Invitation Style.  |
  | `manualInvitationImageType` | string | N/A | N/A | | Including`fromGallery` and `fromMyComputer`.  |
  | `manualInvitationImage` | [Image](#image-object) | N/A | N/A | | Image of Invitation.  |
  | `manualInvitationCloseAreaXOffset` | integer | N/A | N/A | | |
  | `manualInvitationCloseAreaYOffset` | integer | N/A | N/A | | |
  | `manualInvitationCloseAreaWidth` | integer | N/A | N/A | | |
  | `manualInvitationCloseAreaHeight` | integer | N/A | N/A | | |
  | `manualInvitationTextAreaXOffset` | integer | N/A | N/A | | |
  | `manualInvitationTextAreaYOffset` | integer | N/A | N/A | | |
  | `manualInvitationTextAreaWidth` | integer | N/A | N/A | | |
  | `manualInvitationTextAreaHeight` | integer | N/A | N/A | | |
  | `manualInvitationText` | string | N/A | N/A | | |
  | `manualInvitationTextFont` | string | N/A | N/A | | Including `timesNewRoman`, `tahoma`, `verdana`, `arial`, `comicSansMs` and `courier`. |
  | `manualInvitationTextSize` | string | N/A | N/A | | Including `XXSmall`, `XSmall`, `small`, `medium`, `large`, `XLarge` and `XXLarge`. |
  | `isManualInvitationTextBold` | boolean | N/A | N/A | | |
  | `isManualInvitationTextItalic` | boolean | N/A | N/A | | |
  | `manualInvitationTextColor` | string | N/A | N/A | | |

### Auto Invitation Object

  Auto Invitation Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `name` | string | N/A | yes | | |
  | `isEnable` | boolean | N/A | N/A | | Whether the auto invitation is enabled or not. |
  | `isDisplayedOnceInOneSession` | boolean | N/A | N/A | | |
  | `order` | integer | N/A | N/A | | |
  | `imageType` | [Image](#image-object) | N/A | N/A | | Including`fromGallery` and `fromMyComputer`. |
  | `closeAreaXOffset` | integer | N/A | N/A | | |
  | `closeAreaYOffset` | integer | N/A | N/A | | |
  | `closeAreaWidth` | integer | N/A | N/A | | |
  | `closeAreaHeight` | integer | N/A | N/A | | |
  | `textAreaXOffset` | integer | N/A | N/A | | |
  | `textAreaYOffset` | integer | N/A | N/A | | |
  | `textAreaWidth` | integer | N/A | N/A | | |
  | `textAreaHeight` | integer | N/A | N/A | | |
  | `text` | string | N/A | N/A | | |
  | `textFont` | string | N/A | N/A | | Including `timesNewRoman`, `tahoma`, `verdana`, `arial`, `comicSansMs` and `courier`. |
  | `textSize` | string | N/A | N/A | | Including `XXSmall`, `XSmall`, `small`, `medium`, `large`, `XLarge` and `XXLarge`. |
  | `isTextBold` | boolean | N/A | N/A | | |
  | `isTextItalic` | boolean | N/A | N/A | | |
  | `textColor` | string | N/A | N/A | | |
  | `position` | string | N/A | N/A | | Including `centerWithOverlay`, `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`.  |
  | `conditionMetType` | string | N/A | N/A | | Including `all`, `any` and `logicalExpression`. |
  | `logicalExpression` | string | N/A | N/A | | |
  | `condition` | [Live Chat Condition](#Live-Chat-Condition-Object)[] | N/A | N/A | | |

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
  | `style` | string | N/A | N/A | | Including `bubble`, `popup` and `chatWindow`. |

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
  | `field` | [Campaign Form Field](#Campaign-Form-Field-Object)[] | N/A | N/A | | These System Fields are prebuilt and can’t be deleted: `agent wrap-up category`, `agent wrap-up comments`.  |

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
  | `defaultLanguage` | string | N/A | N/A | | The languages are defined in cPanel.  |
  | `isCustomLanguageEnabled` | boolean | N/A | N/A | | |
  | `isTextDirectionRightToLeft` | boolean | N/A | N/A | | |
  | `customLanguageItem` | [Custom Language](#Custom-Language-Object)[] | N/A | N/A | | |

### Custom Language Object

  Custom Language Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `systemName` | string | N/A | N/A | | |
  | `customText` | string | N/A | N/A | | |

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
  | `isEnable` | boolean |  | N/A | N/A |  false | Whether the routing rule is enabled or not. |
  | `type` | string |  | N/A | N/A | | Including `simple` and `customRule`. |
  | `routeTo` | [Agent](#Agent-Object) or [Department](#Department-Object) | yes | N/A | N/A | |  |
  | `priority` | string |  | N/A | N/A | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `percentageToBot` | integer |  | N/A | N/A | | |
  | `customRule` | [Custom Rule](#Custom-Rule-Object)[] |  | N/A | N/A | | |
  | `actionWhenNoRuleMatched` | string |  | N/A | N/A | | Including `routeToSite`, `routeToDepartment`, `routeToAgent` and `redirectToOfflineMessage`. |
  | `routeToWhenNoRuleMatched` | [Agent](#Agent-Object) or [Department](#Department-Object) | yes | N/A | N/A | |  |
  | `priorityWhenNoRuleMatched` | string |  | N/A | N/A | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `percentageToBotWhenNoRuleMatched` | integer |  | N/A | N/A | | |
  | `emailsToReceiveOfflineMessage` | string |  | N/A | N/A | |  |

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

- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Get a list of custom rules](#get-all-Custom-Rule)
- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Get a custom rule by id](#get-a-Custom-Rule-by-id)
- `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Create a custom rule](#create-a-new-Custom-Rule)
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Update a custom rule](#update-a-Custom-Rule)
- `DELETE /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Delete a custom rule](#delete-a-Custom-Rule)

## Related Object Json Format

### Custom Rule Object

  Custom Rule Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `id` | Guid | yes | | N/A | | Id of the current item. |
  | `isEnable` | boolean | | N/A | N/A | | Whether the custom rule is enabled or not. |
  | `name` | string | | N/A | N/A | | |
  | `order` | integer | | N/A | N/A | | |
  | `routeTo` | [Agent](#Agent-Object) or [Department](#Department-Object) | yes | N/A | N/A | |  |
  | `priority` | string | | N/A | N/A | | Including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `percentageToBot` | integer | | N/A | N/A | | |
  | `conditionMetType` | string | | N/A | N/A | | Including `all`, `any` and `logicalExpression`. |
  | `logicalExpression` | string | | N/A | N/A | | |
  | `condition` | [Live Chat Condition](#Live-Chat-Condition-Object)[] | | N/A | N/A | | |

### Live Chat Condition Object

  Live Chat Condition Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `field` | string | N/A | N/A | | |
  | `operator` | integer | N/A | N/A | | Include `is`, `isNot`, `contains`, `doesnotcontain`, `isMoreThan`, `isNotMoreThan`, `isLessThan`, `isNotLessThan` and `regularExpression`. |
  | `value` | string | N/A | N/A | | |
  | `order` | integer | N/A | N/A | | |

## Routing Endpoints

### Get all Custom Rule

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
  | `isEnable` | boolean | | N/A | N/A | | Whether the chatbot integration is enabled or not. |
  | `selectedChatbot` | [Chatbot](#Chatbot-Object) | yes | N/A | N/A | | |
  | `isChatbotAllocatedWhenAgentOnline` | boolean | | N/A | N/A | | |
  | `ifDistributeChatsToChatbotByQueueLength` | boolean | | N/A | N/A | | |
  | `ifDistributeChatsToChatbotByPercentage` | boolean | | N/A | N/A | | |
  | `queueLength` | integer | | N/A | N/A | | Allocate chats to Chatbot when the queue reaches the preset length. |
  | `percentageToChatbot` | smallint | | N/A | N/A | | |
  | `isChatbotAllocatedWhenAgentOffline` | boolean | | N/A | N/A | | |

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
  | `isEnable` | boolean | N/A | N/A | | Whether the KB integration is enabled or not. |
  | `selectedKB` | [KB](#KB-Object) | N/A | N/A | | |
  | `isSearchAllowedBeforeChatting` | boolean | N/A | N/A | | |
  | `greetingMessageBeforeChatting` | string | N/A | N/A | | |
  | `isSearchAllowedBeforeOfflineMessage` | boolean | N/A | N/A | | |
  | `greetingMessageBeforeOfflineMessage` | string | N/A | N/A | | |
  | `articlesShowedInSearchResult` | integer | N/A | N/A | | |

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
  | `field` | [type](#Live-Chat-Field-Object) | N/A | N/A | | |
  | `isVisible` | boolean | N/A | N/A | | Whether the field is visible or not. |
  | `isRequired` | boolean | N/A | N/A | | Whether the field is required or not when submitting the form |
  | `order` | integer | N/A | N/A | | The order of the field. |
  | `ratingGrade` | [type](#Rating-Grade-Object) | N/A | N/A | | |

### Rating Grade Object

  Rating Grade is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | Id of the current item. |
  | `grade` | integer | N/A | N/A | | |
  | `label` | string | N/A | N/A | | |
  | `isVisible` | boolean | N/A | N/A | | |

### Live Chat Field Object

  Live Chat Field is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid | yes | N/A | | Id of the current item. |
  | `isSystem` | boolean | N/A | N/A | | whether the field is system or not. |
  | `name` | string | N/A | N/A | | |
  | `type` | string | N/A | N/A | | The [Live Chat Field Type](#Live-Chat-Field-Type) of the field. |
  | `option` | [Live Chat Field Option](#Live-Chat-Field-Option-Object)[] | N/A | N/A | | Live Chat Field Option, available whey Type is `radioBox`, `dropdownList`, `checkboxList`. |
  | `leftText` | string | N/A | N/A | | Available whey Type is NPS. |
  | `rightText` | string | N/A | N/A | | Available whey Type is NPS. |
  | `optionGroup` | [Live Chat Field Option Group](#Live-Chat-Field-Option-Group-Object)[] | N/A | N/A | | Live Chat Field Option Group, available whey Type is `checkboxListwithOptionGroups`. |

### Live Chat System Field

  Live Chat System Field is one key of the following keys:

  | System Field | Type | Only Available Forms | Is Required |
  | - | - | :-: | - |
  | `name` | `textBox` | Name field, `Pre Chat Form` or `Offline Message Form` only. | N/A |
  | `email` | `textBox` | Email field, `Pre Chat Form` or `Offline Message Form` only. | N/A |
  | `phone` | `textBox` | Phone field, `Pre Chat Form` or `Offline Message Form` only. | N/A |
  | `company` | `textBox` | Company field, `Pre Chat Form` or `Offline Message Form` only. | N/A |
  | `product service` | `dropdownList` | Product and Service field, `Pre Chat Form` only. | N/A |
  | `department` | `dropdownList` | Department field, `Pre Chat Form` or `Offline Message Form` only. | N/A |
  | `ticket id` | `textBox` | Ticket field, `Pre Chat Form` or `Offline Message Form` only.  | N/A |
  | `rating` | `rating` | Rating field, `Post Chat Form` only. | N/A |
  | `rating comment` | `textArea` | Comments field, `Post Chat Form` only. | N/A |
  | `subject` | `textBox` | Subject field, `Offline Message Form` only. | yes |
  | `message` | `textArea` | Content field, `Offline Message Form` only. | N/A |
  | `attachment` | `file` | Attachment field, `Offline Message Form` only. | N/A |
  | `category` | `dropdownList` or `checkboxListwithOptionGroups`  | category field , `agent wrap-up` only | N/A |
  | `wrap-up comment` | `textArea` | comment field , `agent wrap-up` only | N/A |

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
  | `value` | string | N/A | N/A | | |
  | `order` | integer | N/A | N/A | | |

### Live Chat Field Option Group Object

  Live Chat Field Option Group Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `name` | string | N/A | N/A | | |
  | `order` | integer | N/A | N/A | | |
  | `option` | [Live Chat Field Option](#Live-Chat-Field-Option-Object)[]  | N/A | N/A | | |

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

### Remove a ban

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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `id` | Guid  | yes | no || id of the custom variable. |
  | `name` | string  | no | yes || name of the custom variable |.
  | `type` | string  | no | yes || type of the custom variable., including `text`, `integer` and `decimal`. |
  | `value` | string  | no | nos || value of the custom variable. |
  |`hyperlink` | string  | no | no ||  hyperlink of the custom variable. |

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
