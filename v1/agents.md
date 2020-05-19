# Agents
What can you do with Agent?
Comm100 Live Chat API enables you to do the followings with the Agent resource. Only agents with **"Manage Agent & Agent Groups"** permission have access to these resources.

### Available Paths

| Method | Name | Path
| --- | --- | ---
| GET | [Get List of Agents](#get-list-of-agents) | /api/v1/livechat/operators
| GET | [Get a Single Agent](#get-a-single-agent) | /api/v1/livechat/operators/{email}
| POST | [Create a New Agent](#create-a-new-agent) | /api/v1/livechat/operators
| PUT | [Update an Agent](#update-an-agent) | /api/v1/livechat/operators/{email}
| PUT | [Reset an API Key](#reset-an-api-key) | /api/v1/livechat/operators/{email}/reset_api_key
| DELETE | [Remove an Agent](#remove-an-agent) | /api/v1/livechat/operators/{email}

## Get List of Agents
Gets a list of agents.

### Path
```shell
GET https://hosted.comm100.com/api/v1/livechat/operators
```

### Response
| Property | Description
| --- | ---
| `id`| the id of the agent
| `display_name` | the name of the agent
| `email` | the email of the agent
| `status` | the status of the agent, int `0` indicates online, `1` indicates away, `2` indicates offline
| `ongoing_chats`| the total number of ongoing chats the agent has
| `departments` | the departments the agent belongs to
| `max_chats_count` | the maximum number of concurrent chats that will be automatically routed to the agent when Auto Accept Chat Requests is enabled

### Example
Sample request:
```shell
curl "https://hosted.comm100.com/api/v1/livechat/operators" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
[
    {
        "api_key": "ef43f9362aac4f60ad428cb4d072f2c8", 
        "departments": [
            1,
            2
        ],
        "email": "tester@comm100.com",
        "id" : 1,
        "max_chats_count": 5,
        "name": "tester",
        "ongoing_chats": 2,
        "status": 0
    },
    {
        "api_key": "5ce7c8010251448f91b7eedc7931c1e9", 
        "departments": [
            2,
            3
        ],
        "email": "roy@comm100.com",
        "id": 2, 
        "max_chats_count": 5,
        "name": "roy",
        "ongoing_chats": 0,
        "status": 1
    },
    ...
]
```

## Get a Single Agent
Gets specific agent by email.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/operators/{email}
```

### Parameters
| Property | Description
| --- | ---
| `email`| the email of the agent

### Response
| Property | Description
| --- | ---
| `first_name` | the first name of the agent
| `last_name` | the last name of the agent
| `phone` | the phone of the agent
| `title` | the title of the agent
| `description` | the description of the agent
| `is_admin` | whether the agent is an administrator
| `is_active` | whether the agent is active

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/operators/tester@comm100.com" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "api_key": "ef43f9362aac4f60ad428cb4d072f2c8",
    "departments": [ 
        1,
        2
    ], 
    "description": "live chat support",
    "display_name": "tester",
    "email": "tester@comm100.com",
    "first_name": "tester",
    "id": 1, 
    "is_active": true,
    "is_admin": true,
    "last_name": "Comm100",
    "max_chats_count": 5,
    "ongoing_chats": 0, 
    "phone": "1-877-305-0464",
    "status": 0,
    "title": "support",
}
```

## Create a New Agent
Creates a new agent.

### Path

    POST https://hosted.comm100.com/api/v1/livechat/operators

### Parameters
| Property | Mandatory | Description
| --- | ---
| `email`| yes | the email of the agent(Email must be unique)
| `password` | yes | the password of the agent
| `display_name` | yes | the display name of the agent
| `first_name` | yes | the first name of the agent
| `last_name` | yes | the last name of the agent
| `phone` | no | the phone of the agent
| `title` | no | the title of the agent
| `description` | no | the description of the agent
| `is_admin` | no | defaults to `false`
| `is_active` | no | defaults to `true`
| `depsrtments` | no | defaults to `null`
| `max_chats_count` | no | defaults to `3`. Note: This setting only works when you separately set max chat count for each operator. If you set the max chat count together for all agents, you need to set in your Comm100 account.

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/operators" \
    -X POST \
    -d "email=kelly@comm100.com&display_name=Kelly_Comm100&first_name=Kelly \
        &last_name=Blair&password=Comm100&departments=1,2&max_chats_count=5" \
    –u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{ 
    "api_key": "20d35dc30a204892b7d78d1acdf1298e",
    "departments": [ 
        1,
        2
    ], 
    "description": "",
    "display_name": "Kelly_Comm100",
    "email": "kelly@comm100.com",
    "first_name": "Kelly",
    "id": 2, 
    "is_active": true,
    "is_admin": false,
    "last_name": "Blair",
    "max_chats_count": 5,
    "ongoing_chats": 0, 
    "phone": "1-877-305-0464",
    "status": 2,
    "title": ""
}
```
## Update an Agent
Updates a specified agent. 

### Path
```bash
POST https://hosted.comm100.com/api/v1/livechat/operators/{email}
```

## Reset an API Key
Reset the API key of a specific agent.

### Path
```bash
PUT https://hosted.comm100.com/api/v1/livechat/operators/{email}/reset_api_key
```

### Parameters
| Property | Description
| --- | ---
| `email` | the email of the agent

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/operators/tester@comm100.com/reset_api_key" \
    -X PUT –u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{ 
    "api_key": "20d35dc30a204892b7d78d1acdf1298e",
    "departments": [ 
        1,
        2
    ], 
    "description": "",
    "display_name": "Kelly_Comm100",
    "email": "tester@comm100.com",
    "first_name": "test",
    "id": 2, 
    "is_active": "true",
    "is_admin": "false",
    "last_name": "Comm100",
    "max_chats_count": 5,
    "ongoing_chats": 0, 
    "phone": "1-877-305-0464",
    "status": 2,
    "title": "support",
}
```

## Remove an Agent
Deletes a specific agent.

### Path
```bash
DELETE https://hosted.comm100.com/api/v1/livechat/operators/{email}
```

### Parameters
| Property | Description
| --- | ---
| `email` | the email of the agent

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/operators/roy@comm100.com" \
    -X DELETE –u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "result": "Operator 'roy@comm100.com' has been removed."
}
```