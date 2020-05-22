# LivechatRestfulAPI

Comm100 Live Chat API allows you to pull the raw LiveChat data from Comm100 Live Chat into your systems.

<div>

## Campaigns

  You need the `Manage Campaigns` permission to manage campaigns and customize the settings for campaigns.

- `Campaigns` - Campaigns Manage
  - `GET /api/v2/livechat/campaigns` - Get a list of campaigns
  - `GET /api/v2/livechat/campaigns/{id}` - Get a campaign by id
  - `POST /api/v2/livechat/campaigns` - Create a new campaign
  - `PUT /api/v2/livechat/campaigns/{id}` - Update a campaign
  - `DELETE /api/v2/livechat/campaigns/{id}` - Remove a campaign
- `Campaign Settings` - setting of campaign
  - `GET /api/v2/livechat/campaigns/{id}/code` - Get installation code of a campaign
  - `GET /api/v2/livechat/campaigns/{id}/chatButton` - Get settings of ChatButton for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/chatButton` - Update settings of ChatButton for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/chatWindow`  - Get settings of ChatWindow for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/chatWindow`  - Update settings of ChatWindow for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/preChat`  - Get settings of PreChat for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/preChat`  - Update settings of PreChat for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/postChat` - Get settings of PostChat for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/postChat` - Update settings of PostChat for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/offlineMessage`  - Get settings of OfflineMessage for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/offlineMessage`  - Update settings of OfflineMessage for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/invitation`  - Get settings of invitation for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/invitation`  - Update settings of invitation for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`  - Get a autoInvitation for a campaign
  - `POST /api/v2/livechat/campaigns/{id}/invitation/autoInvitations`  - Create a new auto invitation for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`  - Update auto invitation for a campaign
  - `DELETE /api/v2/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`  - Delete auto invitation for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/agentWrapup`  - Get settings of Agent Wrap Up for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/agentWrapup`  - Update settings of Agent Wrap Up for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/RoutingRules` - Get settings of Routing Rules for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/RoutingRules` - Update settings of Routing Rules for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/RoutingRule/customRules/{customeRule_id}` - Get a custom rule for a campaign
  - `POST /api/v2/livechat/campaigns/{id}/RoutingRule/customRules` - Create a new custom rule for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/RoutingRule/customRules/{customeRule_id}` - Update a custom rule for a campaign
  - `DELETE /api/v2/livechat/campaigns/{id}/RoutingRule/customRules/{customeRule_id}` - Delete a custom rule for a campaign
  - `GET /api/v2/livechat/campaigns/{id}/language` - Get settings of Language for a campaign
  - `PUT /api/v2/livechat/campaigns/{id}/language` - Update settings of Language for a campaign

<div>

### Model

#### Campaign JSON Format

  Campaign is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no | id of the campaign |
  | `name` | string  | no | yes | name of the campaign |
  | `description` | string  | no | no | description of the campaign |
  | `language` | string  | no | yes | language of the campaign |

</div>
<div>

### Endpoint

#### Get a list of campaigns

  `GET /api/v2/livechat/campaigns`

- Parameters:

    No parameters

- Response:

    An array of [Campaign](#campaign-json-format)

#### Example

Sample request:

```shell
curl https://hosted.comm100.com/api/v2/livechat/campaigns  
     -X GET -k -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"
```

Sample response:

```json
[
    {
        "id": 1,
        "name": "Default Plan",
        "description": "Default Plan",
        "language": "English"
    },
    {
        "id": 4,
        "name": "CP_english",
        "description": "campaign test",
        "language": "English"
    },
    {
        "id": 10,
        "name": "CP_france",
        "description": "this is campaign test",
        "language": "French"
    },
    ...
]
```

#### Get a campaign by id

  `GET /api/v2/livechat/campaigns/{id}`

- Parameters:

    No parameters

- Response:

    [Campaign](#campaign-json-format)
  
#### Example

Sample request:

```shell
curl https://hosted.comm100.com/api/v2/livechat/campaigns/4  
     -X GET -k -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"
```

Sample response:

```json
{
    "id": 4,
    "name": "CP_english",
    "description": "campaign test",
    "language": "English"
}
```

#### Create a new campaign
  
  `POST /api/v2/livechat/campaigns`

- Parameters:

    [Campaign](#campaign-json-format)

- Response:

    [Campaign](#campaign-json-format)
  
#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "grubbytest","description" : "grubby","language" : "english"}"    
     https://hosted.comm100.com/api/v2/livechat/campaigns
```

Sample response:

```json
{
    "id": 20,
    "name": "grubbytest",
    "description": "grubby",
    "language": "English"
}
```  

#### Update a campaign

  `PUT /api/v2/livechat/campaigns/{id}`

- Parameters:

    Campaign Object

