## Note
- //这个文档废弃了。    不需要这些接口了。 转发平台调用的接口和agent console调用一样的接口。
- 这个API是共享平台提供给APP中心调用的，用于转发Message和回调消息发送的结果。

## Objects

### message 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `originalConversationId` | integer | id of conversation | 
| `integrationAccountId`| string | integration account id | 
| `contactIdentityId`| string | id of contact identity |
| `channelId` | string | channel id | 
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
    - integrationAccountId: string, channel account id,
    - contactIdentityId: string, contact identity id,
    - originalMessageId: string,
    - originalMessageUrl: string,
    - subject: string, for email message, email subject,
    - originalParentId: string, 
    - originalConversationId: string
    - cc: string, message cc emails, 
    - contents: [content](#content)[],
    - sendByType: string, `agent`, 
    - sendById: string, agent id,
- Response 
    - code: string
    - message: string

### Callback result
`put api/v3/anytime/platform/conversations/messages/{id}`
- Parameters
    - sendStatus: string, `success`, `failed`
    - message: string, message text, for example: fail reason
- Response 
    - httpStatusCode