# Campaigns
Gets a full list of your campaigns and some campaign related data. Only agents with **"Manage Campaigns"** permission have access to  these resources.

### Available Paths

| Method | Name | Path
| --- | --- | ---
| GET | [Get List of Campaigns](#get-list-of-campaigns) | /api/v1/livechat/campaigns
| GET | [Get a Single Campaign](#get-a-single-campaign) | /api/v1/livechat/campaigns/{id}/prechat<br />/api/v1/livechat/campaigns/{id}/postChat<br />/api/v1/livechat/campaigns/{id}/offlineMessage<br />/api/v1/livechat/campaigns/{id}/invitation/autoInvitations<br />/api/v1/livechat/campaigns/{id}/agentWrapup

## Get List of Campaigns
Returns a list of campaigns.

### Response
| Property | Description
| --- | ---
| `id`| the id of the campaign
| `name` | the name of the campaign
| `description` | the description of the campaign

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/campaigns" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 1,
        "name": "test campaign",
        "description": "This is a campaign for testing."
    },
    {
        "id": 2,
        "name": "Website Campaign",
        "description": ""
    },
    ...
]
```

## Get a Single Campaign
Gets detailed data of a campaign, such as the [**pre-chat fields**](#pre-chat), [**post chat fields**](#post-chat), [**offline message fields**](#offline-message), etc.

### Pre-Chat
Gets the field list of Pre-Chat form.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/campaigns/{id}/prechat
```