- Response:

    [Campaign](#campaign-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "grubbytest1","description" : "grubby1","language" : "english"}"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/20
```

Sample response:

```json
{
    "id": 20,
    "name": "grubbytest1",
    "description": "grubby1",
    "language": "English"
}
```

#### Remove a campaign
  
  `DELETE /api/v2/livechat/campaigns/{id}`

- Parameters

    No parameters.

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/campaigns/20
```

Sample response:

```json
"Campaign with id '20' has been removed."
```

</div>
</div>
<div>

## Installation Code

<div>

### Endpoint

#### Get installation code of a campaign
  
  `GET /api/v2/livechat/campaigns/{id}/code`

- Parameters:

    No parameters

- Response

  - `code` - installation code for the campaign.

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/code
```

Sample response:

```javascript
<!--Begin Tester Code-->
<div id=\"livechat-button-1\"></div>
  <script type=\"text/javascript\">
    var Comm100API=Comm100API||{};(function(t){function e(e){var a=document.createElement(\"script\"),c=document.getElementsByTagName(\"script\")[0];a.type=\"text/javascript\",a.async=!0,a.src=e+t.site_id,c.parentNode.insertBefore(a,c)}t.chat_buttons=t.chat_buttons||[],t.chat_buttons.push({code_plan:1,div_id:\"livechat-button-1\"}),t.site_id=[SiteId],t.main_code_plan=1,e(\"  
     https://hosted.comm100.com/chatserver/livechat.ashx?siteId=\"),setTimeout(function(){t.loaded||e(\"  
     https://hosted.comm100.com/chatserver/livechat.ashx?siteId=\")},5e3)})(Comm100API||{})
  </script>
<!--End Tester Code-->
```

</div>
</div>
<div>

## Chat Button

<div>

### Model

#### Chat Button JSON Format

  Chat Button is represented as simple flat JSON objects with the following keys:  

  | NameN| Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `type` | string | no | yes | type of the button, including `adaptive`, `image` and `textLink`. |
  | `isHideOffline` | boolean | no | no | whether the chat button is visible when no agent is online.`true` means that button is invisible. |
  | `isUseDomainRestriction` | boolean | no | no | whether the domain restriction is enabled or not. |
  | `allowedDomains` | array | no | no | an array of domains/urls, on which the chat button is visible. |
  | `adaptive.themeColor` | string | no | no | the theme color of the chat button, available when `type` is `adaptive`. |
  | `adaptive.icon` | string | no | no | icon of the chat button, available when `type` is `adaptive`. |
  | `image.type` | string | no | no |  `gallery` or `custom` |
  | `image.onlineImageId` | int | no | no | id of the image when any agents is online, available when `type` is `image`. |
  | `image.offlineImageId` | int | no | no | id of the image when no agent is online, available when `type` is `image`. |
  | `image.isFloat` | boolean | no | no |    whether the chat button is float or not, available when `type` is `image`. |
  | `image.position.type` | string | no | no | position of the chat button, including `centered`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`, available when `type` is `image`. |
  | `image.position.x` | string | no | no | vertical axis of the button, allowed as a number or percentage like `10` or `10%`, available when `type` is `image`. |
  | `image.position.y` | string | no | no | horizontal axis of the button, allowed as a number or percentage like `10` or `10%`, available when `type` is `image`. |
  | `image.mobile.type` | string | no | no | the type of button on mobile device, including `text` and `image`, available when `type` is `image`. |
  | `image.mobile.onlineText` | string | no | no | the content of text on mobile device when online, available when `image.mobile.type` is `text` and `type` is `image`. |
  | `image.mobile.offlineText` | string | no | no | the content of text on mobile device when no agent is online, available when `image.mobile.type` is `text` and `type` is `image`. |
  | `image.mobile.themeColor` | string | no | no | the theme color of chatbutton on mobile device, available when `image.mobile.type` is `text` and `type` is `image`. |
  | `image.mobile.onlineImageId` | string | no | no | the id of image on mobile device when any agents is online, available when `image.mobile.type` is `image` and `type` is `image`. |
  | `image.mobile.offlineImageId` | string | no | no | the id of image on mobile device when no agent is online, available when `image.mobile.type` is `image` and `type` is `image`. |
  | `image.mobile.position` | string | no | no | position of the chat button on mobile device, including `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle`, `RightMiddle`, `leftBottom` and `rightBottom`, available when `image.mobile.type` is `image` and `type` is `image`. |
  | `textLink.text` | string | no | no | the content of the text link, available when `type` is `textLink`. |

</div>
<div>

### Endpoint

#### Get ChatButton configuration of a campaign
  
  `GET /api/v2/livechat/campaigns/{id}/chatButton`

- Parameters:

    No parameters

- Response:

    [Chat Button](#chat-button-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/chatbutton
```

Sample response:

```json
{
    "type": "image",
    "isHideOffline": false,
    "isUseDomainRestriction": false,
    "allowedDomains": [ ],
    "adaptive": {
        "themeColor": "#329fd9",
        "icon": 0
    },
    "image": {
        "type": "gallery",
        "onlineImageId": 4275,
        "offlineImageId": 4274,
        "isFloat": true,
        "position": {
            "type": "bottomright",
            "x": "20",
            "y": "0%"
        },
        "mobile": {
            "type": "text",
            "onlineText": "Chat with us",
            "offlineText": "Leave a message",
            "themeColor": "#329FD9",
            "onlineImageId": 0,
            "offlineImageId": 0,
            "position": "bottommiddle"
        }
    },
    "textLink": {
        "text": "Chat Now"
    }
}
```

#### Update ChatButton configuration for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/chatButton`

- Parameters:

    [Chat Button](#chat-button-json-format)

- Response:

    [Chat Button](#chat-button-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json" -d "{"type" : "adaptive"}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/chatbutton
```

Sample response:

```json
{
    "type": "adaptive",
    "isHideOffline": false,
    "isUseDomainRestriction": false,
    "allowedDomains": [ ],
    "adaptive": {
        "themeColor": "#329FD9",
        "icon": 0
    },
    "image": {
        "type": "gallery",
        "onlineImageId": 4275,
        "offlineImageId": 4274,
        "isFloat": true,
        "position": {
            "type": "bottomright",
            "x": "20",
            "y": "0%"
        },
        "mobile": {
            "type": "text",
            "onlineText": "Chat with us",
            "offlineText": "Leave a message",
            "themeColor": "#329FD9",
            "onlineImageId": 0,
            "offlineImageId": 0,
            "position": "bottommiddle"
        }
    },
    "textLink": {
        "text": "Chat Now"
    }
}
```

</div>
</div>
<div>

## Chat Window

<div>

### Model

#### Chat Window JSON Format

  Chat Window is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `style` | string | no | yes | style of the window's theme, including `classic`, `simple` and `bubble`. |
  | `color` | string | no | yes | color of the window's theme. |
  | `type` | string | no | yes | type of the chat window, including `embedded` and `popup`. |
  | `customCSS` | string | no | no | the content of custom css. |
  | `popup.title` | string | no | no | title of the chat window, available when `type` is `popup`. |
  | `options.isCanPrintTranscript` | boolean | no | no | chat details can be printed |
  | `options.isCanEmailTranscript` | boolean | no | no | chat transcripts can be emailed to visitors |
  | `options.email.isFromAgent` | boolean | no | no | whether email is set from agent email or from a specified address. |
  | `options.email.fromEmail` | string | no | no | a specified email for from address. |
  | `options.email.fromName` | string | no | no | a specified name for from address. |
  | `options.isCanSwitchToOffline` | boolean | no | no | allow visitors to switch to Offline Message Window while waiting for chat. |
  | `options.isCanSendFile` | boolean | no | no | whether the agent can send file or not. |
  | `options.isCanAudioChat` | boolean | no | no | whether the agent can use audio chat. |
  | `options.isCanVideoChat` | boolean | no | no | whether the agent can use video chat. |
  | `options.isCanSentSeen`  | boolean | no | no | whether there is read receipt for message on the visitor side. |
  | `options.isCanDownloadPDF` | boolean | no | no | whether the visitor can download the chat transcript in PDF format. |
  | `advanced.isAutoEndChatWhenVisitorInactivity` | boolean | no | no | whether chat ends automatically if visitors don't respond. |
  | `advanced.timeAutoEndChatWhenVisitorInactivity` | integer | no | no | the time during which there is no visitor response received, the time unit is Second and the values can be `180`, `300`, `600`, `900`, `1200`, `1800` or `3600`.  |
  | `advanced.isAutoSendTranscriptToEmail` | boolean | no | no | whether the agent can send transcript email after chat ending. |
  | `advanced.transcriptEmailAddress` | string | no | no | the email address for sending transcript email. |
  | `advanced.transcriptEmailSubject` | string | no | no | the subject address for sending transcript email. |
  | `advanced.greetingMessage` | string | no | no | the content of greeting message. |
  | `advanced.isUseCustomJS` | boolean | no | no | whether the agent can add custom js to chat window or not. |
  | `advanced.customJS` | string | no | no | the content of custom javascript. |
  | `advanced.ifEnableChatQueueMaxLength` | boolean | no | no | Whether to open chat queue function. |
  | `advanced.chatQueueMaxLength` | int | no | no | chat queue maximum length. |
  | `advanced.chatQueueMaxWaitTime` | int | no | no | chat queue maximum wait time. |
  | `advanced.chatQueueLimitsMessage` | string | no | no | message when chat get limit. |
  | `header.type` | string | no | no | type of the header, including `agentInfo`, `bannerImage` and `avatarAndLogo` when `style` is `classic`, including `agentInfo` `bannerImage` when `style` is `simple`. |
  | `header.agentInfo.isShowAvatar` | boolean | no | no | whether the avatar of the agent is visible or not, available when `style` is `classic`or `simple` and `header.type` is `agentInfo` or `avatarAndLogo`. |
  | `header.agentInfo.isShowTitle` | boolean | no | no | whether the title of the agent is visible or not, available when `style` is `classic`or `simple` and `header.type` is `agentInfo`. |
  | `header.agentInfo.isShowBio` | boolean | no | no | whether the bio of the agent is visible or not, available when `style` is `classic`or `simple` and `header.type` is `agentInfo`. |
  | `header.banner.imageType` | string | no | no | `custom` or `gallery` |
  | `header.banner.imageId` | int | no | no | id of the image in the header of chat window, available when `style` is `classic`or `simple` and `header.type` is `bannerImage`. |
  | `header.avatarAndLogo.isShowAvatar` | boolean | no | no | whether the agent avatar is visible or not, available when `style` is `classic` and `header.type` is `avatarAndLogo`. |
  | `header.avatarAndLogo.isShowLogo` | boolean | no | no | whether the logo of the company is visible or not, available when `style` is `classic` and `header.type` is `avatarAndLogo`. |
  | `header.avatarAndLogo.logoImageId` | int | no | no | id of the company logo image in the header of chat window, available when `style` is `classic` and `header.type` is `avatarAndLogo`. |
  | `body.isShowAvatar` | boolean | no | no | whether the avatar of the agent is visible or not in the message body, available when `style` is `classic`or `simple`. |
  | `body.isShowBackground` | boolean | no | no | whether the texture and picture of the background is visible or not in the message body, available when `style` is `classic`or `simple`. |
  | `body.backgroudImageId` | int | no | no | id of the company image in the message body, available when `style` is `classic`or `simple`. |

</div>
<div>

### Endpoint

#### Get ChatWindow configuration of a campaign

  `GET /api/v2/livechat/campaigns/{id}/chatWindow`

- Parameters:

    No parameters

- Response:

    [Chat Window](#chat-window-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/chatwindow
```

Sample response:

```json
{
    "style": "classic",
    "color": "#329fd9",
    "type": "embedded",
    "popup": {
        "title": "Comm100 Live Chat - Chat Window"
    },
    "options": {
        "isCanPrintTranscript": false,
        "isCanEmailTranscript": true,
        "email": {
            "isFromAgent": true,
            "fromEmail": "",
            "fromName": ""
        },
        "isCanSwitchToOffline": true,
        "isCanSendFile": true,
        "isCanAudioChat": false,
        "isCanVideoChat": false,
        "isCanSentSeen" : false,
        "isCanDownloadPDF" : true
    },
    "advanced": {
        "isAutoEndChatWhenVisitorInactivity": false,
        "timeAutoEndChatWhenVisitorInactivity": 0,
        "isAutoSendTranscriptToEmail": false,
        "transcriptEmailAddress": "",
        "transcriptEmailSubject": "Chat transcript: {!Agent.Name} with {!Visitor.Name}",
        "greetingMessage": "",
        "isUseCustomJS": false,
        "customJS": "",
        "ifEnableChatQueueMaxLength": false,
        "chatQueueMaxLength": 10,
        "chatQueueMaxWaitTime": 10,
        "chatQueueLimitsMessage": ""

    },
    "customCSS": "",
    "header": {
        "type": "agentinfo",
        "agentInfo": {
            "isShowAvatar": true,
            "isShowTitle": false,
            "isShowBio": false
        },
        "banner": {
            "imageId": 4290,
            "imageType": "gallery"
        },
        "avatarAndLogo": {
            "isShowLogo": true,
            "isAvatar": true,
            "logoImageId": 0
        }
    },
    "body": {
        "isShowAvatar": true,
        "isShowBackground": true,
        "backgroundImageId": 0
    }
}
```

#### Update ChatWindow configuration of a campaign

  `PUT /api/v2/livechat/campaigns/{id}/chatWindow`

- Parameters:

    [Chat Window](#chat-window-json-format)

- Response:

    [Chat Window](#chat-window-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"style" : "bubble","color" : "#329fd9","type" : "popup"}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/chatwindow
```

Sample response:

```json
{
    "style": "bubble",
    "color": "#329FD9",
    "type": "popup",
    "popup": {
        "title": "Comm100 Live Chat - Chat Window"
    },
    "options": {
        "isCanPrintTranscript": false,
        "isCanEmailTranscript": true,
        "email": {
            "isFromAgent": true,
            "fromEmail": "",
            "fromName": ""
        },
        "isCanSwitchToOffline": true,
        "isCanSendFile": true,
        "isCanAudioChat": false,
        "isCanVideoChat": false,
        "isCanSentSeen" : false,
        "isCanDownloadPDF" : true
    },
    "advanced": {
        "isAutoEndChatWhenVisitorInactivity": false,
        "timeAutoEndChatWhenVisitorInactivity": 0,
        "isAutoSendTranscriptToEmail": false,
        "transcriptEmailAddress": "",
        "transcriptEmailSubject": "Chat transcript: {!Agent.Name} with {!Visitor.Name}",
        "greetingMessage": "",
        "isUseCustomJS": false,
        "customJS": "",
        "ifEnableChatQueueMaxLength": false,
        "chatQueueMaxLength": 10,
        "chatQueueMaxWaitTime": 10,
        "chatQueueLimitsMessage": ""
    },
    "customCSS": "",
    "header": {
        "type": "agentinfo",
        "agentInfo": {
            "isShowAvatar": true,
            "isShowTitle": false,
            "isShowBio": false
        },
        "banner": {
            "imageId": 4290,
            "imageType": "gallery"
        },
        "avatarAndLogo": {
            "isShowLogo": true,
            "isAvatar": true,
            "logoImageId": 0
        }
    },
    "body": {
        "isShowAvatar": true,
        "isShowBackground": true,
        "backgroundImageId": 0
    }
}
```

</div>
</div>
<div>

## Pre-Chat

<div>

### Model

#### Pre-Chat JSON Format

  Pre-Chat is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `isEnable` | boolean | no | yes | whether the pre-chat is enabled or not. |
  | `header.isShowTeamName` | boolean | no | no | whether the team name is visible or not in the header. |
  | `header.teamName` | string | no | no | the team name displayed in the header. |
  | `header.isShowAvatars` | boolean | no | no | whether the avatar of the agent is visible or not in the header. |
  | `greetingMessage` | string | no | no | content of the greeting message. |
  | `socialLogin.isUseFacebook` | boolean | no | no | whether Facebook is enabled or not in social login. |
  | `isRememberVisitorInfo` | boolean | no | no | whether visitor info is remembered or not from pre-chat form. |
  | `fieldLayout` | string | no | no | the layout style of the field display, supporting `vertical` or `horizontal`. |
  | `fields` | Array | no | no | an array of [field](#field-json-format) object |

#### Field JSON Format

  Field is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no | id of the field |
  | `name` | string | no | yes | name of the field |
  | `type` | string | no | yes | the [type](#field-type) of the field |
  | `isSystem` | boolean | yes | no | whether the field is system field or not. |
  | `isVisible` | boolean | no | no | whether the field is visible or not. |
  | `isRequired` | boolean | no | no | whether the field is required or not when submitting the form |
  | `options` | string | no | no | the options of the field. |

#### Field Type

  Field Type is one key of the following keys:

  | Name | isSystem | Description |
  | - | :-: | - |
  | `name` | yes | Name field, `Pre Chat Form` or `Offline Message Form` only. |
  | `email` | yes | Email field, `Pre Chat Form` or `Offline Message Form` only. |
  | `phone` | yes | Phone field, `Pre Chat Form` or `Offline Message Form` only. |
  | `company` | yes | Company field, `Pre Chat Form` or `Offline Message Form` only. |
  | `product service` | yes | Product and Service field, `Pre Chat Form` only. |
  | `department` | yes | Department field, `Pre Chat Form` or `Offline Message Form` only. |
  | `ticket id` | yes | Ticket field, `Pre Chat Form` or `Offline Message Form` only.  |
  | `rating` | yes | Rating field, `Post Chat Form` only. |
  | `comments` | yes | Comments field, `Post Chat Form` only. |
  | `subject` | yes | Subject field, `Offline Message Form` only. |
  | `message` | yes | Content field, `Offline Message Form` only. |
  | `attachment` | yes | Attachment field, `Offline Message Form` only. |
  | `cardNumber` | yes | card number field , `Secure Form` only. |
  | `expirationDate` | yes | expiration date field, `Secure Form` only |
  | `cscOrCvv` | yes | csc/cvv field , `Secure Form` only |
  | `nameOnCard` | yes | name on card field , `Secure Form` only |
  | `category` | yes | category field , `agent wrap-up` only |
  | `comment` | yes | comment field , `agent wrap-up` only |
  | `text` | no | Text field.  |
  | `textarea` | no | Textarea field.  |
  | `radio` | no | Radio Box field.  |
  | `checkbox` | no | Check Box field.  |
  | `select` | no | Drop Down List field.  |
  | `checkboxList` | no | Check Box List field.  |

</div>
<div>

### Endpoint

#### Get Pre-Chat configuration of a campaign

  `GET /api/v2/livechat/campaigns/{id}/prechat`

- Parameters:

    No parameters

- Response:

    [Pre-Chat](#pre-chat-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/prechat
```

Sample response:

```json
{
    "isEnable": false,
    "header": {
        "isShowTeamName": true,
        "teamName": "Our Team",
        "isShowAdatar": true
    },
    "greetingMessage": "Welcome to our website. We are excited to chat with you!",
    "socialLogin": {
        "isUseFacebook": false
    },
    "isRememberVisitorInfo": true,
    "fieldLayout": "vertical",
    "fields": []
}
```

#### Update Pre-Chat configuration for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/prechat`

- Parameters:

    [Pre-Chat](#pre-chat-json-format)

- Response:

    [Pre-Chat](#pre-chat-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isenable" : true, "fieldLayout" : "vertical"}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/prechat
```

Sample response:

```json
{
    "isEnable": true,
    "header": {
        "isShowTeamName": true,
        "teamName": "Our Team",
        "isShowAdatar": true
    },
    "greetingMessage": "Welcome to our website. We are excited to chat with you!",
    "socialLogin": {
        "isUseFacebook": false
    },
    "isRememberVisitorInfo": false,
    "fieldLayout": "vertical",
    "fields": [
        {
            "id": 1,
            "name": "Name",
            "type": "text",
            "isSystem": true,
            "isVisible": true,
            "isRequired": true,
            "options": ""
        },
        ...
    ]
}
```

</div>
</div>
<div>

## Post-Chat

<div>

### Model

#### Post-Chat JSON Format

  Post-Chat is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `isEnable` | boolean | no | yes | whether the post-chat is enabled or not. |
  | `greetingMessage` | string | no | no | content of the greeting message. |
  | `fieldLayout` | string | no | no | the layout style of the field, supporting `vertical` or `horizontal` style. |
  | `fields` | Array | no | no | an array of [field](#field-json-format) object

</div>
<div>

### Endpoint

#### Get Post-Chat configuration of a campaign

  `GET /api/v2/livechat/campaigns/{id}/postchat`

- Parameters:

    No parameters

- Response:

    [Post-Chat](#post-chat-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/postchat
```

Sample response:

```json
{
    "isEnable": false,
    "greetingMessage": "Please comment on our service performance so that we can serve you better. Thanks for your time!",
    "fieldLayout": "vertical",
    "fields": [ ]
}
```

#### Update Post-Chat configuration of a campaign

  `PUT /api/v2/livechat/campaigns/{id}/postchat`

- Parameters:

    [Post-Chat](#post-chat-json-format)

- Response:

    [Post-Chat](#post-chat-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isenable" : true}"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/postchat
```

Sample response:

```json
{
    "isEnable": true,
    "greetingMessage": "Please comment on our service performance so that we can serve you better. Thanks for your time!",
    "fieldLayout": "vertical",
    "fields": [
        {
            "id": 17,
            "name": "Rating",
            "type": "rating",
            "isSystem": true,
            "isVisible": true,
            "isRequired": false,
            "options": "Poor Fair Good Very Good Excellent"
        },
        ...
    ]
}
```

</div>
</div>
<div>

## Offline Messages

<div>

### Model

#### Offline Message JSON Format

  Offline Message is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `isUseOwnPage`| boolean | no | yes | whether the custom offline message page is used or not. |
  | `page.url`| string | no | no | url of custom offline message page. |
  | `page.isOpenInNewWindow` | boolean | no | no | whether to open the custom offline message page in a new window or not. |
  | `greetingMessage` | string | no | no | content of the greeting message.
  | `header.isShowTeamName` | boolean | no | no | whether the name of the agent is visible or not in the header. |
  | `header.isShowAvatar` | boolean | no | no | whether the avatar of the agent is visible or not in the header. |
  | `header.teamName` | string | no | no | the team name displayed in the header. |
  | `fieldLayout` | string | no | no | the layout style of the field, supporting `vertical` or `horizontal` style. |
  | `fields` | Array | no | no | an array of [field](#field-json-format) object |

</div>
<div>

### Endpoint

#### Get OfflineMessage configuration of a campaign

  `GET /api/v2/livechat/campaigns/{id}/offlineMessage`

- Parameters:

    No parameters

- Response:

    [Offline Message](#offline-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/offlinemessage
```

Sample response:

```json
{
    "isUseOwnPage": true,
    "greetingMessage": "Please leave us a message and we will get back to you shortly.",
    "page": {
        "url": "",
        "isOpenInNewWindow": true
    },
    "header": {
        "isShowTeamName": true,
        "isShowAvator": true,
        "teamName": "Our Team"
    },
    "fieldLayout": "vertical",
    "fields": [
        {
            "id": 8,
            "name": "Name",
            "type": "text",
            "isSystem": true,
            "isVisible": true,
            "isRequired": true,
            "options": ""
        },
        ...
    ]
}
```

#### Update OfflineMessage configuration of a campaign

  `PUT /api/v2/livechat/campaigns/{id}/offlineMessage`

- Parameters:

    [Offline Message](#offline-message-json-format)

- Response:

    [Offline Message](#offline-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
    74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
    -X PUT -H "Content-Type: application/json"  
     -d "{"isUseOwnPage" : false}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/offlinemessage
```

Sample response:

```json
{
    "isUseOwnPage": false,
    "greetingMessage": "Please leave us a message and we will get back to you shortly.",
    "page": {
        "url": "",
        "isOpenInNewWindow": true
    },
    "header": {
        "isShowTeamName": true,
        "isShowAvator": true,
        "teamName": "Our Team"
    },
    "fieldLayout": "vertical",
    "fields": []
}
```

</div>
</div>
<div>

## Invitations

<div>

### Model

#### Invitation Window JSON Format

  Invitation Window is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `message.content` |string  | no | no | content of the invitation message. |
  | `message.font` |string  | no | no | the font of the text, including `times new roman`, `tahoma`, `verdana`, `arial`, `comic sans ms` and `courier`. |
  | `message.bold` | boolean  | no | no | whether the text is bold or not. |
  | `message.fontsize` |string  | no | no | the size of text, including `xx-small`, `x-small`, `small`, `medium`, `large`, `x-large` and `xx-large`. |
  | `message.italic` | boolean  | no | no | whether the text is italic or not. |
  | `message.color` |string  | no | no | the color of text. |
  | `popup.position` |string  | no | no | the position of invitation window, including `centered`, `centeredWithOverlay`, `topLeft`, `topMiddle`, `topRight`, `bottomLeft`, `bottomMiddle`, `bottomRight`, `leftMiddle` and `rightMiddle`. |
  | `popup.imageType` | string | no | no | `custom` or `gallery` |
  | `popup.imageId` | int  | no | no | id of the invitation image. |
  | `popup.messageFrame.x` |int  | no | no | coordinate x of the text area |
  | `popup.messageFrame.y` |int  | no | no | coordinate y of the text area |
  | `popup.messageFrame.width` |int  | no | no | width of the text area |
  | `popup.messageFrame.height` |int  | no | no | height of the text area |
  | `popup.closeFrame.x` |int  | no | no | coordinate x of the close area |
  | `popup.closeFrame.y` |int  | no | no | coordinate y of the close area |
  | `popup.closeFrame.width` |int  | no | no | width of the close area |
  | `popup.closeFrame.height` |int  | no | no | height of the close area |

#### Auto Invitation JSON Format

  Auto Invitation is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no | id of the auto invitation. |
  | `name` | string | no | yes | name of auto invitation. |
  | `isEnable` | boolean | no | no | whether the auto invitation is enabled or not. |
  | `isPopupOnlyOneTime` | boolean | no | no | whether to pop up only once during one visit |
  | `invitationWindow` | [InvitationWindow](#invitation-window-json-format) | no | no | an invitation window json object. |
  | `conditions` | [Conditions](#conditions-json-format) | no | no | an trigger condition json object. |

#### Conditions JSON Format

  Conditions is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `when` | string | no | no | when the rule is triggered, including `all`, `any` and `logicalExpression` |
  | `logicalExpression` | string | no | no | the logical expression of the conditions |
  | `list` | array | no | no |an array of [condition](#condition-json-format) |

#### Condition JSON Format

  Condition is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `number` | int | no | yes | the number of the condition, used in logic expression |
  | `field` | string  | no | yes | the name of the visitor field |
  | `operator` | string  | no | yes | a comparison operator |
  | `value` | string  | no | yes | the value of a visitor field |

</div>
<div>

### Endpoint

#### Get invitation configuration of a campaign

  `GET /api/v2/livechat/campaigns/{id}/invitation`

- Parameters:

    No parameters

- Response

  - `style` - the layout style of invitation window, including `bubble`, `popup` and `embedded`
  - `autoInvitations` - an array of [Auto invitation](#auto-invitation-json-format) json object.
  - `manualInvitation` - [Invitation window](#invitation-window-json-format) json object

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation
```

Sample response:

```json
{
    "style": "popup",
    "autoInvitations": [
        {
            "id": 1,
            "name": "Spent on website more than 30 seconds",
            "isEnable": false,
            "isPopupOnlyOneTime": true,
            "invitationWindow": {
                "message": {
                    "content": "Hello, how may I help you?",
                    "font": "Verdana",
                    "bold": true,
                    "fontsize": "large",
                    "italic": false,
                    "color": "#484848"
                },
                "popup": {
                    "position": "centered",
                    "image": {
                        "id": 4639,
                        "type": "gallery"
                    },
                    "messageFrame": {
                        "x": 25,
                        "y": 25,
                        "width": 250,
                        "height": 80
                    },
                    "closeFrame": {
                        "x": 245,
                        "y": 155,
                        "width": 100,
                        "height": 30
                    }
                }
            },
            "conditions": {
                "when": "all",
                "logicalExpression": "",
                "list": [
                    {
                        "number": 1,
                        "field": "TimeOnWebSite",
                        "operator": "morethan",
                        "value": "30"
                    }
                ]
            }
        },
        ...
    ],
    "manualInvitation": {
        "message": {
            "content": "Hello, how may I help you?",
            "font": "Verdana",
            "bold": true,
            "fontsize": "large",
            "italic": false,
            "color": "#484848"
        },
        "popup": {
            "position": "centered",
            "image": {
                "id": 4639,
                "type": "gallery"
            },
            ...
        }
    }
}
```

#### Update invitation style of a campaign

  `PUT /api/v2/livechat/campaigns/{id}/invitation`

- Parameters

  - `style` - mandatory, the layout style of invitation window, including `bubble`, `popup` and `embedded`

- Response

  - `style` - the layout style of invitation window, including `bubble`, `popup` and `embedded`
  - `autoInvitations` - an array of [Auto invitation](#auto-invitation-json-format) json object.
  - `manualInvitation` - [Invitation window](#invitation-window-json-format) json object

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
    -X PUT -H "Content-Type: application/json"  
     -d "{"style": "bubble"}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation
```

Sample response:

```json
{
    "style": "bubble",
    "autoInvitations": [
        {
            "id": 1,
            "name": "Spent on website more than 30 seconds",
            "isEnable": false,
            "isPopupOnlyOneTime": true,
            "invitationWindow": {
                "message": {
                    "content": "Hello, how may I help you?",
                    "font": "Verdana",
                    "bold": true,
                    "fontsize": "large",
                    "italic": false,
                    "color": "#484848"
                },
                "popup": {
                    "position": "centered",
                    "image": {
                        "id": 4639,
                        "type": "gallery"
                    },
                    "messageFrame": {
                        "x": 25,
                        "y": 25,
                        "width": 250,
                        "height": 80
                    },
                    "closeFrame": {
                        "x": 245,
                        "y": 155,
                        "width": 100,
                        "height": 30
                    }
                }
            },
            "conditions": {
                "when": "all",
                "logicalExpression": "",
                "list": [
                    {
                        "number": 1,
                        "field": "TimeOnWebSite",
                        "operator": "morethan",
                        "value": "30"
                    }
                ]
            }
        },
        ...
    ],
    "manualInvitation": {
        "message": {
            "content": "Hello, how may I help you?",
            "font": "Verdana",
            "bold": true,
            "fontsize": "large",
            "italic": false,
            "color": "#484848"
        },
        "popup": {
            "position": "centered",
            "image": {
                "id": 4639,
                "type": "gallery"
            },
            "messageFrame": {
                "x": 128,
                "y": 55,
                "width": 250,
                "height": 80
            },
            "closeFrame": {
                "x": 245,
                "y": 155,
                "width": 100,
                "height": 30
            }
        }
    }
}
```

#### Update manual invitation for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/invitation/manualInvitation`

- Parameters:

    [Invitation Window](#invitation-window-json-format)

- Response:

    [Invitation Window](#invitation-window-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkoUYutNz4W
    t3iC80BlfjLcPnYOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
     -X PUT -H "application/json"  
     -d "{"message":{"content":"justfortestmessagecontent"}}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation/manualInvitation
```

Sample response:

```json
{
    "message": {
        "content": "justfortestmessagecontent",
        "font": "Verdana",
        "bold": true,
        "fontsize": "large",
        "italic": false,
        "color": "#484848"
    },
    "popup": {
        "position": "centered",
        "image": {
            "id": 4639,
            "type": "gallery"
        },
        "messageFrame": {
            "x": 128,
            "y": 55,
            "width": 250,
            "height": 80
        },
        "closeFrame": {
            "x": 245,
            "y": 155,
            "width": 100,
            "height": 30
        }
    }
}
```

#### Get an auto invitation for a campaign

  `GET /api/v2/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`

- Parameters:

    No parameters

- Response:

    [Auto invitation](#auto-invitation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation/autoinvitations/1
```

Sample response:

```json
{
    "id": 1,
    "name": "Spent on website more than 30 seconds",
    "isEnable": false,
    "isPopupOnlyOneTime": true,
    "invitationWindow": {
        "message": {
            "content": "Hello, how may I help you?",
            "font": "Verdana",
            "bold": true,
            "fontsize": "large",
            "italic": false,
            "color": "#484848"
        },
        "popup": {
            "position": "centered",
            "image": {
                "id": 4639,
                "type": "gallery"
            },
            "messageFrame": {
                "x": 25,
                "y": 25,
                "width": 250,
                "height": 80
            },
            "closeFrame": {
                "x": 245,
                "y": 155,
                "width": 100,
                "height": 30
            }
        }
    },
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": [
            {
                "number": 1,
                "field": "TimeOnWebSite",
                "operator": "morethan",
                "value": "30"
            }
        ]
    }
}
```
  
#### Create a new auto invitation for a campaign

  `POST /api/v2/livechat/campaigns/{id}/invitation/autoInvitations`

- Parameters:

    [Auto invitation](#auto-invitation-json-format)

- Response:

    [Auto invitation](#auto-invitation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "justfortestautoinvitation","isenable" : false}"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation/autoInvitations
```

Sample response:

```json
{
    "id": 1,
    "name": "justfortestautoinvitation",
    "isEnable": false,
    "isPopupOnlyOneTime": true,
    "invitationWindow": {
        "message": {
            "content": "Hello, how may I help you?",
            "font": "Verdana",
            "bold": true,
            "fontsize": "large",
            "italic": false,
            "color": "#484848"
        },
        "popup": {
            "position": "centered",
            "image": {
                "id": 4639,
                "type": "gallery"
            },
            "messageFrame": {
                "x": 25,
                "y": 25,
                "width": 250,
                "height": 80
            },
            "closeFrame": {
                "x": 245,
                "y": 155,
                "width": 100,
                "height": 30
            }
        }
    },
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": [
            {
                "number": 1,
                "field": "TimeOnWebSite",
                "operator": "morethan",
                "value": "30"
            }
        ]
    }
}
```

#### Update an auto invitation for a campaign
  
  `PUT /api/v2/livechat/campaigns/{id}/invitation/autoInvitations/{autoInvitation_id}`

- Parameters:

    [Auto invitation](#auto-invitation-json-format)

- Response:

    [Auto invitation](#auto-invitation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "justfortestautoinvitation11111"}"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation/autoInvitations/1
```

Sample response:

```json
{
    "id": 1,
    "name": "justfortestautoinvitation11111",
    "isEnable": false,
    "isPopupOnlyOneTime": true,
    "invitationWindow": {
        "message": {
            "content": "Hello, how may I help you?",
            "font": "Verdana",
            "bold": true,
            "fontsize": "large",
            "italic": false,
            "color": "#484848"
        },
        "popup": {
            "position": "centered",
            "image": {
                "id": 4639,
                "type": "gallery"
            },
            "messageFrame": {
                "x": 25,
                "y": 25,
                "width": 250,
                "height": 80
            },
            "closeFrame": {
                "x": 245,
                "y": 155,
                "width": 100,
                "height": 30
            }
        }
    },
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": [
            {
                "number": 1,
                "field": "TimeOnWebSite",
                "operator": "morethan",
                "value": "30"
            }
        ]
    }
}
```

#### Delete an auto invitation for a campaign

  ` DELETE /api/v2/livechat/campaigns/{id}/invitation/autoInvitations/{auto_invitation_id}`

- Parameters:

    No parameters

- Response:

    Status: Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/campaigns/1/invitation/autoInvitations/1
```

Sample response:

```json
"Auto Invitation with id '1' has been removed."
```

</div>
</div>
<div>

## Agent Wrapups

<div>

### Endpoint

#### Get agent wrapup of a campaign

  `GET /api/v2/livechat/campaigns/{id}/agentWrapup`
- Parameters:

    no parameters

- Response:

    an array of [Field](#field-json-format)
  
#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"   
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/agentwrapup
```

Sample response:

```json
[
    {
        "id": 19,
        "name": "Category",
        "type": "wrapupcategory",
        "isSystem": true,
        "isVisible": true,
        "isRequired": false,
        "options": "Inquiry Suggestion Complaint Junk"
    },
    ...
]
```

#### Update agent wrapup for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/agentWrapup`

- Parameters:

    an array of [Field](#field-json-format)

- Response:

    an array of [Field](#field-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh  
     74BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw  
    4mWLEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkutNz4W  
    t3iC80BlOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"  
     -X PUT -H "Content-Type: application/json"  
     -d "[{"id": 19, "name": "testtest", "type": "text", "isSystem": false,  
     "isVisible": true, "isRequired": false, "options": ""}]"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/agentWrapup
```

Sample response:

```json
[
    {
        "id": 19,
        "name": "testtest",
        "type": "text",
        "isSystem": false,
        "isVisible": true,
        "isRequired": false,
        "options": ""
    },
    ...
]
```

</div>
</div>
<div>

## Routing Rules

<div>

### Model

#### Routing Rule JSON Format

  Route Rule is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `isEnable` | boolean | no | yes |whether the routing rules is enabled or not.
  | `type` |string | no | no |the type of routing, including `simple` and `rules`. |
  | `simpleRouteToObject` | string | no | no | the role of route , including `department` and `agent` |
  | `simpleRouteToId` | integer | no | no | id of the route object |
  | `simpleRoutePriority` | string | no | no | the priority of the route object, including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `rules` | array | no | no | an array of [Custom Rule](#custom-rule-json-format) json object. |
  | `failType` | string | no | no |the type of failed routing, including `route` and `offlineMessage`. |
  | `fail.routeTobject` | string | no | no | the rule of failed route , including `department` and `agent` |
  | `fail.routeToId` | integer | no | no | id of the route object |
  | `fail.routePriority` | string | no | no | the priority of failed route object, including `lowest`, `low`, `normal`, `high` and `highest`. |
  | `fail.offlineMessageEmails` | string  | no | no | redirect them to Offline Message Window and forward their messages to the email |
  | `botTakePercentageForRoute` | string  | no | no | percentage routed to Bot |
  | `botTakePercentageForFailRoute` | string  | no | no | percentage of routes routed to Bots after a route failure |

#### Custom Rule JSON Format

  Custom Rule is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no | id of the custom rule |
  | `order` | integer | no | no | order of the custom rule |
  | `isEnable` | boolean | no | yes |whether the custom rule is enabled or not. |
  | `name` | string | no | yes |name of the custom rule |
  | `conditions` | [Conditions](#conditions-json-format)  | no | no | an trigger condition json object. |
  | `routeToObject` | string | no | yes | type of the route, including `agent` and `department`, value `department` is available when config of department is open. |
  | `routeToId` | integer | no | yes | id of the route object |
  | `routePriority` | string | no | no | the priority of the route object, including `lowest`, `low`, `normal`, `high` and `highest`. |
  
</div>
<div>

### Endpoint

#### Get Routing Rules of a campaign

  `GET /api/v2/livechat/campaigns/{id}/routingrules`

- Parameters:

    No parameters

- Response:

    [Routing Rule](#routing-rule-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/routingrules
```

Sample response:

```json
{
    "isEnable": false,
    "type": "simple",
    "simpleRouteToObject": "department",
    "simpleRouteToId": 0,
    "simpleRoutePriority": "normal",
    "failType": "route",
    "fail": {
        "routeToObject": "department",
        "routeToId": 0,
        "routePriority": "normal",
        "offlineMessageEmails": ""
    },
    "rules": [],
    "botTakePercentageForRoute": 20,
    "botTakePercentageForFailRoute": 0,
}
```

#### Update Routing Rules for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/routingrules`

- Parameters:

    [Routing Rule](#routing-rule-json-format)

- Response:

    [Routing Rule](#routing-rule-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isenable" : true}"    
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/routingrules
```

Sample response:

```json
{
    "isEnable": true,
    "type": "simple",
    "simpleRouteToObject": "department",
    "simpleRouteToId": 0,
    "simpleRoutePriority": "normal",
    "failType": "route",
    "fail": {
        "routeToObject": "department",
        "routeToId": 0,
        "routePriority": "normal",
        "offlineMessageEmails": ""
    },
    "rules": []
}
```

#### Get a custom rule of a campaign

  `GET /api/v2/livechat/campaigns/{id}/routingrule/customrules/{custom_rule_id}`

- Parameters:

    No parameters

- Response:

    [Custom Rule](#custom-rule-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/routingrule/customrules/6
```

Sample response:

```json
{
    "id": 6,
    "order": 1,
    "name": "justfortest",
    "isEnable": true,
    "routeToObject": "agent",
    "routeToId": 1,
    "routePriority": "normal",
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": []
    }
}
```

#### Create a new custom rule for a campaign

  `POST /api/v2/livechat/campaigns/{id}/routingrule/customrules`

- Parameters:

    [Custom Rule](#custom-rule-json-format)

- Response:

    [Custom Rule](#custom-rule-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "justfortest","routetoobject" : "agent","routetoid" : "1","isenable" : true}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/routingrule/customrules
```

Sample response:

```json
{
    "id": 6,
    "order": 1,
    "name": "justfortest",
    "isEnable": true,
    "routeToObject": "agent",
    "routeToId": 1,
    "routePriority": "normal",
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": []
    }
}
```

#### Update a custom rule for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/routingrule/customrules/{custom_rule_id}`
  
- Parameters:

    [Custom Rule](#custom-rule-json-format)

- Response:

    [Custom Rule](#custom-rule-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "testupdate","routetoobject" : "department","routetoid" : "2","isenable" : false}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/routingrule/customrules/6
```

Sample response:

```json
{
    "id": 6,
    "order": 1,
    "name": "testupdate",
    "isEnable": false,
    "routeToObject": "department",
    "routeToId": 2,
    "routePriority": "normal",
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": [ ]
    }
}
```

#### Delete a custom rule for a campaign

  `DELETE /api/v2/livechat/campaigns/{id}/routingrule/customrules/{custom_rule_id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x -DELETE https://hosted.comm100.com/api/v2/livechat/campaigns/1/routingrule/customrules/6
```

Sample response:

```json
"Custom Rule with id '6' has been removed."
```

</div>
</div>
<div>

## Languages

<div>

### Model

#### Campaign Language JSON Format

  Language is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `isUseDefaultLanguageText` | boolean | no | yes | whether use default language text or not. |
  | `isRTL` | boolean | no | no | whether the language is from right to left. |
  | `languageTexts` | array | no | no | an array of [Language Text](#language-text-json-format) |

#### Language Text JSON Format

  Language Text is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `category` | string | yes | yes | the module of custom language, including `buttons`, `fields`, `prompts`, `system messages`, `audio chat`, `video chat`, `cobrowsing`, `screen sharing`, `transcript email to visitors`, `text on mobile browsers`, `embedded window` and `bot`. |
  | `name` | string | yes | yes | the name of the language item |
  | `defaultText` | string | yes | no | the default text of field in the custom language. |
  | `currentText` | string | no | no | current text of field in the custom language. |
  | `macros` | string | yes | no | macros used for the field in the custom language. |

</div>
<div>

### Endpoint

#### Get Language for a campaign

  `GET /api/v2/livechat/campaigns/{id}/language`

- Parameters:

    No parameters

- Response:

    [Campaign Language](#campaign-language-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/language
```

Sample response:

```json
{
    "isUseDefaultLanguageText": false,
    "isRTL": false,
    "languageTexts": []
}
```

#### Update settings of Language for a campaign

  `PUT /api/v2/livechat/campaigns/{id}/language`

- Parameters:

    [Campaign Language](#campaign-language-json-format)

- Response:

    [Campaign Language](#campaign-language-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isUseDefaultLanguageText": true}"
     https://hosted.comm100.com/api/v2/livechat/campaigns/1/language
```

Sample response:

```json
{
    "isUseDefaultLanguageText": true,
    "isRTL": false,
    "languageTexts": [
        {
            "category": "Buttons",
            "name": "Yes",
            "defaultText": "Yes",
            "currentText": "Yes",
            "macros": ""
        },
        ...
    ]
}
```

</div>
</div>
<div>

## Canned Messages

  You need `Manage Pulbic Canned Messages` permission to manage the canned messages.

- `GET /api/v2/livechat/cannedMessages` -get a list of canned Messages
- `GET /api/v2/livechat/cannedMessages/{id}`  -get a single canned Message
- `POST /api/v2/livechat/cannedMessages` -create a new canned Message
- `PUT /api/v2/livechat/cannedMessages/{id}`  -update a canned Message
- `DELETE /api/v2/livechat/cannedMessages/{id}`  -remove a canned Message

<div>

### Model

#### Canned Message JSON Format

  Canned Message is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no | id of the canned message. |
  | `name` | string | no | yes | name of the canned message. |
  | `message` | string | no | yes | content of the canned message. |
  | `shortcuts` | string | no | no | shortcuts of the canned message. |
  | `categoryId` | integer | no | no | id of the category of the canned message, default is `0` |
  | `isPrivate` | boolean | yes | no | whether the canned message is private or not, default is `false` |

</div>
<div>

### Endpoint

#### Get a list of canned messages

  `GET /api/v2/livechat/cannedMessages`

- Parameters:

    No parameters

- Response:

    An array of [Canned Message](#canned-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/cannedMessages
```

Sample response:

```json
[
    {
        "id": 16,
        "isPrivate": false,
        "name": "{{randstr}}",
        "message": "{{randstr}}",
        "categoryId": 0,
        "shortCuts": "bye"
    },
    ...
]
```

#### Get a single canned message

  `GET /api/v2/livechat/cannedMessages/{id}`

- Parameters:

    No parameters

- Response:

    [Canned Message](#canned-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/cannedmessages/16
```

Sample response:

```json
{
    "id": 16,
    "isPrivate": false,
    "name": "{{randstr}}",
    "message": "{{randstr}}",
    "categoryId": 0,
    "shortCuts": "bye"
}
```

#### Create a new canned message

  `POST /api/v2/livechat/cannedMessages`

- Parameters:

    [Canned Message](#canned-message-json-format)

- Response:

    [Canned Message](#canned-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"isprivate" : true,"name" : "test","message" : "testmessage"}"   
     https://hosted.comm100.com/api/v2/livechat/cannedmessages
```

Sample response:

```json
{
    "id": 69,
    "isPrivate": true,
    "name": "test",
    "message": "testmessage",
    "categoryId": 0,
    "shortCuts": ""
}
```

#### Update a canned message

  `PUT /api/v2/livechat/cannedMessages/{id}`

- Parameters:

    [Canned Message](#canned-message-json-format)

- Response:

    [Canned Message](#canned-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isprivate" : true,"name" : "testupdate","message" : "testmessageupdate"}"   
     https://hosted.comm100.com/api/v2/livechat/cannedmessages/69
```

Sample response:

```json
{
    "id": 69,
    "isPrivate": true,
    "name": "testupdate",
    "message": "testmessageupdate",
    "categoryId": 0,
    "shortCuts": ""
}
```

#### Remove a canned message

  `DELETE /api/v2/livechat/cannedMessages/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/cannedmessages/69
```

Sample response:

```json
Response: Status: 200 OK
```

</div>
</div>
<div>

## Canned Message Categories

  You need `Manage Pulbic Canned Messages` permission to manage canned message category.
- `GET /api/v2/livechat/cannedMessageCategories` -get a list of canned Messages Categories
- `GET /api/v2/livechat/cannedMessageCategories/{id}`  -get a single canned Messages Category
- `POST /api/v2/livechat/cannedMessageCategories` -create a new canned Messages Category
- `PUT /api/v2/livechat/cannedMessageCategories/{id}`  -update a canned Messages Category
- `DELETE /api/v2/livechat/cannedMessageCategories/{id}`  -remove a canned Messages Category

<div>

### Model

#### Canned Message Category JSON Format

  Canned Message Category is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no |id of the canned message category. |
  | `name` | string  | no | yes |name of the canned message category. |
  | `parentId` | integer  | no | yes | id of the parent category of the canned message category. |
  | `isPrivate` | string  | no | yes | whether the canned message category is private or not. |

</div>
<div>

### Endpoint

#### Get a list of canned message categories

  `GET /api/v2/livechat/cannedMessageCategories`

- Parameters:

    No parameters

- Response:

    An array of [Canned Message Category](#canned-message-category-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/cannedmessagecategories
```

Sample response:

```json
[
    {
        "id": 1,
        "isPrivate": false,
        "name": "puddddtresult",
        "parentId": 0
    },
    ...
]
```

#### Get a single canned message category

  `GET /api/v2/livechat/cannedMessageCategories/{id}`

- Parameters:

    No parameters

- Response:

    [Canned Message Category](#canned-message-category-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/cannedmessagecategories/3
```

Sample response:

```json
{
    "id": 3,
    "isPrivate": false,
    "name": "puddddtresultgggg",
    "parentId": 1
}
```

#### Create a new canned message category

  `POST /api/v2/livechat/cannedMessageCategories`

- Parameters:

    [Canned Message Category](#canned-message-category-json-format)

- Response:

    [Canned Message Category](#canned-message-category-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"isprivate" : true,"name" : "justfortest","parentid" : "0"}"    
     https://hosted.comm100.com/api/v2/livechat/cannedmessagecategories
```

Sample response:

```json
{
    "id": 5,
    "isPrivate": true,
    "name": "justfortest",
    "parentId": 0
}
```

#### Update a canned message category

  `PUT /api/v2/livechat/cannedMessageCategories/{id}`

- Parameters:

    [Canned Message Category](#canned-message-category-json-format)

- Response:

    [Canned Message Category](#canned-message-category-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isprivate" : true,"name" : "justfortestupdate","parentid" : "0"}"    
     https://hosted.comm100.com/api/v2/livechat/cannedmessagecategories/5
```

Sample response:

```json
{
    "id": 5,
    "isPrivate": true,
    "name": "justfortestupdate",
    "parentId": 0
}
```

#### Remove a canned message category

  `DELETE /api/v2/livechat/cannedMessageCategories/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE https://hosted.comm100.com/api/v2/livechat/cannedmessagecategories/5
```

Sample response:

```json
Response: Status: 200 OK
```

</div>
</div>
<div>

## Departments

  You need `Manage Settings` permission to manage department.
- `GET /api/v2/livechat/departments` -get a list of departments
- `GET /api/v2/livechat/departments/{id}`  -get a single department
- `POST /api/v2/livechat/departments` -create a new department
- `PUT /api/v2/livechat/departments/{id}`  -update a department
- `DELETE /api/v2/livechat/departments/{id}`  -remove a department

<div>

### Model

#### Department JSON Format

  Department is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no |id of the department. |
  | `name` | string | no | yes |name of the department. |
  | `description` | string | no | no |description of the department. |
  | `agents` | array | no | no | an array of agent in the department. |
  | `groups` | array | no | no | an array of group in the department. |
  | `allocationRule` | string | no | no | rule of chat allocation, including `load balancing` , `round robin` and `capability weighted`. |
  | `isLastChattedPreferred` | boolean | no | no |whether last-chatted agent is preferred or not. |
  | `backupDepartmentId` | integer | no | no | id of back up department |
  | `offlineMessageTo` | string | no | no | object which mail offline messages of the department to, including `allAgents` and `emailAddresses` |
  | `emailAddresses` | string | no | no | the email addresses which mail offline messages of the department to |

</div>
<div>

### Endpoint

#### Get a list of departments

  `GET /api/v2/livechat/departments`

- Parameters:

    No parameters

- Response:

    An array of [Department](#department-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/departments
```

Sample response:

```json
[
    {
        "id": 2,
        "name": "<script>alert('dde')</script>",
        "description": "<script>alert('dde111')</script>",
        "agents": [
            1
        ],
        "groups": [ ],
        "offlineMessageTo": "allAgents",
        "emailAddresses": "",
        "allocationRule": "load balancing",
        "isLastChattedPreferred": true,
        "backupDepartmentId": 1
    },
    ...
]
```

#### Get a single department

  `GET /api/v2/livechat/departments/{id}`

- Parameters:

    No parameters

- Response:

    [Department](#department-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/departments/2
```

Sample response:

```json
{
    "id": 2,
    "name": "<script>alert('dde')</script>",
    "description": "<script>alert('dde111')</script>",
    "agents": [
        1
    ],
    "groups": [ ],
    "offlineMessageTo": "allAgents",
    "emailAddresses": "",
    "allocationRule": "load balancing",
    "isLastChattedPreferred": true,
    "backupDepartmentId": 1
}
```

#### Create a new department

  `POST /api/v2/livechat/departments`

- Parameters:

    [Department](#department-json-format)

- Response:

    [Department](#department-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "test"}"    
     https://hosted.comm100.com/api/v2/livechat/departments
```

Sample response:

```json
{
    "id": 7,
    "name": "test",
    "description": "",
    "agents": [ ],
    "groups": [ ],
    "offlineMessageTo": "allAgents",
    "emailAddresses": "",
    "allocationRule": "load balancing",
    "isLastChattedPreferred": false,
    "backupDepartmentId": 0
}
```

#### Update a department

  `PUT /api/v2/livechat/departments/{id}`

- Parameters:

    [Department](#department-json-format)

- Response:

    [Department](#department-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "testupdate"}"    
     https://hosted.comm100.com/api/v2/livechat/departments/7
```

Sample response:

```json
{
    "id": 7,
    "name": "testupdate",
    "description": "",
    "agents": [ ],
    "groups": [ ],
    "offlineMessageTo": "allAgents",
    "emailAddresses": "",
    "allocationRule": "load balancing",
    "isLastChattedPreferred": false,
    "backupDepartmentId": 0
}
```

#### Remove a department

  `DELETE /api/v2/livechat/departments/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/departments/7
```

Sample response:

```json
"Department '7' has been removed."
```

</div>
</div>
<div>

## Custom Away Status

  You need `Manage Settings` permission to manage custom away status.
- `GET /api/v2/livechat/customAwayStatus` - get a list of custom away status
- `GET /api/v2/livechat/customAwayStatus/{id}` - get a single custom away status
- `POST /api/v2/livechat/customAwayStatus` - create a new custom away status
- `PUT /api/v2/livechat/customAwayStatus/{id}` - update a custom away status
- `DELETE /api/v2/livechat/customAwayStatus/{id}` - remove a custom away status

<div>

### Model

#### Custom Away Status JSON Format

  Custom Away Status is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no | id of the custom away status. |
  | `name` | string | no | yes | name of the custom away status. |
  | `isVisible` | boolean | no | no | whether the custom away status is visible or not. |

</div>
<div>

### Endpoint

#### Get a list of custom away status

  `GET /api/v2/livechat/customAwayStatus`

- Parameters:

    No parameters

- Response:

    An array of [Custom Away Status](#custom-away-status-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/customawaystatus
```

Sample response:

```json
[
    {
        "id": 100,
        "name": "Away",
        "isVisible": true
    },
    ...
]
```

#### Get a single custom away status

  `GET /api/v2/livechat/customAwayStatus/{id}`

- Parameters:

    No parameters

- Response:

    [Custom Away Status](#custom-away-status-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/customawaystatus/100
```

Sample response:

```json
{
    "id": 100,
    "name": "Away",
    "isVisible": true
}
```

#### Create a new custom away status

  `POST /api/v2/livechat/customAwayStatus`

- Parameters:

    [Custom Away Status](#custom-away-status-json-format)

- Response:

    [Custom Away Status](#custom-away-status-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "test"}"    
     https://hosted.comm100.com/api/v2/livechat/customawaystatus
```

Sample response:

```json
{
    "id": 156,
    "name": "test",
    "isVisible": false
}
```

#### Update a custom away status

  `PUT /api/v2/livechat/customAwayStatus/{id}`

- Parameters:

    [Custom Away Status](#custom-away-status-json-format)

- Response:

    [Custom Away Status](#custom-away-status-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "testupdate"}"    
     https://hosted.comm100.com/api/v2/livechat/customawaystatus/156
```

Sample response:

```json
{
    "id": 156,
    "name": "testupdate",
    "isVisible": false
}
```

#### Remove a custom away status

  `DELETE /api/v2/livechat/customAwayStatus/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/customawaystatus/156
```

Sample response:

```json
"Custom Away Status '156' has been removed."
```

</div>
</div>
<div>

## Bans

  You need `Manage Ban List` permission to manage the ban list.

- `GET /api/v2/livechat/bans` -get a list of bans
- `GET /api/v2/livechat/bans/{id}`  -get a single ban
- `POST /api/v2/livechat/bans` -create a new ban
- `PUT /api/v2/livechat/bans/{id}`  -update a ban
- `DELETE /api/v2/livechat/bans/{id}`  -remove a ban

<div>

### Model

#### Ban JSON Format

  Ban is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no |id of the ban. |
  | `type` | string  | no | yes | type of ban, including `visitor` and `ip` |
  | `visitorId` | string | no | no | visitor's id of the ban if `type` is `visitor`  |
  | `ipAddress` | string  | no | yes | ip address of the ban if `type` is `ip`, it can be a specific ip `192.168.8.113` or ip range `192.168.8.0/24` or `192.168.8.0-192.168.8.255` |
  | `comment` | string  | no | no | comment of the ban. |

</div>
<div>

### Endpoint

#### Get a list of bans

  `GET /api/v2/livechat/bans`

- Parameters:

    No parameters

- Response:

    An array of [Ban](#ban-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/bans
```

Sample response:

```json
[
    {
        "id": 7,
        "type": "visitor",
        "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7",
        "ipAddress": "",
        "comment": ""
    },
    ...
]
```

#### Get a single ban

  `GET /api/v2/livechat/bans/{id}`

- Parameters:

    No parameters

- Response:

    [Ban](#ban-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/bans/7
```

Sample response:

```json
{
    "id": 7,
    "type": "visitor",
    "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7",
    "ipAddress": "",
    "comment": ""
}
```

#### Create a new ban

  `POST /api/v2/livechat/bans`

- Parameters:

    [Ban](#ban-json-format)

- Response:

    [Ban](#ban-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"type" : "ip","ipaddress" : "192.168.1.1"}"
     https://hosted.comm100.com/api/v2/livechat/bans
```

Sample response:

```json
{
    "id": 8,
    "type": "ip",
    "visitorId": "",
    "ipAddress": "192.168.1.1",
    "comment": ""
}
```

#### Update a ban

  `PUT /api/v2/livechat/bans/{id}`

- Parameters:

    [Ban](#ban-json-format)

- Response:

    [Ban](#ban-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"type" : "ip","ipaddress" : "192.168.1.2"}"    
     https://hosted.comm100.com/api/v2/livechat/bans/8
```

Sample response:

```json
{
    "id": 8,
    "type": "ip",
    "visitorId": "",
    "ipAddress": "192.168.1.2",
    "comment": ""
}
```

#### Remove a ban

  `DELETE /api/v2/livechat/bans/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/bans/7
```

Sample response:

```json
"Ban '7' has been removed."
```

</div>
</div>
<div>

## Conversion Actions

  You need `Manage Settings` permission to manage conversion action.

- `GET /api/v2/livechat/conversionActions` -get a list of conversion actions
- `GET /api/v2/livechat/conversionActions/{id}`  -get a conversion action
- `POST /api/v2/livechat/conversionActions` -create a new conversion action
- `PUT /api/v2/livechat/conversionActions` -update conversion action
- `POST /api/v2/livechat/conversionActions/achieved` -make api conversion succesful

<div>

### Model

#### Conversion Action JSON Format

  Conversion Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no |id of the conversion action. |
  | `name` | string | no | yes |  name of the conversion action. |
  | `isEnable` | boolean | no | no | whether the conversion action is enabled or not. |
  | `type` | string | no | no | type of the conversion action, including `url`, `customVariable` and `livechatapi`. |
  | `customVariable` | string  | no | no |  the name of the custom variable, available when `type` is `customVariable`. |
  | `matchType` | string | no | no |  match type of the conversion action, available when `type` is `customVariable` or `url`. |
  | `matchValue` | string | no | no |  match value of the conversion action, available when `type` is `customVariable` or `url`. |
  | `isCaseSensitive` | boolean | no | no |  whether the conversion action is case sensitive or not, available when `type` is `url`. |
  | `isAssignValue` | boolean | no | no |  whether a value is assigned for the conversion action or not. |
  | `isAssignValueFromCustomVariable` | boolean | no | no |  whether the value for assigning to the conversion action comes from an assigned value or a custom variable, `true` means from custom variable |
  | `assignValue` | string | no | no |  the value assigned for the conversion action |
  | `customVariableForAssignValue` | string | no | no |  the value comes from the custom variable |

#### Api Conversion JSON Format

  Api Conversion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `conversion_name` | string | no | yes |  name of the conversion action. |
  | `visitorId` | string | no | no | type of the conversion action, including `url`, `customVariable` and `livechatapi`. |
  | `value` | string  | no | no |  the name of the custom variable, available when `type` is `customVariable`. |

#### Api Conversion Action Result JSON Format

  Api Conversion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `error_code` | string | no | yes |  0: ok; 1: the conversion name does not exist; 2: the visitorId does not exist; 3: error adding conversion-related Data to system. |
  | `error_message` | string | no | no | error message. |


</div>
<div>

### Endpoint

#### Get a list of conversion actions

  `GET /api/v2/livechat/conversionActions`

- Parameters:

    No parameters

- Response:

    An array of [Conversion Action](#conversion-action-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"
     https://hosted.comm100.com/api/v2/livechat/conversionactions
```

Sample response:

```json
[
    {
        "id": 4,
        "name": "justfortest2",
        "isEnable": false,
        "type": "Url",
        "customVariable": "",
        "matchType": "Is",
        "matchValue": "",
        "isCaseSensitive": false,
        "isAssignValue": false,
        "isAssignValueFromCustomVariable": false,
        "assignValue": "0",
        "customVariableForAssignValue": ""
    },
    ...
]
```

#### Get a single conversion action

  `GET /api/v2/livechat/conversionActions/{id}`

- Parameters:

    No parameters

- Response:

    [Conversion Action](#conversion-action-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"
     https://hosted.comm100.com/api/v2/livechat/conversionactions/3
```

Sample response:

```json
{
    "id": 3,
    "name": "justfortest",
    "isEnable": false,
    "type": "Url",
    "customVariable": "",
    "matchType": "Is",
    "matchValue": "",
    "isCaseSensitive": false,
    "isAssignValue": false,
    "isAssignValueFromCustomVariable": false,
    "assignValue": "0",
    "customVariableForAssignValue": ""
}
```

#### Create a new conversion action

  `POST /api/v2/livechat/conversionActions`

- Parameters:

    [Conversion Action](#conversion-action-json-format)

- Response:

    [Conversion Action](#conversion-action-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "justfortest"}"   
     https://hosted.comm100.com/api/v2/livechat/conversionactions
```

Sample response:

```json
{
    "id": 3,
    "name": "justfortest",
    "isEnable": false,
    "type": null,
    "customVariable": null,
    "matchType": null,
    "matchValue": null,
    "isCaseSensitive": false,
    "isAssignValue": false,
    "isAssignValueFromCustomVariable": false,
    "assignValue": null,
    "customVariableForAssignValue": null
}
```

#### Update a conversion action

  `PUT /api/v2/livechat/conversionActions/{id}`

- Parameters:

    [Conversion Action](#conversion-action-json-format)

- Response:

    [Conversion Action](#conversion-action-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "justfortestupdate"}"   
     https://hosted.comm100.com/api/v2/livechat/conversionactions/3
```

Sample response:

```json
{
    "id": 3,
    "name": "justfortestupdate",
    "isEnable": false,
    "type": "Url",
    "customVariable": "",
    "matchType": "Is",
    "matchValue": "",
    "isCaseSensitive": false,
    "isAssignValue": false,
    "isAssignValueFromCustomVariable": false,
    "assignValue": "0",
    "customVariableForAssignValue": ""
}
```

#### make api conversion succesful

  `POST /api/v2/livechat/conversionActions/achieved`

- Parameters:

    [Api Conversion](#api-conversion-action-json-format)

- Response:

    [Action Result](#api-conversion-action-result-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"conversion_name" : "justfortestupdate", 
     "visitorId": "ae165aad-b561-145b-427c-ba89849ff3c7", "value": "test"}"
     https://hosted.comm100.com/api/v2/livechat/conversionactions/achieved
```

Sample response:

```json
{
    "code": 0,
    "message": "ok",
}
```

</div>
</div>
<div>

## Visitor Segmentations

  You need `Manage Settings` permission to manage visitor segmentation.

- `GET /api/v2/livechat/visitorSegmentations` -get a list of visitor segments
- `GET /api/v2/livechat/visitorSegmentations/{id}`  -get a visitor segment
- `POST /api/v2/livechat/visitorSegmentations` -create a new visitor segment
- `PUT /api/v2/livechat/visitorSegmentations/{id}`  -update a visitor segment
- `DELETE /api/v2/livechat/visitorSegmentations/{id}`  -remove a visitor segment

<div>

### Model

#### Visitor Segmentation JSON Format

Visitor Segmentation is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` |integer  | yes | no |id of the visitor segment.
  | `name` |string  | no | yes | name of the visitor segment.
  | `color` |string  | no | no | color of the visitor segment
  | `isEnable` |boolean  | no | no | whether the visitor segment is enabled or not.
  | `priority` |int  | no | no | priority of the visitor segment.
  | `description` |string  | no | no | description of the visitor segment.
  | `conditions` |[Conditions](#conditions-json-format)  | no | no | an trigger condition json object. |
  | `notification` | string or object  | no | no | `none` or `{"agents":[1,2,3]}` or `{"agents": [1,2]"}` |

</div>
<div>

### Endpoint

#### Get a list of visitor segmentations

  `GET /api/v2/livechat/visitorSegmentations`

- Parameters:

    No parameters

- Response:

    An array of [Visitor Segmentation](#visitor-segmentation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/visitorsegmentations
```

Sample response:

```json
[
    {
        "id": 1,
        "name": "livechat15293908029",
        "color": "339FD9",
        "isEnable": false,
        "priority": 0,
        "description": "",
        "conditions": {
            "when": "All",
            "logicalExpression": "",
            "list": [
                {
                    "number": 1,
                    "field": "CurrentPageUrl",
                    "operator": "Include",
                    "value": "xx"
                }
            ]
        },
        "notification": "None"
    },
    ...
]
```

#### Get a single visitor segmentation

  `GET /api/v2/livechat/visitorSegmentations/{id}`

- Parameters:

    No parameters

- Response:

    [Visitor Segmentation](#visitor-segmentation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/visitorsegmentations/2
```

Sample response:

```json
{
    "id": 2, 
    "name": "justfortggggeggggst2",
    "color": "4CD9A1",
    "isEnable": true,
    "priority": 1,
    "description": "fhbsh",
    "conditions": {
        "when": "LogicalExpression",
        "logicalExpression": "",
        "list": []
    },
    "notification": "{\"departments\": []}"
}
```

#### Create a new visitor segmentation

  `POST /api/v2/livechat/visitorSegmentations`

- Parameters:

    [Visitor Segmentation](#visitor-segmentation-json-format)

- Response:

    [Visitor Segmentation](#visitor-segmentation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "justfortest"}"    
     https://hosted.comm100.com/api/v2/livechat/visitorsegmentations
```

Sample response:

```json
{
    "id": 6,
    "name": "justfortest",
    "color": "339FD9",
    "isEnable": false,
    "priority": 0,
    "description": "",
    "conditions": {
        "when": "all",
        "logicalExpression": "",
        "list": []
    },
    "notification": null
}
```

#### Update a visitor segmentation

  `PUT /api/v2/livechat/visitorSegmentations/{id}`

- Parameters:

    [Visitor Segmentation](#visitor-segmentation-json-format)

- Response:

    [Visitor Segmentation](#visitor-segmentation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "justfortestupdate"}"    
     https://hosted.comm100.com/api/v2/livechat/visitorsegmentations/6
```

Sample response:

```json
{
    "id": 6,
    "name": "justfortestupdate",
    "color": "339FD9",
    "isEnable": false,
    "priority": 2,
    "description": "",
    "conditions": {
        "when": "LogicalExpression",
        "logicalExpression": "",
        "list": [ ]
    },
    "notification": "None"
}
```

#### Remove a visitor segmentation

  `DELETE /api/v2/livechat/visitorSegmentations/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/visitorsegmentations/6
```

Sample response:

```json
Response: Status: 200 OK
```

</div>
</div>
<div>

## Visitor SSO Settings

  You need `Manage Settings` permission to setting sso for a site.

- `GET /api/v2/livechat/visitorSSO` -Get SSO settings of visitor
- `PUT /api/v2/livechat/visitorSSO`  -Update configuration of visitor

<div>

### Model

#### SSO Data Mapping JSON Format

Data Mapping is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `ssoAttribute` |string  | no | yes | SSO attribute name |
  | `comm100Field` |string  | no | yes | Comm100 field name |

#### Campaign SSO Options JSON Format

SignIn Options is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `campaignId` |integer  | yes | no |id of the campaign. |
  | `signInType` |string  | no | no | type of the sign in, including `no`, `optional` and `required`. |
  | `isSkipPrechat` |boolean  | no | no | whether the pre-chat form is skipped when visitors sign in. |

#### Visitor SSO Settings JSON Format

Visitor SSO Settings is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `siteId` |integer  | yes | no |id of the site which the visitor SSO belongs to. |
  | `isEnable` |boolean  | no | yes |  whether visitor SSO is enabled or not. |
  | `signInUrl` |string  | no | no | url for visitor to sign in |
  | `idpCertificate` | string  | no | no | base64 of the Identity Provider Verification Certificate content. |
  | `idpCertificateFileName` |string  | no | no |  file name of the certificate. |
  | `dataMappings` |array  | no | no |  an array of [SSO Data mapping](#sso-data-mapping-json-format) |
  | `campaignSSOOptions` |array  | no | no |  an array of [SignIn Options](#singin-options-json-format) |

</div>
<div>

### Endpoint

#### Get sso settings of the visitor

  `GET /api/v2/livechat/visitorSSO`

- Parameters:

    No parameters

- Response:

    [Visitor SSO Settings](#visitor-sso-settings-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/visitorsso
```

Sample response:

```json
{
    "siteId": 6000000,
    "isEnable": true,
    "signInUrl": "http://www.xzcs11ffffffff1a",
    "idpCertificate": "amdoamdoaGdmcnRk",
    "idpCertificateFileName": "r.txt",
    "dataMappings": [
        {
            "ssoAttribute": "test999",
            "comm100Field": "{!Visitor.Name}"
        },
        {
            "ssoAttribute": "test666",
            "comm100Field": "{!Prechat.Company}"
        }
    ],
    "campaignSSOOptions": [
        {
            "campaignId": 1,
            "signInType": "no",
            "isSkipPrechat": false
        }
    ]
}
```

#### Update sso settings of visitor

  `PUT /api/v2/livechat/visitorSSO`

- Parameters:

    [Visitor SSO Settings](#visitor-sso-settings-json-format)

- Response:

    [Visitor SSO Settings](#visitor-sso-settings-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isenable" : false}"    
     https://hosted.comm100.com/api/v2/livechat/visitorsso
```

Sample response:

```json
{
    "siteId": 6000000,
    "isEnable": false,
    "signInUrl": "http://www.xzcs11ffffffff1a",
    "idpCertificate": "amdoamdoaGdmcnRk",
    "idpCertificateFileName": "r.txt",
    "dataMappings": [
        {
            "ssoAttribute": "test999",
            "comm100Field": "{!Visitor.Name}"
        },
        {
            "ssoAttribute": "test666",
            "comm100Field": "{!Prechat.Company}"
        }
    ],
    "campaignSSOOptions": [
        {
            "campaignId": 1,
            "signInType": "no",
            "isSkipPrechat": false
        }
    ]
}
```

</div>
</div>
<div>

## Visitor

  You need `Manage Settings` permission to manage visitors.

- `GET /api/v2/livechat/visitors` -get a list of visitor
- `GET /api/v2/livechat/visitors/chatting`  -get a list of chatting visitor
- `GET /api/v2/livechat/visitors/{id}`  -get a visitor
- `PUT /api/v2/livechat/visitors/{id}`  -update a visitor's custom variable

<div>

### Model

#### Visitor JSON Format

The visitor is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` |string  | yes | no |id of the visitor.
  | `name` |string  | no | yes | name of the visitor.
  | `email` |string  | no | no | the email of the visitor
  | `status` |int  | no | no | the status of the visitor.
  | `page_views` |int  | no | no | the total number of web pages the visitor viewed on your website.
  | `browser` |string  | no | no | the browser the visitor is using.
  | `chats` |int  | no | no | the total times of chats a visitor has made on your website from the first time to present.
  | `city` |string  | no | no | the city of the visitor.
  | `country` |string  | no | no | the country of the visitor.
  | `current_browsing` |string  | no | no | the page the visitor is currently looking at.
  | `custom_fields` |[Custom field](#Custom-Field-Value-json-format)  | no | no | the values of custom fields entered by visitors in the pre-chat window. Operators can also update the value(s) during chat in Visitor Monitor.
  | `custom_variable` |[Custom variable](#Custom-Variable-Result-json-format)  | no | no | the information of custom variables captured from the web page visitors viewed.
  | `department` |int  | no | no | the department the visitor selected in the pre-chat window. Operators can also update their value while chatting with visitors.
  | `first_visit_time` |datetime  | no | no | the time the visitor first visited a web page pasted with Comm100 Live Chat code.
  | `flash_version` |string  | no | no | the flash version of the browser the visitor is using.
  | `ip` |string  | no | no | the IP of the visitor.
  | `keywords` |string  | no | no | the keywords the visitor used to search for your website.
  | `landing_page` |string  | no | no | the title and URL of the first page of your website the visitor visited.
  | `language` |string  | no | no | the language the visitor is using.
  | `operating_system` |string  | no | no | the operating system of the visitor's device.
  | `phone` |string  | no | no | the phone of the visitor.
  | `product_service` |string  | no | no | the product/service the visitor selected in the pre-chat window. Operators can also update their value while chatting with visitors.
  | `referrer_url` |string  | no | no | the URL of the page from which a visitor comes to your website.
  | `screen_resolution` |string  | no | no | the screen resolution of the visitor's device.
  | `search_engine` |string  | no | no | the search engine the visitor used to search for your website.
  | `state` |int  | no | no | the state of the visitor.
  | `time_zone` |string  | no | no | the time zone of the visitor.
  | `visit_time` |datetime  | no | no | the starting time when this visitor visits your website this time.
  | `visits` |int  | no | no | the total times of visits a visitor has made on your website from the first time to present.

#### Custom Field Value JSON Format

 Custom field is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no | id of the custom field. |
  | `name` | string | no | yes | name of the custom field. |
  | `value` | string | no | no | value of the custom field. |

#### Custom Variable Result JSON Format

 Custom variable is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `name` | string | no | yes | name of the custom variable. |
  | `value` | string | no | no | value of the custom variable. |
  | `url` | string | no | no | url of the custom variable. |

</div>
<div>

### Endpoint

#### Get a list of visitors

  `GET /api/v2/livechat/visitors`

- Parameters:

    No parameters

- Response:

    An array of [Visitor](#visitor-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"
     https://hosted.comm100.com/api/v2/livechat/visitors
```

Sample response:

```json
[
    {
        "page_views": 1,
        "browser": "Firefox 67.0",
        "chats": 0,
        "city": "Changsha",
        "company": "",
        "country": "China",
        "current_browsing": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
        "custom_fields": null,
        "custom_variables": [
            {
                "name": "justfortestupdate",
                "value": "text",
                "url": "bbbbb"
            }
        ],
        "department": -1,
        "email": "",
        "first_visit_time": "2019-06-11T03:05:42.537Z",
        "flash_version": "",
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "ip": "218.76.52.108",
        "keywords": "",
        "landing_page": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
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

#### Get a list of chatting visitors

  `GET /api/v2/livechat/visitors/chatting`

- Parameters:

    No parameters

- Response:

    An array of [Visitor](#visitor-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"
     https://hosted.comm100.com/api/v2/livechat/visitors/chatting
```

Sample response:

```json
[
    {
        "page_views": 1,
        "browser": "Firefox 67.0",
        "chats": 0,
        "city": "Changsha",
        "company": "",
        "country": "China",
        "current_browsing": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
        "custom_fields": null,
        "custom_variables": [
            {
                "name": "justfortestupdate",
                "value": "text",
                "url": "bbbbb"
            }
        ],
        "department": -1,
        "email": "",
        "first_visit_time": "2019-06-11T03:05:42.537Z",
        "flash_version": "",
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "ip": "218.76.52.108",
        "keywords": "",
        "landing_page": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
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

#### Get a single visitor

  `GET /api/v2/livechat/visitors/{id}`

- Parameters:

    No parameters

- Response:

    [Visitor](#visitor-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d
```

Sample response:

```json
    {
        "page_views": 1,
        "browser": "Firefox 67.0",
        "chats": 0,
        "city": "Changsha",
        "company": "",
        "country": "China",
        "current_browsing": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
        "custom_fields": null,
        "custom_variables": [
            {
                "name": "justfortestupdate",
                "value": "text",
                "url": "bbbbb"
            }
        ],
        "department": -1,
        "email": "",
        "first_visit_time": "2019-06-11T03:05:42.537Z",
        "flash_version": "",
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "ip": "218.76.52.108",
        "keywords": "",
        "landing_page": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
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

#### Update a visitor's custom variable

  `PUT /api/v2/livechat/visitors/{id}`

- Parameters:

    Array of [Custom Variable Result](#custom-variable-result-json-format)

- Response:

    [Visitor](#visitor-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "[{"name" : "justfortestupdate","value" : "text","url" : "bbbbb"}]"    
     https://hosted.comm100.com/api/v2/livechat/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d
```

Sample response:

```json
    {
        "page_views": 1,
        "browser": "Firefox 67.0",
        "chats": 0,
        "city": "Changsha",
        "company": "",
        "country": "China",
        "current_browsing": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
        "custom_fields": null,
        "custom_variables": [
            {
                "name": "justfortestupdate",
                "value": "text",
                "url": "bbbbb"
            },
            ...
        ],
        "department": -1,
        "email": "",
        "first_visit_time": "2019-06-11T03:05:42.537Z",
        "flash_version": "",
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "ip": "218.76.52.108",
        "keywords": "",
        "landing_page": "https://hosted.comm100.com/LiveChatFunc/PlanPreview.aspx?codePlanId=5000329&SSL=1&siteid=10000",
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

</div>
</div>
<div>

## Auto Allocation

 You need `Manage Settings` permission to config for a site.

- `GET /api/v2/livechat/autoAllocation` - Get auto allocation configuration
- `PUT /api/v2/livechat/autoAllocation`  - Update auto allocation configuration

<div>

### Model

#### Auto Allocation JSON format

  Auto Allocation is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `isEnable` | boolean | no | yes | whether the auto allocation is enabled or not. |
  | `allocationRule` | string | no | no | rule of chat allocation, including `load balancing` , `round robin` and `capability weighted` |
  | `isLastChattedPreferred` | boolean | no | no | whether last-chatted agent is preferred or not |
  | `isMaxChatForAllAgents` | boolean | no | no | whether to set the same maximum number of chats for all agents |
  | `maxChatForAllAgents` | integer | no | no | maximum number of chats for all agents |
  | `isAllocateChatWhenAgentInAudioVideo` | boolean | no | no | whether to allocate chats to agents who are having audio or video chats |
  | `isAllowAgentManualAcceptChat` | boolean | no | no | whether to allow agent to manually accept chat in agent console |

</div>
<div>

### Endpoint

#### Get auto allocation configuration

  `GET /api/v2/livechat/autoAllocation`

- Parameters:

    No Parameters

- Response:

    [Auto Allocation](#auto-allocation-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/autoallocation
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

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"isenable" : false}"    
     https://hosted.comm100.com/api/v2/livechat/autoallocation
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

</div>
</div>
<div>

## Live Chat Config

  You need `Manage Settings` permission to config for a site.
- `GET /api/v2/livechat/configs` -Get configuration for a site
- `PUT /api/v2/livechat/configs`  -Update configuration of a site

<div>

### Model

#### Live Chat Config JSON Format

  Live Chat Config is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `siteId` | integer  | yes | no |id of the site which the configuration belongs to. |
  | `isEnableMultipleCampaigns` | boolean  | no | no |  whether multiple campaigns are enabled or not in the site. |
  | `isEnableAutoAllocation` | boolean  | no | no | whether auto allocation is enabled or not in the site. |
  | `isEnableCustomAwayStatus` | boolean  | no | no | whether custom away status is enabled or not in the site. |
  | `isEnableDepartment` | boolean  | no | no | whether department is enabled or not in the site. |
  | `isEnableAutoTranslation` | boolean  | no | no |  whether auto translation is enabled or not in the site. |
  | `isEnableAudioAndVideoChat` | boolean  | no | no |  whether audio&video chat is enabled or not in the site. |
  | `isEnableVisitorSegmentation` | boolean  | no | no |  whether visitor segmentation is enabled or not in the site. |
  | `isEnableVisitorSSO` | boolean  | no | no |  whether visitor SSO is enabled or not in the site. |
  | `isEnableCreditCardMasking` | boolean  | no | no |  whether Credit card masking is enabled or not in the site. |
  | `isEnableCustomVariables` | boolean  | no | no |  whether custom variables are enabled or not in the site.
  | `isEnableSalesforce` | boolean  | no | no |  whether Salesforce integration is enabled or not in the site.
  | `isEnableZendesk` | boolean  | no | no |  whether Zendesk integration is enabled or not in the site.
  | `isEnableGoogleAnalytics` | boolean  | no | no |  whether Google Analytics integration is enabled or not in the site.
  | `isEnableGotoMeeting` | boolean  | no | no |  whether GotoMeeting integration is enabled or not in the site.
  | `isEnableJoinme` | boolean  | no | no |  whether Joinme integration is enabled or not in the site.

</div>
<div>

### Endpoint

#### Get configurationuration for a site

  `GET /api/v2/livechat/configs`

- Parameters:

    No parameters

- Response:

    Site Config Json Object.

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/configs
```

Sample response:

```json
{
    "siteId": 6000000,
    "isEnableMultipleCampaigns": true,
    "isEnableAutoAllocation": false,
    "isEnableCustomAwayStatus": true,
    "isEnableDepartment": false,
    "isEnableAutoTranslation": true,
    "isEnableAudioAndVideoChat": false,
    "isEnableVisitorSegmentation": true,
    "isEnableVisitorSSO": false,
    "isEnableCreditCardMasking": true,
    "isEnableCustomVariables": true,
    "isEnableSalesforce": false,
    "isEnableZendesk": true,
    "isEnableGoogleAnalytics": true,
    "isEnableGotoMetting": true,
    "isEnableJoinme": true
}
```

#### Update configuration of a site

  `PUT /api/v2/livechat/configs`

- Parameters:

    Site Config Json Object.

- Response:

    Site Config Json Object.

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"siteid" : "6000000","isenablesalesforce" : true}"    
     https://hosted.comm100.com/api/v2/livechat/configs
```

Sample response:

```json
{
    "siteId": 6000000,
    "isEnableMultipleCampaigns": true,
    "isEnableAutoAllocation": false,
    "isEnableCustomAwayStatus": true,
    "isEnableDepartment": false,
    "isEnableAutoTranslation": true,
    "isEnableAudioAndVideoChat": false,
    "isEnableVisitorSegmentation": true,
    "isEnableVisitorSSO": false,
    "isEnableCreditCardMasking": true,
    "isEnableCustomVariables": true,
    "isEnableSalesforce": true,
    "isEnableZendesk": true,
    "isEnableGoogleAnalytics": true,
    "isEnableGotoMetting": true,
    "isEnableJoinme": true
}
```

</div>
</div>
<div>

## Secure Forms

- `GET /api/v2/livechat/secureForms` -get a list of secure forms
- `GET /api/v2/livechat/secureForms/{id}`  -get a secure form
- `POST /api/v2/livechat/secureForms` -create a new secure form
- `PUT /api/v2/livechat/secureForms/{id}`  -update a secure form
- `DELETE /api/v2/livechat/secureForms/{id}`  -remove a secure form

<div>

### Model

#### Secure Form JSON Format

Secure Form is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no | id of the secure form. |
  | `name` | string  | no | yes | name of the secure form. |
  | `description` | string  | no | no | description of the secure form. |
  | `fields` | array | no | no | an array of [Field](#field-json-format) |

</div>
<div>

### Endpoint

#### Get a list of secure forms

  `GET /api/v2/livechat/secureForms`

- Parameters:

    No parameters

- Response:

    An array of [Secure Form](#secure-form-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/secureforms
```

Sample response:

```json
[
    {
        "id": 4,
        "name": "justfortest",
        "description": "",
        "fields": [
            {
                "id": 13,
                "name": "Card Number",
                "type": "cardNumber",
                "isSystem": true,
                "isVisible": false,
                "isRequired": false,
                "options": ""
            },
            ...
        ]
    },
    ...
]
```

#### Get a single secure form

  `GET /api/v2/livechat/secureForms/{id}`

- Parameters:

    No parameters

- Response:

    [Secure Form](#secure-form-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/secureforms/5
```

Sample response:

```json
{
    "id": 5,
    "name": "justfortest2",
    "description": "",
    "fields": [
        {
            "id": 17,
            "name": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "options": ""
        },
        ...
    ]
}
```

#### Create a new secure form

  `POST /api/v2/livechat/secureForms`

- Parameters:

    [Secure Form](#secure-form-json-format)

- Response:

    [Secure Form](#secure-form-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "justfortest"}"    
     https://hosted.comm100.com/api/v2/livechat/secureforms
```

Sample response:

```json
{
    "id": 4,
    "name": "justfortest",
    "description": "",
    "fields": [
        {
            "id": 13,
            "name": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "options": ""
        },
        ...
    ]
}
```

#### Update a secure form

  `PUT /api/v2/livechat/secureForms/{id}`

- Parameters:

    [Secure Form](#secure-form-json-format)

- Response:

    [Secure Form](#secure-form-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "justfortestupdate"}"    
     https://hosted.comm100.com/api/v2/livechat/secureforms/4
```

Sample response:

```json
{
    "id": 4,
    "name": "justfortestupdate",
    "description": "",
    "fields": [
        {
            "id": 13,
            "name": "Card Number",
            "type": "cardNumber",
            "isSystem": true,
            "isVisible": false,
            "isRequired": false,
            "options": ""
        },
        ...
    ]
}
```

#### Remove a secure form

  `DELETE /api/v2/livechat/secureForms/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/secureforms/4
```

Sample response:

```json
"Secure Form with id '4' has been removed."
```

</div>
</div>
<div>

## Webhooks

- `GET /api/v2/livechat/webhooks` - Get a list of webhooks
- `POST /api/v2/livechat/webhooks` - Create a new webhook
- `PUT /api/v2/livechat/webhooks/{id}` - Update a webhook
- `DELETE /api/v2/livechat/webhooks/{id}`  - Remove a webhook

<div>

### Model

#### Webhook JSON Format

Webhook is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  |`id` | integer  | yes | no | id of the webhook. |
  |`event`| string  | no | yes | event of webhook, including `offlineMessageSubmitted`, `operatorEventNotification`, `chatStarted`, `chatEnded`, `chatWrappedUp`, `chatRequested` and `chatTransferred`. |
  |`targetUrl`| string  | no | yes |  target url of the webhook. |

</div>
<div>

### Endpoint

#### Get a list of webhooks

  `GET /api/v2/livechat/webhooks`

- Parameters:

    No parameters

- Response:

    An array of [Webhook](#webhook-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/webhooks
```

Sample response:

```json
[
    {
        "id": 2,
        "event": "chatWrappedUp",
        "targetUrl": "http://www.aa.com"
    },
    ...
]
```

#### Create a new webhook

  `POST /api/v2/livechat/webhooks`

- Parameters:

    [Webhook](#webhook-json-format)

- Response:

    [Webhook](#webhook-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"event" : "chatwrappedup","targeturl" : "http://www.baidu.com"}"    
     https://hosted.comm100.com/api/v2/livechat/webhooks
```

Sample response:

```json
{
    "id": 16,
    "event": "chatWrappedUp",
    "targetUrl": "http://www.baidu.com"
}
```

#### Update a webhook

  `PUT /api/v2/livechat/webhooks/{id}`

- Parameters:

    [Webhook](#webhook-json-format)

- Response:

    [Webhook](#webhook-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"event" : "chatwrappedup","targeturl" : "http://www.google.com"}"    
     https://hosted.comm100.com/api/v2/livechat/webhooks/16
```

Sample response:

```json
{
    "id": 16,
    "event": "chatWrappedUp",
    "targetUrl": "http://www.google.com"
}
```

#### Remove a webhook

  `DELETE /api/v2/livechat/webhooks/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK  

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE  https://hosted.comm100.com/api/v2/livechat/webhooks/16
```

Sample response:

```json
"WebHook with id '16' has been removed."
```

</div>
</div>
<div>

## Custom Variables

- `GET /api/v2/livechat/customVariables` -Get a list of custom variables
- `POST /api/v2/livechat/customVariables` -Create a new custom variable
- `PUT /api/v2/livechat/customVariables/{id}`  -Update a custom variable
- `DELETE /api/v2/livechat/customVariables/{id}`  -Remove a custom variable

<div>

### Model

#### Custom Variable JSON Format

Custom Variable is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no | id of the custom variable. |
  | `name` | string  | no | yes | name of the custom variable |.
  | `type` | string  | no | yes | type of the custom variable., including `text`, `integer` and `decimal`. |
  | `value` | string  | no | no | value of the custom variable. |
  |`hyperlink` | string  | no | no |  hyperlink of the custom variable. |

</div>
<div>

### Endpoint

#### Get a list of Custom Variables

  `GET /api/v2/livechat/customVariables`

- Parameters:

    No parameters

- Response:

    An array of [Custom Variable](#custom-variable-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/customvariables
```

Sample response:

```json
[
    {
        "id": 2,
        "name": "test",
        "type": "text",
        "value": "'lizz'",
        "hyperlink": "{!Visitor.IP}"
    },
    ...
]
```

#### Create a new Custom Variable

  `POST /api/v2/livechat/customVariables`

- Parameters:

    [Custom Variable](#custom-variable-json-format)

- Response:

    [Custom Variable](#custom-variable-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X POST -H "Content-Type: application/json"  
     -d "{"name" : "justfortest","type" : "text","value" : "aaaaa"}"    
     https://hosted.comm100.com/api/v2/livechat/customvariables
```

Sample response:

```json
{
    "id": 6,
    "name": "justfortest",
    "type": "text",
    "value": "aaaaa",
    "hyperlink": ""
}
```

#### Update a Custom Variable

  `PUT /api/v2/livechat/customVariables/{id}`

- Parameters:

    [Custom Variable](#custom-variable-json-format)

- Response:

    [Custom Variable](#custom-variable-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"name" : "justfortestupdate","type" : "text","value" : "bbbbb"}"    
     https://hosted.comm100.com/api/v2/livechat/customvariables/7
```

Sample response:

```json
{
    "id": 7,
    "name": "justfortestupdate",
    "type": "text",
    "value": "bbbbb",
    "hyperlink": ""
}
```

#### Remove a Custom Variable

  `DELETE /api/v2/livechat/customVariables/{id}`

- Parameters:

    No parameters

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X DELETE https://hosted.comm100.com/api/v2/livechat/customvariables/7
```

Sample response:

```json
"Custom Variable '7' has been removed."
```

</div>
</div>
<div>

## Agents

- `GET /api/v2/livechat/agents/{id}` -Get agent info in livechat  
- `PUT /api/v2/livechat/agents/{id}` -Update agent info in livechat

<div>

### Model

#### Agent JSON Format

 Agent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | yes | id of the agent.
  | `status` | string  | no | no | status of the agent, including `online`, `away`, `offline` and custom away status defined by site |
  | `ongoingChats` | string  | yes | no | total number of ongoing chats the agent has |
  | `departments` | array  | no | no | an array of department id |
  | `maxChatsCount` | integer  | no | no | the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled |
  | `isAcceptAllocation` | boolean | no | no | whether the agent accept auto allocation |

</div>
<div>

### Endpoint

#### Get agent info in livechat  

  `GET /api/v2/livechat/agents/{id}`

- Parameters:

    No parameters

- Response:

    [Agent](#agent-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v2/livechat/agents/1
```

Sample response:

```json
{
    "id": 1,
    "status": "online",
    "ongoingChats": 0,
    "departments": [
        1,
        2
    ],
    "maxChatsCount": 20,
    "isAcceptAllocation": false
}
```

#### Update agent info in livechat

  `PUT /api/v2/livechat/agents/{id}`

- Parameters:

    [Agent](#agent-json-format)

- Response:

    [Agent](#agent-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X PUT -H "Content-Type: application/json"  
     -d "{"maxchatscount" : "30"}"    
     https://hosted.comm100.com/api/v2/livechat/agents/1
```

Sample response:

```json
{
    "id": 1,
    "status": "online",
    "ongoingChats": 0,
    "departments": [
        1,
        2
    ],
    "maxChatsCount": 30,
    "isAcceptAllocation": false
}
```

</div>
</div>
<div>

## Chats

- `Get /api/v2/livechat/chats` - Get chats list.
- `Get /api/v2/livechat/chats/{id}` - Get a single chat.
- `DELETE /api/v2/livechat/chats/{id}` - Remove a chat.
- `DELETE /api/v2/livechat/chats` - Batch remove chats.

<div>

### Model

#### Custom Variable Value JSON Format

 Custom Variable is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | no | id of the custom variable. |
  | `name` | string | no | yes | name of the custom variable. |
  | `value` | string | no | no | value of the custom variable. |

#### Attachment JSON Foramt

 Attachment is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `name` | string | no | yes | name of the attachment. |
  | `uri` | string | no | no | uri of the attachment. |

#### Chat Message JSON Format

  Chat Message is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `time` | datetime  | no | no | the time of this message sent |
  | `sender` | string | no | no | name of this message's sender |
  | `type` | stirng | no | no | type of this message, maybe `agent` or `visitor` or `system` |
  | `content` | string | no | no | content of this message's sender |
  | `isNoteMessage` | boolean | no | no | Whether the message is a note message |

#### Chat Wrapup JSON Format

  Chat Wrapup is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `category` | array | no | no | array of [Chat Wrapup Category](#chat-wrapup-category-json-format) |
  | `comment` | string | no | no | comment of this chat's wrapup |
  | `fields` | array | no | no | array of [Custom Field Value](#custom-field-value-json-format) |

#### Chat Wrapup Category JSON Format

  Chat Wrapup Category is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `category` | string | no | no | category of this wrapup |
  | `group` | string | no | no | group of this wrapup |

#### Post-Chat Survey JSON Format

  Post Chat Survey is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `ratingGrade` | string | no | no | rating grade of this chat's survey |
  | `ratingComment` | string | no | no | rating comment of this chat's survey |
  | `fields` | array | no | no | array of [Custom Field Value](#custom-field-value-json-format) |
  
#### Agent JSON Format

  Agent is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer  | yes | yes | id of the agent |
  | `name` | string  | no | no | name of the agent |
  | `email` | string  | yes | no | email of the agent |
  
#### Chat JSON Format

 Chat is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |  
  | `id` | string  | yes | yes | id of the chat. |
  | `ssoUserId` | string | yes | no | SSO id of visitor |
  | `name` | string | no | no | name of the visitor |
  | `email` | string | no | no | email of the visitor |
  | `department` | string | no | no | department the visitor selected in the pre-chat window. Agent can also update the value while chatting with visitors. |
  | `agents` | array | no | no | array of [Agent](#Agent-Chat-Json-Format) |
  | `prechatFields` | array | no | no | values of custom fields entered by visitors in the pre-chat window. An array of [Custom Field Value](#custom-field-value-json-format). |
  | `customVariables` | array | no | no | information of custom variables captured from the web page visitors viewed. An array of [Custom Variable Value](#custom-variable-value-json-format). |
  | `requestTime` | datetime | no | no | time when the chat is requested |
  | `waitingTime` | string | no | no | amount of time a visitor waits for before his/her chat request gets accepted |
  | `endTime` | datetime | no | no | time when the chat ends |
  | `chatTranscript` | array | no | no | array of [Chat Message](#chat-message-json-format) |
  | `attachments` | array | no | no | files the operator sends to the visitor or vice versa as well as the screenshots sent to the operator by the visitor through Comm100 Screen  Capture. An array of [Attachment](#attachment-json-foramt) |
  | `noteAttachments` | array | no | no | files the operator sends as the note attachment. An array of [Attachment](#attachment-json-foramt) |
  | `postChat` | [Post-Chat Survey](#post-chat-survey-json-format) | no | no | post chat survey of this chat |
  | `wrapup` | [Chat Wrapup](#chat-wrapup-json-format) | no | no | agent wrapup for this chat |

</div>
<div>

### Endpoint

#### Get chats list

- End Point

  `Get /api/v2/livechat/chats`

- Parameters:

  - `timeFrom` - the beginning of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timeTo` - the end of the query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timezone` - time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as ±hh:mm.
  - `agentId` - id of the agent who participate in the chat.
  - `departmentId` - id of the department which the chat belongs to.
  - `categoryId` - id of the category which the chat belongs to.
  - `visitorId` - id of the visitor which the chat belongs to.
  - `keywords` - the key words of inquiring the chat
  - `conditions` - the condition list of inquiring the chat `conditions[0][field]=email&conditions[0][operate]=contains&conditions[0][value]=comm100`
    - `field` - field name of the condition.
    - `operate` - operate expression of the condition.
    - `value` - the value correspond with the field.
  - `pageIndex` -the page index of query, starts at 0.
  - `pageSize` - the page size of this query. defaults to 10, maximum is 100.

- Response
  - `total` - total count of the list.
  - `previousPage` - URL of the previous page, if there is no previous page, shows the first page.
  - `nextPage` - URL of the next page, if there is no next page, shows empty.
  - `chats` - an array of [Chat](#chat-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X GET https://hosted.comm100.com/api/v2/livechat/chats
```

Sample response:

```json
{
    "total": 8,
    "previousPage": "https://hosted.comm100.com/api/v2.0/livechat/chats?pageIndex=0",
    "nextPage": "",
    "chats": [
        {
            "id": "7b1a47f5-6dd5-4d29-a14d-725effdad6bd",
            "ssoUserId": "",
            "name": "asd",
            "email": "asd@12.com",
            "department": "",
            "agents": [
                {
                    "id": 446,
                    "display_name": "li yu1",
                    "email": "benjamin11@comm100.com"
                }
            ],
            "prechatFields": [
                {
                    "id": 85926,
                    "name": "Agreement",
                    "value": "I agree with the agreement"
                }
            ],
            "customVariables": [],
            "requestTime": "2019-01-16T09:12:45.027",
            "waitingTime": "00:00:01",
            "endTime": "2019-01-16T09:40:23.773",
            "chatTranscript": [
                {
                    "time": "01/16/2019 09:12:45",
                    "sender": "",
                    "type": "enumSystem",
                    "content": "If you do not want to wait, please click here to leave us a message."
                },
                ...
            ],
            "attachments": [],
            "postChat": {
                "ratingGrade": "-1",
                "ratingComment": "",
                "fields": []
            },
            "wrapup": null
        },
        ...
    ]
}
```

#### Get a single chat

  `Get /api/v2/livechat/chats/{id}`

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
     -X GET https://hosted.comm100.com/api/v2/livechat/chats/7b1a47f5-6dd5-4d29-a14d-725effdad6bd
```

Sample response:

```json
{
    "id": "7b1a47f5-6dd5-4d29-a14d-725effdad6bd",
    "ssoUserId": "",
    "name": "asd",
    "email": "asd@12.com",
    "department": "",
    "agents": [
        {
            "id": 446,
            "display_name": "li yu1",
            "email": "benjamin11@comm100.com"
        }
    ],
    "prechatFields": [
        {
            "id": 85926,
            "name": "Agreement",
            "value": "I agree with the agreement"
        }
    ],
    "customVariables": [],
    "requestTime": "2019-01-16T09:12:45.027",
    "waitingTime": "00:00:01",
    "endTime": "2019-01-16T09:40:23.773",
    "chatTranscript": [
        {
            "time": "01/16/2019 09:12:45",
            "sender": "",
            "type": "enumSystem",
            "content": "If you do not want to wait, please click here to leave us a message."
        },
        ...
    ],
    "attachments": [],
    "postChat": {
        "ratingGrade": "-1",
        "ratingComment": "",
        "fields": []
    },
    "wrapup": null
}
```

#### Remove a chat

  `DELETE /api/v2/livechat/chats/{id}`

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
    -X DELETE  https://hosted.comm100.com/api/v2/livechat/chats/7b1a47f5-6dd5-4d29-a14d-725effdad6bd
```

Sample response:

```json
"Chat '7b1a47f5-6dd5-4d29-a14d-725effdad6bd' has been removed."
```

#### batch remove chats

  `DELETE /api/v2/livechat/chats`

- Parameters

    ids: int array of id

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer yP7Agz9nzzpgyPTxfM6ajBgIMhuaoz_p1XvLgKyULP7SzIbCRUb3Qscheh7
    4BceSrdZ61_LrJ4saBNJPP8NJdsrx5CbWSOfVlqHU9-dp7lVgBZbVg661SOcDM0dMYb8nOZ4rixC79j-lHw4mW
    LEhJAtUzqsfkG3QamG0VklLNThmPvRttwyLGqzZFY3keXNw5ivxy1Mr5smAJDWPfzKKQZXJIkoUYutNz4Wt3iC
    80BlfjLcPnYOPFbAMnDdtvKjle6gf2V1WkHA-JW9W9QZc7A"
    --header 'Content-Type: application/x-www-form-urlencoded'
    --data '[0]=7b1a47f5-6dd5-4d29-a14d-725effdad6bd&[1]=aa93493d-e2f7-4c37-9333-b5da5c25b972'
    -X DELETE  https://hosted.comm100.com/api/v2/livechat/chats
```

Sample response:

```json
"Chats have been removed."
```

</div>
</div>
<div>

## Offline Messages

- `Get /api/v2/livechat/offlineMessages` -Get Offline messages list.
- `Get /api/v2/livechat/offlineMessages/{id}` - Get a single messages.
- `DELETE /api/v2/livechat/offlineMessages/{id}` - Remove a messages.

<div>

### Model

#### Offline Message JSON format

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

</div>
<div>

### Endpoint

#### Get messages list

  `Get /api/v2/livechat/offlineMessages`

- Parameters:
  - `timeFrom` - the beginning of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timeTo` - the end of the query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timezone` - time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as ±hh:mm.
  - `campaignId` - id of the campaign which the offline message
  - `departmentId` - id of the department which the offline message belongs to
  - `agentId` - id of the agent that this offline message belongs to
  - `visitorSegment` - id of the visitor segment which the visitor belongs to.
  - `keywords` - the key words of inquiring the  offline message.
  - `pageIndex` -the page index of query, starts at 0.

- Response
  - `total` -total count of the list.
  - `previousPage` -URL of the previous page, if there is no previous page, shows the first page.
  - `nextPage` -URL of the next page, if there is no next page, shows empty.
  - `offlineMessages` - an array of [Offline Message](#offline-message-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X GET https://hosted.comm100.com/api/v2/livechat/offlinemessages
```

Sample response:

```json
{
    "total": 28,
    "previousPage": "https://hosted.comm100.com/api/v2.0/livechat/offlinemessages?pageIndex=0",
    "nextPage": "https://hosted.comm100.com/api/v2.0/livechat/offlinemessages?pageIndex=1",
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
                    "uri": "https://hosted.comm100.com/api/v2.0/livechat/download?id=411&downloadtype=offlinemessage"
                }
            ]
        },
        ...
    ]
}
```

#### Get a single messages

  `Get /api/v2/livechat/offlinemessages/{id}`

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
     -X GET https://hosted.comm100.com/api/v2/livechat/offlinemessages/a2317d24-bec0-43e5-aaf5-2eae29ce948f
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
            "uri": "https://hosted.comm100.com/api/v2.0/livechat/download?id=411&downloadtype=offlinemessage"
        }
    ]
}
```

#### Remove a messages

  `DELETE /api/v2/livechat/offlinemessages/{id}`

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
    -X DELETE  https://hosted.comm100.com/api/v2/livechat/offlinemessages/a2317d24-bec0-43e5-aaf5-2eae29ce948f
```

Sample response:

```json
"Chat 'a2317d24-bec0-43e5-aaf5-2eae29ce948f' has been removed."
```

</div>
</div>
<div>

## Missed & Refused Chats

### Get missed and refused chats list

  `Get /api/v2/livechat/missedAndRefusedChats`

- Parameters
  - `timeFrom` - the beginning of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timeTo` - the end of the query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timezone` - time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as ±hh:mm.
  - `type` - type of the chat, including `missed` and `refused`.
  - `campaignId` - id of the campaign which the message of the chat happened in.
  - `departmentId` - id of the department which the chat belongs to.
  - `visitorSegmentation` - id of the visitor segment which visitor belongs to.
  - `pageIndex` -the page index of query.
  - `pageSize` - the page size of this query, defaults to 10, maximum is 100.

- Response
  - `total` -total count of the list.
  - `previousPage` -url of the previous page, if there is no previous page, shows the first page.
  - `nextPage` -url of the next page, if there is no next page, shows empty.
  - `missedAndRefusedChats` - list of the object that has the following parameters
    - `type` - type of the chat, including `missed` and `refused`.
    - `chat` - [Chat](#chat-json_format)

<div>

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X GET https://hosted.comm100.com/api/v2/livechat/missedAndRefusedChats
```

Sample response:

```json
{
    "total": 32,
    "previousPage": "https://hosted.comm100.com/api/v2.0/livechat/missedAndRefusedChats?pageIndex=0",
    "nextPage": "https://hosted.comm100.com/api/v2.0/livechat/missedAndRefusedChats?pageIndex=1",
    "missedAndRefusedChats": [
        {
            "type": "Missed",
            "chat": {
                "id": "a1217d24-bec0-43e5-aaf7-2eae29ce948f",
                "ssoUserId": "hehe",
                "name": "183.129.213.10",
                "email": "",
                "department": "",
                "agents": [],
                "prechatFields": [],
                "customVariables": [],
                "requestTime": "2019-01-16T03:06:19.38",
                "waitingTime": "00:00:03",
                "endTime": "2019-01-16T03:06:22.457",
                "chatTranscript": null,
                "attachments": [],
                "postChat": {
                    "ratingGrade": "-1",
                    "ratingComment": "",
                    "fields": []
                },
                "wrapup": null
            }
        },
        ...
    ]
}
```

</div>
</div>
<div>

## Agent Chats

### get agent chats list

  `Get /api/v2/livechat/agentChats`

- Parameters:
  - `timeFrom` - the beginning of the query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timeTo` - the end of the query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`
  - `timezone` - time zone of the `timeFrom` and `timeTo`, defaults to UTC time, format as ±hh:mm.
  - `agentId` - id of the agent who participated in the chat.
  - `keywords` - the key words of inquiring the chat

- Response
  - `agentChats` - `array` agent chats list
    - `agents` - `array`, agent names of the agent chat conversation
    - `transcript` - list of the object that has following parameters
      - `time` - `datetime`, time of this message was sent
      - `sender` - `string`, sender name of this message
      - `content` - `string`, content of this message


<div>

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -X GET https://hosted.comm100.com/api/v2/livechat/agentChats
```

Sample response:

```json
{
    "agentChats": [
        {
            "agents": [
                "bella",
                "bella02"
            ],
            "transcript": [
                {
                    "time": "2017-11-18T03:58:38.97",
                    "sender": "bella",
                    "content": "..."
                },
                {
                    "time": "2017-11-18T03:58:58.923",
                    "sender": "bella",
                    "content": "v2-52efe86ea1817b7069a37e3e662c51c7_r.jpg"
                }
            ]
        },
        ...
    ]
}
```

</div>
</div>
&#32;