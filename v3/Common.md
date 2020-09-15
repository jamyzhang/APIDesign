# Common

| Object | Path |
| - | - | 
|[Site](#site)| `/api/v3/site`|
|[Agent](#agents)| `/api/v3/agents`|
|[Contact](#contact)| `/api/v3/contacts`|
|[Role](#roles)| `/api/v3/roles`|
|[Agent Single Sign On](#agent-SSO-Settings)| `/api/v3/agentSignleSignOn`|
|[Audit Log](#audit-logs)| `/api/v3/auditLogs`|
|[Canned Message](#canned-Messages)| `/api/v3/cannedMessages`|
|[Canned Message Category](#canned-Message-Categories)| `/api/v3/cannedMessageCategories`|
|[Credit Card Masking](#credit-Card-Masking)| `/api/v3/creditCardMasking`|
|[Department](#departments)| `/api/v3/departments`|
|[Ip Restriction](#ip-restriction) | `/api/v3/ipRestriction` |
|[Password Policy](#password-Policy)| `/api/v3/passwordPolicy`|
|[Tag](#tag)| `/api/v3/tags`|
|[Webhook](#webhook)| `/api/v3/webhooks`|

<div>

## Site

  You need `Manage Site Profile` permission to manage site.
  
- `GET /api/v3/site/profile` -Get profile of a single site
- `PUT /api/v3/site/profile` -Update profile of a site

<div>

### Model

#### Site Profile Json Format

  Site profile is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  | `id` | integer | read-only, id of the site
  | `siteName` | string | required, name of the site
  | `firstName` | string | required, first name of the site
  | `lastName` | string | required, last name of the site
  | `mobileNumber` | string | optional, mobile number of the site
  | `company` | string | required, company the site belongs to
  | `website` | string | required, website of the site
  | `phoneNumber` | string | optional, phone number of the site
  | `title` | string | optional, title of the site
  | `faxNumber` | string | optional, fax number of the site
  | `mailAddress` | string | optional, mail address of the site
  | `city` | string | optional, city which the site is in
  | `stateOrProvince` | string | optional, state or province which the site is in
  | `postalOrZipCode` | string | optional, postal or zip code of the site
  | `country` | string | optional, country which the site's company belongs to
  | `companySize` | string | optional, number of staff in the site's company
  | `timeZone` | string | optional, time zone which the site's company belongs to
  | `datetimeFormat` | string | optional, date/time format which the site will display
  | `subdomain` | string | optional, subdomain of the site

</div>
<div>

### Endpoint

#### Get the profile of a single site

  `GET /api/v3/site/profile`

- Parameters

  No parameters

- Response

  [Site Profile](#Site-Profile-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"
     https://hosted.comm100.com/api/v3/site/profile
```

  Sample response:

```json
{
    "id": 6000000,
    "siteName": "comm100",
    "firstName": "test",
    "lastName": "comm100",
    "mobileNumber": "",
    "company": "comm100",
    "website": "www.comm100.com",
    "phoneNumber": "123456",
    "title": "",
    "faxNumber": "",
    "mailAddress": "",
    "city": "",
    "stateOrProvince": "",
    "postalOrZipCode": "",
    "country": "China",
    "companySize": "101-180",
    "timeZone": "71",
    "datetimeFormat": "MM/dd/yyyy HH:mm:ss",
    "subdomain": "mysubdomain.comm100.io"
}
```

#### Update the profile of a site  

  `PUT /api/v3/site/profile`

- Request Parameters

  [Site Profile](#Site-Profile-Json-Format)

- Response

  [Site Profile](#Site-Profile-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"sitename": 'sitename',"firstName": 'test',"lastName": 'comm100',"website": 'www.comm100.com',"company": 'comm100',"timezone": '71'}"    
     https://hosted.comm100.com/api/v3/site/profile
```

  Sample response:

```json
{
    "id": 6000000,
    "siteName": "sitename",
    "firstName": "test",
    "lastName": "comm100",
    "mobileNumber": "",
    "company": "comm100",
    "website": "www.comm100.com",
    "phoneNumber": "123456",
    "title": "",
    "faxNumber": "",
    "mailAddress": "",
    "city": "",
    "stateOrProvince": "",
    "postalOrZipCode": "",
    "country": "China",
    "companySize": "101-180",
    "timeZone": "71",
    "datetimeFormat": "MM/dd/yyyy HH:mm:ss",
    "subdomain": "mysubdomain.comm100.io"
}
```

</div>
</div>
<div>

## Agents

- You need `Manage Agent & Agent Roles` permission to manage agents.
  - `GET /api/v3/agents` - Get a list of agents
  - `GET /api/v3/agents/{id}` - Get a single agent
  - `POST /api/v3/agents` - Create a new agent
  - `PUT /api/v3/agents/{id}` - Update an agent  
  - `DELETE /api/v3/agents/{id}` - Remove an agent
  - `PUT /api/v3/agents/{id}/password` - Admin set an agent's password
  - `PUT /api/v3/agents/{id}/unlock` - unlock the agent
  - `GET /api/v3/agents/{id}/permissions` - Get list of an agent's permissions.
  - `PUT /api/v3/agents/{id}/permissions` - Update permissions for an agent.
  - `GET /api/v3/agents/{id}/effectivePermissions` -Get a list of agent's effective permissions, including the permissions of the agent and the permissions of the roles which the agent belongs to.

- You can manage your own profile
  - `GET /api/v3/agents/me` - Get current agent
  - `PUT /api/v3/agents/me` - Update own profile
  - `PUT /api/v3/agents/me/password` - Change own password

<div>

### Model

#### Agent Json Format

  Agent is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  | `id` | string | read-only, id of the agent.
  | `email` | string | required, email of the agent.
  | `displayName` | string | required, display name of the agent.
  | `firstName` | string | required, first name of the agent
  | `lastName` | string | required, last name of the agent
  | `title` | string | optional, title of the agent
  | `bio` | string | optional, bio of the agent
  | `mobilePhone` | string | optional, mobile phone number of the agent
  | `timeZone` | string | optional, time zone of the agent
  | `dateTimeFormat` | string | optional, date/time format selected by an agent to display on the site.
  | `roles` | array  | optional, the list of roles to which an agent belongs to.
  | `isAdmin` | boolean | optional, whether the agent is an administrator or not.
  | `isActive` | boolean | optional, whether the agent is active or not.
  | `isLocked` | boolean | optional, whether the agent is locked or not.
  | `availableChannels` | array | optional, the list of available channels of the agent.

</div>
<div>

### Endpoint

#### Get a list of agents

  `GET /api/v3/agents`

- Query Parameters

    Optional:
  - `pageIndex`: integer, the page index of a query.

- Response
  - `total`: integer, total count of the list.
  - `previousPage`: string, url of the previous page.
  - `nextPage`: string, url of the next page.
  - `agents`: [Agent](#Agent-Json-Format)[].

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/agents
```

  Sample response:

```json
{
    "total": 1,
    "previousPage": "",
    "nextPage": "",
    "agents": [
        {
            "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
            "email": "test@comm100.com",
            "displayName": "test comm100",
            "firstName": "test",
            "lastName": "comm100",
            "title": "",
            "bio": "",
            "mobilePhone": "",
            "timeZone": "-1",
            "dateTimeFormat": "MM/dd/yyyy HH:mm:ss",
            "roles": [],
            "isAdmin": true,
            "isActive": true,
            "isLocked": false,
            "availableChannels": []
        }
    ]
}
```

#### Get a single agent

  `GET /api/v3/agents/{id}`

- Path Parameters
  
  - id, string, id of the agent.

- Response
  
  [Agent](#Agent-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/agents/9F4709DB-C391-4896-94BA-3A17BE12D9E2
```

  Sample response:

```json
{
    "id": "9F4709DB-C391-4896-94BA-3A17BE12D9E2",
    "email": "test@comm100.com",
    "displayName": "test comm100",
    "firstName": "test",
    "lastName": "comm100",
    "title": "",
    "bio": "",
    "mobilePhone": "",
    "timeZone": "-1",
    "dateTimeFormat": "MM/dd/yyyy HH:mm:ss",
    "roles": [],
    "isAdmin": true,
    "isActive": true,
    "isLocked": false,
    "availableChannels": []
}
```

#### Create a new agent
  
  `POST /api/v3/agents`

- Request Parameters

  [Agent](#Agent-Json-Format)

- Response

  [Agent](#Agent-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x POST -H "Content-Type: application/json"  
     -d "{"email": 'test@test.com',"displayname": 'testname',"firstname": 'first', 
     "lastname": 'lastname',"title": 'title',"password": '123456',"timezone": '31',"mobilephone": '12345678911'}"
     https://hosted.comm100.com/api/v3/agents
```

  Sample response:

```json
{
    "id": "2B356016-2B44-49C0-B4E6-05902E55DAFD",
    "email": "test@test.com",
    "displayName": "testname",
    "firstName": "first",
    "lastName": "lastname",
    "title": "title",
    "bio": "",
    "mobilePhone": "12345678911",
    "timeZone": "31",
    "dateTimeFormat": "MM/dd/yyyy HH:mm:ss",
    "roles": [],
    "isAdmin": false,
    "isActive": true,
    "isLocked": false,
    "availableChannels": []
}
```

#### Update an agent

  `PUT /api/v3/agents/{id}`

- Path Parameters
  
  - id, string, id of the agent.

- Request Parameters

  [Agent](#Agent-Json-Format)

- Response
  
  [Agent](#Agent-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
      -x PUT -H "Content-Type: application/json"  
      -d "{"email": 'test1@test.com',"displayname": 'testname',"firstname": 'first',"lastname": 'lastname', 
     "title": 'title',"password": '123456',"timezone": '31',"mobilephone": '12345678911'}"
     https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD
```

  Sample response:

```json
{
    "id": "2B356016-2B44-49C0-B4E6-05902E55DAFD",
    "email": "test1@test.com",
    "displayName": "testname",
    "firstName": "first",
    "lastName": "lastname",
    "title": "title",
    "bio": "",
    "mobilePhone": "12345678911",
    "timeZone": "31",
    "dateTimeFormat": "MM/dd/yyyy HH:mm:ss",
    "roles": [ ],
    "isAdmin": true,
    "isActive": true,
    "isLocked": false,
    "availableChannels": []
}
```

#### Remove an agent

  `DELETE /api/v3/agents/{id}`

- Path Parameters
  
  - id, string, id of the agent.

- Response

  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x DELETE https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD
```

  Sample response:

```json
Status: 200 OK
```

#### Admin sets an agent's password

  `PUT /api/v3/agents/{id}/password`

- Path Parameters
  
  - id, string, id of the agent.

- Request Parameters
  
  - `password`: string, the new password of the agent

- Response

  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT  
     -d "{"password":"234567"}"  https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD/password
```

  Sample response:

```json
Status: 200 OK
```

#### Unlock an Agent

  `PUT /api/v3/agents/{id}/unlock`

- Path Parameters
  
  - id, string, id of the agent.

- Response
  
  Status: 200 OK  

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT
     -d ""  https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD/unlock
```

  Sample response:

```json
Status: 200 OK
```

#### Get an agent's permissions

  `GET /api/v3/agents/{id}/permissions`

- Path Parameters
  
  - id, string, id of the agent.

- Response

  A map of permission groups by Products

```json
  {
    "realtimeConversations": {
      "acceptChats": true,
      "viewAllHistory": true,
      "viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,
      "deleteTranscripts": false,
      "manageCampaigns": false,
      "manageSettings": false,
      "manageCustomVariables": false,
      "manageSecureForm": false,
      "manageBan": false,
      "viewReports": false,
      "refuseChats": false,
      "inviteVisitorsToChat": false,
      "joinChats": true,
      "transferChats": true,
      "monitorAllChats": false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor": false,
      "manageCustomMetrics": false,
      "viewAllInSiteVisitors": false,
      "viewAllAgents": false,
    },    
    "anytimeConversations": {
      "manageAssignedToMeConversations": true,
      "viewConversationsWithNoDepartment": false, 
      "manageConversationsWithNoDepartment": false,
      "viewConversationsInMyDepartments": false, 
      "manageConversationsInMyDepartments": false,
      "manageBlockedSenders": false,
      "manageJunckMessages": false, 
      "viewAllConversations": false, 
      "manageAllConversions": false, 
      "permanentlyDeleteConversations": false,
      "manageAllViews": false,
      "manageChannels": false,
      "manageSettings": false,
      "viewReports": false,
    },
    "ai": {
      "manageAndTakeOverBotChats": false, 
      "manageBot": false, 
      "manageBotContent": false, 
    },
    "knowledgeBase": {
      "manageArticles": false,
      "manageCustomPages": false,
      "manageDesign": false, 
      "manageImages": false,
      "manageMultipleKnowledageBases": false, 
    },
    "global": {
      "manageAgentAndRoles": true,
      "manageDepartments": false,
      "manageCustomAwayStatus": false, 
      "manageMyProfile": false,
      "manageBillingInfo": false,
      "manageProducts": false,
      "viewBalanceHistory": false,
      "manageSiteProfile": false,
      "viewAuditLog": false,
      "manageSecurity": false,  
      "manageCreditCardMasking": false,
      "managePublicCannedMessages": false,
      "managePrivateCannedMessages": false,
      "manageIntegration": false,
      "chatWithAgents": false,
      "setOtherAgentToAway": false,
      "logOtherAgentOff": false,
      "viewAgentChatsInMyDepartment": false,
      "viewAllAgentChats": false,
      "manageTags": false,
      "manageChannels": false,
      "viewContacts": false,
      "manageContacts": false,
    }
  }
```

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD/permissions
```

  Sample response:

```json
{
    "realtimeConversations": {
      "acceptChats": true,
      "viewAllHistory": true,
      "viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,
      "deleteTranscripts": false,
      "manageCampaigns": false,
      "manageSettings": false,
      "manageCustomVariables": false,
      "manageSecureForm": false,
      "manageBan": false,
      "viewReports": false,
      "refuseChats": false,
      "inviteVisitorsToChat": false,
      "joinChats": true,
      "transferChats": true,
      "monitorAllChats": false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor": false,
      "manageCustomMetrics": false,
      "viewAllInSiteVisitors": false,
      "viewAllAgents": false,
    },    
    "anytimeConversations": {
      "manageAssignedToMeConversations": true,
      "viewConversationsWithNoDepartment": false, 
      "manageConversationsWithNoDepartment": false,
      "viewConversationsInMyDepartments": false, 
      "manageConversationsInMyDepartments": false,
      "manageBlockedSenders": false,
      "manageJunckMessages": false, 
      "viewAllConversations": false, 
      "manageAllConversions": false, 
      "permanentlyDeleteConversations": false,
      "manageAllViews": false,
      "manageChannels": false,
      "manageSettings": false,
      "viewReports": false,
    },
    "ai": {
      "manageAndTakeOverBotChats": false, 
      "manageBot": false, 
      "manageBotContent": false, 
    },
    "knowledgeBase": {
      "manageArticles": false,
      "manageCustomPages": false,
      "manageDesign": false, 
      "manageImages": false,
      "manageMultipleKnowledageBases": false, 
    },
    "global": {
      "manageAgentAndRoles": true,
      "manageDepartments": false,
      "manageCustomAwayStatus": false, 
      "manageMyProfile": false,
      "manageBillingInfo": false,
      "manageProducts": false,
      "viewBalanceHistory": false,
      "manageSiteProfile": false,
      "viewAuditLog": false,
      "manageSecurity": false,  
      "manageCreditCardMasking": false,
      "managePublicCannedMessages": false,
      "managePrivateCannedMessages": false,
      "manageIntegration": false,
      "chatWithAgents": false,
      "setOtherAgentToAway": false,
      "logOtherAgentOff": false,
      "viewAgentChatsInMyDepartment": false,
      "viewAllAgentChats": false,
      "manageTags": false,
      "manageChannels": false,
      "viewContacts": false,
      "manageContacts": false,
    }
}
```

#### Update Permissions for an Agent

  `PUT /api/v3/agents/{id}/permissions`

- Path Parameters
  
  - id, string, id of the agent.

- Request Parameters

  A map of permission groups by Products

- Response

  A map of permission groups by Products

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
      -H "content-type: application/json" -x PUT  
     -d "{"realtimeConversations":{"acceptChats": true,"viewAllHistory": true,"viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,"deleteTranscripts": false,"manageCampaigns": false,"manageSettings": false,
      "manageCustomVariables": true,"manageSecureForm": true,"manageBan": false,"viewReports": false,
      "refuseChats": false,"inviteVisitorsToChat": false,"joinChats": true,"transferChats": true,
      "monitorAllChats": false,"monitorChatsInMyDepartment": false,"captureVisitor": false,
      "manageCustomMetrics": false,"viewAllInSiteVisitors": true,"viewAllAgents": true}}"   
     https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD/permissions
```

  Sample response:

```json
{
    "realtimeConversations": {
      "acceptChats": true,
      "viewAllHistory": true,
      "viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,
      "deleteTranscripts": false,
      "manageCampaigns": false,
      "manageSettings": false,
      "manageCustomVariables": true,
      "manageSecureForm": true,
      "manageBan": false,
      "viewReports": false,
      "refuseChats": false,
      "inviteVisitorsToChat": false,
      "joinChats": true,
      "transferChats": true,
      "monitorAllChats": false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor": false,
      "manageCustomMetrics": false,
      "viewAllInSiteVisitors": true,
      "viewAllAgents": true,
    },    
    "anytimeConversations": {
      "manageAssignedToMeConversations": true,
      "viewConversationsWithNoDepartment": false, 
      "manageConversationsWithNoDepartment": false,
      "viewConversationsInMyDepartments": false, 
      "manageConversationsInMyDepartments": false,
      "manageBlockedSenders": false,
      "manageJunckMessages": false, 
      "viewAllConversations": false, 
      "manageAllConversions": false, 
      "permanentlyDeleteConversations": false,
      "manageAllViews": false,
      "manageChannels": false,
      "manageSettings": false,
      "viewReports": false,
    },
    "ai": {
      "manageAndTakeOverBotChats": false, 
      "manageBot": false, 
      "manageBotContent": false, 
    },
    "knowledgeBase": {
      "manageArticles": false,
      "manageCustomPages": false,
      "manageDesign": false, 
      "manageImages": false,
      "manageMultipleKnowledageBases": false, 
    },
    "global": {
      "manageAgentAndRoles": true,
      "manageDepartments": false,
      "manageCustomAwayStatus": false, 
      "manageMyProfile": false,
      "manageBillingInfo": false,
      "manageProducts": false,
      "viewBalanceHistory": false,
      "manageSiteProfile": false,
      "viewAuditLog": false,
      "manageSecurity": false,  
      "manageCreditCardMasking": false,
      "managePublicCannedMessages": false,
      "managePrivateCannedMessages": false,
      "manageIntegration": false,
      "chatWithAgents": false,
      "setOtherAgentToAway": false,
      "logOtherAgentOff": false,
      "viewAgentChatsInMyDepartment": false,
      "viewAllAgentChats": false,
      "manageTags": false,
      "manageChannels": false,
      "viewContacts": false,
      "manageContacts": false,
    }
}
```

#### Get a List of an Agent's Eeffective Permissions

  `GET /api/v3/agents/{id}/effectivePermissions`

- Path Parameters
  
  - id, string, id of the agent.

- Response
  
  An array of Agent Permission Object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/agents/2B356016-2B44-49C0-B4E6-05902E55DAFD/effectivepermissions
```

  Sample response:

```json
{
    "realtimeConversations": {
      "acceptChats": true,
      "viewAllHistory": true,
      "viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,
      "deleteTranscripts": false,
      "manageCampaigns": false,
      "manageSettings": false,
      "manageCustomVariables": true,
      "manageSecureForm": true,
      "manageBan": false,
      "viewReports": false,
      "refuseChats": false,
      "inviteVisitorsToChat": false,
      "joinChats": true,
      "transferChats": true,
      "monitorAllChats": false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor": false,
      "manageCustomMetrics": false,
      "viewAllInSiteVisitors": true,
      "viewAllAgents": true,
    },    
    "anytimeConversations": {
      "manageAssignedToMeConversations": true,
      "viewConversationsWithNoDepartment": false, 
      "manageConversationsWithNoDepartment": false,
      "viewConversationsInMyDepartments": false, 
      "manageConversationsInMyDepartments": false,
      "manageBlockedSenders": false,
      "manageJunckMessages": false, 
      "viewAllConversations": false, 
      "manageAllConversions": false, 
      "permanentlyDeleteConversations": false,
      "manageAllViews": false,
      "manageChannels": false,
      "manageSettings": false,
      "viewReports": false,
    },
    "ai": {
      "manageAndTakeOverBotChats": false, 
      "manageBot": false, 
      "manageBotContent": false, 
    },
    "knowledgeBase": {
      "manageArticles": false,
      "manageCustomPages": false,
      "manageDesign": false, 
      "manageImages": false,
      "manageMultipleKnowledageBases": false, 
    },
    "global": {
      "manageAgentAndRoles": true,
      "manageDepartments": false,
      "manageCustomAwayStatus": false, 
      "manageMyProfile": false,
      "manageBillingInfo": false,
      "manageProducts": false,
      "viewBalanceHistory": false,
      "manageSiteProfile": false,
      "viewAuditLog": false,
      "manageSecurity": false,  
      "manageCreditCardMasking": false,
      "managePublicCannedMessages": false,
      "managePrivateCannedMessages": false,
      "manageIntegration": false,
      "chatWithAgents": false,
      "setOtherAgentToAway": false,
      "logOtherAgentOff": false,
      "viewAgentChatsInMyDepartment": false,
      "viewAllAgentChats": false,
      "manageTags": false,
      "manageChannels": false,
      "viewContacts": false,
      "manageContacts": false,
    }
}
```

#### Get current Agent

  `GET /api/v3/agents/me`

- Parameters

  No parameters
  
- Response
  
  [Agent](#Agent-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/agents/me
```

  Sample response:

```json
{
    "id": "2B356016-2B44-49C0-B4E6-05902E55DAFD",
    "email": "test1@test.com",
    "displayName": "testname",
    "firstName": "first",
    "lastName": "lastname",
    "title": "title",
    "bio": "",
    "mobilePhone": "12345678911",
    "timeZone": "31",
    "dateTimeFormat": "MM/dd/yyyy HH:mm:ss",
    "roles": [],
    "isAdmin": true,
    "isActive": true,
    "isLocked": false,
    "availableChannels": []
}
```

#### Update Your Own Profile

  `PUT /api/v3/agents/me`

- Request Parameters

  [Agent](#Agent-Json-Format)

- Response

  [Agent](#Agent-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"email": 'test4@test.com',"displayname": 'testname',"firstname": 'first',
     "lastname": 'lastname',"title": 'title',"timezone": '31',"mobilephone": '12345678911'}"
     https://hosted.comm100.com/api/v3/agents/me
```

  Sample response:

```json
{
    "id": "2B356016-2B44-49C0-B4E6-05902E55DAFD",
    "email": "test4@test.com",
    "displayName": "testname",
    "firstName": "first",
    "lastName": "lastname",
    "title": "title",
    "bio": "",
    "mobilePhone": "12345678911",
    "timeZone": "31",
    "dateTimeFormat": "MM/dd/yyyy HH:mm:ss",
    "roles": [],
    "isAdmin": true,
    "isActive": true,
    "isLocked": false,
    "availableChannels": []
}
```

#### Change Your Own password

  `PUT /api/v3/agents/me/password`

- Request Parameters

  - `currentPassword`: string, current password of curreng agent
  - `newPassword`: string, new password of current agent

- Response

  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"currentpassword": '123456', "newpassword": '111111'}"
     https://hosted.comm100.com/api/v3/agents/me/password
```

  Sample response:

```json
Status: 200 OK
```

</div>
</div>

<div>

## Contact

- You need `Manage Contacts` permission to manage contacts.
  - `GET /api/v3/contacts` - Search contacts
  - `GET /api/v3/contacts/{id}` - Get a contact by contact id
  - `PUT /api/v3/contacts/{id}` - Update a contact
  - `POST /api/v3/contacts` - Create a contact
  - `DELETE /api/v3/contacts/{id}` - Remove a contact
  - `POST  /api/v3/contacts/{contactId}/identities` - Add contact identity
  - `PUT  /api/v3/contacts/{contactId}/identities/{id}` - Update contact identity
  - `DELETE  /api/v3/contacts/{contactId}/identities/{id}` - Delete contact identity

<div>

### Model

#### Contact Json Format

 Contact is represented as simple flat JSON objects with the following keys:  

| Name | Type | Description |
| - | - | - |
| `id` | string | read-only, id of contact |
| `name` | string | required, the name of the contact |
| `alias` | string | optional, the alias name of the contact |
| `identities` | [identity](#identity)[] | optional, identity array of the contact |
| `description` | string | optional, a small description of the contact |
| `company` | string | optional, the primary company name which this contact belongs to |
| `title` | string | optional, the title of the contact|
| `phoneNumber` | string | optional, telephone number of the contact|
| `faxNumber` | string | optional, fax number of the contact |
| `address` | string | optional, the address of the contact  |
| `city` | string | optional, the city of the contact  |
| `stateOrProvince` | string | optional, the state or province of the contact |
| `country` | string | optional, the country of the contact |
| `postalOrZipCode` | string | optional, the postal or zip code of the contact  |
| `createdTime` | datetime | optional, the time the contact was created |
| `tags` | [tag](#tag)[] | optional, tag array of the contact  |

 ### Identity
| Name | Type | Description | 
| - | - | - |
| `id` | string | read-only, the id of identity |
| `type` | string | required, `emailAddress`, `SSOUserId`, `externalId`, `smsNumber`, `facebookAccount`, `twitterAccount`, `weChatAccount` |
| `value` | string | required, the value of one identity, should be unique |

 - Note: We currently only allow one for each type.

</div>
<div>
 
 ### Endpoints

 #### Search contacts

- Max 50 contacts are responded for each request.
- `GET  /api/v3/contacts`

- Query Parameters

      Optional:
    - `pageIndex`: integer, default 1
    - `keywords`: string, search scope includes: name/identity id/identity value/alias 

- Response

    - `contacts`: [Contact](#contact)[]
    - `total`: integer, total number of contacts.
    - `previousPage`: string, next page uri, the first page return null.
    - `nextPage`: string, the last page return null.
    - `currentPage`: string, current page uri.

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/contacts?keywords=comm100
```

  Sample response:

```json
{
    "total": 1,
    "previousPage": "",
    "nextPage": "",
    "nextPage": "?keywords=comm100&pageindex=1",
    "contacts": [
        {
            "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
            "name": "tony",
            "alias": "test comm100",
            "identities": [],
            "description": "test",
            "company": "comm100",
            "title": "",
            "phoneNumber": "",
            "faxNumber": "-1",
            "address": "",
            "city": "",
            "stateOrProvince": "",
            "country": "",
            "postalOrZipCode": "",
            "createdTime": "2019-05-08T10:21:44.403",
            "tags": []
        }
    ]
}
```

#### Get a contact by contact id

`GET  /api/v3/contacts/{id}`

- Path Parameters

  - id: string, id of the contact

- Response

  [Contact](#contact)


#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

  Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "name": "tony",
    "alias": "test comm100",
    "identities": [],
    "description": "test",
    "company": "comm100",
    "title": "",
    "phoneNumber": "",
    "faxNumber": "-1",
    "address": "",
    "city": "",
    "stateOrProvince": "",
    "country": "",
    "postalOrZipCode": "",
    "createdTime": "2019-05-08T10:21:44.403",
    "tags": []
}
```

 #### Create a contact

`POST  /api/v3/contacts`

- Request Parameters 

   [Contact](#contact)

 - Response

   [Contact](#contact)


#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x POST -H "Content-Type: application/json"  
     -d "{"name": 'tony',"alias": 'test comm100',"identities": [{"id": 'ABCD053B-97DB-4E2F-9B7F-664CA3A14951', "type": 'emailAddress', "value": 'test@comm100.com'}]}"    
     https://hosted.comm100.com/api/v3/contacts
```

Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "name": "tony",
    "alias": "test comm100",
    "identities": [
      {
        "id": "ABCD053B-97DB-4E2F-9B7F-664CA3A14951",
        "type": "emailAddress",
        "value": "test@comm100.com"
      }
    ],
    "description": "test",
    "company": "comm100",
    "title": "",
    "phoneNumber": "",
    "faxNumber": "-1",
    "address": "",
    "city": "",
    "stateOrProvince": "",
    "country": "",
    "postalOrZipCode": "",
    "createdTime": "2019-05-08T10:21:44.403",
    "tags": []
}
```


 #### Update a contact

`PUT  /api/v3/contacts/{id}`

- Path Parameters

    - id: string, id of the contact

- Request Parameters

  [Contact](#contact)

- Response

  [Contact](#contact)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"name": 'jason',"alias": 'my alias'}"    
     https://hosted.comm100.com/api/v3/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "name": "jason",
    "alias": "my alias",
    "identities": [
      {
        "id": "ABCD053B-97DB-4E2F-9B7F-664CA3A14951",
        "type": "emailAddress",
        "value": "test@comm100.com"
      }
    ],
    "description": "test",
    "company": "comm100",
    "title": "",
    "phoneNumber": "",
    "faxNumber": "-1",
    "address": "",
    "city": "",
    "stateOrProvince": "",
    "country": "",
    "postalOrZipCode": "",
    "createdTime": "2019-05-08T10:21:44.403",
    "tags": []
}
```

 #### Delete a contact

 `DELETE  /api/v3/contacts/{id}`

- Path Parameters

    - id: string, id of the contact

- Response

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE https://hosted.comm100.com/api/v3/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

Sample response:

```json
Status: 200 OK
```

 #### Add identity

`POST  /api/v3/contacts/{contactId}/identities`

- Path Parameters

    - contactId: string, contact id

- Request Parameters

    [Identity](#identity)

- Response

    [Identity](#identity)


#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x POST -H "Content-Type: application/json"  
     -d "{"type": 'smsNumber', "value": '123456789'}"    
     https://hosted.comm100.com/api/v3/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities
```

Sample response:

```json
{
    "id": "18266526-49F7-4DB3-937A-CE9902E90BA3",
    "type": "smsNumber",
    "value": "123456789"
}
```

 #### Update identity

`PUT  /api/v3/contacts/{contactId}/identities/{id}`

- Path Parameters

    - contactId: string, contact id
    - id: string, contact identity id

- Request Parameters

    - value: string, the value of this identity.

- Response

    [Identity](#identity)


#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"value": '987654321'}"    
     https://hosted.comm100.com/api/v3/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities/18266526-49F7-4DB3-937A-CE9902E90BA3
```

Sample response:

```json
{
    "id": "18266526-49F7-4DB3-937A-CE9902E90BA3",
    "type": "smsNumber",
    "value": "987654321"    
}
```

 #### Delete identity

 `DELETE  /api/v3/contacts/{contactId}/identities/{id}`

- Path Parameters

    - contactId: string, contact id
    - id: string, contact identity id

- Response

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE https://hosted.comm100.com/api/v3/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities/18266526-49F7-4DB3-937A-CE9902E90BA3
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>

<div>

## Roles

  You need `Manage Agent & Agent Roles` permission to manage roles.
- `GET /api/v3/roles` - Get a list of roles
- `GET /api/v3/roles/{id}` - Get a single roles
- `POST /api/v3/roles` - Create a new role
- `PUT /api/v3/roles/{id}` - Update a role
- `DELETE /api/v3/roles/{id}` - Remove a role
- `GET /api/v3/roles/{id}/permissions` - Get a role's permissions.
- `PUT /api/v3/roles/{id}/permissions` - Update permissions for a role.

<div>

### Model

#### Role Json Format

 Role is represented as simple flat JSON objects with the following keys:  

| Name | Type | Description |
| - | - | - |
| `id` | string | read-only, id of the role. |
| `isSystem` | bool | read-only, indicator that the role is maintained by the system |
| `name` | string | required, name of the role. |
| `description` | string | optional, the description of the role. |
| `agents` | array | optional, a list of agents in current role. |

</div>
<div>

### Endpoint

#### Get list of Roles

  `GET /api/v3/roles`

- Parameters
  
  No parameters

- Response
  
  [Role](#Role-Json-Format)[]

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/roles
```

  Sample response:

```json
[
    {
        "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F42",
        "name": "Site Administrators",
        "description": "This role includes all site administrators in the system. ",
        "isSystem": true,
        "agents": [
        {
          "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F41",
          "name": "f 1"
        },
        {
          "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F43",
          "name": "f 69"
        }
        ...
        ]
    },
    {
        "id": "4FCE64E9-615C-4036-B8EF-07D3B8AF7F42",
        "name": "All Agents",
        "description": "This role includes all agents in the system. ",
        "isSystem": true,
        "agents": [
        {
          "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F41",
          "name": "f 1"
        },
        {
          "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F43",
          "name": "f 69"
        }
        ...
        ]
    }
]
```

#### Get a single Role

  `GET /api/v3/roles/{id}`

- Path Parameters:

    - id, string, id of the role.

- Response
  
  [Role](#Role-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/roles/4FCE64E9-615C-4036-B8EF-07D3B8AF7F42
```

  Sample response:

```json
{
    "id": "4FCE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "name": "Site Administrators",
    "description": "This role includes all site administrators in the system. ",
    "isSystem": true,
    "agents": [
    {
      "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F41",
      "name": "f 1"
    },
    {
      "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F43",
      "name": "f 69"
    }
    ...
    ]
}
```

#### Create a new Role
  
  `POST /api/v3/roles`

- Request Parameters
  
  [Role](#Role-Json-Format)

- Response
  
  [Role](#Role-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x POST -H "Content-Type: application/json"  
     -d "{"name": 'testaddname'}"    
     https://hosted.comm100.com/api/v3/roles
```

  Sample response:

```json
{
    "id": "55CE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "name": "testaddname",
    "description": "",
    "isSystem": false,
    "agents": []
}
```

#### Update a Role

  `PUT /api/v3/roles/{id}`

- Request Parameters
  
  [Role](#Role-Json-Format)

- Response
  
  [Role](#Role-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"name": 'testchangename'}"    
     https://hosted.comm100.com/api/v3/roles/3FCE64E9-615C-4036-B8EF-07D3B8AF7F42
```

  Sample response:

```json
{
    "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "name": "testchangename",
    "description": "This role includes all site administrators in the system. ",
    "isSystem": true,
    "agents": [ ]
}
```

#### Remove a Role

  `DELETE /api/v3/roles/{id}`

- Path Parameters
  
  - id, string, id of the role.

- Response
  
  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x DELETE  https://hosted.comm100.com/api/v3/roles/55CE64E9-615C-4036-B8EF-07D3B8AF7F42
```

  Sample response:

```json
Status: 200 OK
```

#### Get a Role's Permissions

  `GET /api/v3/roles/{id}/permissions`

- Path Parameters:

    - id, string, id of the role.

- Response

  A map of permission roles by Products

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/roles/3FCE64E9-615C-4036-B8EF-07D3B8AF7F42/permissions
```

  Sample response:

```json
{
    "realtimeConversations": {
      "acceptChats": true,
      "viewAllHistory": true,
      "viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,
      "deleteTranscripts": false,
      "manageCampaigns": false,
      "manageSettings": false,
      "manageCustomVariables": true,
      "manageSecureForm": true,
      "manageBan": false,
      "viewReports": false,
      "refuseChats": false,
      "inviteVisitorsToChat": false,
      "joinChats": true,
      "transferChats": true,
      "monitorAllChats": false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor": false,
      "manageCustomMetrics": false,
      "viewAllInSiteVisitors": true,
      "viewAllAgents": true,
    },    
    "anytimeConversations": {
      "manageAssignedToMeConversations": true,
      "viewConversationsWithNoDepartment": false, 
      "manageConversationsWithNoDepartment": false,
      "viewConversationsInMyDepartments": false, 
      "manageConversationsInMyDepartments": false,
      "manageBlockedSenders": false,
      "manageJunckMessages": false, 
      "viewAllConversations": false, 
      "manageAllConversions": false, 
      "permanentlyDeleteConversations": false,
      "manageAllViews": false,
      "manageChannels": false,
      "manageSettings": false,
      "viewReports": false,
    },
    "ai": {
      "manageAndTakeOverBotChats": false, 
      "manageBot": false, 
      "manageBotContent": false, 
    },
    "knowledgeBase": {
      "manageArticles": false,
      "manageCustomPages": false,
      "manageDesign": false, 
      "manageImages": false,
      "manageMultipleKnowledageBases": false, 
    },
    "global": {
      "manageAgentAndRoles": true,
      "manageDepartments": false,
      "manageCustomAwayStatus": false, 
      "manageMyProfile": false,
      "manageBillingInfo": false,
      "manageProducts": false,
      "viewBalanceHistory": false,
      "manageSiteProfile": false,
      "viewAuditLog": false,
      "manageSecurity": false,  
      "manageCreditCardMasking": false,
      "managePublicCannedMessages": false,
      "managePrivateCannedMessages": false,
      "manageIntegration": false,
      "chatWithAgents": false,
      "setOtherAgentToAway": false,
      "logOtherAgentOff": false,
      "viewAgentChatsInMyDepartment": false,
      "viewAllAgentChats": false,
      "manageTags": false,
      "manageChannels": false,
      "viewContacts": false,
      "manageContacts": false,
    }
}
```

#### Update Permissions for a Role

  `PUT /api/v3/roles/{id}/permissions`

- Path Parameters:

    - id, string, id of the role.

- Request Parameters

  A map of permission groups by Products

- Response

  A map of permission groups by Products

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -H "content-type: application/json" -x PUT  
     -d "{"realtimeConversations":{"acceptChats": true,"viewAllHistory": true,"viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,"deleteTranscripts": false,"manageCampaigns": false,"manageSettings": false,
      "manageCustomVariables": true,"manageSecureForm": true,"manageBan": false,"viewReports": false,
      "refuseChats": false,"inviteVisitorsToChat": false,"joinChats": true,"transferChats": true,
      "monitorAllChats": false,"monitorChatsInMyDepartment": false,"captureVisitor": false,
      "manageCustomMetrics": false,"viewAllInSiteVisitors": true,"viewAllAgents": true}}" 
     https://hosted.comm100.com/api/v3/roles/3FCE64E9-615C-4036-B8EF-07D3B8AF7F42/permissions
```

  Sample response:

```json
{
    "realtimeConversations": {
      "acceptChats": true,
      "viewAllHistory": true,
      "viewHistoryInMyDepartment": false,
      "viewMyOwnAllTranscripts": false,
      "deleteTranscripts": false,
      "manageCampaigns": false,
      "manageSettings": false,
      "manageCustomVariables": true,
      "manageSecureForm": true,
      "manageBan": false,
      "viewReports": false,
      "refuseChats": false,
      "inviteVisitorsToChat": false,
      "joinChats": true,
      "transferChats": true,
      "monitorAllChats": false,
      "monitorChatsInMyDepartment": false,
      "captureVisitor": false,
      "manageCustomMetrics": false,
      "viewAllInSiteVisitors": true,
      "viewAllAgents": true,
    },    
    "anytimeConversations": {
      "manageAssignedToMeConversations": true,
      "viewConversationsWithNoDepartment": false, 
      "manageConversationsWithNoDepartment": false,
      "viewConversationsInMyDepartments": false, 
      "manageConversationsInMyDepartments": false,
      "manageBlockedSenders": false,
      "manageJunckMessages": false, 
      "viewAllConversations": false, 
      "manageAllConversions": false, 
      "permanentlyDeleteConversations": false,
      "manageAllViews": false,
      "manageChannels": false,
      "manageSettings": false,
      "viewReports": false,
    },
    "ai": {
      "manageAndTakeOverBotChats": false, 
      "manageBot": false, 
      "manageBotContent": false, 
    },
    "knowledgeBase": {
      "manageArticles": false,
      "manageCustomPages": false,
      "manageDesign": false, 
      "manageImages": false,
      "manageMultipleKnowledageBases": false, 
    },
    "global": {
      "manageAgentAndRoles": true,
      "manageDepartments": false,
      "manageCustomAwayStatus": false, 
      "manageMyProfile": false,
      "manageBillingInfo": false,
      "manageProducts": false,
      "viewBalanceHistory": false,
      "manageSiteProfile": false,
      "viewAuditLog": false,
      "manageSecurity": false,  
      "manageCreditCardMasking": false,
      "managePublicCannedMessages": false,
      "managePrivateCannedMessages": false,
      "manageIntegration": false,
      "chatWithAgents": false,
      "setOtherAgentToAway": false,
      "logOtherAgentOff": false,
      "viewAgentChatsInMyDepartment": false,
      "viewAllAgentChats": false,
      "manageTags": false,
      "manageChannels": false,
      "viewContacts": false,
      "manageContacts": false,
    }
}
```

</div>
</div>
<div>

## Agent SSO Settings

  You need `Manage Security` permission to manage agent sso settings.
- `GET /api/v3/agentSignleSignOn` - Get configuration of agent sso settings
- `PUT /api/v3/agentSignleSignOn` - Update configuration of agent sso settings

<div>

### Model

#### Agent SSO Settings Config Json Format

 Agent SSO Settings is represented as simple flat JSON objects with the following keys:  

| Name | Type | Description |
| - | - | - |
| `ssoType` | string | required, `SAML` or `JWT` |
| `samlSSOUrl` | string | required, the url that Comm100 will invoke to redirect the agents to your Identity Provider |
| `samlRemoteLogoutUrl` | string | required, the url that Comm100 will redirect your agents to after they log out |
| `certificate` | string | required, base64 of the saml identity provider certificate content. |
| `certificateName` | string | required, file name of the certificate. |
| `jwtRemoteLoginUrl` | string | required, the url that Comm100 will redirect your agents to for remote authentication. |
| `jwtRemoteLogoutUrl` | string | required, the url that Comm100 will redirect your agents to after they log out. |
| `sharedSecret` | string | required, token between you and Comm100. |

</div>
<div>

### Endpoint

#### Get configuration of agent sso settings

  `Get /api/v3/agentSignleSignOn`

- Parameters
  
  No parameters

- Response
  
  [Agent SSO Settings](#Agent-SSO-Settings-Config-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/agentSignleSignOn
```

  Sample response:

```json
{
    "ssoType": "SAML",
    "samlSSOUrl": "https://secure.comm100.com/login",
    "samlRemoteLogoutUrl": "https://test.comm100.com/logout",
    "certificate": "amdoamdoaGdmcnRk",
    "certificateName": "test.cer",
    "jwtRemoteLoginUrl": "",
    "jwtRemoteLogoutUrl": "",
    "sharedSecret": "",
}
```

#### Update configuration of agent sso settings

  `PUT /api/v3/agentSignleSignOn`

- Request Parameters
  
  [Agent SSO Settings](#Agent-SSO-Settings-Config-Json-Format)

- Response

  [Agent SSO Settings](#Agent-SSO-Settings-Config-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -H "content-type: application/json" -x PUT  
     -d "{"ssoType": "JWT","samlSSOUrl": "https://secure.comm100.com/login",
    "samlRemoteLogoutUrl": "https://test.comm100.com/logout","certificate": "amdoamdoaGdmcnRk",
    "certificateName": "test.cer","jwtRemoteLoginUrl": "https://integration.comm100.com/jwt/accounts/login",
    "jwtRemoteLogoutUrl": "https://integration.comm100.com/jwt/home/logout",
    "sharedSecret": "NTamMDM5NzctOTayMys0Y2RjLWEwNTUdOTJibWRjszY5OGE1"}"    
     https://hosted.comm100.com/api/v3/agentSignleSignOn
```

  Sample response:

```json
{
    "ssoType": "JWT",
    "samlSSOUrl": "https://secure.comm100.com/login",
    "samlRemoteLogoutUrl": "https://test.comm100.com/logout",
    "certificate": "amdoamdoaGdmcnRk",
    "certificateName": "test.cer",
    "jwtRemoteLoginUrl": "https://integration.comm100.com/jwt/accounts/login",
    "jwtRemoteLogoutUrl": "https://integration.comm100.com/jwt/home/logout",
    "sharedSecret": "NTamMDM5NzctOTayMys0Y2RjLWEwNTUdOTJibWRjszY5OGE1",
}
```

</div>
</div>
<div>

## Audit Logs

  You need `View Audit Log` permission to view audit logs.

- `Get /api/v3/auditLogs` - Get audit Logs list.

<div>

### Model

#### Audit Logs Config Json Format

 Audit Logs is represented as simple flat JSON objects with the following keys:  

| Name | Type | Description |
| - | - | - |
| `id` | string | read-only, id of audit log |
| `actionTime` | datetime | read-only, the time of the action. |
| `agentName` | string | read-only, the agent which did the action. |
| `product` | string | read-only, the module which the action belongs to. |
| `actionType` | string | read-only, the type of the action. |
| `actionSummary` | string | read-only, the summary of the action. |

</div>
<div>

### Endpoint

#### Get audit Logs list

  `Get /api/v3/auditLogs`

- Query Parameters
  - `dateFrom`: datetime, the date from which agent did the action, format as `yyyy-MM-ddTHH:mm:ss`.
  - `dateTo`: datetime, the date when an agent ended the action, format as `yyyy-MM-ddTHH:mm:ss`.

    optional：
  - `product`: string, the product which the action belongs to, including `Real-time Conversation`, `Anytime Conversations`, `Knowledge Base`, `AI`, `Global`.
  - `type`: string, the action type.
  - `agentId`: string, id of the agent who did the action.
  - `keywords`: string, the key words associated with the action
  - `pageIndex`: integer, the page index of the query.

- Response
  - `total`: integer, total count for the list.
  - `previousPage`: string, url of the previous page.
  - `nextPage`: string, url of the next page.
  - `logs`: [audit log](#Audit-Logs-Config-Json-Format)[]

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer XCUScuZK21qDa2Tqyo0HF1rvoHC6OTIKZRkj-GgKUcsVyaXyhC7sNfGRyZc5vUGXXeI9wzo 
        74KX9xXrDTA3QR4XCXcaslq7a17ubllUwRRoMqt-cxYETrb5WFjOv4GRvM8nRO5H5nangeGJMHgJczhyiu7897kYvdlRHO 
        udnoYbkwBPNMKUzQN9hiRNtZi8eV3Faf8OZYSWGxFZPvWcNHqY78WGXwnYww_UNB1HzME7UKcvY1Auxhdq_ZR-UncaiNoM 
        46OBYYbU5nNXbKDFPAA"   
     https://hosted.comm100.com/api/v3/auditlogs?datefrom=2018-07-17&dateto=2018-08-08
```

  Sample response:

```json
{
    "total": 1,
    "previousPage": null,
    "nextPage": null,
    "logs": [
        {
            "id": "669F1B97-457B-4256-A78A-73433E328F3D",
            "actionTime": "2018-08-08T10:21:44.403",
            "agentName": "testname",
            "product": "Real-time Conversation",
            "actionType": "Chats Auto Allocation Management",
            "actionSummary": "Enable chats auto allocation"
        }
    ]
}
```

</div>
</div>

<div>

## Canned Messages

  You need `Manage Pulbic Canned Messages` permission to manage canned message.

- `GET /api/v3/cannedMessages` -get a list of canned Messages
- `GET /api/v3/cannedMessages/{id}`  -get a single canned Message
- `POST /api/v3/cannedMessages` -create a new canned Message
- `PUT /api/v3/cannedMessages/{id}`  -update a canned Message
- `DELETE /api/v3/cannedMessages/{id}`  -remove a canned Message

<div>

### Model

#### Canned Message JSON Format

  Canned Message is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  | `id` | string | read-only, id of the canned message. |
  | `name` | string | required, name of the canned message. |
  | `message` | string | required, content of the canned message. |
  | `shortcuts` | string | optional, shortcuts of the canned message. |
  | `categoryId` | string | required, id of the category of the canned message. |
  | `isPrivate` | boolean | required, whether the canned message is private or not, default is `false`. |
  | `channelType` | string | required, type the canned message, we now have `default` or `email`. |
  | `emailHtmlMessage` | string | optional, email html message of the canned message. |
  | `emailTextMessage` | string | optional, email plain text message of the canned message. |

</div>
<div>

### Endpoint

#### Get list of canned messages

  `GET /api/v3/cannedMessages`

- Parameters:

    No parameters

- Response:

    [Canned Message](#canned-message-json-format)[]

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/cannedMessages
```

Sample response:

```json
[
    {
        "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F42",
        "isPrivate": false,
        "name": "test Canned Message name",
        "message": "bye bye",
        "categoryId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42",
        "shortCuts": "bye",
        "channelType": "default",
        "emailHtmlMessage": "",
        "emailTextMessage": ""
    },
    ...
]
```

#### Get a single canned message

  `GET /api/v3/cannedMessages/{id}`

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
     https://hosted.comm100.com/api/v3/cannedmessages/3FCE64E9-615C-4036-B8EF-07D3B8AF7F42
```

Sample response:

```json
{
    "id": "3FCE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "isPrivate": false,
    "name": "test Canned Message name",
    "message": "bye bye",
    "categoryId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "shortCuts": "bye",
    "channelType": "default",
    "emailHtmlMessage": "",
    "emailTextMessage": ""
}
```

#### Create a new canned message

  `POST /api/v3/cannedMessages`

- Request Parameters:

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
     -x POST -H "Content-Type: application/json"  
     -d "{"isprivate": false,"name": 'test',"message": 'testmessage',"channelType": 'default',"emailHtmlMessage": '',"emailTextMessage": ''}"   
     https://hosted.comm100.com/api/v3/cannedmessages
```

Sample response:

```json
{
    "id": "217F8029-DCAC-4CFA-9859-DAA4C0410B4A",
    "isPrivate": false,
    "name": "test",
    "message": "testmessage",
    "categoryId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "shortCuts": "",
    "channelType": "default",
    "emailHtmlMessage": "",
    "emailTextMessage": ""
}
```

#### Update a canned message

  `PUT /api/v3/cannedMessages/{id}`

- Path Parameters:

    - id, string, id of the canned message.

- Request Parameters:

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
     -x PUT -H "Content-Type: application/json"  
     -d "{"isprivate": false,"name": 'testupdate',"message": 'testmessageupdate',"channelType": 'email',"emailHtmlMessage": 'test email html message',"emailTextMessage": 'test email text message'}"   
     https://hosted.comm100.com/api/v3/cannedmessages/217F8029-DCAC-4CFA-9859-DAA4C0410B4A
```

Sample response:

```json
{
    "id": "217F8029-DCAC-4CFA-9859-DAA4C0410B4A",
    "isPrivate": false,
    "name": "testupdate",
    "message": "testmessageupdate",
    "categoryId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42",
    "shortCuts": "",
    "channelType": "email",
    "emailHtmlMessage": "test email html message",
    "emailTextMessage": "test email text message"
}
```

#### Remove a canned message

  `DELETE /api/v3/cannedMessages/{id}`

- Path Parameters:

    - id, string, id of the canned message.

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE  https://hosted.comm100.com/api/v3/cannedmessages/217F8029-DCAC-4CFA-9859-DAA4C0410B4A
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>
<div>

## Canned Message Categories

  You need `Manage Pulbic Canned Messages` permission to manage canned message category.
- `GET /api/v3/cannedMessageCategories` -get a list of canned Messages Categories
- `GET /api/v3/cannedMessageCategories/{id}`  -get a single canned Messages Category
- `POST /api/v3/cannedMessageCategories` -create a new canned Messages Category
- `PUT /api/v3/cannedMessageCategories/{id}`  -update a canned Messages Category
- `DELETE /api/v3/cannedMessageCategories/{id}`  -remove a canned Messages Category

<div>

### Model

#### Canned Message Category JSON Format

  Canned Message Category is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  | `id` | string | read-only, id of the canned message category. |
  | `name` | string | required, name of the canned message category. |
  | `parentId` | string | required, id of the parent category of the canned message category. |
  | `isPrivate` | boolean | required, whether the canned message category is private or not. |

</div>
<div>

### Endpoint

#### Get list of canned message categories

  `GET /api/v3/cannedMessageCategories`

- Parameters:

    No parameters

- Response:

    [Canned Message Category](#canned-message-category-json-format)[]

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/cannedmessagecategories
```

Sample response:

```json
[
    {
        "id": "7F79B926-1E8C-438B-8F07-53D2914149A6",
        "isPrivate": false,
        "name": "puddddtresult",
        "parentId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42"
    },
    ...
]
```

#### Get a single canned message category

  `GET /api/v3/cannedMessageCategories/{id}`

- Path Parameters:

    - id, string, id of the canned message category.

- Response:

    [Canned Message Category](#canned-message-category-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/cannedmessagecategories/7F79B926-1E8C-438B-8F07-53D2914149A6
```

Sample response:

```json
{
    "id": "7F79B926-1E8C-438B-8F07-53D2914149A6",
    "isPrivate": false,
    "name": "puddddtresultgggg",
    "parentId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42"
}
```

#### Create a new canned message category

  `POST /api/v3/cannedMessageCategories`

- Request Parameters:

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
     -x POST -H "Content-Type: application/json"  
     -d "{"isprivate": false,"name": 'justfortest',"parentid": '0'}"    
     https://hosted.comm100.com/api/v3/cannedmessagecategories
```

Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "isPrivate": false,
    "name": "justfortest",
    "parentId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42"
}
```

#### Update a canned message category

  `PUT /api/v3/cannedMessageCategories/{id}`

- Path Parameters:

    - id, string, id of the canned message category.

- Request Parameters:

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
     -x PUT -H "Content-Type: application/json"  
     -d "{"isprivate": false,"name": 'justfortestupdate',"parentid": '0'}"    
     https://hosted.comm100.com/api/v3/cannedmessagecategories/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "isPrivate": false,
    "name": "justfortestupdate",
    "parentId": "4ACE64E9-615C-4036-B8EF-07D3B8AF7F42"
}
```

#### Remove a canned message category

  `DELETE /api/v3/cannedMessageCategories/{id}`

- Path Parameters:

    - id, string, id of the canned message category.

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE https://hosted.comm100.com/api/v3/cannedmessagecategories/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>


<div>

## Credit Card Masking

  You need `Manage Credit Card Masking` permission to manage credit card masking.
- `GET /api/v3/creditcardMasking` - Get configuration of credit card masking
- `PUT /api/v3/creditcardMasking` - Update configuration of credit card masking

<div>

### Model

#### Credit Card Masking Config Json Format

 Credit Card Masking is represented as simple flat JSON objects with the following keys:  

| Name | Type |  Description |
| - | - | - |
| `isEnable` | boolean | required, whether Credit Card Masking are enabled or not. |

</div>
<div>

### Endpoint

#### Get configuration of credit card masking

  `Get /api/v3/creditcardMasking`

- Parameters
  
  No parameters

- Response
  
  [Credit Card Masking](#Credit-Card-Masking-Config-Json-Format) Config Object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/creditcardMasking
```

  Sample response:

```json
{
    "isEnable": false
}
```

#### Update configuration of credit card masking

  `PUT /api/v3/creditcardMasking`

- Request Parameters:

  [Credit Card Masking](#Credit-Card-Masking-Config-Json-Format) Config Object

- Response

  [Credit Card Masking](#Credit-Card-Masking-Config-Json-Format) Config Object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -H "content-type: application/json" -x PUT  
     -d "{"isEnable": 'true'}"    
     https://hosted.comm100.com/api/v3/creditcardMasking
```

  Sample response:

```json
{
    "isEnable": true
}
```

</div>
</div>
<div>

## Departments

  You need `Manage Departments` permission to manage department.
- `GET /api/v3/departments` -get a list of departments
- `GET /api/v3/departments/{id}`  -get a single department
- `POST /api/v3/departments` -create a new department
- `PUT /api/v3/departments/{id}`  -update a department
- `DELETE /api/v3/departments/{id}`  -remove a department

<div>

### Model

#### Department JSON Format

  Department is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  | `id` | string | read-only, id of the department. |
  | `name` | string | required, name of the department. |
  | `description` | string | optional, description of the department. |
  | `agents` | array | optional, an array of agent in the department. |
  | `roles` | array | optional, an array of role in the department. |
  | `availableChannels` | array | optional, the list of available channels of the department.|

</div>
<div>

### Endpoint

#### Get list of departments

  `GET /api/v3/departments`

- Parameters:

    No parameters

- Response:

    [Department](#department-json-format)[]

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/departments
```

Sample response:

```json
[
    {
        "id": "0399B614-F4E9-42A0-B0DA-8C9422D7121A",
        "name": "<script>alert('dde')</script>",
        "description": "<script>alert('dde111')</script>",
        "agents": [
            "BBEBE689-0993-461A-A820-C6D30FD3C66F"
        ],
        "roles": [ ],
        "availableChannels": []
    },
    ...
]
```

#### Get a single department

  `GET /api/v3/departments/{id}`

- Path Parameters:

    - id: string, id of the department.

- Response:

    [Department](#department-json-format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/departments/0399B614-F4E9-42A0-B0DA-8C9422D7121A
```

Sample response:

```json
{
    "id": "0399B614-F4E9-42A0-B0DA-8C9422D7121A",
    "name": "<script>alert('dde')</script>",
    "description": "<script>alert('dde111')</script>",
    "agents": [
        "BBEBE689-0993-461A-A820-C6D30FD3C66F"
    ],
    "roles": [ ],
    "availableChannels": []
}
```

#### Create a new department

  `POST /api/v3/departments`

- Request Parameters:

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
     -x POST -H "Content-Type: application/json"  
     -d "{"name": 'test'}"    
     https://hosted.comm100.com/api/v3/departments
```

Sample response:

```json
{
    "id": "BBEBE689-0993-461A-A820-C6D30FD3C66F",
    "name": "test",
    "description": "",
    "agents": [ ],
    "roles": [ ],
    "availableChannels": []
}
```

#### Update a department

  `PUT /api/v3/departments/{id}`

- Path Parameters:

    - id: string, id of the department.

- Request Parameters:

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
     -x PUT -H "Content-Type: application/json"  
     -d "{"name": 'testupdate'}"    
     https://hosted.comm100.com/api/v3/departments/BBEBE689-0993-461A-A820-C6D30FD3C66F
```

Sample response:

```json
{
    "id": "BBEBE689-0993-461A-A820-C6D30FD3C66F",
    "name": "testupdate",
    "description": "",
    "agents": [ ],
    "roles": [ ],
    "availableChannels": []
}
```

#### Remove a department

  `DELETE /api/v3/departments/{id}`

- Path Parameters:

    - id: string, id of the department.

- Response:

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE  https://hosted.comm100.com/api/v3/departments/BBEBE689-0993-461A-A820-C6D30FD3C66F
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>
<div>

## IP Restriction

  You need `Manage Security` permission to manage ip restrictions.
- `GET /api/v3/ipRestriction` - Get configuration of ip restrictions
- `PUT /api/v3/ipRestriction` - Update configuration of ip restrictions
- `GET /api/v3/ipRestriction/ipRanges` - Get authorized ip range list for ip restrictions
- `PUT /api/v3/ipRestriction/ipRanges/{id}` - Update an authorized ip range
- `POST /api/v3/ipRestriction/ipRanges/{id}` - Create a new ip range for ip restriction
- `DELETE /api/v3/ipRestriction/ipRanges/{id}` - Remove an ip range for ip restriction

<div>

### Model

#### IP Restriction Config Json Format

 Ip Restrictions is represented as simple flat JSON objects with the following keys:  

| Name | Type |  Description |
| - | - | - |
| `isEnable` | boolean | optional, whether IP Restrictions are enabled or not. |
| `isEnableForMobile` | boolean | optional, whether IP Restrictions are enabled or not for mobile app access. |

</div>
<div>

### Endpoint

#### Get configuration of ip restriction

  `Get /api/v3/ipRestriction`

- Parameters
  
  No parameters

- Response
  
  [IP Restriction](#IP-Restriction-Config-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/iprestriction
```

  Sample response:

```json
{
    "isEnable": true,
    "isEnableForMobile": false
}
```

#### Update configuration of ip restriction

  `PUT /api/v3/ipRestriction`

- Parameters
  
  [IP Restriction](#IP-Restriction-Config-Json-Format)

- Response

  [IP Restriction](#IP-Restriction-Config-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -H "content-type: application/json" -x PUT  
     -d "{"isEnable":false,"isEnableForMobile":false}"    
     https://hosted.comm100.com/api/v3/iprestriction
```

  Sample response:

```json
{
    "isEnable": false,
    "isEnableForMobile": false
}
```

#### Ip Range Json Format

  Ip Range is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  | `id` | string  | read-only, id of an ip range. |
  | `from` | string  | required, where an ip range starts from. |
  | `to` | string  | required, where an ip range ends. |

#### Get ip range list of ip restriction
  
  `Get /api/v3/ipRestriction/ipRanges`

- Parameters

  No parameters

- Response

  [Ip Range](#Ip-Range-Json-Format)[]

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/iprestriction/ipranges
```

  Sample response:

```json
[
    {
        "id": "669F1B97-457B-4256-A78A-73433E328F3D",
        "from": "192.168.1.1",
        "to": "192.168.1.2"
    },
    ...
]
```

#### Create a new ip range for ip restrictions

  `POST /api/v3/ipRestriction/ipRanges`

- Request Parameters

  [Ip Range](#Ip-Range-Json-Format)

- Response

  [Ip Range](#Ip-Range-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x POST -H "Content-Type: application/json"  
     -d "{"from": '192.168.1.3',"to": '192.168.1.4'}"    
     https://hosted.comm100.com/api/v3/iprestriction/ipranges
```

  Sample response:

```json
{
    "id": "62BB51E9-BF58-4AAE-AFCE-CE33504B8A17",
    "from": "192.168.1.3",
    "to": "192.168.1.4"
}
```
#### Update ip range for ip restriction

  `PUT /api/v3/ipRestriction/ipRanges/{id}`

- Path Parameters

  - id: string, id of an ip range. 

- Request Parameters
  
  [Ip Range](#Ip-Range-Json-Format)

- Response

  [Ip Range](#Ip-Range-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -H "content-type: application/json" -x PUT  
     -d "{"from": '192.168.1.4',"to": '192.168.1.5'}"    
     https://hosted.comm100.com/api/v3/iprestriction/ipranges/62BB51E9-BF58-4AAE-AFCE-CE33504B8A17
```

  Sample response:

```json
{
    "id": "62BB51E9-BF58-4AAE-AFCE-CE33504B8A17",
    "from": "192.168.1.4",
    "to": "192.168.1.5"
}
```

#### Remove a ip range for ip restriction

  `DELETE /api/v3/ipRestriction/ipRanges/{id}`

- Path Parameters

  - id: string, id of an ip range. 

- Response

  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x DELETE https://hosted.comm100.com/api/v3/iprestriction/ipranges/62BB51E9-BF58-4AAE-AFCE-CE33504B8A17
```

  Sample response:

```json
Status: 200 OK
```

</div>
</div>

<div>

## Password Policy

  You need `Manage Security` permission to manage password policy.
- `GET /api/v3/passwordPolicy` - Get configuration of password policy
- `PUT /api/v3/passwordPolicy` - Update configuration of password policy

<div>

### Model

#### Password Policy Config Json Format

 Password Policy is represented as simple flat JSON objects with the following keys:  

| Name | Type |  Description |
| - | - | - |
| `isVerifyPasswordMinimumLength` | boolean | optional, whether verification of password minimum length is required or not. |
| `minimumPasswordLength` | integer | optional, the least number of characters that can make up a password |
| `isVerifyPasswordHistory` | boolean | optional, whether verification of history passwords is required or not. |
| `verificationValueOfPasswordHistory` | integer | optional, the number of history passwords that cannot be duplicated. |
| `isEnablePasswordExpirationLimit` | boolean | optional, whether enable valid time limit for password or not. |
| `passwordExpireInDays` | integer | optional, the number of days a password is valid for. |
| `isVerifyPassworfComplexity` | boolean | optional, whether a password is required to follow the complexity rules or not. |
| `isVerifyAgentName` | boolean | optional, whether a password cannot contain an agent’s name is enabled or not. |
| `isVerifyCommonPhrases` | boolean | optional, whether a password can be made of common phrases or not. |
| `isVerifyMaximumChangeTimes` | boolean | optional, whether enable password change times limit within 24 hours or not. |
| `maximumChangeTimes` | integer | optional, the maximum allowed change times for a password within 24 hours. |
| `isLockAccountAfterCertainFailedLoginAttempts` | boolean | optional, whether the account will be locked after a certain number of failed login attempts or not. |
| `allowedFailedLoginAttempts` | integer | optional, the allowed number of failed login attempts. |

</div>
<div>

### Endpoint

#### Get configuration of password policy

  `Get /api/v3/passwordPolicy`

- Parameters
  
  No parameters

- Response
  
  [Password Policy](#Password-Policy-Config-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/passwordPolicy
```

  Sample response:

```json
{
    "isVerifyPasswordMinimumLength": false,
    "minimumPasswordLength": 8,
    "isVerifyPasswordHistory": false,
    "verificationValueOfPasswordHistory": 1,
    "isEnablePasswordExpirationLimit": false,
    "passwordExpireInDays": 1,
    "isVerifyPassworfComplexity": false,
    "isVerifyAgentName": false,
    "isVerifyCommonPhrases": false,
    "isVerifyMaximumChangeTimes": false,
    "maximumChangeTimes": 8,
    "isLockAccountAfterCertainFailedLoginAttempts": false,
    "allowedFailedLoginAttempts": 1,
}
```

#### Update configuration of password policy

  `PUT /api/v3/passwordPolicy`

- Request Parameters
  
  [Password Policy](#Password-Policy-Config-Json-Format)

- Response

  [Password Policy](#Password-Policy-Config-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -H "content-type: application/json" -x PUT  
     -d "{"isVerifyPasswordMinimumLength": true,"minimumPasswordLength": 16}"    
     https://hosted.comm100.com/api/v3/passwordPolicy
```

  Sample response:

```json
{
    "isVerifyPasswordMinimumLength": true,
    "minimumPasswordLength": 16,
    "isVerifyPasswordHistory": false,
    "verificationValueOfPasswordHistory": 1,
    "isEnablePasswordExpirationLimit": false,
    "passwordExpireInDays": 1,
    "isVerifyPassworfComplexity": false,
    "isVerifyAgentName": false,
    "isVerifyCommonPhrases": false,
    "isVerifyMaximumChangeTimes": false,
    "maximumChangeTimes": 8,
    "isLockAccountAfterCertainFailedLoginAttempts": false,
    "allowedFailedLoginAttempts": 1,
}
```

</div>
</div>


<div>

## Tag

- You need `Manage Tags` permission to manage tags.
  - `GET /api/v3/tags` - Search tags
  - `GET /api/v3/tags/{id}` - Get a tag by tag id
  - `PUT /api/v3/tags/{id}` - Update a tag
  - `POST /api/v3/tags` - Create a tag
  - `DELETE /api/v3/tags/{id}` - Remove a tag

<div>

### Model

#### Tag Json Format

 Tag is represented as simple flat JSON objects with the following keys:  

| Name | Type | Description |
| - | - | - |
| `id` | string | read-only, id of tag |
| `name` | string | required, the name of the tag |

</div>
<div>
 
 ### Endpoints

 #### Get tags

- `GET  /api/v3/tags`

- Parameters

  No parameters

- Response

  [tag](#Tag-Json-Format)[]

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/tags
```

  Sample response:

```json
[    
    {
        "id": "843D009B-7D93-43F0-83AA-E29347BB947D",
        "name": "tony's tag1"
    },
    {
        "id": "954609B-7D93-43F0-83AA-E29347BB947D",
        "name": "tony's tag2"
    }    
]
```

#### Get a tag by tag id

`GET  /api/v3/tags/{id}`

- Path Parameters

  - id: string, id of the tag

- Response

  [Tag](#Tag-Json-Format)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/tags/954609B-7D93-43F0-83AA-E29347BB947D
```

Sample response:

```json
{
    "id": "954609B-7D93-43F0-83AA-E29347BB947D",
    "name": "tony's tag2"
}
```

 #### Create a tag

`POST  /api/v3/tags`

- Request Parameters

   [Tag](#Tag-Json-Format)

 - Response

   [Tag](#Tag-Json-Format)


 #### Update a tag

`PUT  /api/v3/tag/{id}`

- Path Parameters

  - id: string, id of the tag

- Request Parameters

  [Tag](#Tag-Json-Format)

- Response

  [Tag](#Tag-Json-Format)

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"name": 'test update tag'}"
     https://hosted.comm100.com/api/v3/tags/954609B-7D93-43F0-83AA-E29347BB947D
```

  Sample response:

```json
{
    "id": "954609B-7D93-43F0-83AA-E29347BB947D",
    "name": "test update tag"
}
```

 #### Delete a tag

 `DELETE  /api/v3/tags/{id}`

- Path Parameters

  - id: string, id of the tag

- Response

  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"  
     -x DELETE https://hosted.comm100.com/api/v3/tags/843D009B-7D93-43F0-83AA-E29347BB947D
```

  Sample response:

```json
Status: 200 OK
```

</div>
</div>
<div>

## Webhooks

- `GET /api/v3/webhooks` - Get a list of webhooks
- `POST /api/v3/webhooks` - Create a new webhook
- `PUT /api/v3/webhooks/{id}` - Update a webhook
- `DELETE /api/v3/webhooks/{id}`  - Remove a webhook

<div>

### Model

#### Webhook JSON Format

Webhook is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |
  | - | - | - |
  |`id`| string | read-only, id of the webhook. |
  |`event`| string | required, event of webhook, including `offlineMessageSubmitted`, `operatorEventNotification`, `chatStarted`, `chatEnded`, `chatWrappedUp`, `chatRequested` and `chatTransferred`, `chat.FileUploaded`, `offlineMessage.FileUploaded`, `anytimeConversation.FileUploaded`. |
  |`targetUrl`| string | required, target url of the webhook. |

</div>
<div>

### Endpoint

#### Get list of webhooks

  `GET /api/v3/webhooks`

- Parameters:

    No parameters

- Response:

    [Webhook](#webhook-json-format)[]

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"   
     https://hosted.comm100.com/api/v3/webhooks
```

Sample response:

```json
[
    {
        "id": "36E4A18F-3AE7-4192-BCF4-CB5CA6320908",
        "event": "chatWrappedUp",
        "targetUrl": "http://www.aa.com"
    },
    ...
]
```

#### Create a new webhook

  `POST /api/v3/webhooks`

- Request Parameters:

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
     -x POST -H "Content-Type: application/json"  
     -d "{"event": 'chatwrappedup',"targeturl": 'http://www.baidu.com'}"    
     https://hosted.comm100.com/api/v3/webhooks
```

Sample response:

```json
{
    "id": "36E4A18F-3AE7-4192-BCF4-CB5CA6320908",
    "event": "chatWrappedUp",
    "targetUrl": "http://www.baidu.com"
}
```

#### Update a webhook

  `PUT /api/v3/webhooks/{id}`

- Path parameters:

  - id: string, id of the webhook.

- Request Parameters:

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
     -x PUT -H "Content-Type: application/json"  
     -d "{"event": 'chatwrappedup',"targeturl": 'http://www.google.com'}"    
     https://hosted.comm100.com/api/v3/webhooks/36E4A18F-3AE7-4192-BCF4-CB5CA6320908
```

Sample response:

```json
{
    "id": "36E4A18F-3AE7-4192-BCF4-CB5CA6320908",
    "event": "chatWrappedUp",
    "targetUrl": "http://www.google.com"
}
```

#### Remove a webhook

  `DELETE /api/v3/webhooks/{id}`

- Path Parameters:

    - id: string, id of the webhook.

- Response:

    Status: 200 OK  

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE  https://hosted.comm100.com/api/v3/webhooks/36E4A18F-3AE7-4192-BCF4-CB5CA6320908
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>
&#32;
