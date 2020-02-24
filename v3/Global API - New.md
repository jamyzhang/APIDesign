# Global Restfull API

  | Change Version | API Version | Change notes | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v3 |  | 2020-02-17 | Hardy |

# Summary

- Global
  - [site](#site)
  - [agent](#agent)
    - [permission](#permission)
    - [shift](#shift)
  - [role](#role)
    - [agent](#agent)
    - [permission](#permission)
  - [department](#department)
    - [agent](#agent)
    - [shift](#shift)
  - [contact](#contact)
    - [contact identity](#contact-identity)
  - [visitor](#visitor)
  - [public canned message category](#public-canned-message-category)
  - [public canned message](#public-canned-message)
  - [private canned message category](#private-canned-message-category)
  - [private canned message](#private-canned-message)
  - [agent away status](#agent-away-status)
  - [whitelisted login IP range](#whitelisted-login-ip-range)
  - [agent sso](#agent-sso)
  - [visitor sso](#visitor-sso)
  - [shift](#shift)
  - [audit log](#audit-log)
  

# Site
  You need `Manage Site` permission to manage site 
  + `GET /api/v3/globalSettings/site` - [Get profile of a single site](#get-site-info)
  + `PUT /api/v3/globalSettings/site` - [Update profile of a site](#update-site-info)

# Agent
  + `GET /api/v3/globalSettings/agents` - [Get a list of agents in site](#get-all-agents)  include department, role
  + `GET /api/v3/globalSettings/agents/{id}` - [Get an agent by id](#get-an-agent)  include department, role
  + `GET /api/v3/globalSettings/roles/{roleId}/agents` - [Get a list of agents by role id](#get-an-agent)  include department, role
  + `GET /api/v3/globalSettings/departments/{departmentId}/agents` - [Get a list of agents by department id](#get-an-agent)  include department, role
  + `GET /api/v3/globalSettings/agents/me` - [Get current agent](#get-current-agent)  include department, role
  + `POST /api/v3/globalSettings/agents` - [create a new agent](#get-all-agents)
  + `POST /api/v3/globalSettings/agents/{id}:unlock` - [unlock the agent](#get-all-agents)
  + `POST /api/v3/globalSettings/agents/{id}:changePassword` - [Admin set an agent's password](#get-all-agents)
  + `PUT /api/v3/globalSettings/agents/{id}` - [update an agent](#get-all-agents)
  + `PUT /api/v3/globalSettings/agents/me` - [update current agent](#get-all-agents)
  + `POST /api/v3/globalSettings/agents/me:changePassword` - [Change own password](#get-all-agents)
  + `DELETE /api/v3/globalSettings/agents/{id}` - [delete an agent](#get-all-agents)

# Role
  + `GET /api/v3/globalSettings/roles` - [Get a list of roles in site](#get-all-roles)  include agent, permission
  + `GET /api/v3/globalSettings/roles/{id}` - [Get a role by id](#get-an-agent) include agent, permission
  + `POST /api/v3/globalSettings/roles` - [create a new role](#get-all-agents)
  + `PUT /api/v3/globalSettings/roles/{id}` - [update a role](#get-all-agents)
  + `DELETE /api/v3/globalSettings/roles/{id}` - [delete a role](#get-all-agents)

# Department
  + `GET /api/v3/globalSettings/departments` - [Get a list of departments in site](#get-all-departments) include agent
  + `GET /api/v3/globalSettings/departments/{id}` - [Get a department by id](#get-an-agent) include agent
  + `POST /api/v3/globalSettings/departments` - [create a new department](#get-all-agents)
  + `PUT /api/v3/globalSettings/departments/{id}` - [update a department](#get-all-department)
  + `DELETE /api/v3/globalSettings/departments/{id}` - [delete a department](#get-all-departments)

# Permission
  + `GET /api/v3/globalSettings/roles/{roleId}/permission` - [Get role permission](#get-an-agent)
  + `GET /api/v3/globalSettings/agents/{agentId}/permission` - [Get agent permission](#get-an-agent)
  + `GET /api/v3/globalSettings/agents/{agentId}/permission:effective` - [Get a list of agent's effective permissions,including the permissions of the agent and the permissions of the roles which the agent belongs to](#get-an-agent) 
  + `PUT /api/v3/globalSettings/roles/{roleId}/permission` - [update role permission](#get-all-agents)
  + `PUT /api/v3/globalSettings/agents/{agentId}/permission` - [update agent permission](#get-all-agents)
  
# Shift

- `GET /api/v3/globalSettings/shifts` - [Get a list of shifts in site](#get-all-shifts-in-site)
- `GET /api/v3/globalSettings/departments/{departmentId}/shifts` - [Get a list of shift by department id](#get-a-shift-by-department-id)
- `GET /api/v3/globalSettings/agents/{agentId}/shifts` - [Get a list of shifts by agent id](#get-a-shift-by-agent-id)
- `GET /api/v3/globalSettings/shifts/{id}` - [Get a shift by id](#get-a-shift-by-id)
- `POST /api/v3/globalSettings/shifts` - [create a new shift](#create-a-new-shift)
- `PUT /api/v3/globalSettings/shifts/{id}` - [update a shift](#update-a-shift)
- `DELETE /api/v3/globalSettings/shifts/{id}` - [delete a shift](#delete-a-shift)

## Related Object Json Format

### Shift Object

  Shift Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | no | | Id of the current item.  |
  | `name` | string  | | no | no | | Name of the shift. |
  | `timeZone` | boolean  | | no | no | | Enum. Time Zone selected for this shift. |
  | `holidays` | [Holiday](#Holiday-Object)[]  | | no | no | | |
  | `members` | [Agent](#Agent-Object)[] or [Department](#Department-Object)[] | yes | no | no | | |
  | `workingHours` | [Working Hours](#Working-Hours-Object)[]  | | no | no | | |

### Holiday Object

  Holiday Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `name` | string  | no | no | | The name of holiday. |
  | `holiday` | date  | no | no | | The date of the holiday. |

### Working Hours Object

  Working Hours Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `dayofWeek` | string  | no | no | | Including `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday` and `sunday`. |
  | `startTime` | datetime  | no | no | | |
  | `endTime` | datetime  | no | no | | |
  | `awayStatus` | [Agent Away Status](#Agent-Away-Status-Object)  | no | no | | |

## Shift Endpoints

### Get all Shifts in site

  `GET /api/v3/globalSettings/shifts`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `department`, `agent` |

#### Response

the response is: list of [Shift](#Shift-Object) Object

### Get a Shift by id

  `GET /api/v3/livechat/shift/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message |

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `department`, `agent` |

#### Response

the response is: [Shift](#Shift-Object) Object

### Get a Shift by department id

  `GET /api/v3/globalSettings/departments/{departmentId}/shifts`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `departmentId` | Guid | yes  |  the unique Id of the department |

#### Response

the response is: [Shift](#Shift-Object) Object

### Get a Shift by agent id

  `GET /api/v3/globalSettings/agents/{agentId}/shifts`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `agentId` | Guid | yes  |  the unique Id of the agent |

#### Response

the response is: [Shift](#Shift-Object) Object

### Create a new Shift

  `POST /api/v3/globalSettings/shifts`

#### Parameters

Request Body

  The request body contains data with the [Shift](#Shift-Object) structure

#### Response

the response is: [Shift](#Shift-Object) Object

### Update a Shift

  `PUT /api/v3/globalSettings/shifts/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the shift |

Request Body

  The request body contains data with the [Shift](#Shift-Object) structure

#### Response

the response is: [Shift](#Shift-Object) Object

### Delete a Shift

  `DELETE /api/v3/globalSettings/shifts/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the shift |

#### Response

HTTP/1.1 204 No Content

# Contact
?? 根据ssoId 查询 contact (查看 zendesk api)
  + `GET /api/v3/globalSettings/contacts` - [Get a list of contacts in site](#get-all-contacts)  通过 query string 来实现复杂查询
  + `GET /api/v3/globalSettings/contacts/{id}` - [Get a contact by id](#get-an-contact)
  + `POST /api/v3/globalSettings/contacts` - [create a new contact](#get-all-agents)
  + `PUT /api/v3/globalSettings/contacts/{id}` - [update a contact](#get-all-agents)
  + `DELETE /api/v3/globalSettings/contacts/{id}` - [delete a contact](#get-all-agents)

# Contact Identity
  + `GET /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [Get a list of contactIdentities in a contact](#get-all-agents)
  + `GET /api/v3/globalSettings/contactIdentities/{id}` - [Get a contactIdentity by id](#get-an-agent)
  + `POST /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [create a new contactIdentity](#get-all-agents)
  + `PUT /api/v3/globalSettings/contactIdentities/{id}` - [update a contactIdentity](#get-all-agents)
  + `DELETE /api/v3/globalSettings/contactIdentities/{id}` - [delete a contactIdentity](#get-all-agents)

# Visitor

  You need `Manage Settings` permission to manage visitor.

- `GET /api/v3/globalSettings/visitors` - [Get all visitors in site](#get-all-visitors-in-site)
- `GET /api/v3/globalSettings/visitors/{id}` - [Get a visitor by id](#get-a-visitor-by-id)  

## Related Object Json Format

### Visitor Object

  Visitor Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | yes | N/A | | Name of the visitor. |
  | `email` | string  | yes | N/A | | Email of the visitor. |
  | `numberOfVisits` | integer  | yes | N/A | | The total number of web pages the visitor viewed on your website. |
  | `numberOfChats` | integer  | yes | N/A | | The total times of chats a visitor has made on your website from the first time to present. |
  | `firstVisitTime` | datetime  | yes | N/A | | The time the visitor first visited a web page pasted with Comm100 Live Chat code. |

## Visitor Endpoints

### Get all visitors in site

  `GET /api/v3/globalSettings/visitors`

#### Parameters

    no parameters

#### Response

the response is: list of [Visitor](#Visitor-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/visitors
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "name": "test",
        "email": "",
        "numberOfVisits": 4,
        "numberOfChats": 1,
        "firstVisitTime": "2019-06-12T07:41:40.486Z"
    },
    ...
]
```

### Get a visitor by id

  `GET /api/v3/globalSettings/visitors/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes |  the unique Id of the visitor |

#### Response

the response is: [Visitor](#Visitor-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/visitors/7273e957-02cb-4c03-a84c-44283fcfd47d
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
  "name": "test",
  "email": "",
  "numberOfVisits": 4,
  "numberOfChats": 1,
  "firstVisitTime": "2019-06-12T07:41:40.486Z"
}
```

# Public Canned Message Category

  You need `Manage Pulbic Canned Messages` permission to manage canned message category.

- `GET /api/v3/globalSettings/publicCannedMessageCategories` - [Get all public canned message categories in site](#get-all-Public-Canned-Message-Categories-in-site)
- `GET /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [Get a public canned message category by id](#get-a-Public-Canned-Message-Category-by-id)
- `POST /api/v3/globalSettings/publicCannedMessageCategories` - [create a new public canned message category](#create-a-new-Public-Canned-Message-Category)
- `PUT /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [update a public canned message category](#update-a-Public-Canned-Message-Category)
- `DELETE /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [delete a public canned message category](#delete-a-Public-Canned-Message-Category)

## Related Object Json Format

### Public Canned Message Category Object

  Public Canned Message Category Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | no | yes | | Name of the canned message category. |
  | `parentId` | Guid | no | yes | | Id of the public canned message category. |
  | `createdBy` | Guid | N/A | N/A | | Which agent create the current item. |

## Public Canned Message Endpoints

### Get all Public Canned Message Categories in site

  `GET /api/v3/globalSettings/publicCannedMessageCategories`

#### Parameters

    no parameters

#### Response

the response is: list of [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/publicCannedMessageCategories
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
        "name": "puddddtresult",
        "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC",
        "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
    },
    ...
]
```

### Get a Public Canned Message Category by id

  `GET /api/v3/globalSettings/publicCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message category |

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/publicCannedMessageCategories/5A563046-374D-3C4E-4D4A-2CA3812A42C8
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "name": "puddddtresult",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
}
```

### Create a new Public Canned Message Category

  `POST /api/v3/globalSettings/publicCannedMessageCategories`

#### Parameters

Request Body

  The request body contains data with the [Public Canned Message Category](#Public-Canned-Message-Category-Object) structure

example:
```Json
{
  "name": "testtest",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "testtest",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/publicCannedMessageCategories
```

Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
  "id": "7D3E7435-F956-29FE-C089-57241AFBB297",
  "name": "testtest",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
}
```

### Update a Public Canned Message Category

  `PUT /api/v3/globalSettings/publicCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message category |

Request Body

  The request body contains data with the [Public Canned Message Category](#Public-Canned-Message-Category-Object) structure

example:
```Json
{
  "name": "testtest22222",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "testtest22222",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/publicCannedMessageCategories/7D3E7435-F956-29FE-C089-57241AFBB297
```

Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
  "id": "7D3E7435-F956-29FE-C089-57241AFBB297",
  "name": "testtest22222",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
}
```

### Delete a Public Canned Message Category

  `DELETE /api/v3/globalSettings/publicCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message category |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/publicCannedMessageCategories/7D3E7435-F956-29FE-C089-57241AFBB297
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Public Canned Message

  You need `Manage Pulbic Canned Messages` permission to manage canned message.

- `GET /api/v3/globalSettings/publicCannedMessages` - [Get all public canned messages in site](#get-all-Public-Canned-Messages-in-site)
- `GET /api/v3/globalSettings/publicCannedMessages/{id}` - [Get a public canned message by id](#get-a-Public-Canned-Message-by-id)
- `POST /api/v3/globalSettings/publicCannedMessages` - [create a new public canned message](#create-a-new-Public-Canned-Message)
- `PUT /api/v3/globalSettings/publicCannedMessages/{id}` - [update a public canned message](#update-a-Public-Canned-Message)
- `DELETE /api/v3/globalSettings/publicCannedMessages/{id}` - [delete a public canned message](#delete-a-Public-Canned-Message)

## Related Object Json Format

### Public Canned Message Object

  Public Canned Message Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | N/A | | Id of the canned message.  |
  | `name` | string | | no | yes | | Name of the canned message. |
  | `message` | string | | no | yes | | |
  | `IfSetHTMLMessageForEmail` | boolean  | | no | no | false | |
  | `HTMLMessage` | string  | | no | no | | |
  | `categoryId` | Guid | | no | no | | |
  | `category` | [Public Canned Message Category](#Public-Canned-Message-Category-Object)  | yes | no | no | |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `publicCannedMessageCategory` is included. |
  | `createdBy` | Guid | | N/A | N/A | | Which agent create the current item. |
  | `shortcuts` | string  | | no | no | | Whether the custom away status is system or not. |
  | `similarQuestions` | [Similar Question](#Similar-Question-Object)[]  | | no | no | | Available when Agent Assist is enabled. |

### Similar Question Object

  Similar Question Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `question` | string  | no | no | | |

## Public Canned Message Endpoints

### Get all Public Canned Messages in site

  `GET /api/v3/globalSettings/publicCannedMessages`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `publicCannedMessageCategory` |

#### Response

the response is: list of [Public Canned Message](#Public-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages?include=publicCannedMessageCategory
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "C354EA75-BAAF-9994-9307-D001FBE1882A",
        "name": "publicCannedMessageCategory",
        "message": "publicCannedMessageCategory",
        "IfSetHTMLMessageForEmail": false,
        "HTMLMessage": "",
        "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
        "category":    { // include public canned message category
          "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
          "name": "puddddtresult",
         "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC",
          "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
        },
        "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
        "shortcuts": "",
        "similarQuestions": [{
          "question": "are you ok?"
        },
        ...  
        ]
    },
    ...
]
```

### Get a Public Canned Message by id

  `GET /api/v3/globalSettings/publicCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message |

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `publicCannedMessageCategory` |

#### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages/C354EA75-BAAF-9994-9307-D001FBE1882A?include=publicCannedMessageCategory
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "C354EA75-BAAF-9994-9307-D001FBE1882A",
  "name": "publicCannedMessageCategory",
  "message": "publicCannedMessageCategory",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "category":    { // include public canned message category
    "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
    "name": "puddddtresult",
    "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC",
    "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
  },
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  },
  ...  
  ]
}
```

### Create a new Public Canned Message

  `POST /api/v3/globalSettings/publicCannedMessages`

#### Parameters

Request Body

  The request body contains data with the [Public Canned Message](#Public-Canned-Message-Object) structure

example:
```Json
{
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

#### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "19B21FEE-B0C5-2A61-0D34-26FB057D15EE",
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

### Update a Public Canned Message

  `PUT /api/v3/globalSettings/publicCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message |

Request Body

  The request body contains data with the [Public Canned Message](#Public-Canned-Message-Object) structure

example:
```Json
{
  "name": "test11111",
  "message": "test11111",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

#### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "test11111",
  "message": "test11111",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages/19B21FEE-B0C5-2A61-0D34-26FB057D15EE
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "19B21FEE-B0C5-2A61-0D34-26FB057D15EE",
  "name": "test11111",
  "message": "test11111",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

### Delete a Public Canned Message

  `DELETE /api/v3/globalSettings/publicCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages/19B21FEE-B0C5-2A61-0D34-26FB057D15EE
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Private Canned Message Category

- `GET /api/v3/globalSettings/privateCannedMessageCategories` - [Get all private canned message categories in site](#get-all-Private-Canned-Message-Categories-in-site)
- `GET /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [Get a private canned message category by id](#get-a-Private-Canned-Message-Category-by-id)
- `POST /api/v3/globalSettings/privateCannedMessageCategories` - [create a new private canned message category](#create-a-new-Private-Canned-Message-Category)
- `PUT /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [update a private canned message category](#update-a-Private-Canned-Message-Category)
- `DELETE /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [delete a private canned message category](#delete-a-Private-Canned-Message-Category)

## Related Object Json Format

### Private Canned Message Category Object

  Private Canned Message Category Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | no | yes | | Name of the canned message category. |
  | `parentId` | Guid  | no | yes | | Parent of the canned message category. |
  | `createdBy` | Guid | N/A | N/A | | Which agent create the current item. |

## Private Canned Message Category Endpoints

### Get all Private Canned Message Categories in site

  `GET /api/v3/globalSettings/privateCannedMessageCategories`

#### Parameters

    no parameters

#### Response

the response is: list of [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/privateCannedMessageCategories
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "119043D0-76A6-D3C1-B594-493111CE1552",
        "name": "tstestsetsteset",
        "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F",
        "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
    },
    ...
]
```

### Get a Private Canned Message Category by id

  `GET /api/v3/globalSettings/privateCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message category |

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/privateCannedMessageCategories/119043D0-76A6-D3C1-B594-493111CE1552
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "119043D0-76A6-D3C1-B594-493111CE1552",
  "name": "tstestsetsteset",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
}
```

### Create a new Private Canned Message Category

  `POST /api/v3/globalSettings/privateCannedMessageCategories`

#### Parameters

Request Body

  The request body contains data with the [Private Canned Message Category](#Private-Canned-Message-Category-Object) structure

example:
```Json
{
  "name": "testtest111111",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "testtest111111",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/privateCannedMessageCategories
```

Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
  "id": "FFD377AA-81FA-EC53-1E57-DD73C0B36F6C",
  "name": "testtest111111",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
}
```

### Update a Private Canned Message Category

  `PUT /api/v3/globalSettings/privateCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message category |

Request Body

  The request body contains data with the [Private Canned Message Category](#Private-Canned-Message-Category-Object) structure

example:
```Json
{
  "name": "testtest22222",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
}
```

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "testtest22222",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/privateCannedMessageCategories/FFD377AA-81FA-EC53-1E57-DD73C0B36F6C
```

Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
  "id": "FFD377AA-81FA-EC53-1E57-DD73C0B36F6C",
  "name": "testtest22222",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
}
```

### Delete a Private Canned Message Category

  `DELETE /api/v3/globalSettings/privateCannedMessageCategories/{id}`

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/privateCannedMessageCategories/FFD377AA-81FA-EC53-1E57-DD73C0B36F6C
```

Response
```Json
  HTTP/1.1 204 No Content
```

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message category |

#### Response

HTTP/1.1 204 No Content

# Private Canned Message

- `GET /api/v3/globalSettings/privateCannedMessages` - [Get all private canned messages in site](#get-all-Private-Canned-Messages-in-site)
- `GET /api/v3/globalSettings/privateCannedMessages/{id}` - [Get a private canned message by id](#get-a-Private-Canned-Message-by-id)
- `POST /api/v3/globalSettings/privateCannedMessages` - [create a new private canned message](#create-a-new-Private-Canned-Message)
- `PUT /api/v3/globalSettings/privateCannedMessages/{id}` - [update a private canned message](#update-a-Private-Canned-Message)
- `DELETE /api/v3/globalSettings/privateCannedMessages/{id}` - [delete a private canned message](#delete-a-Private-Canned-Message)

## Related Object Json Format

### Private Canned Message Object

  Private Canned Message Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | N/A | | Id of the current item.  |
  | `name` | string  | | no | no | | Name of the canned message. |
  | `message` | string  | | no | no | | |
  | `IfSetHTMLMessageForEmail` | boolean  | | no | no | false | |
  | `HTMLMessage` | string  | | no | no | | |
  | `categoryId` | Guid | | no | no | | |
  | `category` | [Private Canned Message Category](#Private-Canned-Message-Category-Object)  | yes | no | no | |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `privateCannedMessageCategory` is included. |
  | `createdBy` | Guid | | N/A | N/A | | Which agent create the current item. |
  | `shortcuts` | string  | | no | no | | Whether the custom away status is system or not. |
  | `similarQuestions` | [Similar Question](#Similar-Question-Object)[]  | | no | no | | Available when Agent Assist is enabled. |

## Private Canned Message Endpoints

### Get all Private Canned Messages in site

  `GET /api/v3/globalSettings/privateCannedMessages`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `privateCannedMessageCategory` |

#### Response

the response is: list of [Private Canned Message](#Private-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages?include=privateCannedMessageCategory
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "AB71E95A-1FA5-E19D-9BA4-9C2144598C57",
        "name": "privateCannedMessageCategory",
        "message": "privateCannedMessageCategory",
        "IfSetHTMLMessageForEmail": false,
        "HTMLMessage": "",
        "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
        "category":    { // include private canned message category
          "id": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
          "name": "justfortest",
         "parentId": "A73FA2EB-4CE3-B195-94C6-567A24F7BDDC",
          "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
        },
        "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
        "shortcuts": "",
        "similarQuestions": [{
          "question": "are you ok?"
        },
        ...  
        ]
    },
    ...
]
```

### Get a Private Canned Message by id

  `GET /api/v3/globalSettings/privateCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message |

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `privateCannedMessageCategory` |

##### Response

the response is: [Private Canned Message](#Private-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages/AB71E95A-1FA5-E19D-9BA4-9C2144598C57?include=privateCannedMessageCategory
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "C354EA75-BAAF-9994-9307-D001FBE1882A",
  "name": "privateCannedMessageCategory",
  "message": "privateCannedMessageCategory",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "category":    { // include private canned message category
    "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
    "name": "puddddtresult",
    "parentId": "A73FA2EB-4CE3-B195-94C6-567A24F7BDDC",
    "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99"
  },
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  },
  ...  
  ]
}
```

### Create a new Private Canned Message

  `POST /api/v3/globalSettings/privateCannedMessages`

#### Parameters

Request Body

  The request body contains data with the [Private Canned Message](#Private-Canned-Message-Object) structure

example:
```Json
{
  "name": "privateCannedMessageCategorytest1111",
  "message": "privateCannedMessageCategorytest1111",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

#### Response

the response is: [Private Canned Message](#Private-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "privateCannedMessageCategorytest1111",
  "message": "privateCannedMessageCategorytest1111",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F",
  "name": "privateCannedMessageCategorytest1111",
  "message": "privateCannedMessageCategorytest1111",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

### Update a Private Canned Message

  `PUT /api/v3/globalSettings/privateCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message |

Request Body

  The request body contains data with the [Private Canned Message](#Private-Canned-Message-Object) structure

example:
```Json
{
  "name": "privateCannedMessageCategorytest2222",
  "message": "privateCannedMessageCategorytest2222",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

#### Response

the response is: [Private Canned Message](#Private-Canned-Message-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "privateCannedMessageCategorytest2222",
  "message": "privateCannedMessageCategorytest2222",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages/822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F",
  "name": "privateCannedMessageCategorytest2222",
  "message": "privateCannedMessageCategorytest2222",
  "IfSetHTMLMessageForEmail": false,
  "HTMLMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "createdBy": "3C196E14-AC28-4831-A423-5D09D71F2B99",
  "shortcuts": "",
  "similarQuestions": [{
    "question": "are you ok?"
  }]
}
```

### Delete a Private Canned Message

  `DELETE /api/v3/globalSettings/privateCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages/822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F
```

Response
```Json
  HTTP/1.1 204 No Content
```

#### Similar Question Object

  Similar Question Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `question` | string  | no | no | | |

# Agent Away Status

  You need `Manage Settings` permission to manage visitor.

- `GET /api/v3/globalSettings/agentAwayStatuses` - [Get all agent away statuses in site](#get-all-Agent-Away-Statuses-in-site)
- `GET /api/v3/globalSettings/agentAwayStatuses/{id}` - [Get an agent away status by id](#get-a-Agent-Away-Status-by-id)
- `POST /api/v3/globalSettings/agentAwayStatuses` - [create a new agent away status](#create-a-new-Agent-Away-Status)
- `PUT /api/v3/globalSettings/agentAwayStatuses/{id}` - [update an agent away status](#update-a-Agent-Away-Status)
- `DELETE /api/v3/globalSettings/agentAwayStatuses/{id}` - [delete an agent away status](#delete-a-Agent-Away-Status)

## Related Object Json Format

### Agent Away Status Object

  Agent Away Status Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | no | yes | | Name of the agent away status. |
  | `isSystem` | boolean  | no | no | false | Whether the agent away status is system or not. |
  | `order` | integer  | no | no | | The order of the agent away status. |

## Agent Away Status Endpoints

### Get all Agent Away Statuses of a site

  `GET /api/v3/globalSettings/agentAwayStatuses`

#### Parameters

    no parameters

#### Response

the response is: list of [Agent Away Status](#Agent-Away-Status-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
        "name": "agentAwayStatuses",
        "isSystem": false,
        "order": 1
    },
    ...
]
```

### Get a Agent Away Status by id

  `GET /api/v3/globalSettings/agentAwayStatuses/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the agent away status |

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses/BAACB779-2E41-27C5-B23D-1C8F2058862D
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
  "name": "agentAwayStatuses",
  "isSystem": false,
  "order": 1
}
```

### Create a new Agent Away Status

  `POST /api/v3/globalSettings/agentAwayStatuses`

#### Parameters

Request Body

  The request body contains data with the [Agent Away Status](#Agent-Away-Status-Object) structure

example:
```Json
{
  "name": "agentAwayStatuses11",
  "isSystem": false,
  "order": 1
}
```

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "agentAwayStatuses11",
  "isSystem": false,
  "order": 1
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "D4F6BA7F-9BB6-C509-8BB9-0705B3E500F2",
  "name": "agentAwayStatuses11",
  "isSystem": false,
  "order": 1
}
```

### Update a Agent Away Status

  `PUT /api/v3/globalSettings/agentAwayStatuses/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the agent away status |

Request Body

  The request body contains data with the [Agent Away Status](#Agent-Away-Status-Object) structure

example:
```Json
{
  "name": "agentAwayStatuses22",
  "isSystem": false,
  "order": 1
}
```

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "agentAwayStatuses22",
  "isSystem": false,
  "order": 1
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses/D4F6BA7F-9BB6-C509-8BB9-0705B3E500F2
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "D4F6BA7F-9BB6-C509-8BB9-0705B3E500F2",
  "name": "agentAwayStatuses22",
  "isSystem": false,
  "order": 1
}
```

### Delete a Agent Away Status

  `DELETE /api/v3/globalSettings/agentAwayStatuses/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the agent away status |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses/D4F6BA7F-9BB6-C509-8BB9-0705B3E500F2
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Whitelisted Login IP Range
  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges` - [Get a list of whitelistedLoginIPRanges in site](#get-all-contacts) 
  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [Get a whitelistedLoginIPRange by id](#get-an-contact) 
  + `POST /api/v3/globalSettings/whitelistedLoginIPRanges` - [create a new whitelistedLoginIPRange](#get-all-agents)
  + `PUT /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [update a whitelistedLoginIPRange](#get-all-agents)
  + `DELETE /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [delete a whitelistedLoginIPRange](#get-all-agents)

# Agent SSO  

  You need `Manage Settings` permission to setting sso for a site.

- `GET /api/v3/globalSettings/agentSSO` - [Get Agent SSO](#get-agent-sso)
- `PUT /api/v3/globalSettings/agentSSO` - [update Agent SSO](#update-agent-sso)

## Related Object Json Format

### Agent SSO Object

  Agent SSO Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | - | :-: | :-: | :-: | - | 
  | `isEnabled` | boolean  | | no | N/A | false | |
  | `protocolType` | string |  | no | N/A | | including `SAMLSSO` and `JWTSSO`. |
  | `SAMLSSOURL` | string |  | no | N/A | |Only available when Type is SAML SSO. |
  | `SAMLLogoutURL` | string |  | no | N/A | | Only available when Type is SAML SSO. |
  | `SAMLCertificateFile` | string |  | no | N/A | | File key of SAML certificate file, Only available when Type is SAML SSO. |
  | `SAMLCertificateFileName` | string |  | no | N/A | | Only available when Type is SAML SSO. |
  | `JWTLoginURL` | string |  | no | N/A | | Only available when Type is JWT SSO. |
  | `JWTLogoutURL` | string |  | no | N/A | | Only available when Type is JWT SSO.  |
  | `JWTSecret` | string |  | no | N/A | | Only available when Type is JWT SSO.  |

## Agent SSO Endpoints

### Get Agent SSO

  `GET /api/v3/globalSettings/agentSSO`

#### Parameters

    no parameters

#### Response

the response is: [Agent SSO](#Agent-SSO-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/globalSettings/agentSSO
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
    "isEnabled": true,
    "protocolType": "SAMLSSO",
    "SAMLSSOURL": "",
    "SAMLLogoutURL": "",
    "SAMLCertificateFile": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----",
    "SAMLCertificateFileName": "certi.pl",
}
```

### Update Agent SSO

  `PUT /api/v3/globalSettings/agentSSO`

#### Parameters

Request Body

  The request body contains data with the [Agent SSO](#Agent-SSO-Object) structure

 example:
```Json
  {
    "isEnabled": true,
    "protocolType": "JWTSSO",
    "JWTLoginURL": "",
    "JWTLogoutURL": "",
    "JWTSecret": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----"
  }
```

#### Response

the response is: [Agent SSO](#Agent-SSO-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "isEnabled": true,
    "protocolType": "JWTSSO",
    "JWTLoginURL": "",
    "JWTLogoutURL": "",
    "JWTSecret": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----"
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/agentSSO
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

{
    "isEnabled": true,
    "protocolType": "JWTSSO",
    "JWTLoginURL": "",
    "JWTLogoutURL": "",
    "JWTSecret": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----"
}
```

# Visitor SSO  

  You need `Manage Settings` permission to setting sso for a site.

- `GET /api/v3/globalSettings/visitorSSO` - [Get Visitor SSO](#get-visitor-sso)
- `PUT /api/v3/globalSettings/visitorSSO` - [update Visitor SSO](#update-visitor-sso)

## Related Object Json Format

### Visitor SSO Object

  Visitor SSO Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `isEnabled` | boolean  | | no | N/A | false | |
  | `loginURL` | string  | | no | N/A | | |
  | `logoutURL` | string  | | no | N/A | | |
  | `changePasswordURL` | string  | | no | N/A | | |
  | `certificateFile` | string  | | no | N/A | | File key of certificate file. |
  | `certificateFileName` | string  | | no | N/A | | |
  | `fieldMappings` | [Field Mapping](#Field-Mapping-Object)[]  | | no | N/A | | |
  | `perCampaign` | [Visitor SSO Campaign](#Visitor-SSO-Campaign-Object)[]  |  | no | N/A | | |

### Field Mapping Object

Field Mapping is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `attribute` | string | | no | N/A | | SSO attribute name. |
  | `comm100Field` | string | | no | N/A | | the Comm100 field name |

### Visitor SSO Campaign Object

Visitor SSO Campaign is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `campaignId` | Guid |  | no | N/A | | Id of the campaign. |
  | `campaign` | [Campaign](#Campaign-Object)  | yes | N/A | N/A | | Available only when campaign is included  |
  | `signInOption` | string |  | no | N/A | | Type of the sign in, including `noSignIn`, `signInOptional` and `signInRequired`. |
  | `isPrechatFromSkipped` | boolean |  | no | N/A | false | Whether the pre-chat form is skipped when visitors sign in. |

## Visitor SSO Endpoints

### Get Visitor SSO

  `GET /api/v3/globalSettings/visitorSSO`

#### Parameters

Query string

  | Name  | Type | Required | Default | Description |
  | - | - | :-: | :-: | - |
  | `include` | string | no  | |  Available value: `campaign` |

#### Response

the response is: [Visitor SSO](#Visitor-SSO-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/globalSettings/visitorSSO?include=campaign
```
Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json
 
{
    "isEnabled": true,
    "loginURL": "http://www.xzcs11ffffffff1a",
    "logoutURL": "http://www.xzcs11ffffffff1a",
    "changePasswordURL": "http://www.xzcs11ffffffff1a",
    "certificateFile": "amdoamdoaGdmcnRk",
    "certificateFileName": "r.txt",
    "fieldMappings": [
        {
            "attribute": "test999",
            "comm100Field": "{!Visitor.Name}"
        },
        {
            "attribute": "test666",
            "comm100Field": "{!Prechat.Company}"
        }
    ],
    "perCampaign": [
        {
            "campaignId": "cdab2038-1d6c-4fa0-bbf0-17be2e5b39ec",
            "campaign": { //include campaign
                "id":"cdab2038-1d6c-4fa0-bbf0-17be2e5b39ec",
                "name":"testCampaign",
                ...
            },
            "signInOption": "noSignIn",
            "isPrechatFromSkipped": false
        }
    ]
}
```

### Update Visitor SSO

  `PUT /api/v3/globalSettings/visitorSSO`

#### Parameters

Request Body

  The request body contains data with the [Visitor SSO](#Visitor-SSO-Object) structure

example:
```Json
  {
    "isEnabled": true,
    "loginURL": "http://www.xzcs11ffffffff1a",
    "logoutURL": "http://www.xzcs11ffffffff1a",
    "changePasswordURL": "http://www.xzcs11ffffffff1a",
    "certificateFile": "amdoamdoaGdmcnRk",
    "certificateFileName": "r.txt",
    "fieldMappings": [
        {
            "attribute": "test999",
            "comm100Field": "{!Visitor.Name}"
        },
        {
            "attribute": "test666",
            "comm100Field": "{!Prechat.Company}"
        }
    ],
    "perCampaign": [
        {
            "campaignId": "cdab2038-1d6c-4fa0-bbf0-17be2e5b39ec",
            "signInOption": "noSignIn",
            "isPrechatFromSkipped": false
        }
    ]
  }
```

#### Response

the response is: [Visitor SSO](#Visitor-SSO-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "isEnabled": true,
    "loginURL": "http://www.xzcs11ffffffff1a",
    "logoutURL": "http://www.xzcs11ffffffff1a",
    "changePasswordURL": "http://www.xzcs11ffffffff1a",
    "certificateFile": "amdoamdoaGdmcnRk",
    "certificateFileName": "r.txt",
    "fieldMappings": [
        {
            "attribute": "test999",
            "comm100Field": "{!Visitor.Name}"
        },
        {
            "attribute": "test666",
            "comm100Field": "{!Prechat.Company}"
        }
    ],
    "perCampaign": [
        {
            "campaignId": "cdab2038-1d6c-4fa0-bbf0-17be2e5b39ec",
            "signInOption": "noSignIn",
            "isPrechatFromSkipped": false
        }
    ]
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/visitorSSO
```
Response
```Json
  HTTP/1.1 200 OK
  Content-Type:  application/json

  {
    "isEnabled": true,
    "loginURL": "http://www.xzcs11ffffffff1a",
    "logoutURL": "http://www.xzcs11ffffffff1a",
    "changePasswordURL": "http://www.xzcs11ffffffff1a",
    "certificateFile": "amdoamdoaGdmcnRk",
    "certificateFileName": "r.txt",
    "fieldMappings": [
        {
            "attribute": "test999",
            "comm100Field": "{!Visitor.Name}"
        },
        {
            "attribute": "test666",
            "comm100Field": "{!Prechat.Company}"
        }
    ],
    "perCampaign": [
        {
            "campaignId": "cdab2038-1d6c-4fa0-bbf0-17be2e5b39ec",
            "signInOption": "noSignIn",
            "isPrechatFromSkipped": false
        }
    ]
  }
```

# Audit Log
  + `GET /api/v3/globalSettings/auditLogs` - [Get audit logs list](#get-an-agent) include agent
  https://www.comm100.com/doc/api/introduction.htm#/Account?id=audit-logs