# Global Restfull API

  | Change Version | API Version | Change notes | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v3 |  | 2020-02-17 | Hardy |

# Summary

- Global
  - [site](#site) Get PUT
  - [agent](#agent) include role, permission, shift  Get ../agents
    - [permission](#permission)
    - [shift](#shift)
  - [role](#role) include agent, permission
    - [agent](#agent)
    - [permission](#permission)
  - [department](#department) include agent, shift
    - [agent](#agent)  ../departments/{depid}/agents
    - [shift](#shift)
  - [contact](#contact)
    - [contact identity](#contact-identity)
  - [visitor](#visitor)  GetList, GetbyId
  - [public canned message category](#public-canned-message-category)
  - [public canned message](#public-canned-message)
  - [private canned message category](#private-canned-message-category)
  - [private canned message](#private-canned-message)
  - [agent away status](#agent-away-status)
  - [whitelisted login IP range](#whitelisted-login-ip-range)
  - [agent sso](#agent-sso) include agent Get, PUT
  - [visitor sso](#visitor-sso) Get, PUT
  - [shift](#shift)
  - [oauth client](#oauth-client) Get  ? 这个接口怎么处理
  - [audit log](#audit-log) include agent;  GetList（分页） Get
  

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
  |`id` | Guid | | yes | N/A | | Id of the current item.  |
  | `name` | string  | | N/A | N/A | | Name of the shift. |
  | `timeZone` | boolean  | | N/A | N/A | | Enum. Time Zone selected for this shift. |
  | `holiday` | [Holiday](#Holiday-Object)[]  | | N/A | N/A | | |
  | `member` | [Agent](#Agent-Object)[] or [Department](#Department-Object)[] | yes | N/A | N/A | | |
  | `workingHours` | [Working Hours](#Working-Hours-Object)[]  | | N/A | N/A | | |

### Holiday Object

  Holiday Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `name` | string  | N/A | N/A | | The name of holiday. |
  | `holiday` | date  | N/A | N/A | | The date of the holiday. |

### Working Hours Object

  Working Hours Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `dayofWeek` | string  | N/A | N/A | | Including `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday` and `sunday`. |
  | `startTime` | datetime  | N/A | N/A | | |
  | `endTime` | datetime  | N/A | N/A | | |
  | `awayStatus` | [Agent Away Status](#Agent-Away-Status-Object)  | N/A | N/A | | |

## Shift Endpoints

### Get all Shifts in site

  `GET /api/v3/globalSettings/shifts`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `department`, `agent` |

#### Response

the response is: [Shift](#Shift-Object) Object

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

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the shift |

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

- `GET /api/v3/globalSettings/visitors` - [Get a list of visitors in site](#get-all-visitors-in-site)
- `GET /api/v3/globalSettings/visitors/{id}` - [Get a visitor by id](#get-a-visitors-by-id)  

## Related Object Json Format

### Visitor Object

  Visitor Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | N/A | N/A | | Name of the visitor. |
  | `email` | string  | N/A | N/A | | Email of the visitor. |
  | `numberOfVisits` | integer  | N/A | N/A | | The total number of web pages the visitor viewed on your website. |
  | `numberOfChats` | integer  | N/A | N/A | | The total times of chats a visitor has made on your website from the first time to present. |
  | `firstVisitTime` | datetime  | N/A | N/A | | The time the visitor first visited a web page pasted with Comm100 Live Chat code. |

## Visitor Endpoints

### Get all visitors in site

  `GET /api/v3/globalSettings/visitors`

#### Response

the response is: [Visitor](#Visitor-Object) Object

### Get a visitors by id

  `GET /api/v3/globalSettings/visitors/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes |  the unique Id of the visitor |

#### Response

the response is: [Visitor](#Visitor-Object) Object

# Public Canned Message Category

  You need `Manage Pulbic Canned Messages` permission to manage canned message category.

- `GET /api/v3/globalSettings/publicCannedMessageCategories` - [Get a list of publicCannedMessageCategories in site](#get-all-Public-Canned-Message-Categories-in-site)
- `GET /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [Get a publicCannedMessageCategory by id](#get-a-Public-Canned-Message-Category-by-id)
- `POST /api/v3/globalSettings/publicCannedMessageCategories` - [create a new publicCannedMessageCategory](#create-a-new-Public-Canned-Message-Category)
- `PUT /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [update a publicCannedMessageCategory](#update-a-Public-Canned-Message-Category)
- `DELETE /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [delete a publicCannedMessageCategory](#delete-a-Public-Canned-Message-Category)

## Related Object Json Format

### Public Canned Message Category Object

  Public Canned Message Category Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | N/A | yes | | Name of the canned message category. |
  | `parent` | [Public Canned Message Category](#Public-Canned-Message-Category-Object) | N/A | yes | | Parent of the canned message category. |
  | `createBy` | [Agent](#Agent-Object)  | N/A | N/A | | Which agent create the current item. |

## Public Canned Message Endpoints

### Get all Public Canned Message Categories in site

  `GET /api/v3/globalSettings/publicCannedMessageCategories`

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

### Get a Public Canned Message Category by id

  `GET /api/v3/globalSettings/publicCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message category |

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

### Create a new Public Canned Message Category

  `POST /api/v3/globalSettings/publicCannedMessageCategories`

#### Parameters

Request Body

  The request body contains data with the [Public Canned Message Category](#Public-Canned-Message-Category-Object) structure

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

### Update a Public Canned Message Category

  `PUT /api/v3/globalSettings/publicCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message category |

Request Body

  The request body contains data with the [Public Canned Message Category](#Public-Canned-Message-Category-Object) structure

#### Response

the response is: [Public Canned Message Category](#Public-Canned-Message-Category-Object) Object

### Delete a Public Canned Message Category

  `DELETE /api/v3/globalSettings/publicCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message category |

#### Response

HTTP/1.1 204 No Content

# Public Canned Message

  You need `Manage Pulbic Canned Messages` permission to manage canned message.

- `GET /api/v3/globalSettings/publicCannedMessages` - [Get a list of publicCannedMessages in site](#get-all-Public-Canned-Messages-in-site)
- `GET /api/v3/globalSettings/publicCannedMessages/{id}` - [Get a publicCannedMessage by id](#get-a-Public-Canned-Message-by-id)
- `POST /api/v3/globalSettings/publicCannedMessages` - [create a new publicCannedMessage](#create-a-new-Public-Canned-Message)
- `PUT /api/v3/globalSettings/publicCannedMessages/{id}` - [update a publicCannedMessage](#update-a-Public-Canned-Message)
- `DELETE /api/v3/globalSettings/publicCannedMessages/{id}` - [delete a publicCannedMessage](#delete-a-Public-Canned-Message)

## Related Object Json Format

### Public Canned Message Object

  Public Canned Message Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | N/A | | Id of the current item.  |
  | `name` | string | | N/A | yes | | Name of the canned message. |
  | `message` | string | | N/A | yes | | |
  | `IfSetHTMLMessageForEmail` | boolean  | | N/A | N/A | false | |
  | `HTMLMessage` | string  | | N/A | N/A | | |
  | `category` | [Public Canned Message Category](#Public-Canned-Message-Category-Object)  | yes | N/A | N/A | |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `publicCannedMessageCategory` is included. |
  | `createBy` | [Agent](#Agent-Object)  | | N/A | N/A | | Which agent create the current item. |
  | `shortcuts` | string  | | N/A | N/A | | Whether the custom away status is system or not. |
  | `channel` | string  | | N/A | N/A | `email` | Include `default`,`email`. The default channel canned message works for all channel. Email channel canned message only works for Email channel. If a specific Channel is not added, use the Default Channel Canned Messages. |
  | `similarQuestion` | [Similar Question](#Similar-Question-Object)[]  | | N/A | N/A | | Available when Agent Assist is enabled. |

### Similar Question Object

  Similar Question Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `question` | string  | N/A | N/A | | |

## Public Canned Message Endpoints

### Get all Public Canned Messages in site

  `GET /api/v3/globalSettings/publicCannedMessages`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `publicCannedMessageCategory` |

#### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

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

##### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

### Create a new Public Canned Message

  `POST /api/v3/globalSettings/publicCannedMessages`

#### Parameters

Request Body

  The request body contains data with the [Public Canned Message](#Public-Canned-Message-Object) structure

#### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

### Update a Public Canned Message

  `PUT /api/v3/globalSettings/publicCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message |

Request Body

  The request body contains data with the [Public Canned Message](#Public-Canned-Message-Object) structure

#### Response

the response is: [Public Canned Message](#Public-Canned-Message-Object) Object

### Delete a Public Canned Message

  `DELETE /api/v3/globalSettings/publicCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the public canned message |

#### Response

HTTP/1.1 204 No Content

# Private Canned Message Category

- `GET /api/v3/globalSettings/privateCannedMessageCategories` - [Get a list of privateCannedMessageCategories in site](#get-all-Private-Canned-Message-Categories-in-site)
- `GET /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [Get a privateCannedMessageCategory by id](#get-a-Private-Canned-Message-Category-by-id)
- `POST /api/v3/globalSettings/privateCannedMessageCategories` - [create a new privateCannedMessageCategory](#create-a-new-Private-Canned-Message-Category)
- `PUT /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [update a privateCannedMessageCategory](#update-a-Private-Canned-Message-Category)
- `DELETE /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [delete a privateCannedMessageCategory](#delete-a-Private-Canned-Message-Category)

## Related Object Json Format

### Private Canned Message Category Object

  Private Canned Message Category Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | N/A | yes | | Name of the canned message category. |
  | `parent` | string  | N/A | yes | | Parent of the canned message category. |
  | `createBy` | [Agent](#Agent-Object)  | N/A | N/A | | Which agent create the current item. |

## Private Canned Message Category Endpoints

### Get all Private Canned Message Categories in site

  `GET /api/v3/globalSettings/privateCannedMessageCategories`

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

### Get a Private Canned Message Category by id

  `GET /api/v3/globalSettings/privateCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message category |

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

### Create a new Private Canned Message Category

  `POST /api/v3/globalSettings/privateCannedMessageCategories`

#### Parameters

Request Body

  The request body contains data with the [Private Canned Message Category](#Private-Canned-Message-Category-Object) structure

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

### Update a Private Canned Message Category

  `PUT /api/v3/globalSettings/privateCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message category |

Request Body

  The request body contains data with the [Private Canned Message Category](#Private-Canned-Message-Category-Object) structure

#### Response

the response is: [Private Canned Message Category](#Private-Canned-Message-Category-Object) Object

### Delete a Private Canned Message Category

  `DELETE /api/v3/globalSettings/privateCannedMessageCategories/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message category |

#### Response

HTTP/1.1 204 No Content

# Private Canned Message

- `GET /api/v3/globalSettings/privateCannedMessages` - [Get a list of privateCannedMessages in site](#get-all-Private-Canned-Messages-in-site)
- `GET /api/v3/globalSettings/privateCannedMessages/{id}` - [Get a privateCannedMessage by id](#get-a-Private-Canned-Message-by-id)
- `POST /api/v3/globalSettings/privateCannedMessages` - [create a new privateCannedMessage](#create-a-new-Private-Canned-Message)
- `PUT /api/v3/globalSettings/privateCannedMessages/{id}` - [update a privateCannedMessage](#update-a-Private-Canned-Message)
- `DELETE /api/v3/globalSettings/privateCannedMessages/{id}` - [delete a privateCannedMessage](#delete-a-Private-Canned-Message)

## Related Object Json Format

### Private Canned Message Object

  Private Canned Message Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | N/A | | Id of the current item.  |
  | `name` | string  | | N/A | N/A | | Name of the canned message. |
  | `message` | string  | | N/A | N/A | | |
  | `IfSetHTMLMessageForEmail` | boolean  | | N/A | N/A | false | |
  | `HTMLMessage` | string  | | N/A | N/A | | |
  | `category` | [Private Canned Message Category](#Private-Canned-Message-Category-Object)  | yes | N/A | N/A | |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `privateCannedMessageCategory` is included. |
  | `createBy` | [Agent](#Agent-Object)  | | N/A | N/A | | Which agent create the current item. |
  | `shortcuts` | string  | | N/A | N/A | | Whether the custom away status is system or not. |
  | `channel` | string  | | N/A | N/A | `email` | Include `default`,`email`. The default channel canned message works for all channel. Email channel canned message only works for Email channel. If a specific Channel is not added, use the Default Channel Canned Messages. |
  | `similarQuestion` | [Similar Question](#Similar-Question-Object)[]  | | N/A | N/A | | Available when Agent Assist is enabled. |

## Private Canned Message Endpoints

### Get all Private Canned Messages in site

  `GET /api/v3/globalSettings/privateCannedMessages`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `privateCannedMessageCategory` |

#### Response

the response is: [Private Canned Message](#Private-Canned-Message-Object) Object

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

### Create a new Private Canned Message

  `POST /api/v3/globalSettings/privateCannedMessages`

#### Parameters

Request Body

  The request body contains data with the [Private Canned Message](#Private-Canned-Message-Object) structure

#### Response

the response is: [Private Canned Message](#Private-Canned-Message-Object) Object

### Update a Private Canned Message

  `PUT /api/v3/globalSettings/privateCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message |

Request Body

  The request body contains data with the [Private Canned Message](#Private-Canned-Message-Object) structure

#### Response

the response is: [Private Canned Message](#Private-Canned-Message-Object) Object

### Delete a Private Canned Message

  `DELETE /api/v3/globalSettings/privateCannedMessages/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the private canned message |

#### Response

HTTP/1.1 204 No Content

#### Similar Question Object

  Similar Question Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `question` | string  | N/A | N/A | | |

# Agent Away Status

  You need `Manage Settings` permission to manage visitor.

- `GET /api/v3/globalSettings/agentAwayStatuses` - [Get a list of agentAwayStatuses in site](#get-all-Agent-Away-Status-in-site)
- `GET /api/v3/globalSettings/agentAwayStatuses/{id}` - [Get an agentAwayStatus by id](#get-a-Agent-Away-Status-by-id)
- `POST /api/v3/globalSettings/agentAwayStatuses` - [create a new agentAwayStatus](#create-a-new-Agent-Away-Status)
- `PUT /api/v3/globalSettings/agentAwayStatuses/{id}` - [update an agentAwayStatus](#update-a-Agent-Away-Status)
- `DELETE /api/v3/globalSettings/agentAwayStatuses/{id}` - [delete an agentAwayStatus](#delete-a-Agent-Away-Status)

## Related Object Json Format

### Agent Away Status Object

  Agent Away Status Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | N/A | | Id of the current item.  |
  | `name` | string  | N/A | yes | | Name of the agent away status. |
  | `isSystem` | boolean  | N/A | N/A | | Whether the agent away status is system or not. |
  | `order` | integer  | N/A | N/A | | The order of the agent away status. |

## Agent Away Status Endpoints

### Get all Agent Away Status of a site

  `GET /api/v3/globalSettings/agentAwayStatuses`

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

### Get a Agent Away Status by id

  `GET /api/v3/globalSettings/agentAwayStatuses/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the agent away status |

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

### Create a new Agent Away Status

  `POST /api/v3/globalSettings/agentAwayStatuses`

#### Parameters

Request Body

  The request body contains data with the [Agent Away Status](#Agent-Away-Status-Object) structure

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

### Update a Agent Away Status

  `PUT /api/v3/globalSettings/agentAwayStatuses/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the agent away status |

Request Body

  The request body contains data with the [Agent Away Status](#Agent-Away-Status-Object) structure

#### Response

the response is: [Agent Away Status](#Agent-Away-Status-Object) Object

### Delete a Agent Away Status

  `DELETE /api/v3/globalSettings/agentAwayStatuses/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the agent away status |

#### Response

HTTP/1.1 204 No Content

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

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `isEnabled` | boolean  | N/A | N/A | | |
  | `protocolType` | string  | N/A | N/A | | including `SAMLSSO` and `JWTSSO`. |
  | `SAMLSSOURL` | string  | N/A | N/A | |Only available when Type is SAML SSO. |
  | `SAMLLogoutURL` | string  | N/A | N/A | | Only available when Type is SAML SSO. |
  | `SAMLCertificateFile` | string  | N/A | N/A | | File key of SAML certificate file, Only available when Type is SAML SSO. |
  | `SAMLCertificateFileName` | string  | N/A | N/A | | Only available when Type is SAML SSO. |
  | `JWTLoginURL` | string  | N/A | N/A | | Only available when Type is JWT SSO. |
  | `JWTLogoutURL` | string  | N/A | N/A | | Only available when Type is JWT SSO.  |
  | `JWTSecret` | string  | N/A | N/A | | Only available when Type is JWT SSO.  |
  | `createdTime` | datetime  | yes | N/A | | API does not need to provide it. |
  | `createdBy` | [Agent](#Agent-Object)  | yes | N/A | | Which agent create the current item. API does not need to provide it. |
  | `lastUpdatedTime` | datetime  | yes | N/A | | API does not need to provide it. |
  | `lastUpdatedBy:` | [Agent](#Agent-Object)  | yes | N/A | | Which agent update the current item last time. API does not need to provide it. |

## Agent SSO Endpoints

### Get Agent SSO

  `GET /api/v3/globalSettings/agentSSO`

#### Response

the response is: [Agent SSO](#Agent-SSO-Object) Object

### Update Agent SSO

  `PUT /api/v3/globalSettings/agentSSO`

#### Parameters

Request Body

  The request body contains data with the [Agent SSO](#Agent-SSO-Object) structure

#### Response

the response is: [Agent SSO](#Agent-SSO-Object) Object

# Visitor SSO  

  You need `Manage Settings` permission to setting sso for a site.

- `GET /api/v3/globalSettings/visitorSSO` - [Get Visitor SSO](#get-visitor-sso)
- `PUT /api/v3/globalSettings/visitorSSO` - [update Visitor SSO](#update-visitor-sso)

## Related Object Json Format

### Visitor SSO Object

  Visitor SSO Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `isEnabled` | boolean  | | N/A | N/A | | |
  | `loginURL` | string  | | N/A | N/A | | |
  | `logoutURL` | string  | | N/A | N/A | | |
  | `changePasswordURL` | string  | | N/A | N/A | | |
  | `certificateFile` | string  | | N/A | N/A | | File key of certificate file. |
  | `certificateFileName` | string  | | N/A | N/A | | |
  | `fieldMappings` | [Agent](#Field-Mapping-Object)[]  | | N/A | N/A | | |
  | `perCampaign` | [Agent](#Visitor-SSO-Campaign-Object)[]  | yes | N/A | N/A | | |

### Field Mapping Object

Field Mapping is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Default | Description |
  | - | - | :-: | :-: | - |
  | `attribute` | string  | N/A | yes | SSO attribute name. |
  | `comm100Field` | [Live Chat Field](#Live-Chat-Field-Object) or [Custom Variable](#Custom-Variable-Object) | N/A | yes | Id of the Comm100 field. |

### Visitor SSO Campaign Object

Visitor SSO Campaign is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Default | Description |
  | - | - | :-: | :-: | - |
  | `campaign` | [Campaign](#Campaign-Object)  | yes | N/A | Id of the campaign. |
  | `signInOption` | string  | N/A | N/A | Type of the sign in, including `noSignIn`, `signInOptional` and `signInRequired`. |
  | `isPrechatFromSkipped` | boolean  | N/A | N/A | Whether the pre-chat form is skipped when visitors sign in. |

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

### Update Visitor SSO

  `PUT /api/v3/globalSettings/visitorSSO`

#### Parameters

Request Body

  The request body contains data with the [Visitor SSO](#Visitor-SSO-Object) structure

#### Response

the response is: [Visitor SSO](#Visitor-SSO-Object) Object

# Audit Log
  + `GET /api/v3/globalSettings/auditLogs` - [Get audit logs list](#get-an-agent) include agent
  https://www.comm100.com/doc/api/introduction.htm#/Account?id=audit-logs