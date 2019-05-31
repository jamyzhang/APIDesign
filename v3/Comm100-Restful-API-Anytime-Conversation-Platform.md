## Note
- 这个API是共享平台提供给APP中心调用的，用于转发Message和回调消息发送的结果。

## Objects

### message 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `conversationId` | integer | id of conversation | 
| `type` | string | `note`, `email`, `reply`, `socialMessage`, `chat`, `offlineMessage` |
| `directType` | string | `receive`, `send` |
| `accountId`| string | integrated account id | 
| `contactIdentityId`| string | id of contact identity |
| `source` | string | `agentConsole`, `helpDesk`, `webForm`, `API`, `chat`, `offlineMessage` | 
| `originalMessageId` | string | original message id|
| `originalMessageLink` | string | origial message link |
| `parentId` | string | parent id |
| `quoteTweetId` | string | quote tweet id |  
| `texts` | [text](#text)[] | text of message |  
| `quote` | string | quoted content of the message, only for email message |  
| `subject` | string | subject | 
| `cc` | string | cc email addresses |  
| `attachments` | [attachment](#attachment)[] | attachment array| 
| `mentionedAgentIds` | integer[] | only for Note, @mentioned agents id array |
| `isRead`| boolean | | 
| `sendStatus` | string | `sucess`, `sending`, `fail` |
| `sendertId`| string | id of agent or contact | 
| `senderType`| string | `agent` or `contact` or `system` | 
| `time` | datetime | the sent time of the message | 
 
### attachment 
| Name | Type | Description | 
| - | - | - |
| `id` | string | attachment unique id |
| `messageId` | string | message id |
| `type` | string | attachment type |
| `mimetype` | string | attachment mime type |
| `originalId` | string | original id |
| `originalLink` | string | original link |
| `text` | string | attachment text or description |
| `fileName` | string | attachment file name| 
| `url` | string | attachment download link | 
| `previewUrl` | string | preview url | 
| `size` | int | attachment size |
| `scale` | string | scale for location |
| `isAvailable` | boolean | if the attachment is available | 

### new attachment 
| Name | Type | Description | 
| - | - | - |
| `type` | string | attachment type |
| `mimetype` | string | attachment mime type |
| `originalId` | string | original id |
| `originalLink` | string | original link |
| `text` | string | attachment text or description |
| `fileName` | string | attachment file name| 
| `url` | string | attachment download link | 
| `previewUrl` | string | preview url | 
| `size` | int | attachment size |
| `scale` | string | scale for location |

### text
| Name | Type | Description | 
| - | - | - |
| `id` | string | id |
| `format` | string | `plaintext`, `html` |
| `content` | string | plain text or html body |

## EndPoints

### Post a message 
`post api/v3/anytime/platform/conversations/{id}/messages` 
- Parameters  
    - type: string, `note`, `email`, `reply`, `socialMessage`, required
    - accountId: string, channel account id,
    - contactIdentityId: string, contact identity id,
    - originalId: string,
    - originalLink: string,
    - subject: string, for email message, email subject,
    - text: 
        - format: string, `plaintext`, `html`
        - content: string, 
    - cc: string, message cc emails, 
    - parentId: string, 
    - quoteTweetId: string,
    - sendByType: string, `agent`, 
    - sendById: string, agent id,
    - attachments: [attachment](#new-attachment)[], attachment array
- Response 
    - [message](#message) 

### Feedback result
`post api/v3/anytime/platform/conversations/messages/{id}`
- Parameters
    - sendStatus: string, `success`, `failed`
    - message: string