#### Parameters
| Property | Description
| --- | ---
| `id`| the id of the campaign, which can be obtained from the [list of all campaigns](#get-list-of-campaigns)

#### Response
| Property | Description
| --- | ---
| `isEnable` | whether the pre-chat of the current campaign is enabled or not
| `greetingMessage` | the message shown in pre-chat form, available when pre-chat is enabled
| `socialLogin` | containing `isEnableGoogle` and `isEnableFacebook`, whether Facebook login or Google is enabled or not 
| `isRememberForm` | whether to remember visitor info collected from pre-chat form or not, available when pre-chat is enabled
| `fieldLayoutStyle` | the layout of fields in visitor side windows including Pre-Chat, Offline Message and Post Chat windows. `vertical`, `horizontal` 
| `fields` | the fields available in pre-chat form

#### Field Structure

| Property | Description
| --- | ---
| `id` | the id of the field
| `name` | the name of the field
| `type` | the type of the field. All field types are listed [here](#field-type).
| `isSystem` | whether the field is system field or not
| `isVisible` | whether the field is visible or not
| `isRequired` | whether the field is required or not
| `options` | a list of options available. When type = department, to get the department options showing on your pre-chat form, you can use the API for Department. When `type = department` it is not accessible, you can get the options via   

#### Field Type
System Field

| Type | Description
| --- | ---
| name | Name field
| email | Email field
| phone | Phone field
| company | Company field
| product | Product and Service field, used in pre-chat form
| department | Department field
| ticket | Ticket field
| rating | Rating field, available in post chat form
| comment | Comment field
| subject | Subject field, available in offline message form
| content | Content field, available in offline message form
| attachment | Attachment field, available in offline message form
| category | Category field, available in agent wrap-up form


Custom Field

| Type | Description
| --- | ---
| text | Text field
| textarea | Textarea field
| radio | Radio Box field
| checkbox | Check Box field
| select | Drop Down List field
| checkboxList | Check Box List field

#### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/campaigns/1/prechat" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "isEnable": true,
    "greetingMessage": "Welcome to our website. We are excited to chat with you!",
    "socialLogin": {
        "isEnableGoogle": false,
        "isEnableFacebook": false,
    },
    "isRememberForm": false,
    "fieldLayoutStyle": "vertical",
    "fields": [
        {
            "id": 1,
            "name": "Name",
            "type": "name",
            "isSystem": true,
            "isVisible": true,
            "isRequired": true,
            "options": []
        },
        {
            "id": 2,
            "name": "Email",
            "type": "email",
            "isSystem": true,
            "isVisible": true,
            "isRequired": true,
            "options": []
        },
        {
            "id": 3,
            "name": "Company",
            "type": "company",
            "isSystem": true,
            "isVisible": true,
            "isRequired": false,
            "options": []
        },
        {
            "id": 4,
            "name": "Is this the first you visit our website?",
            "type": "checkbox",
            "isSystem": false,
            "isVisible": true,
            "isRequired": true,
            "options": [
                "false",
                "true"
            ]
        }
    ]
}
```

### Post Chat
Gets the fields of Post Chat form.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/campaigns/{id}/postChat
```

#### Parameters
| Property | Description
| --- | ---
| `id` | the id of the campaign, which can be obtained from the [list of all campaigns](#get-list-of-campaigns)

#### Response
| Property | Description
| --- | ---
| `isEnable` | whether the post chat of the current campaign is enabled or not
| `greetingMessage` | the message shown in post chat form, available when post chat is enabled
| `fieldLayoutStyle` | the layout of fields in visitor side windows including Pre-Chat, Offline Message and Post Chat windows. `vertical`, `horizontal`
| `fields` | the [fields](#field-structure) available in the post chat form

#### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/campaigns/1/postChat" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "isEnable": true,
    "greetingMessage": "Please comment on our service performance so that we can serve you better. Thanks for your time!",
    "fieldLayoutStyle": "vertical",
    "fields": [
        {
            "id": 6,
            "name": "Rating",
            "type": "rating",
            "isSystem": true,
            "isVisible": true,
            "isRequired": true,
            "options": [
                "Poor",
                "Fair",
                "Good",
                "Very Good",
                "Excellent"
            ]
        },
        {
            "id": 7,
            "name": "Comment",
            "type": "comment",
            "isSystem": true,
            "isVisible": true,
            "isRequired": false,
            "options": []
        }
    ]
}
```

### Offline Message
Gets the field list of offline messge.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/campaigns/{id}/offlineMessage
```

#### Parameters
| Property | Description
| --- | ---
| `id`| the id of the campaign, which can be obtained from the [list of all campaigns](#get-list-of-campaigns)

#### Response
| Property | Description
| --- | ---
| `isUseCustomOfflinePage` | whether to redirect visitors to your own page when no agents are available
| `customOfflinePage` | available when `isUseCustomOfflinePage = true`, containing `url` and `isOpenInNewWindow`
| `greetingMessage` | the greeting message shown in offline message window, available when isUseCustomOfflinePage is disabled
| `fieldLayoutStyle` | the layout of fields in visitor side windows including Pre-Chat, Offline Message and Post Chat windows. `vertical`, `horizontal`
| `fields` | the [fields](#field-structure) available in the offline message form

#### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/campaigns/1/offlineMessage" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "isEnable": true,
    "greetingMessage": "Please leave us a message and we will get back to you shortly.",
    "fieldLayoutStyle": "vertical",
    "fields": [
        {
            "id": 16,
            "name": "Subject",
            "type": "subject",
            "isSystem": true,
            "isVisible": true,
            "isRequired": true,
            "options": []
        },
        {
            "id": 17,
            "name": "Content",
            "type": "content",
            "isSystem": true,
            "isVisible": true,
            "isRequired": false,
            "options": []
        },
        {
            "id": 18,
            "name": "Attachment",
            "type": "attachment",
            "isSystem": true,
            "isVisible": true,
            "isRequired": false,
            "options": []
        }
    ]
}
```

### Auto Invitation
Gets the list of Auto Invitations.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/campaigns/{id}/invitation/autoInvitations
```

#### Parameters
| Property | Description
| --- | ---
| `id`| the id of the campaign, which can be obtained from the [list of all campaigns](#get-list-of-campaigns)

#### Response
| Property | Description
| --- | ---
| `id` | the id of the auto invitation
| `name` | the name of the auto invitation
| `isEnable` | whether the auto invitation is enabled

#### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/campaigns/1/invitation/autoInvitations" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 24,
        "name": "Spent on website more than 30 seconds",
        "isEnable": false
    },
    {
        "id": 25,
        "name": "Visited website more than once (returning visitors)",
        "isEnable": false
    },
    {
        "id": 26,
        "name": "Visited more than 5 pages",
        "isEnable": false
    }
]
```

### Agent Wrap-Up
Gets the field list of Agent Wrap-Up form.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/campaigns/{id}/agentWrapup
```

#### Parameters
| Property | Description
| --- | ---
| `id`| the id of the campaign, which can be obtained from the [list of all campaigns](#get-list-of-campaigns)

#### Response
| Property | Description
| --- | ---
| `fields` | the [fields](#field-structure) available in agent wrap-up form

For the **Category** field, when under the Basic mode, its structure is the same as other fields; when under the Advanced mode, this field will have `categories` property instead of `options`. You can reference the following example.

#### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/campaigns/1/agentWrapup" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 32,
        "name": "Category",
        "type": "category",
        "isSystem": true,
        "isVisible": true,
        "isRequired": true,
        "categories": [
            {
                "name": "Product",
                "options": [
                    "Live Chat",
                    "Ticket"
                ]
            },
            {
                "name": "Account",
                "options": [
                    "Forget Password",
                    "Change Password Failure"
                ]
            }
        ]
    },
    {
        "id": 33,
        "name": "Comment",
        "type": "comment",
        "isSystem": true,
        "isVisible": true,
        "isRequired": false,
        "options": []
    }
]
```

