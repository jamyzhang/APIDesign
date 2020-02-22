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

# Online Visitor  

//修改ER
//todo

- `GET /api/v3/livechat/visitors` - [Get a list of visitors in livechat](#get-all-visitors)
- `GET /api/v3/livechat/visitors/{id}` - [Get a visitor by id](#get-a-visitor)  
- `POST /api/v3/livechat/visitors/{id}/customVariables:change` - [update a visitor's custom variables](#update-a-visitor-custom-variables)

# Online Agent  

//修改ER
//todo

- `GET /api/v3/livechat/agents` - [Get a list of agents in livechat](#get-all-agents)
- `GET /api/v3/livechat/agents/{id}` - [Get an agent by id](#get-an-agent)  
- `PUT /api/v3/livechat/agents/{id}` - [Update an agent](#update-an-agent)  

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

the response is: [Campaign](#Campaign-Object) Object

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

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the campaign |

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

the response is: [Auto Invitation](#Auto-Invitation-Object) Object

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
  | `id` | Guid | yes  |  the unique Id of the auto invitation |

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

- `GET /api/v3/livechat/campaigns/{campaignId}/routing` - [Get settings of routing for a campaign](#get-site-info) include department, agent
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing` - [Update settings of routing for a campaign](#update-site-info)

# Custom Rule

- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Get a list of custom rules](#get-site-info) include department, agent
- `GET /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Get a custom rule by id](#get-site-info) include department, agent
- `POST /api/v3/livechat/campaigns/{campaignId}/routing/customRules` - [Create a custom rule](#get-site-info)
- `PUT /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Update a custom rule](#update-site-info)
- `DELETE /api/v3/livechat/campaigns/{campaignId}/routing/customRules/{id}` - [Delete a custom rule](#delete-a-customer-segment)

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

- `GET /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Get a list of form fields of Pre-Chat for a campaign](#get-site-info)
- `POST /api/v3/livechat/campaigns/{campaignId}/preChat/campaignFormFields` - [Create a form field of Pre-Chat for a campaign](#update-site-info)
- `GET /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Get a list of form fields of Post Chat for a campaign](#get-site-info)
- `POST /api/v3/livechat/campaigns/{campaignId}/postChat/campaignFormFields` - [Create a form field of Post Chat for a campaign](#update-site-info)
- `GET /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Get a list of form fields of offline message for a campaign](#get-site-info)
- `POST /api/v3/livechat/campaigns/{campaignId}/offlineMessage/campaignFormFields` - [Create a form field of offline message for a campaign](#update-site-info)
- `GET /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Get a list of form fields of agent wrapup for a campaign](#get-site-info)
- `POST /api/v3/livechat/campaigns/{campaignId}/agentWrapup/campaignFormFields` - [Create a form field of agent wrapup for a campaign](#update-site-info)
- `GET /api/v3/livechat/campaignFormFields/{id}` - [Get a campaign form field by id](#get-a-campaign-form-field)
- `PUT /api/v3/livechat/campaignFormFields/{id}` - [Update a campaign form field](#update-a-campaign-form-field)
- `DELETE /api/v3/livechat/campaignFormFields/{id}` - [Delete a campaign form field](#delete-a-campaign-form-field)

# Ban

- `GET /api/v3/livechat/bans` - [Get a list of bans](#get-site-bans) include visitor, agent
- `GET /api/v3/livechat/bans/{id}` - [Get a ban by id](#get-a-ban) include visitor, agent
- `POST /api/v3/livechat/bans` - [Create a ban](#get-a-ban)
- `PUT /api/v3/livechat/bans/{id}` - [Update a ban](#update-a-ban)
- `DELETE /api/v3/livechat/bans/{id}` - [Delete a ban](#delete-a-ban)

# Conversion Action

- `GET /api/v3/livechat/conversionActions` - [Get a list of conversion actions](#get-site-campaigns) include customVariable, agent
- `GET /api/v3/livechat/conversionActions/{id}` - [Get a conversion action by id](#get-a-campaign)  include customVariable, agent
- `POST /api/v3/livechat/conversionActions` - [Create a conversion action](#get-a-campaign)
- `PUT /api/v3/livechat/conversionActions/{id}` - [Update a conversion action](#update-a-campaign)
- `POST /api/v3/livechat/conversionActions:achieved`[Make api conversion succesful](#make-api-conversion-succesful)

# Secure Form

- `GET /api/v3/livechat/secureForms` - [Get a list of secureForms](#get-site-secure-forms)
- `GET /api/v3/livechat/secureForms/{id}` - [Get a secure form by id](#get-a-secure-form)
- `POST /api/v3/livechat/secureForms` - [Create a secure form](#get-a-secure-form)
- `PUT /api/v3/livechat/secureForms/{id}` - [Update a secure form](#update-a-secure-form)
- `DELETE /api/v3/livechat/secureForms/{id}` - [Delete a secure form](#delete-a-secure-form)

# Custom Variable

- `GET /api/v3/livechat/customVariables` - [Get a list of custom variables](#get-site-custom-variables)
- `GET /api/v3/livechat/campacustomVariablesigns/{id}` - [Get a custom variable by id](#get-a-custom-variable)
- `POST /api/v3/livechat/customVariables` - [Create a custom variable](#get-a-custom-variable)
- `PUT /api/v3/livechat/customVariables/{id}` - [Update a custom variable](#update-a-custom-variable)
- `DELETE /api/v3/livechat/customVariables/{id}` - [Delete a custom variable](#delete-a-custom-variable)

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
