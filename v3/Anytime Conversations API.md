## Note 
- 这里的API是共享平台提供给APP中心调用的，用于转发第三方APP过来的外部的Message，回调更新消息发送结果，以及更新缓层，不需要开放给客户。

## Objects

### message 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `channelId` | string | channel id | 
| `channelAccountId`| string | channel account id | 
| `contactIdentity`| [contactIdentity](#contactIdentity) | contact identity |
| `originalConversationId` | integer | id of conversation | 
| `originalMessageId` | string | original message id|
| `originalMessageUrl` | string | origial message url |
| `originalParentId` | string | parent id |
| `subject` | string | subject | 
| `cc` | string | cc email addresses |  
| `contents` | [content](#content)[] | content array| 
| `mentionedAgentIds` | integer[] | only for Note, @mentioned agents id array |
| `isRead`| boolean | if the message read by agent | 
| `sendStatus` | string | `sucess`, `sending`, `failed` |
| `senderId`| string | id of contact | 
| `senderType`| string | `contact` | 
| `time` | datetime | the sent time of the message | 
 
### contactIdentity 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of contact identity | 
| `account` | string | contact account, email address, facebook id, twitter id, sms number... |
| `name` | string | original channel name |
| `avatarUrl` | string | original channel avatar url |
| `originalContactInfoUrl` | string | original channel contact info URL | 

 ### content
| Name | Type | Description | 
| - | - | - | 
| `id` | string | guid | 
| `type` | string | content type, `text`, `htmlText`, `video`,`audio`, `picture`, `file`, `location` |  
| `text` | string | text | 
| `htmlText` | string | html text |
| `name` | string | file name| 
| `url` | string | download link | 
| `title` | string | media title| 
| `latitude` | string | latitude | 
| `longitude` | string | longitude | 
| `scale` | string | scale for location |
| `desc` | string | description | 

## EndPoints

### Post a message 
`post api/v3/anytime/platform/conversations/messages` 
- Parameters  
    - channelId： string, channel Id, required,
    - channelAccountId: string, channel account id,
    - contactIdentity: 
        - account: string, 
        - name: string,
        - avatarUrl: string,
        - originalContactInfoUrl: string
    - originalParentId: string, 
    - originalConversationId: string
    - originalMessageId: string,
    - originalMessageUrl: string,
    - subject: string, for email message, email subject,
    - cc: string, message cc emails, 
    - contents: [content](#content)[],
- Response 
    - code: string
    - message: string

### Callback result
`put api/v3/anytime/platform/conversations/messages/{id}`
- Parameters
    - sendStatus: string, `success`, `failed`
    - originalMessageId: string, 
    - originalMessageUrl: string,
    - content[]: 
        - id: string
        - url: string 
- Response 
    - httpStatusCode

### Update Cache
`put api/v3/anytime/platform/caches`
- Parameters
    - cacheItem: `channel`, `channelAccount`, `version`, `app`, `versionChannel`
    - actionType: `updated`
- Response
    - httpStatusCode
