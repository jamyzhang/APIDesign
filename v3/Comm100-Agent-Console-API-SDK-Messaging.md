# General
## Basic Data Structure

  ```javascript
  //Conversation
  const conversation = {
    id: number,
    guid: string,
    relatedType: string, // enum: contact, visitor or agent
    relatedId: string, // the id of contact, visitor or agent
    contactOrVisitor: Object, // contact or visitor instance
    subject: string,
    assignedAgent: {
        id: string,
        name: string,
        email: string
    },
    assignedDepartment: {
        id: string,
        name: string,
    },
    originalId: string,
    priority: string, // urgent, high, normal or low
    status: string, // new, pendingInternal, pendingExternal, onHold or resolved
    hasDraft: boolean,
    isDeleted: boolean,
    isRead: boolean,
    isReadByContact: boolean,
    isEditable: boolean,
    isActive: boolean,
    isMultiChannel: boolean,
    tag: [{
        id: string,
        name: string,
    }], // tags
    mentionedAgents: [{
        agentId: string,
        isRead: boolean,
        messageId: string,
    }],
    customFields: [{
        id: string,
        name: string,
    }],
    createdById: string, // contact id, agent id or visitor id
    createdByType:  string, // agent, contact or system or visitor
    createdAt: string,
    lastUpdatedAt: string,
    lastStatusChangedAt: string,
    lastRepliedAt: string,
    lastRepliedById: number,
    lastRepliedByType: string, // agent, contact or system
    slaPolicyId: string,
    firstRespondBreachAt: string,
    nextRespondBreachAt: string,
    resolveBreachAt: string,
    nextSLABreachAt: string,
    lastMessage: Object // message instance
  }

  // Message
  const message = {
    id: string,
    conversationId: integer,
    channelId: string,
    type: string,
    directType: messageDirectType,
    channelAccountId: string,
    contactIdentityId: string,
    originalMessageId: string,
    originalMessageUrl: string,
    parentId: string,
    subject: string,
    cc: string,
    contents: [{
        id: string,
        type: string, // text, htmlText, video, audio, picture, file or location
        text: string,
        htmlText: string,
        name: string,
        url: string,
        title: string,
        latitude: string,
        longitude: string,
        scale: string,
        desc: string,
    }],
    mentionedAgentIds: string[],
    isRead: boolean,
    sendStatus: messageStatus,
    senderId: string,
    senderType: messageSenderType,
    time: string,
}

 // Attachment
  const attachment = { 
    guid: string,
    fileName: string,
    url: string,
    isAvailable: boolean,
  }

  // Department
  const department = {
      id: string,
      name: string,
  }
  
  // Agent
  const agent = {
    id: number,
    email: string,
    name: string,
    firstName: string,
    lastName: string,	 
    title: string,	 
    bio: string, 
    mobilePhone: string,
    isAdmin: boolean,
    timeZone: string,
    dateTimeFormat: string,
  }
```

# Objects
## Agent

  ```javascript
  /** @type {object(agent)} **/
    Comm100AgentConsoleAPI.get('agentconsole.currentAgent');
  ```

## conversation
### get the information of current conversation

```javascript
/** @type {object(conversation)} **/
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation');
```

### subject
   
```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.subject');
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.subject', value);
```
### contact

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.contact'); 
//Only the ID of the contact can be set
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.contact', value);
//Example
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.contact', { id: 1 });
```

### department assignee

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.departmentAssignee');
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.departmentAssignee', value);
//Example
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.departmentAssignee', { id: 1 });
```
### agent assignee

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.agentAssignee');
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.agentAssignee', value);
//Example
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.agentAssignee', {id: 1 });
```

### priority

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.priority');
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.priority', value);
```

### status

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.status');
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.status', value);
```
### tags

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.tags');
Comm100AgentConsoleAPI.do('agentconsole.messaging.currentConversation.tags.add', value);
Comm100AgentConsoleAPI.do('agentconsole.messaging.currentConversation.tags.remove', value);
//Example
Comm100AgentConsoleAPI.do('agentconsole.messaging.currentConversation.tags.add', {id: 1});
Comm100AgentConsoleAPI.do('agentconsole.messaging.currentConversation.tags.remove', {id: 1});
```

### custom fields

```javascript
Comm100AgentConsoleAPI.get('agentconsole.messaging.currentConversation.customFields:[field id]');
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.customFields:[field id]', value);
//sample
Comm100AgentConsoleAPI.set('agentconsole.messaging.currentConversation.customFields:123', 'test');
```

# Event
## Change Events
- this event is triggered when the current conversation property value has changed.

```javascript
    const propertyChangedEvent = {
        data:{
            oldData,
            newData
        }
    }

Comm100AgentConsoleAPI.on('agentconsole.currentConversation.subject.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.contact.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.departmentAssignee.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.agentAssignee.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.priority.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.status.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.tags.changed', function(event) {});
Comm100AgentConsoleAPI.on('agentconsole.currentConversation.customFields:[field id].changed', function(event) {});
```

# Action
- Append text to the input box of current conversation

```javascript
Comm100AgentConsoleAPI.do('agentconsole.messaging.currentConversation.reply.append', value)
Comm100AgentConsoleAPI.do('agentconsole.messaging.currentConversation.note.append', value)
```
  