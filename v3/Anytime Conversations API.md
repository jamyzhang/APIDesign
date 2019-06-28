# Authentication 
- Comm100 anytime Conversation API provides 2 authentication methods: 
    - API_key Authentication 
    - OAuth Authentication 
- [document](https://www.comm100.com/doc/api/introduction.htm#/) 

# Parameter introduction 
- Incoming parameters:
    - Get API passes parameters through the query string 
    - Put/Post API passes parameters through json data. 
    - DateTime Parameters: 
        - All time parameters need to be entered in the standard format of <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO-8601</a>
- All time values are UTC time. The caller can convert to different time zones where needed. 

# Includes
- Following APIs can use `Includes` as parameters to get related objects.

    | Endpoints | Support including parameters |
    | - | - |
    | `get api/v3/anytime/conversations` | assignedAgent, assignedDepartment, contactOrVisitor, createdBy, lastRepliedBy |
    | `get api/v3/anytime/conversations/{id}` | assignedAgent, assignedDepartment, contactOrVisitor, createdBy, lastRepliedBy, messages, eventLogs |
    | `get api/v3/anytime/conversations/{id}/messages` | sender |
    | `get api/v3/anytime/deletedConversations` | assignedAgent, assignedDepartment, contactOrVisitor, createdBy, lastRepliedBy |
    | `get api/v3/anytime/deletedConversations/{id}` | assignedAgent, assignedDepartment, contactOrVisitor, createdBy, lastRepliedBy, messages |
    | `get api/v3/anytime/deletedConversations/{id}/messages` | sender |
    | `get api/v3/anytime/portalConversations/{id}` | contact, messages |
    | `get api/v3/anytime/portalConversations` | contact |
    | `get api/v3/anytime/portalConversations/{id}/messages` | sender | 

- Sample:
    - request: `get api/v3/anytime/conversations/{id}?include=assignedAgent,createdBy,messages`
    - response:

        ``` javascript
        {
            "id": 1,
            "assignedAgentId": 1,
            "assignedAgent": {  //included the agent object
                "id": 1,
                //...
            },
            "relatedType": "contact",
            "relatedId":2,
            "createdById": 3,
            "createdByType": "agent",
            "createdBy": {  //included the agent or contact object according to the createdByType.
                "id": 3,
                //...
            },
            "messages":[    //included the messages.
                {
                    "id": 56, 
                    //...
                },
                {
                        "id": 57, 
                    //...
                }
            ]
            //...
        } 
        ``` 

# Resource List 
|Name|EndPoint|Note| 
|---|---|---| 
|[Conversation](#conversations)|/api/v3/anytime/conversations| Conversations | 
|[PortalConversation](#portalConversations)|/api/v3/anytime/portalConversations| Portal conversations |
|[Attachment](#attachments)|/api/v3/anytime/attachments| Upload attachment for conversations | 
|[View](#views)|/api/v3/anytime/views| Agent console views| 
|[Routing](#Routing)|/api/v3/anytime/routing| Routing | 
|[AutoAllocation](#AutoAllocations)|/api/v3/anytime/autoAllocation| Auto allocations | 
|[Trigger](#Triggers)|/api/v3/anytime/triggers| Triggers| 
|[SLAPolicy](#SLAPolicies)|/api/v3/anytime/SLAPolicies| SLA policies | 
|[WorkingTime&Holiday](#WorkingTime&Holiday)|/api/v3/anytime/workingTime| Work time and holiday | 
|[Fields&Mapping](#fields&mapping)|/api/v3/anytime/fields| System fields and custom fields | 
|[BlockedSender](#blockedsenders)|/api/v3/anytime/blockedSenders| Blocked email or domain | 
|[Junk](#junks)|/api/v3/anytime/junks| Emails from blocked senders | 
|[ChannelAccount](#channel-accounts)|/api/v3/anytime/channelAccounts| Channel accounts | 
|[Channel](#channels)|/api/v3/anytime/channels| integrated channels | 
|[Report](#reports)|/api/v3/anytime/reports| Anytime conversation reports | 

# Conversations 
## objects 
### conversation 
| Name | Type | Description | 
| - | - | - | 
| `id` | integer | id of conversation | 
| `guid` | string | guid of conversation | 
| `relatedType` | string | `contact`, `visitor`, `agent`| 
| `relatedId` | string | contact id, visitor id, agent id | 
| `subject` | string | conversation subject | 
| `assignedAgentId` | string | assigned agent id | 
| `assignedDepartmentId` | string | assigned department id | 
| `originalId` | string | original id on social platform | 
| `priority` | string | `urgent`, `high`, `normal`, `low` | 
| `status` | string | `new`, `pendingInternal`, `pendingExternal`, `onHold`, `closed` | 
| `hasDraft` | boolean | if has draft | 
| `isDeleted` | boolean | if deleted | 
| `isRead` | boolean | if the conversation is read | 
| `isReadByContact` | boolean | if the portal conversation is read by contact |
| `isEditable`| boolean | if the current agent can update\reply the conversation | 
| `isActive`| boolean | if open in my active work area by agent | 
| `tagIds` | string[] | tag id array | 
| `mentionedAgents`|[mentioned agent](#mentioned-agent)[]| mentioned agents list | 
| `customFields` | [custom field value](#custom-field-value)[] | custom field value array | 
| `createdById` | string | contact id or agent id or visitor id| 
| `createdByType` | string | agent or contact or system or visitor | 
| `createdTime` | datetime | create time of conversation | 
| `lastActivityTime` | datetime | last activity time of conversation | 
| `lastStatusChangeTime` | datetime | last status change time of conversation | 
| `lastRepliedTime` | datetime | last replied time | 
| `lastRepliedById` | integer | contact id or agent id | 
| `lastRepliedByType` | string | `agent` or `contact` or `system`| 
| `slaPolicyId` | string | SLA id of this conversation matched | 
| `firstRespondBreachAt` | datetime | Timestamp that denotes when the first response is due | 
| `nextRespondBreachAt` | datetime | Timestamp that denotes when the next response is due | 
| `resolveBreachAt` | datetime | Timestamp that denotes when the conversation is due to be resolved | 

### custom field value
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of custom field |
| `name` | string | the name of custom field |
| `value` | string | the value of custom field |

### mentioned agent 
| Name | Type | Description | 
| - | - | - | 
| `agentId` | string | the agent id of mentioned | 
| `isRead`| boolean | if the mentioned conversation is read | 
| `messageId`| string | message id| 

### message 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `conversationId` | integer | id of conversation | 
| `channelId` | string | channel Id | 
| `type` | string | `note`, `message` |
| `directType` | string | `receive`, `send` |
| `channelAccountId`| string | channel account id | 
| `contactIdentityId`| string | contact identity id |
| `originalMessageId` | string | original message id, or chat Id or offlineMessageId |
| `originalMessageUrl` | string | origial message link |
| `parentId` | string | parent id |
| `subject` | string | subject | 
| `cc` | string | cc email addresses |  
| `contents` | [content](#content)[] | content array | 
| `mentionedAgentIds` | string[] | only for Note, @mentioned agents id array |
| `isRead`| boolean | if the message read by agent| 
| `sendStatus` | string | `success`, `sending`, `failed` |
| `senderId`| string | id of agent or contact | 
| `senderType`| string | `agent` or `contact` or `system` | 
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

### conversation draft 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message draft | 
| `conversationId` | integer | id of conversation | 
| `channelAccountId`| string | channel account id | 
| `contactIdentityId`| string | id of contact identity |
| `parentId` | string | parent id |
| `subject` | string | subject | 
| `cc` | string | cc email addresses |  
| `contents` | [content](#content)[] | content array | 
| `mentionedAgentIds` | string[] | only for Note, @mentioned agents id array |
| `senderId`| string | id of agent| 
| `time` | datetime | the sent time of the message | 
  
 
## endpoints 
|EndPoint|Note| 
|---|---|
| `get api/v3/anytime/conversations`  |  [List conversations](#List-conversations)  |
| `get api/v3/anytime/conversations/{id}` |  [Get a conversation](#Get-a-conversation)  |
| `post api/v3/anytime/conversations` | [Submit a new conversation](#Submit-a-new-conversation) |
| `put api/v3/anytime/conversations/{id}` | [Update a conversation ](#Update-a-conversation ) |
| `put api/v3/anytime/conversations/`  | [Batch update conversations](#Batch-update-conversations) |
| `put api/v3/anytime/conversations/{id}/read`  | [Mark a conversation as read](#Mark-a-conversation-as-read) |
| `put api/v3/anytime/conversations/{id}/unread`  | [Mark-a-conversation-as-unread ](#) |
| `post api/v3/anytime/conversations/{id}/merge` | [ Merge a conversation ](#Merge-a-conversation) |
| `get api/v3/anytime/conversations/{id}/agents`  | [Get agents of openning conversation](#Get-agents-of-openning-conversation) |
| `get api/v3/anytime/conversations/unreadCount` | [List unread conversations number for views](#List-unread-conversations-number-for-views) |
| `delete api/v3/anytime/conversations/{id}` | [Delete a conversation ](#Delete-a-conversation ) |
| `delete api/v3/anytime/conversations`  | [Batch delete conversations ](#Batch-delete-conversations ) |
| `get api/v3/anytime/conversations/{id}/messages` | [List messages of a conversation](#List-messages-of-a-conversation) |
| `get api/v3/anytime/conversations{id}/messages/{messageId}`  | [Get a message](#Get-a-message) |
| `post api/v3/anytime/conversations/{id}/messages` | [Reply a message](#Reply-a-message) |
| `put api/v3/anytime/conversations/{id}/messages/{messageId}`  | [Update a message](#Update-a-message) |
| `put api/v3/anytime/conversations/{id}/messages/{messageId}/resend`  | [Resend a message](#Resend-a-message) |
| `put api/v3/anytime/conversations/{id}/messages/{messageId}/read` | [Mark a message as read](#Mark-a-message-as-read) |
| `put api/v3/anytime/conversations/{id}/messages/{messageId}/unread`   | [Mark a message as unread ](#Mark-a-message-as-unread) |
| `delete api/v3/anytime/deletedConversations/{id}`  | [Delete a conversation permanently ](#Delete-a-conversation-permanently) |
| `post api/v3/anytime/deletedConversations/{id}/restore `  | [Restore a deleted conversation ](#Restore-a-deleted-conversation) |
| `get api/v3/anytime/deletedConversations/`  | [List deleted conversations ](#List-deleted-conversations ) |
| `get api/v3/anytime/deletedConversations/{id}`  | [Get a deleted conversation](#Get-a-deleted-conversation) |
| `get api/v3/anytime/deletedConversations/{id}/messages`  | [List messages of a deleted conversation](#List-messages-of-a-deleted-conversation) |
| `get api/v3/anytime/conversations/{id}/draft`  | [Get a conversation draft ](#Get-a-conversation-draft) |
| `post api/v3/anytime/conversations/{id}/draft`  | [Create a conversation draft ](#Create-a-conversation-draft) |
| `put api/v3/anytime/conversations/{id}/draft`  | [Update a conversation draft ](#Update-a-conversation-draft) |
| `delete api/v3/anytime/conversations/{id}/draft`  | [ Delete a conversation draft ](#Delete-a-conversation-draft) |


### List conversations 
`get api/v3/anytime/conversations` 
+ Each request returns a maximum of 50 conversations. 
+ Parameters 
    - viewId: string, view id
    - tagId: string, tag id
    - keywords: string
    - timeFrom: DateTime, last reply time, default search the last 30 days
    - timeTo: DateTime, last reply time, default value is the current time
    - timeZoneOffset, float, time zone of your time parameters
    - pageIndex: integer
    - sortBy: string, `nextSLABreach`, `lastReplyTime`, `lastActivityTime`, `priority`, `status` , default value: `lastReplyTime`
    - sortOrder: string, `ascending` or `descending`, default value: `descending`
    - conditions: parameter format: `conditions[0][field]=subject&conditions[0][matchType]=is&conditions[0][value]=hi&conditions[1][field]=status&conditions[1][matchType]=is&conditions[1][value]=new`, fields can be conversation system fields and custom fields.
        - field: string, field name
        - matchType: string 
        - value: string
+ Response 
    - conversations: [conversation](#conversations) list, 
    - total: integer, total number of conversations 
    - previousPage: string, next page uri, the first page return null. 
    - nextPage: string, the last page return null. 
    - currentPage: string, current page uri. 
+ Includes

    | Includes | Description |
    | - | - |
    | assignedAgent | `get api/v3/anytime/conversations?include=assignedAgent` |
    | assignedDepartment | `get api/v3/anytime/conversations?include=assignedDepartment` |
    | contactOrVisitor | `get api/v3/anytime/conversations?include=contactOrVisitor` |
    | createdBy | `get api/v3/anytime/conversations?include=createdBy` |
    | lastRepliedBy | `get api/v3/anytime/conversations?include=lastRepliedBy` | 

### Get a conversation 
`get api/v3/anytime/conversations/{id}` 
+ Parameters 
    - id: integer, conversation  
+ Response 
    - [conversation](#conversation) 
+ Includes

    | Includes | Description |
    | - | - |
    | assignedAgent | `get api/v3/anytime/conversations/{id}?include=assignedAgent` |
    | assignedDepartment | `get api/v3/anytime/conversations/{id}?include=assignedDepartment` |
    | contactOrVisitor | `get api/v3/anytime/conversations/{id}?include=contactOrVisitor` |
    | createdBy | `get api/v3/anytime/conversations/{id}?include=createdBy` |
    | lastRepliedBy | `get api/v3/anytime/conversations/{id}?include=lastRepliedBy` |
    | messages | `get api/v3/anytime/conversations/{id}?include=messages` |
    | eventLogs | `get api/v3/anytime/conversations/{id}?include=eventLogs` |
 
### Submit a new conversation
`post api/v3/anytime/conversations` 
- Parameters 
    - subject: string, conversation subject, required 
    - assignedAgentId: string, agent id
    - assignedDepartmentId: string, department id
    - priority: string, `urgent`, `high`, `normal`, `low`, default value: `normal` 
    - status: string, `new`, `pendingInternal`, `pendingExternal`, `onHold`, `closed`, default value: `new` 
    - customFields: [custom field value](#custom-field-value)[], custom field value array
    - tagIds: string[], tag id array
    - message: the first message of the conversation, required
        - channelId: string, channel Id, required
        - channelAccountId: string, channel account id,
        - contactIdentityId: string, contact identity id,
        - subject: string, for email message, email subject 
        - cc: string, message cc emails
        - contents: [content](#content)[],
+ Response 
    - [conversation](#conversations)

### Update a conversation 
`put api/v3/anytime/conversations/{id}` 
- Parameters 
    - id: integer, conversation id
    - subject: string, conversation subject
    - relatedType: string, `contact`, `visitor`
    - relatedId: string, contact id or visitor id
    - assignedAgentId: string, agent id
    - assignedDepartmentId: string, department id
    - priority: string, priority: `urgent`, `high`, `normal`, `low`
    - status: string, `new`, `pendingInternal`, `pendingExternal,`, `onHold`, `closed`
    - isRead: boolean
    - isActive: boolean
    - customFields: [custom field value](#custom-field-value)[], custom field value array
    - tagIds: integer[], tag id array
- Response 
    - [conversation](#conversation) 

### Batch update conversations
`put api/v3/anytime/conversations/` 
+ Parameters 
    - ids: integer[], conversation id array
    - status, string
    - priority, string
    - assignedAgentId, string
    - assignedDepartmentId, string
    - isRead, boolean
+ Response 
    - [conversation](#conversation) list 

### List messages of a conversation 
`get api/v3/anytime/conversations/{id}/messages` 
+ Parameters 
    - id: integer, conversation id 
+ Response 
    - [message](#message) list 
+ Includes

    | Includes | Description |
    | - | - |
    | sender | `get api/v3/anytime/conversations/{id}/messages?include=sender` |

### Get a message 
`get api/v3/anytime/conversations{id}/messages/{messageId}` 
+ Parameters 
    - id: number, conversation id 
    - messageId: string, message id
+ Response 
    - [message](#message)
+ Includes

    | Includes | Description |
    | - | - |
    | sender | `get api/v3/anytime/conversations/messages/{id}?include=sender` |

### Reply a message 
`post api/v3/anytime/conversations/{id}/messages` 
- Parameters  
    - type: string, `note`, `message`, required
    - channelId: string, channel Id, required
    - channelAccountId: string, channel account id, 
    - subject: string, for email message, email subject
    - cc: string, message cc emails 
    - parentId: string,
    - contents: [content](#content)[]
- Response 
    - [message](#message) 

### Update a message 
`put api/v3/anytime/conversations/{id}/messages/{messageId}` 
- Parameters  
    - id: number, conversation id,
    - messageId: string, message id,
    - sendStatus: string, `success`, `sending`, `failed` 
    - originalMessageId: string, 
    - originalMessageUrl: string,
    - content[]: 
        - id: string
        - url: string
- Response 
    - [message](#message) 

### Resend a message 
`put api/v3/anytime/conversations/{id}/messages/{messageId}/resend` 
- Parameters  
    - id: number, conversation id,
    - messageId: string, message id,
- Response 
    - [message](#message) 


### Mark a conversation as read 
`put api/v3/anytime/conversations/{id}/read` 
+ Parameters 
    - id: integer, conversation id 
+ Response 
    - http status code

### Mark a conversation as unread 
`put api/v3/anytime/conversations/{id}/unread` 
+ Parameters 
    - id: integer, conversation id 
+ Response 
    - http status code

### Mark a message as read 
`put api/v3/anytime/conversations/{id}/messages/{messageId}/read` 
+ Parameters 
    - id: number, conversation id,
    - messageId: string, message id,
+ Response 
    - http status code

### Mark a message as unread 
`put api/v3/anytime/conversations/{id}/messages/{messageId}/unread` 
+ Parameters 
    - id: number, conversation id,
    - messageId: string, message id,
+ Response 
    - http status code

### Get agents of openning conversation 
`get api/v3/anytime/conversations/{id}/agents` 
+ Parameters 
    - id: number, conversation id,
+ Response 
    - agent list

### Delete a conversation 
`delete api/v3/anytime/conversations/{id}` 
- Parameters 
    - id: integer, conversation id
- Response 
    - http status code 

### Batch delete conversations 
`delete api/v3/anytime/conversations` 
+ Parameters 
    - ids: integer[], id array
+ Response 
    - http status code 

### List deleted conversations 
`get api/v3/anytime/deletedConversations/` 
- Parameters 
    - keywords: string
    - pageIndex: integer
    - timeFrom: DateTime, last reply time, default search the last 30 days
    - timeTo: DateTime, last reply time, default value is the current time
- Response 
    - deletedConversations: [conversation](#conversation) list 
    - total: integer, total number of conversations 
    - previousPage: string, next page uri, the first page return null. 
    - nextPage: string, the last page return null. 
    - currentPage: string, current page uri. 
- Includes

    | Includes | Description |
    | - | - |
    | assignedAgent | `get api/v3/anytime/deletedConversations?include=assignedAgent` |
    | assignedDepartment | `get api/v3/anytime/deletedConversations?include=assignedDepartment` |
    | contactOrVisitor | `get api/v3/anytime/deletedConversations?include=contactOrVisitor` |
    | createdBy | `get api/v3/anytime/deletedConversations?include=createdBy` |
    | lastRepliedBy | `get api/v3/anytime/deletedConversations?include=lastRepliedBy` | 

### Get a deleted conversation 
`get api/v3/anytime/deletedConversations/{id}` 
- Parameters 
    - id: integer, conversation id 
- Response 
    - [conversation](#conversation) 
- Includes

    | Includes | Description |
    | - | - |
    | assignedAgent | `get api/v3/anytime/deletedConversations/{id}?include=assignedAgent` |
    | assignedDepartment | `get api/v3/anytime/deletedConversations/{id}?include=assignedDepartment` |
    | contactOrVisitor | `get api/v3/anytime/deletedConversations/{id}?include=contactOrVisitor` |
    | createdBy | `get api/v3/anytime/deletedConversations/{id}?include=createdBy` |
    | lastRepliedBy | `get api/v3/anytime/deletedConversations/{id}?include=lastRepliedBy` |
    | messages | `get api/v3/anytime/deletedConversations/{id}?include=messages` |
    | eventLogs | `get api/v3/anytime/deletedConversations/{id}?include=eventLogs` |

### List messages of a deleted conversation
`get api/v3/anytime/deletedConversations/{id}/messages` 
- Parameters 
    - id: integer, conversation id
- Response 
    - [message](#message) 
- Includes

    | Includes | Description |
    | - | - |
    | sender | `get api/v3/anytime/deletedConversations/{id}/messages?include=sender` |


### Restore a deleted conversation 
`post api/v3/anytime/deletedConversations/{id}/restore ` 
- Parameters 
    - id: integer, conversation id 
- Response 
    - [conversation](#conversation)  

### Delete a conversation permanently 
`delete api/v3/anytime/deletedConversations/{id}` 
- Parameters 
    - id: integer, conversation id 
- Response 
    - http status code 

### Get a conversation draft 
`get api/v3/anytime/conversations/{id}/draft` 
- Parameters 
    - id: integer, conversation id 
- Response 
    - [conversation draft](#conversation-draft) 

### Create a conversation draft 
`post api/v3/anytime/conversations/{id}/draft` 
- Parameters 
    - [conversation draft](#conversation-draft) 
- Response 
    - [conversation draft](#conversation-draft) 

### Update a conversation draft 
`put api/v3/anytime/conversations/{id}/draft` 
- Parameters 
    - [conversation draft](#conversation-draft) 
- Response 
    - [conversation draft](#conversation-draft) 

### Delete a conversation draft 
`delete api/v3/anytime/conversations/{id}/draft` 
- Parameters 
    - id: integer, conversation id 
- Response 
    - http status code 

### Merge a conversation 
`post api/v3/anytime/conversations/{id}/merge`
- Parameters 
    - id: integer, target conversation id, 
    - sourceId: integer, source conversation id 
- Response 
    - [conversation](#conversation) 

### List unread conversations number for views 
`get api/v3/anytime/conversations/unreadCount?viewIds={viewid1}&viewIds={viewid2}&viewIds={viewid3}`
- Parameters 
    - viewIds: view id array 
- Response 
    - allCount: integer, all unread conversation number. 
    - array including: 
        - viewId: string, view id 
        - unreadCount: integer, count unread conversations of a view 
        - unreadMentionedCount: integer, the number of conversations which is unread and mentioned to me 

# PortalConversations
## objects
### portal conversation
| Name | Type | Description |
| - | - | - |
| `id` | integer | id of conversation |
| `subject` | string | subject |
| `contactId` | string | id of the contact who submitted the portal conversation |
| `isClosed` | boolean | if the portal conversation is closed |
| `isReadByContact` | boolean | if the portal conversation is read by contact |
| `customFields` | [custom field value](#custom-field-value)[] | custom field value array |
| `createdTime` | datetime | create time |
| `closedTime` | datetime | close time |

### portal conversation message 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of message | 
| `contents` | [content](#content)[] | content array |
| `senderId`| string | id of agent or contact | 
| `senderType`| string | `agent` or `contact` or `system` | 
| `time` | datetime | |   

## endpoints

## endpoints 

|EndPoint|Note| 
|---|---|
| `get api/v3/anytime/portalConversations/{id}`  | [Get a portal conversation by id](#Get-a-portal-conversation-by-id)  |
| `get api/v3/anytime/portalConversations` | [List portal conversations](#List-portal-conversations) |
| `post api/v3/anytime/portalConversations` | [Submit a portal conversation](#Submit-a-portal-conversation) |
| `put api/v3/anytime/portalConversations/{id}/close` | [Close a portalConversation](#Close-a-portalConversation) |
| `put api/v3/anytime/portalConversations/{id}/reopen`  | [Reopen a portalConversation](#Reopen-a-portalConversation) |
| `get api/v3/anytime/portalConversations/{id}/messages` | [List messages of a portal conversation ](#List-messages-of-a-portal-conversation) |
| `post api/v3/anytime/portalConversations/{id}/messages` | [Reply a portal conversation](#Reply-a-portal-conversation) |
| `put api/v3/anytime/portalConversations/{id}/read` | [Contact mark a portal conversation as read](#Contact-mark-a-portal-conversation-as-read) |
| `put api/v3/anytime/portalConversations/{id}/unread` | [Contact mark a portal conversation as unread](#Contact-mark-a-portal-conversation-as-unread) |

### Get a portal conversation by id
`get api/v3/anytime/portalConversations/{id}`
- Parameters
    - id, integer, portal conversation id
    - contactId, string
- Response
    - [portal conversation](#portal-conversation) 
- Includes

    |Includes| Description |
    | - | - |
    | contact | `get api/v3/anytime/portalConversations/{id}?include=contact` | 
    | messages | `get api/v3/anytime/portalConversations/{id}?include=messages` |
 
### List portal conversations
`get api/v3/anytime/portalConversations`
- Parameters:
    - contactIds, string array, required
- Response: 
    - [portal conversation](#portal-conversation) list
- Includes

    |Includes| Description |
    | - | - |
    | contact | `get api/v3/anytime/portalConversations?include=contact` |  
- Sample
    - `get api/v3/anytime/portalConversations?contactIds=1&contactIds=2&contactIds=3`

### Submit a portal conversation
`post api/v3/anytime/portalConversations`
- Parameters: 
    - subject: string, subject, required
    - contactId: string, id of the contact who submitted the portal conversation
    - customFields: [custom field value](#custom-field-value)[], custom field value array
    - message:  the first portal message
        contents: [content](#content)[]
- Response: 
  - [portal conversation](#portal-conversation) 

### Close a portalConversation
`put api/v3/anytime/portalConversations/{id}/close` 
- Parameters: 
    - id, integer, portal conversation id,
    - contactId, string, required
- Response: 
    - [portal conversation](#portal-conversation) 

### Reopen a portalConversation
`put api/v3/anytime/portalConversations/{id}/reopen` 
- Parameters: 
    - id, integer, portal conversation id,
    - contactId, string, required
- Response: 
    - [portal conversation](#portal-conversation) 

### List messages of a portal conversation 
`get api/v3/anytime/portalConversations/{id}/messages`
- Parameters: 
    - id, integer, conversation id
    - contactId, string, contact id
- Response: 
    - [portal conversation message](#portal-conversation-message) list
- Includes

    |Includes| Description |
    | - | - |
    | sender| `get api/v3/anytime/portalConversations/{id}/messages?include=sender` | 

### Reply a portal conversation
 `post api/v3/anytime/portalConversations/{id}/messages`
- Parameters:
    - id: integer
    - contactId: string required
    - contents: [content](#content)[], 
    - attachments: [attachment](#attachment)[], attachment array
- Response: 
    - [portal conversation message](#portal-conversation-message)

### Contact mark a portal conversation as read
`put api/v3/anytime/portalConversations/{id}/read`
- Parameters 
    - id: integer, conversation id 
- Response 
    - http status code

### Contact mark a portal conversation as unread
`put api/v3/anytime/portalConversations/{id}/unread`
- Parameters 
    - id: integer, conversation id 
- Response 
    - http status code

### event log
| Name | Type | Description | 
| - | - | - | 
| `id` | string | event log id | 
| `conversationId` | integer | id of conversation | 
| `text` | string | event log text | 
| `time` | datetime | event time | 

### List conversation event logs
`get api/v3/anytime/conversations/{id}/eventLogs`
- Parameters 
    - id: integer, conversation id 
- Response 
    - [event log](#event-log)

# Attachments  
## objects
### attachment 
| Name | Type | Description | 
| - | - | - |
| `id` | string | attachment unique id |  
| `fileName` | string | attachment file name| 
| `url` | string | attachment download link |   
| `isAvailable` | boolean | if the attachment is available | 

## endpoints 
### Upload attachment 
`post /api/v3/anytime/attachments` 
- Content-type
    - multipart/form-data
- Parameters 
    - file: file
- Response 
    - [attachment](#attachment) 
    
### Update status of attachment
`Put /api/v3/anytime/attachments/{guid}`
#### Parameters:
- isAvailable - boolean `true` or  `false`
#### Response
- [attachment](#attachment) 

### Delete attachment 
`delete /api/v3/anytime/attachments/{guid}` 
- Parameters 
    - guid: string, the guid of the attachment
- Response 
    - httpStatusCode


# Views 
## objects 
### view 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | view id | 
| `name` | string | view name | 
| `isPrivate` | boolean | if private view| 
| `createdById` | string | agent id | 
| `conditions` | [conditions](#conditions) | view conditions | 

### Conditions 
  | Name | Type |Description |
  | - | - | - | 
  | `when` | string | when the rule is triggered, including `all`, `any` and `logicalExpression` |
  | `logicExpression` | string | the logical expression of the conditions |
  | `list` | [condition](#condition)[] | an array of condition |

### condition
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the condition |
| `type` | string | `view`, `trigger`, `sla`, `routingRule` |
| `fieldId` | string | field id | 
| `matchType` | string | `contains`, `notContains`, `is`, `isNot`, `isMoreThan`, `isLessThan`, `before`, `after` | 
| `value` | string | condition value | 
| `orderNum` | integer | order number | 

## endpoints 
### List views 
`get /api/v3/anytime/views`
- Parameters 
    - no parameters 
- Response 
    - [view](#view) list, without conditions

### Create a new view 
`post api/v3/anytime/views`
- Parameters 
    - name: string, view name, required 
    - isPrivate: boolean, if private view, default value: `false` 
    - conditions: [conditions](#conditions), view conditions
- Response 
    - [view](#view) list 

### Get a view and its conditions 
`get api/v3/anytime/views/{id}` 
- Parameters 
    - id: string, view id 
- Response 
    - [view](#view) 

### Update a view 
`put api/v3/anytime/views/{id}` 
- Parameters 
    - id: string, view id 
    - name: string, view name, required 
    - isPrivate: boolean, if private view 
    - conditions: [conditions](#conditions), view conditions
- Response 
    - [view](#view) 

### Delete a view 
`delete api/v3/anytime/views/{id}` 
- Parameters 
    - id: string, view id 
- Response 
    - http status code 


# Routing
## objects
### routing
| Name | Type | Description |
| - | - | - |
| `isEnabled` | boolean | whether the routing is enabled or not.
| `type` |string | the type of routing, including `simple`and `customRules`. |
| `simpleRouteType` | string | the rule of route ,including `department` and `agent` |
| `simpleRouteToId` | string | id of the route object |
| `simpleRouteWithPriority` | string | `urgent`, `high`, `normal`, `low` |
| `customRules` | [customRule](#customRule)[] | an array of [customRule](#customRule) json object. |
| `matchFailedType` | string | the rule of failed route  including `department` and `agent` |
| `matchFailedrouteToId` | string | id of the routeobject |
| `matchFailedWithPriority` | string | `urgent`, `high`, `normal`, `low` |

### customRule
| Name | Type | Description |
| - | - | - |
| `id` | string | id of the custom rule |
| `routingId` | string | id of the routingId |
| `orderNum` | integer | order of the custom rule |
| `isEnabled` | boolean | whether the custom rule is enabled or not. |
| `name` | string | name of the custom rule |
| `conditions` | [conditions](#conditions)  | an trigger condition json object. |
| `routeType` | string | type of the route, including `agent` and `department`, value `department` is available when config of department is open. 
| `routeToId` | string |id of the route object |
| `routeWithPriority` | string | conversation priority enum number|


## endpoints
### get routing
`get api/v3/anytime/routing`
+ Parameters
    - no parameters
+ Response
    - [routingRule](#routingRule)

### Enable/Disable routing
`put api/v3/anytime/routing/enable`
+ Parameters
    - isEnabled: boolean,
+ Response
    - http status code

### Update routing
`put api/v3/anytime/routing/{id}`
+ Parameters
    - id: string
    - isEnabled: boolean
    - type: string, `simple` or `customRules`
    - simpleRouteType: string, department and agent
    - simpleRouteToId: string
    - simpleRouteWithPriority: string,
    - matchFailedType: string, department and agent
    - matchFailedToId: string
    - matchFailedWithPriority: string
    - orderNum: int, rules execute and display order
+ Response
    - [routing](#routing)

### Enable/Disable a custom rule
`put api/v3/anytime/routing/customRules/{id}/enable`
+ Parameters
    - id: string
    - isEnabled: boolean
+ Response
    - [customRule](#customRule) 

### Create a custom rule
`post api/v3/anytime/routing/customRules`
+ Parameters
    - customRule: [customRule](#customRule)
+ Response
    - [customRule](#customRule)

### Get a custom rule
`get api/v3/anytime/routing/customRules/{id}`
+ Parameters
    - id: string
+ Response
    - [customRule](#customRule)

### Update a custom rule
`put api/v3/anytime/routing/customRules/{id}`
+ Parameters
    - customRule: [customRule](#customRule)
+ Response
    - [customRule](#customRule)


### Delete a custom rule
`put api/v3/anytime/routing/customRules/{id}`
+ Parameters
    - id: string
+ Response
    - http status code

### update the order number of a custom rule
`put api/v3/anytime/routing/customRules/{id}/sort`
+ Parameters
    - id: string
    - type: string, `up`, `down`
+ Response
    - http status code

# AutoAllocations
## objects
### autoAllocationSetting
| Name | Type | Description | 
| - | - | - | 
| `isEnabled` | boolean | if enabled Auto Allocation |
| `departmentAllocationRule`| [allocationRule](#allocationRule)[] | array of department allocation rules |
| `defaultRule`| string | `loadBalancing`, `roundRobin` |
| `defaultPreferLastAssignee`| boolean | prefer to allocate to the last assignee |
| `ifEnableConversationLimitForEachAgent` | boolean | if set maximum number of conversations an agent can be allocated to |
| `conversationLimitForAllAgents` | integer | maximum number of conversations all agents can be allocated to |
| `agentPreferences` | [agentPreference](#agentPreference)[] | agent preference for allocation |
| `excludePendingExternal` | boolean | if exclude `Pending External` status while validating if an agent has reached the max number |
| `excludeOnHold` | boolean | if exclude `On Hold` status while validating if an agent has reached the max number |

### allocationRule
| Name | Type | Description | 
| - | - | - | 
| `departmentId` | string | department id |
| `departmentName` | string | department name |
| `allocationRule`| string | `loadBalancing`, `roundRobin` |
| `preferLastAssignee` | boolean | prefer to allocate to the last assignee |

### agentPreference
| Name | Type | Description | 
| - | - | - | 
| `agentId` | string | agent id |
| `maxConcurrentCount` | integer | the maximum number of the conversations a agent can accept at the same time |
| `isAcceptAllocation` | boolean | if the agent accept conversations |

## endpoints
### Get auto allocation settings
`get api/v3/anytime/autoAllocation`
+ Parameters
    - no parameters
+ Response
    - [autoAllocationSetting](#autoAllocationSetting)

### Enable/Disable auto allocation
`put api/v3/anytime/autoAllocation/enable`
+ Parameters
    - isEnabled: boolean, if enabled auto allocation
+ Response
    - http status code

### Update auto allocation settings
`put api/v3/anytime/autoAllocation`
+ Parameters
    - isEnabled: boolean, if enabled auto allocation
    - allocationRuleSettings: [allocationRuleSetting](#allocationRuleSetting)[]
    - ifEnableConversationLimitForEachAgent: boolean, if set maximum number of conversations an agent can be allocated to
    - conversationLimitForAllAgents: integer, maximum number of conversations all agents can be allocated to
    - allocationAgentPreferences: [allocationAgentPreference](#allocationAgentPreference)[]
    - ifExcludePendingExternal: boolean, if exclude `Pending External` status while validating if an agent has reached the max number
    - ifExcludeOnHold: boolean, if exclude `On Hold` status while validating if an agent has reached the max number
+ Response
    - [autoAllocationSetting](#autoAllocationSetting)

# Triggers
## object
### trigger
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the trigger |
| `description` | string | description of the trigger |
| `isEnabled` | boolean | if enabled the trigger |
| `event` | string |  `conversationCreated`, `conversationReplyReceived`, `agentReplied`, `conversationAssigneeChanged`, `conversationStatusChanged`, ` conversationStatusLastForCertainTime` |
| `conditions` | [conditions](#conditions) | trigger conditions | 
| `ifSetValue` | boolean | if set value |
| `autoUpdate` | [autoUpdate](#autoUpdate)[] | auto update field value |
| `ifSendEmail` | boolean | if send email |
| `ifSendToContacts` | boolean | if send email to contacts|
| `ifSendToAgents` | boolean | if send email to agents |
| `recipientAgentIds` | string[] | agent id array of recipient |
| `subject` | string | subject of the email content |
| `htmlText` | string | html body |
| `plainText` | string | plain text |
| `attachments` | [attachment](#attachment)[] | attachments |
| `ifShowInConversationCorrespondences` | boolean | if show trigger email in Conversation Correspondence |
| `orderNum` | integer | trigger execute and display order |

### autoUpdate
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of the autoUpdate |
| `triggerId` | string | trigger id |
| `fieldId` | string | field id | 
| `value` | string | condition value | 

## endpoints
### List all triggers
`get api/v3/anytime/triggers`
+ Parameters 
    - no parameters
+ Response
    - [trigger](#trigger) list

### Get a trigger
`get api/v3/anytime/triggers/{id}`
+ Parameters
    - id: string, trigger id
+ Response
    - [trigger](#trigger)

### Submit a trigger
`post api/v3/anytime/triggers`
+ Parameters
    - description, string, description of the trigger
    - isEnabled, boolean, if enabled the trigger
    - event, string, `conversationCreated`, `conversationReplyReceived`, `agentReplied`, `conversationAssigneeChanged`, `conversationStatusChanged`, ` conversationStatusLastForCertainTime`
    - conditions, [conditions](#conditions), conditions 
    - ifSetValue, boolean, if set value
    - autoUpdate, [autoUpdate](#autoUpdate)[], auto update field value
    - ifSendEmail, boolean, if send email
    - ifSendToContacts, boolean, if send email to contacts
    - ifSendToAgents, boolean, if send email to agents
    - recipientAgentIds, string[], agent id array of recipient
    - subject, string, subject of the email content
    - htmlText, string, html body
    - plainText, string, plain text
    - attachments, [attachment](#attachment)[], attachment array
    - ifShowInConversationCorrespondences, boolean, if show trigger email in Conversation Correspondence
+ Response
    - [trigger](#trigger)

 ### Update a trigger
`put api/v3/anytime/triggers/{id}`
+ Parameters
    - id, string, id of the trigger
    - description, string, description of the trigger
    - isEnabled, boolean, if enabled the trigger
    - event, string,  `conversationCreated`, `conversationReplyReceived`, `agentReplied`, `conversationAssigneeChanged`, `conversationStatusChanged`, ` conversationStatusLastForCertainTime` 
    - conditions, [conditions](#conditions), conditions 
    - ifSetValue, boolean, if set value
    - autoUpdate, [autoUpdate](#autoUpdate)[], auto update field value
    - ifSendEmail, boolean, if send email
    - ifSendToContacts, boolean, if send email to contacts
    - ifSendToAgents, boolean, if send email to agents
    - recipientAgentIds, string[], agent id array of recipient
    - subject, string, subject of the email content
    - htmlText, string, html body
    - plainText, string, plain text
    - attachments, [attachment](#attachment)[], attachment array
    - ifShowInConversationCorrespondences, boolean, if show trigger email in Conversation Correspondence
+ Response
    - [trigger](#trigger)

### Upgrade/Downgrade a triggers
`put api/v3/anytime/triggers/{id}/sort`
+ Parameters
    - id: string, trigger id
    - type: string, `up`, `down`
+ Response
    - http status code

### Enable/Disable a triggers
`put api/v3/anytime/triggers/{id}`
+ Parameters
    - id: string, trigger id
    - isEnabled: boolean, if enabled the trigger
+ Response
    - http status code

 ### Delete a trigger
`delete api/v3/anytime/triggers/{id}`
+ Parameters
    - id: string, trigger id
+ Response
    - http status code

# SLAPolicies
## objects
### SLAPolicy
| Name | Type | Description | 
| - | - | - | 
| `id` | string | SLA policy id |
| `isEnabled` | boolean | if enabled this SLA policy |
| `firstRespondWithin` | integer | the hours first reply within |
| `nextRespondWithin` | integer | the hours next reply within |
| `resolveRespondWithin` | integer | the hours a conversation should be resolved within |
| `isBusinessHours`| boolean | if `businessHours` or `calenderHours` |
| `conditions` | [conditions](#conditions) | conditions | 
| `orderNum` | integer | SLA execute and display order |

## endpoints
### List all SLA policies
`get api/v3/anytime/SLAPolicies`
+ Parameters
    - no parameters
+ Response
    - [SLAPolicy](#SLApolicy) list

### Get a SLA policy
`get api/v3/anytime/SLAPolicies/{id}`
+ Parameters
    - id: string, SLA policy id
+ Response
    - [SLAPolicy](#SLApolicy)

### Create a SLA policy
`post api/v3/anytime/SLAPolicies`
+ Parameters
    - isEnabled: boolean, if enabled this SLA policy 
    - firstRespondWithin: integer, 
    - nextRespondWithin: integer, 
    - resolveRespondWithin: integer, 
    - isBusinessHours: boolean, `businessHours` or `calenderHours` 
    - conditions: [conditions](#conditions)
+ Response
    - [SLAPolicy](#SLApolicy)

### Update a SLA policy
`put api/v3/anytime/SLAPolicies/{id}`
+ Parameters
    - id: string, SLA policy id 
    - isEnabled: boolean, if enabled this SLA policy 
    - firstRespondWithin: integer,  
    - nextRespondWithin: integer, 
    - resolveRespondWithin: integer,  
    - businessHours: string, `businessHours` or `calenderHours` 
    - conditions: [conditions](#conditions)
+ Response
    - [SLAPolicy](#SLApolicy)

### Delete a SLA policy
`delete api/v3/anytime/SLAPolicies/{id}`
+ Parameters
    - id: string, SLA policy id
+ Response
    - http status code

### Upgrade/Downgrade a SLA policy
`put api/v3/anytime/triggers/{id}/sort`
+ Parameters
    - id: string, SLA policy id
    - type: string, `up`, `down`
+ Response
    - http status code

# WorkingTime&Holiday
## objects
### workingTime
| Name | Type | Description | 
| - | - | - | 
| `dayOfWeek` | string | day of week |
| `isBusinessDay` | boolean |  |
| `startHour` | integer | business start hour |
| `startMin` | integer | business start min |
| `endHour` | integer | business close hour |
| `endMin` | integer | business close min |

### holiday
| Name | Type | Description |
| - | - | - | 
| `id` | string | the id of the holiday |
| `title` | string | the title of the holiday  |
| `date` | datetime | the date of the holiday |

## endpoints
### Get working time setting
`get api/v3/anytime/workingTime`
+ Parameters
    - no parameters
+ Response
    - [workingTime](#workingTime) list

### Update working time settings
`put api/v3/anytime/workingTime`
+ Parameters
    - workingTimes: [workingTime](#workingTime)[]
+ Response
    - http status code

### List all holidays
`get api/v3/anytime/holidays`
+ Parameters
    - no parameters
+ Response
    - [holiday](#holiday) list

### Get a holiday
`get api/v3/anytime/holidays/{id}`
+ Parameters
    - id: string
+ Response
    - [holiday](#holiday)

### Create a holiday
`post api/v3/anytime/holidays`
+ Parameters
    - id: string
    - title: string, title of the holiday
    - date: datetime, date of the holiday
+ Response
    - [holiday](#holiday)

### Update a holiday
`put api/v3/anytime/holidays/{id}`
+ Parameters
    - id: string
    - title: string, title of the holiday
    - date: datetime, date of the holiday
+ Response
    - [holiday](#holiday)

### Delete a holiday
`delete api/v3/anytime/holidays`
+ Parameters
    - id: string
+ Response
    - http status code

# Fields&Mapping 
## objects 
### field 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | field id | 
| `type` | string | `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`, `operator`, `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department` |
| `name` | string | field name | 
| `isSystemField` | boolean | if is system field | 
| `isRequired` | boolean | value if is required | 
| `defaultValue` | string | field default value | 
| `helpText` | string | field help text | 
| `length` | integer | field value max length | 
| `options` | [field option](#fieldoption)[] | value option | 
| `chatFieldMapping` | string | chat field id |
| `offlineMessageFieldMapping` | string | offline message field id |

### fieldOption 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | option id | 
| `name` | string | option name | 
| `value` | string | field value | 
| `orderNum` | integer | option order | 

### fieldMapping
| Name | Type | Description | 
| - | - | - | 
| `fieldId` | string | field id | 
| `chatFieldMapping` | string | chat field id |
| `offlineMessageFieldMapping` | string | offline message field id |

## endpoints 
### List fields and their options 
`get api/v3/anytime/fields` 
+ Parameters
    - isSystemField: boolean, if is system field, optional
+ Response 
    - [field](#field) list 

### Get a field
`get api/v3/anytime/fields/{id}`
+ Parameters
    - id: string, field id
+ Response
    - [field](#field) 

### Create a field
`post api/v3/anytime/fields`
+ Parameters
    - type, string, `text`, `textarea`, `email`, `url`, `date`, `integer`, `float`,     `operator`,     `radio`, `checkbox`, `dropdownList`, `checkboxList`, `link`, `department`
    - name, string, field name 
    - isRequired, boolean, value if is required 
    - defaultValue, string, field default value 
    - helpText, string, field help text 
    - length, integer, field value max length 
    - options, [field option](#fieldoption)[], value option 
+ Response
    - [field](#field) 

### Update a field
`put api/v3/anytime/fields/{id}`
+ Parameters
    - id, string, field id 
    - name, string, field name 
    - isRequired, boolean, value if is required 
    - defaultValue, string, field default value 
    - helpText, string, field help text 
    - length, integer, field value max length 
    - options, [field option](#fieldoption)[], value option 
+ Response
    - [field](#field) 

### Delete a field
`delete api/v3/anytime/fields/{id}`
+ Parameters
    - id, string, field id 
+ Response
    - http status code

### Mapping fields
`put api/v3/anytime/fields/mapping`
+ Parameters
    - fieldMappings: [fieldMapping](#fieldMapping) list
+ Response
    - http status code


# BlockedSenders 
## objects 
### blocked sender 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | the id of blocked sender |
| `value` | string | email or domain | 
| `blockType` | string | `blockEmailasJunk`, `rejectEmail`, `blockDomainasJunk`, `rejectDomain` | 

## endpoints 
### List blocked senders 
`get /api/v3/anytime/blockedSenders` 
+ Parameters 
    - value: string, domain or email address 
+ Response 
    - [block sender](#blocked-sender) list 

### Get a blocked sender
`get /api/v3/anytime/blockedSenders/{id}`
+ Parameters
    - id: string
+ Response
    - [block sender](#blocked-sender) 

### Add/update a blocked sender 
`put api/v3/anytime/blockedSenders` 
+ Parameters 
    - `value`, string, domain or email address 
    - `blockType`, string, `blockEmailasJunk`, `rejectEmail`, `blockDomainasJunk`, `rejectDomain`
+ Response 
    - [block sender](#blocked-sender) 

### Remove a blocked sender 
`delete api/v3/anytime/blockedSenders` 
+ Parameters 
   - value: string, domain or email address 
+ Response 
    - http status code

# Junks 
## objects 
### junk 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id of junk | 
| `channelAccount`| string | channel account id | 
| `contactIdentityId`| string | id of contact identity |
| `source` | string | `agentConsole`, `helpDesk`, `webForm`, `API`, `chat`, `offlineMessage`, etc. | 
| `originalMessageId` | string | original message id|
| `originalMessageUrl` | string | origial message link |
| `parentId` | string | parent id |
| `contents` | [content](#content)[] | contents |   
| `subject` | string | subject | 
| `cc` | string | cc email addresses |  
| `isRead`| boolean | | 
| `senderId`| string | id of agent or contact | 
| `senderType`| string | `agent` or `contact` or `system` | 
| `time` | datetime | the sent time of the junk message | 

## endpoints 
### List junk emails
`get api/v3/anytime/junks` 

- Parameters 
    - keywords: string
    - pageIndex: integer
    - timeFrom: DateTime
    - timeTo: DateTime
- Response 
    - junks: [junk](#junk) list 
    - total: integer
    - previousPage: string, next page uri, the first page return null
    - nextPage: string, the last page return null
    - currentPage: string

### Get a junk email 
`get api/v3/anytime/junks/{id}` 
- Parameters 
    - id: string, email id 
- Response 
    - [junk](#junk) 

### Update a junk 
`put api/v3/anytime/junks/{id}` 
- Parameters 
    - id: string, email id 
    - isRead: boolean, 
- Response 
    - [junk](#junk) 

### Restore a junk email to a normal conversation 
`post api/v3/anytime/junks/{id}/notJunk` 
- Parameters 
    - id: integer, email id 
- Response 
    - [conversation](#conversation) 

### Delete a junk email 
`delete api/v3/anytime/junks/{id}` 
- Parameters 
    - id: integer, junk email id 
- Response 
    - http status code 

# Channel Accounts 

## objects 

### channelAccount 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id | 
| `name` | string | account name |   
| `channelId` | string | channel id |   

## endpoints 
### List channel accounts 
`get api/v3/anytime/channelAccounts` 
- Parameters
    - channelId: string, optional
- Response 
    - [channelAccount](#channelAccount)[] 

### Add an channel account 
`post api/v3/anytime/channelAccounts` 
- Parameters
    - channelAccount: [channelAccount](#channelAccount) 
- Response 
    - [channelAccount](#channelAccount)

### Update an channel account 
`put api/v3/anytime/channelAccounts/{id}` 
- Parameters
    - name: string 
- Response 
    - [channelAccount](#channelAccount)

### Delete an channel account 
`delete api/v3/anytime/channelAccounts/{id}` 
- Parameters
    - id: string,
- Response 
    - http status code


# Channels 
## objects 
### channel 
| Name | Type | Description | 
| - | - | - | 
| `id` | string | id | 
| `name` | string | channel name | 
| `contactIdentityType` | string | contact identity type |
| `icon` | string | icon url |     
| `messageDisplayType` | string | `treeView`, `flatView`, `emailView` |
| `messageMaxLength` | int | outgoing message max length |
| `messageCapability` | string[] | outgoing message support message type |
| `isSupportReplyWithDiffAccount` | bool | If support reply with different channel account |  
| `isSupportDirectlyReply` | bool | If support directyly reply to a contact |  

## endpoints 
### List all integrated channels 
`get api/v3/anytime/channels` 
- Parameters
    - no parameter
- Response 
    - [channel](#channel)[] 


***

# Reports

## EndPoint List 
| endpoint | type | note |
| --- | --- | --- |
| [/api/v3/anytime/reports/realtime/now](#right-now) | GET | real-time report of now |
| [/api/v3/anytime/reports/realtime/today](#realtime-today) | GET | real-time report of today |
| [/api/v3/anytime/reports/realtime/departments](#realtime-department) | GET | real-time report of departments |
| [/api/v3/anytime/reports/realtime/agents](#realtime-agent) | GET | real-time report of agents |
| [/api/v3/anytime/reports/volume/export](#export-volume) | GET | export volume report data |
| [/api/v3/anytime/reports/volume](#report-volume) | GET | report of volume |
| [/api/v3/anytime/reports/channel/export](#export-channel) | GET | export channel report data |
| [/api/v3/anytime/reports/channel](#report-channel) | GET | channel report |
| [/api/v3/anytime/reports/efficiency/export](#export-efficiency) | GET | export efficiency report data|
| [/api/v3/anytime/reports/efficiency](#report-efficiency) | GET | efficiency report |
| [/api/v3/anytime/reports/sla/export](#export-SLA-report) | GET | export SLA report data |
| [/api/v3/anytime/reports/sla](#report-sla) | GET | SLA report data |

## EndPoints

### right now
`GET /api/v3/anytime/reports/realtime/now`
- Parameters：
	- no parameter
- Response:
 	- unassignedConversations: integer
	- openConversations: integer
	- newConversations: integer
	- pendingInternalConversations: integer
	- pendingExternalConversations: integer
	- onHoldConversations: integer
	- urgentPriorityConversations: integer
	- highPriorityConversations: integer

### realtime of lastest sereral days
- `GET /api/v3/anytime/reports/realtime/bytime`
- Parameters:
    - days: int, days number, maximum number 15. 
- Response:
 	- createdConversations: integer
	- resolvedConversations: integer
	- repliedConversations: integer
	- reopenedConverstations: integer

### realtime department
`GET /api/v3/anytime/reports/realtime/departments`
- Parameters：
    - no parameter
- Response:
	- dataList:
		- departmentId: integer,
		- openConversations: integer,
		- todayRepliedConversations: integer,
		- todayResolvedConversations: integer,
		- newConversations: integer,
		- pendingInternalConversations: integer,
		- pendingExternalConversations: integer,
		- onHoldConversations: integer,
		- urgentPriorityConversations: integer,
		- highPriorityConversations: integer,

### realtime agent
`GET/api/v3/anytime/reports/realtime/agents`
- Parameters：
	- viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
- Response:
	- dataList: 
		- agentId: integer,
		- openConversations: integer,
		- todayRepliedConversations: integer,
		- todayResolvedConversations: integer,
		- newConversations: integer,
		- pendingInternalConversations: integer,
		- pendingExternalConversations: integer,
		- onHoldConversations: integer,
		- urgentPriorityConversations: integer,
		- highPriorityConversations: integer,
	
### export volume
`GET /api/v3/anytime/reports/volume/export`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
    - timeUnit: string,
    - dimensionType: string,
    - timeOffset： integer,
    - dateFormat: string,
- Response:csv file


### report volume
`GET /api/v3/anytime/reports/volume`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
    - timeUnit: string,
    - dimensionType: string,
- Response:
	- dataList:
	    - id: integer,
    	- createdConversations: integer,
    	- createdConversationsPercentage:  float,	
    	- closedConversations: integer,
    	- closedConversationsPercentage: float,
    	- repliedConversations: integer,
    	- repliedConversationsPercentage: float,
    	- reopenedConversations: integer,
    	- reopenedConversationsPercentage: float,
    	- openConversations: integer,
    	- openConversationsPercentage: float,
    	- startTime: string,
    	- endTime: string,
	- totalCreatedConversations: integer,
	- totalClosedConversations: integer,
	- totalRepliedConversations: integer,
	- totalReopenedConversations: integer,
	- totalOpenConversations: integer

### export channel
`GET /api/v3/anytime/reports/channel/export`
- Parameters：
	- siteId: integer,
    - startTime: Datetime,
    - endTime: Datetime,
    - viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
    - timeUnit: string,
    - dimensionType: string,
    - timeOffset：integer,
    - dateFormat: string,
- Response:csv file

### report-channel
`GET /api/v3/anytime/reports/channel`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
    - timeUnit: string,
    - dimensionType: string,
- Response:
	- dataList: 
	    - id: integer,
		- name: string,
		- channelEfficiencies: [channelEfficiencies](#channel-efficiency)[]
		- startTime: string,
		- endTime: string,
	- channel total number: [channel total number](#channel-total-messages-number)[]

### channel efficiency
| Name | Type | Description | 
| - | - | - | 
| `channelId` | string | channel id |
| `channelName` | string | channel name |
| `channelMessageNumber` | integer | channel message number |
| `channelPercentage` | float | channel percentage |

### channel total messages number
| Name | Type | Description | 
| - | - | - | 
| `channelId` | string | channel id |
| `channelName` | string | channel name |
| `totalNumber` | integer |  |

### export efficiency
`GET /api/v3/anytime/reports/efficiency/export`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
    - timeUnit: string,
    - dimensionType: string,
    - timeOffset： integer,
    - dateFormat: string,
- Response:csv file

### report efficiency
`GET /api/v3/anytime/reports/efficiency`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - viewType: string, `site`, `agent`, `department`, `account`, `channel`
	- viewValue: integer,
    - timeUnit: string,
    - dimensionType: string, `byTime`, `byAgent`, `byDepartment`, `byChannel`
- Response:
	- dataList:
	    - id: integer,
		- avgAgentResponseTime: string,
		- avgFirstResponseTime: string,
		- avgConversationTime: string,
		- avgContactMessages: float,
		- avgAgentMessages: float, 
		- startTime: string,
		- endTime: string,
	- totalAvgAgentResponseTime: string,
	- totalAvgFirstResponseTime: string,
	- totalAvgConversationTime: string,
	- totalAvgContactMessages: float,
	- totalAvgAgentMessages: float

### export SLA report
`GET /api/v3/anytime/reports/sla/export`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - timeUnit: string, `day`,`week`, `month`
    - dimensionType: string, `slaPolicies`, `agent`, `department`
- Response:
	- dataList:
	    - id: integer,
		- firstRespondTimeAchievedPercentage: float,
		- avgFirstRespondTime: float,
		- nextRespondTimeAchievedPercentage: float,
		- avgNextRespondTime: float,
		- ResolveTimeAchievedPercentage: float, 
        - avgResolveTime: float,
        - breachedTickets: integer, 

### report SLA
`GET /api/v3/anytime/reports/sla`
- Parameters：
    - startTime: Datetime,
    - endTime: Datetime,
    - timeUnit: string, `day`,`week`, `month`
    - dimensionType: string, `slaPolicies`, `agent`, `department`
- Response:
	- dataList:
	   	    - id: integer,
		- firstRespondTimeAchievedPercentage: float,
		- avgFirstRespondTime: float,
		- nextRespondTimeAchievedPercentage: float,
		- avgNextRespondTime: float,
		- ResolveTimeAchievedPercentage: float, 
        - avgResolveTime: float,
        - breachedTickets: integer

* * *

