# Global Restfull API

  | Change Version | API Version | Change notes | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v3 |  | 2020-02-17 | Hardy, Michael|

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

  + `GET /api/v3/globalSettings/site` - [Get profile of a site](#get-profile-of-a-site)
  + `PUT /api/v3/globalSettings/site` - [Update profile of a site](#update-profile-of-a-site)


## Site Related Object Json Format

### Site Object
  Each Comm100 account is treated as a Site and has a unique Site ID.

 | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
 | - | - | :-: | :-: | :-: | :-: | - |
 |`id` | integer  | | N/A | N/A |  |Site ID.|
 |`dateTimeFormat` | string| | no | N/A  | 'MM-dd-yyyy HH:mm:ss'|Date & Time Format of site, value options include : MM-dd-yyy HH:mm:ss, MM/dd/yyyy HH:mm:ss, dd-MM-yyyy HH:mm:ss, dd/MM/yyyy HH:mm:ss, yyyy-MM-dd HH:mm:ss, yyyy/MM/dd HH:mm:ss |
 |`timeZone` | string| | no | N/A  |  | Time zone of site. value include all [Time Zone Option](#time-zone-options) Ids. |
 |`company` | string | | no | N/A  | |Company name.|
 |`companySize` | string| | no | N/A  |  |The number of staff of the company, value options include: 1-20, 21-50, 51-100, 101-180, 181-310, 311-600, Above 600. |
 |`website` | string  | | no | N/A  | |Company website. |
 |`registeredEmail` | string  | | yes | N/A  | |Email used for site registration.|
 |`phone` | string | | no | N/A  | |Company phone number.|
 |`fax` | string | | no | N/A  | |Company fax number.|
 |`mailingAddress` | string | | no | N/A  | |The mailing address of the company.|
 |`city` | string  | | no | N/A  | |City where the company located.|
 |`stateOrProvince` | string  | | no | N/A  | |State/Province where the company located.|
 |`countryOrRegion` | string | | no | N/A  | |Country/Region where the company located.|
 |`postalOrZipCode` | string | | no | N/A  | |Postal/Zip Code where the company located.|
 |`firstName` | string  | | no | N/A  | |First Name of site registrant.|
 |`lastName` | string  | | no | N/A  | |Last Name of site registrant.|

## Site Endpoints

### Get profile of a site
  `GET /api/v3/globalSettings/site`

#### Parameters
    No parameters
#### Response

  the response is [Site](#site-object) Object, just include base informations.

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/site
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "id": 10000,
    "dateTimeFormat":"yyyy-MM-dd hh:mm:ss",
    "timeZone":"canadaCentralStandardTime",
    "company":"BMW",
    "companySize": "Above 600",
    "website":"www.bmw.com",
    "registeredEmail":"bmw@gmail.com",
    "phone":"88654987",
    "fax":"58469215",
    "mailingAddress":"mail@bmw.com",
    "city":"Berlin",
    "stateOrProvince":"",
    "countryOrRegion":"Germany",
    "postalOrZipCode":"10115–14199",
    "firstName":"Jasn",
    "lastName":"Statham",
}
```


### Update profile of a site
  `PUT /api/v3/globalSettings/site`

#### Parameters

Request body

  The request body contains data with the [Site](#site-object) structure

#### Response

  The response is the [Site](#site-object) Object.

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "dateTimeFormat"："yyyy-MM-dd hh:mm:ss"，
    "timeZone"："canadaCentralStandardTime"，
    "company"："BMW"，
    "companySize": "Above 600",
    "website"："www.bwm.com"，
    "registeredEmail"："bmw@gmail.com"，
    "phone"："88654987"，
    "fax"："58469215"，
    "mailingAddress"："mail@bmw.com"，
    "city"："Berlin"，
    "stateOrProvince"：""，
    "countryOrRegion"："Germany"，
    "postalOrZipCode"："10115–14199"，
    "firstName"："Jasn"，
    "lastName"："Statham"，
    ...,
}' -X PUT https://domain.comm100.com/api/v3/globalSettings/site
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "id": 10000,
    "dateTimeFormat": "yyyy-MM-dd hh:mm:ss",
    "timeZone": "canadaCentralStandardTime",
    "company": "BMW",
    "companySize": "Above 600",
    "website": "www.bwm.com",
    "registeredEmail": "bmw@gmail.com",
    "phone": "88654987",
    "fax": "58469215",
    "mailingAddress": "mail@bmw.com",
    "city": "Berlin",
    "stateOrProvince": "",
    "countryOrRegion": "Germany",
    "postalOrZipCode": "10115–14199",
    "firstName": "Jasn",
    "lastName": "Statham",
}
```


# Agent

You need `Manage Agent & Agent Roles` permission to manage agents.

  + `GET /api/v3/globalSettings/agents` - [Get a list of agents in site](#get-a-list-of-agents-in-site)
  + `GET /api/v3/globalSettings/agents/{id}` - [Get an agent by id](#get-an-agent-by-id)
  + `GET /api/v3/globalSettings/roles/{roleId}/agents` - [Get a list of agents by role id](#get-a-list-of-agents-by-role-id)
  + `GET /api/v3/globalSettings/departments/{departmentId}/agents` - [Get a list of agents by department id](#get-a-list-of-agents-by-department-id)
  + `GET /api/v3/globalSettings/agents/me` - [Get current agent](#get-current-agent)
  + `POST /api/v3/globalSettings/agents` - [Create a new agent](#create-a-new-agent)
  + `POST /api/v3/globalSettings/agents/{id}:unlock` - [Unlock the agent](#unlock-the-agent)
  + `POST /api/v3/globalSettings/agents/{id}:changePassword` - [Admin set an agent's password](#admin-set-an-agents-password)
  + `POST /api/v3/globalSettings/agents/me:changePassword` - [Change own password](#change-own-password)
  + `PUT /api/v3/globalSettings/agents/{id}` - [Update an agent](#update-an-agent)
  + `PUT /api/v3/globalSettings/agents/me` - [Update current agent](#update-current-agent)
  + `DELETE /api/v3/globalSettings/agents/{id}` - [Delete an agent](#delete-an-agent)

## Agent Related Object Json Format

### Agent Object
  This is the entity details of the Agent.

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | integer  | | N/A | N/A |  |  |
  |`email` | string| | yes | yes | | Agent login email address, can not change |
  |`displayName` | string  | | no | no | | Different Agents can have the same Display Name. If not offered, will set by first name.|
  |`firstName` | string  | | no | yes | | The first name of the agent|
  |`lastName` | string  | | no | yes | | The last name of agent|
  |`isAdmin` | bool| | no | no | false | Whether the agent is an administrator or not.|
  |`isActive` | bool| | no | no | true | Whether the agent is active or not.|
  |`phone` | string | | no | no | | Mobile phone number of the agent.|
  |`title` | string  | | no | no | | The title of the agent.|
  |`bio` | string  | | no | no | | The bio info of the agent.|
  |`timeZone` | string| | no | no |  | Time zone of agent. value include all [Time Zone Option](#time-zone-options) Ids, if not offered, will set by site time zone. |
  |`datetimeFormat` | string| | no | no |  'MM-dd-yyyy HH:mm:ss' | Date/time format selected by agent to display on the site,value options include : MM-dd-yyy HH:mm:ss, MM/dd/yyyy HH:mm:ss, dd-MM-yyyy HH:mm:ss, dd/MM/yyyy HH:mm:ss, yyyy-MM-dd HH:mm:ss, yyyy/MM/dd HH:mm:ss|
  |`createdTime` | DateTime | | N/A | N/A | UTC | The create time of the agent.|
  |`isLocked` | bool| | yes | N/A | false | Account will be locked after several failed login attempts.|
  |`lockedTime` | DateTime | | N/A | N/A | UTC | When the agent is locked.|
  |`lastLoginTime` | DateTime | | N/A | N/A | UTC | The time of the last login to Comm100 account (Control Panel or Agent Console).|
  |`permissionIds` | integer[]  |  | no | no | NULL | Agent permission settings.|
  |`permissions` | [Permission](#permission)[]  | yes| N/A | N/A | | Agent permission settings. |
  |`roleIds` | Guid[]  |  | no | no | NULL | The list of the role ids which the agent belongs to. If not offered, will use role id of "All Agents" as default. |
  |`roles` | [Role](#role)[]  |yes | N/A | N/A | | The list of the roles which the agent belongs to.|
  |`departmentIds` | Guid[]  |  | no | no | NULL | The list of the department ids which the agent belongs to.|
  |`departments` | [Department](#department)[]  |yes | N/A | N/A | | The list of the roles which the agent belongs to.|
  |`shifts` | [Shift](#shift)[]  | yes | N/A | N/A  | | The list of shifts which the agent belongs to.|



### Agent List Response Object

  Agent List Object for agent list Response, include count and page information.

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`count` | integer  | N/A | yes | no | | The total count of the query  |
  |`nextPage` | string  | N/A | yes | no | | The next page url of the query  |
  |`previousPage` | string  | N/A | yes | no | | The previous page url of the query  |
  |`agents`|   [Agent](#agent-object)[]| N/A | yes| no | | A list of agents. |



## Agent Endpoints

### Get a list of agents in site
  `GET/api/v3/globalSettings/agents`

#### Parameters
   Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no||Available value:`department`,`role`,`permission`,`shift`  |
  |`keywords` | string | no  |  | Filter by keywords in agent display name, email address. |
  |`pageIndex`|integer|no| 1 | The page index of the query. |
  |`pageSize`|integer|no| 10 | The page size of the query. |


#### Response

  The response is a [Agent List Response ](#agent-list-response-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/agents
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "count": 1234,
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/agents?pageIndex=2",
    "previousPage": null,
    "agents": [{
        "id": 68,
        "email": "Tom@gmail.com",
        "displayName":"Tom",
        "firstName":"Tom",
        "lastName":"Green",
        "title":"CEO",
        ...
    }
    ...
    ]
}
```

### Get an agent by id
+ `GET /api/v3/globalSettings/agents/{id}`

#### Parameters

Path parameters

| Name  | Type | Required  | Description |
| - | - | - | - |
|`id` | integer | yes  |  the id of the agent |

Query string

 | Name  | Type | Required  | Default | Description |
 | - | - | - | - | - |
 |`include`|string|no||Available value:`department`,`role`,`permission`,`shift` |

#### Response

The response is a [Agent](#agent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/agents/68?include=role,department
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    ...
}
```

### Get a list of agents by role id
  `GET /api/v3/globalSettings/roles/{roleId}/agents`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`roleId` | Guid | yes  |  The id of the role |

   Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no||Available value:`department`,`role`,`permission`,`shift` |
  |`pageIndex`|integer|no| 1 | The page index of the query. |
  |`pageSize`|integer|no| 10 | The page size of the query. |

#### Response

The response is a [Agent List Response](#agent-list-response-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d6892e6/agents
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "count": 1234,
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d6892e6/agents?pageIndex=2",
    "previousPage": null,
    "agents": [{
        "id": 68,
        "email": "Tom@gmail.com",
        "displayName":"Tom",
        "firstName":"Tom",
        "lastName":"Green",
        "title":"CEO",
        ...
    }
    ...
    ]
}
```


### Get a list of agents by department id
  `GET /api/v3/globalSettings/departments/{departmentId}/agents`

#### Parameters
   Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`departmentId` | Guid | yes  |  The id of the department |

   Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`| string | no ||Available value:`department`,`role`,`permission`,`shift` |
  |`pageIndex`| integer | no | 1 |The page index of the query. |
  |`pageSize`| integer | no | 10 |The page size of the query. |


#### Response

The response is a [Agent List Response](#agent-list-response-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/departments/42dwdaww-92e6-4487-a2e8-92e68d68a2e8/agents
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "count": 1234,
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/departments/42dwdaww-92e6-4487-a2e8-92e68d68a2e8/agents?pageIndex=2",
    "previousPage": null,
    "agents": [{
        "id": 68,
        "email": "Tom@gmail.com",
        "displayName":"Tom",
        "firstName":"Tom",
        "lastName":"Green",
        "title":"CEO",
        ...
    }
    ...
    ]
}
```


### Get current agent
+ `GET /api/v3/globalSettings/agents/me`

#### Parameters
  Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no||Available value:`department`,`role`,`permission`,`shift` |

#### Response

The response is a [Agent](#agent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/agents/me?include=role,department
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    ...
}
```

### Create a new agent
  `POST /api/v3/globalSettings/agents`

####  Parameters

Request body

  The request body contains data with the [Agent](#agent-object) structure

example:
```json
{
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
}
```

#### Response
The response is:
  [Agent](#agent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
} ' -X POST https://domain.comm100.com/api/v3/globalSettings/agents
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/agents/68
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
}
```


### unlock the agent
  `POST /api/v3/globalSettings/agents/{id}:unlock`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the agent |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{} ' -X POST https://domain.comm100.com/api/v3/globalSettings/agents/68:unlock
```
Response
```json
HTTP/1.1 204 No Content
```

### Admin set an agent's password
  `POST /api/v3/globalSettings/agents/{id}:changePassword`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the agent |

Request body

  | Name  | Type | Required | Default | Description |
  | - | - | - | - | - |
  | `password` | string | yes  |  | The new password of agent |

  example:
  ```json
  {
    "password": "Aa5847lkdsc&d",
  }
  ```

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "password": "Aa5847lkdsc&d",
}' -X POST https://domain.comm100.com/api/v3/globalSettings/agents/68:changePassword
```
Response
```json
HTTP/1.1 204 No Content
```

### Change own password
  `POST /api/v3/globalSettings/agents/me:changePassword`

####  Parameters

Request body

  | Name  | Type | Required | Default | Description |
  | - | - | - | - | - |
  | `currentPassword` | string | yes  |  | The current password of agent |
  | `newPassword` | string | yes  |  | The new password of agent |

  example:
  ```json
  {
    "currentPassword": "Aa2541554",
    "newPassword": "Aa5847lkdsc&d",
  }
  ```

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
    "currentPassword": "Aa2541554",
    "newPassword": "Aa5847lkdsc&d",
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/agents/me:changePassword
```

Response
```json
HTTP/1.1 204 No Content
```


### Update an agent
  `PUT /api/v3/globalSettings/agents/{id}`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the agent |

Request body

  The request body contains data with the [Agent](#agent-object) structure

  example:
```json
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
}
```

#### Response
The response is:
  [Agent](#agent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
} ' -X PUT https://domain.comm100.com/api/v3/globalSettings/agents/68
```
Response
```json
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://domain.comm100.com/api/v3/globalSettings/agents/68
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
}
```

### Update current agent

  `PUT /api/v3/globalSettings/agents/me`

####  Parameters

Request body

  The request body contains data with the [Agent](#agent-object) structure

example:
```json
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
}
```

#### Response
The response is: [Agent](#agent-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
} ' -X PUT https://domain.comm100.com/api/v3/globalSettings/me
```

Response
```json
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://domain.comm100.com/api/v3/globalSettings/agents/me
{
    "id": 68,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    "roleIds": [
      "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      ...,
    ]
    ...,
}
```


### Delete an agent
  `DELETE /api/v3/globalSettings/agents/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  the agent id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/agents/68
```
Response
```json
HTTP/1.1 204 No Content
```



# Role
You need `Manage Agent & Agent Roles` permission to manage roles.

  + `GET /api/v3/globalSettings/roles` - [Get a list of roles in site](#get-a-list-of-roles-in-site)
  + `GET /api/v3/globalSettings/roles/{id}` - [Get a role by id](#get-a-role-by-id)
  + `POST /api/v3/globalSettings/roles` - [Create a new role](#create-a-new-role)
  + `PUT /api/v3/globalSettings/roles/{id}` - [Update a role](#update-a-role)
  + `DELETE /api/v3/globalSettings/roles/{id}` - [Delete a role](#delete-a-role)

## Role Related Object Json Format

### Role Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | Guid| | N/A | N/A | |  |
  |`name` | string| | no | yes | | Name.|
  |`description` | string| | no | no | | Description of this role.|
  |`type` | string | | yes | N/A | custom | The options: administrator, agent, custom; administrator and agent are the system role types. They cannot be deleted. |
  |`agentIds` | int[] | | no | no | NULL | The selected agents for this role. |
  |`agents` | [Agent](#agent)[] | yes | N/A | N/A | | The selected agents for this role.|
  |`permissionIds` | int[] | | no | no | NULL | Permissions assigned to this role.|
  |`permissions` | [Permission](#permission)[] | yes | N/A | N/A | | Permissions assigned to this role.|


## Role Endpoints

### Get a list of roles in site
  `GET GET /api/v3/globalSettings/roles`

#### Parameters
  Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no||Available value:`agent`,`permission` |

#### Response

The response is a list of [Role](#role) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles?include=permission
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
[{
  "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "markting",
  "description": "yyyy-MM-dd hh:mm:ss",
  "type": "custom",
  "agentIds":  [
    68,
    ...,
  ],
  "permissionIds" :
    [
      201,
      205,
      ...,
    ],
    "permission" :[
      {
        "name": "Accept Chats",
        "description": "Accept Chats",
        "category": "Live Chat",
      },
      ...,
    ]
},
...,
]
```

### Get a role by id

  `GET /api/v3/globalSettings/roles/{id}`


#### Parameters
  Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The id of the role |

  Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no|| Available value:`agent`,`permission` |

#### Response

The response is a [Role](#role) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "markting",
  "description": "yyyy-MM-dd hh:mm:ss",
  "type": "custom",
  "agentIds":  [
    68,
    ...,
  ],
  "permissionIds" :
    [
      201,
      205,
      ...,
    ],
}
```


### Create a new role

  `POST /api/v3/globalSettings/roles`

####  Parameters

Request body

  The request body contains data with the [Role](#role-object) structure

  example:
```json
 {
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "custom",
      "agentIds":  [
        68,
        ...,
      ],
      "permissionIds" :
        [
         201,
         205,
         ...,
        ],
    }
```

#### Response
The response is:
   [Role](#role-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "custom",
      "agentIds":  [
        68,
        ...,
      ],
      "permissionIds" :
        [
         201,
         205,
         ...,
        ],
        ...,
    },
    }' -X POST https://domain.comm100.com/api/v3/globalSettings/roles
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/roles/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
 {
      "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "name": "markting",
      "description": "yyyy-MM-dd hh:mm:ss",
      "type": "custom",
      "agentIds":  [
        68,
        ...,
      ],
      "permissionIds" :
        [
         201,
         205,
         ...,
        ],
    }
```


### Update a role
  `PUT /api/v3/globalSettings/roles/{id}`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The id of the role |

Request body

  The request body contains data with the  [Role](#role-object) structure

  example:
```json
 {
      "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "name": "markting",
      "description": "yyyy-MM-dd hh:mm:ss",
      "type": "custom",
      "agentIds":  [
        68,
        ...,
      ],
      "permissionIds" :
        [
         201,
         205,
         ...,
        ],
    }
```

#### Response
The response is:
  [Role](#role-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "name": "markting",
      "description": "yyyy-MM-dd hh:mm:ss",
      "type": "custom",
      "agentIds":  [
        68,
        ...,
      ],
        "permissionIds" :
        [
         201,
         205,
         ...,
        ],
    },
    } ' -X PUT https://domain.comm100.com/api/v3/globalSettings/roles/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/roles/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
{
  "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "markting",
  "description": "yyyy-MM-dd hh:mm:ss",
  "type": "custom",
  "agentIds":  [
    68,
    ...,
  ],
  "permissionIds" :
    [
      201,
      205,
      ...,
    ],
}
```

### Delete a role
  `DELETE /api/v3/globalSettings/roles/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The role id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```


# Department

You need `Manage departments` permission to manage departments.

  + `GET /api/v3/globalSettings/departments` - [Get a list of departments in site](#get-all-departments)
  + `GET /api/v3/globalSettings/departments/{id}` - [Get a department by id](#get-a-department)
  + `POST /api/v3/globalSettings/departments` - [Create a new department](#create-a-new-department)
  + `PUT /api/v3/globalSettings/departments/{id}` - [Update a department](#update-a-department)
  + `DELETE /api/v3/globalSettings/departments/{id}` - [Delete a department](#delete-a-department)


## Department Related Object Json Format

### Department Object

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | Guid| | N/A | N/A | |  |
  |`name` | string | | no | yes | |  |
  |`description` | string | | no | no | |  |
  |`isAvailableInChat` | bool| | no | no | false | When it is false, the Department will not be displayed in the Pre-chat window Department drop down list, routing rules, chat transfer etc. Default: true.|
  |`isAvailableInTicketingAndMessaging` | bool| | no | no | false | When it is false, the department name will not be displayed in the 'Assigned Department' field. Default: true.|
  |`offlineMessageMailTo` | string | | no | no | All agents in the department | The value options: All agents in the department, The email address(es).  |
  |`offlineMessageEmailAddresses` | string  | | no | no | | Specific email addresses that mail offline message to. Available and required when Offline Message Mail Type is ‘The email address(es)’.|
  |`agentIds` | int[] | | no | no | NULL | The selected agents for this department.|
  |`agents` | [Agent](#agent)[]| yes | N/A | N/A |  |  |
  |`shifts` | [Shift](#shift)[]| yes | N/A | N/A |  |  |

## Department Endpoints

### get all departments
  `GET /api/v3/globalSettings/departments`

#### Parameters
  Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no||Available value:`agent`,`shift` |

#### Response

  The response is a list of [Department](#department-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/departments
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
[{
  "name": "markting",
  "description": "markting departments",
  "isAvailableInChat": "yes",
  "isAvailableInTicketingAndMessaging": "yes",
  "offlineMessageMailTo": "All agents in the department",
  "offlineMessageEmailAddresses": "",
  "agentIds":  [
    68,
    ...,
  ],
},
...,
]
```

### get a department
  `GET /api/v3/globalSettings/departments/{id}`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The id of the department |

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`include`|string|no||Available value:`agent`,`shift` |

  #### Response

  The response is a [Department](#department-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/departments/4487fc9d-92e6-4487-a2e8-92e68d68927777
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "name": "markting",
  "description": "markting departments",
  "isAvailableInChat": "yes",
  "isAvailableInTicketingAndMessaging": "yes",
  "offlineMessageMailTo": "All agents in the department",
  "offlineMessageEmailAddresses": "",
  "agentIds":  [
    68,
    ...,
  ],
}
```


### Create a new department
  `POST /api/v3/globalSettings/departments`

####  Parameters

Request body

  The request body contains data with the [Department](#department-object) structure

  example:
```json
 {
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailTo": "All agents in the department",
      "offlineMessageEmailAddresses": "",
      "agentIds":  [
        68,
        ...,
      ],
    }
```

#### Response
The response is:
    [Department](#department-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailTo": "All agents in the department",
      "offlineMessageEmailAddresses": "",
      "agentIds":  [
        68,
        ...,
      ],
    }' -X POST https://domain.comm100.com/api/v3/globalSettings/roles
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/departments
{
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailTo": "All agents in the department",
      "offlineMessageEmailAddresses": "",
      "agentIds":  [
        68,
        ...,
      ],
    }
```



### update a department
  `PUT /api/v3/globalSettings/departments/{id}`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The id of the department |

Request body

  The request body contains data with the  [Department](#department-object) structure

  example:
```json
{
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailTo": "All agents in the department",
      "offlineMessageEmailAddresses": "",
      "agentIds":  [
        68,
        ...,
      ],
    }
```

#### Response
The response is:
   [Department](#department-object)  Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "markting",
  "description": "markting departments",
  "isAvailableInChat": "yes",
  "isAvailableInTicketingAndMessaging": "yes",
  "offlineMessageMailTo": "All agents in the department",
  "offlineMessageEmailAddresses": "",
  "agentIds":  [
    68,
    ...,
  ],
}' -X PUT https://domain.comm100.com/api/v3/globalSettings/departments/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/departments/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
{
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailTo": "All agents in the department",
      "offlineMessageEmailAddresses": "",
      "agentIds":  [
        68,
        ...,
      ],
    }
```

### Delete a department
  `DELETE /api/v3/globalSettings/departments/{id}`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  the department id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/departments/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```


# Permission

  Permission is hard-coded.

  + `GET /api/v3/globalSettings/permissions` - [Get all permissions](#get-all-permissions)
  + `GET /api/v3/globalSettings/roles/{roleId}/permissions` - [Get role permissions](#get-role-permissions)
  + `GET /api/v3/globalSettings/agents/{agentId}/permissions` - [Get agent permissions](#get-agent-permissions)
  + `GET /api/v3/globalSettings/agents/{agentId}/permissions:effective` - [Get a list of agent's effective permissions](#get-agent-effective-permissions)
  + `PUT /api/v3/globalSettings/roles/{roleId}/permissions` - [Update role permissions](#update-role-permissions)
  + `PUT /api/v3/globalSettings/agents/{agentId}/permissions` - [Update agent permissions](#update-agent-permissions)


## Permission Related Object Json Format

### Permission Object

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | long | | N/A | N/A |  |  |
  |`name` | string| | yes | no | |  |
  |`description` | string| | yes | no | |  |
  |`category` | string | | yes | no | |The value options include: liveChat, ticketingAndMessaging, bot, globalSettings, knowledgeBase|

## Permission Endpoints

### Get all permission
  `GET /api/v3/globalSettings/permissions`

#### Parameters
    No parameters

#### Response

  The response is a list of [Permission](#permission) Objects

#### Example
  Using curl
  ```
  curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/permissions
  ```
  Response
  ```json
  HTTP/1.1 200 OK
  Content-Type:  application/json[
  {
    "id": 201,
    "name": "Accept Chats",
    "description": "Accept Chats",
    "category": "Live Chat",
  },
  ...,
  ]
  ```



### Get role permissions
  `GET /api/v3/globalSettings/roles/{roleId}/permissions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`roleId` | Guid | yes  |  The id of the role |

#### Response

The response is a [Permission](#permission) Object


#### Example
  Using curl
  ```
  curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d68927777/permissions
  ```
  Response
  ```json
  HTTP/1.1 200 OK
  Content-Type:  application/json[
  {
    "id": 201,
    "name": "Accept Chats",
    "description": "Accept Chats",
    "category": "Live Chat",
  },
  ...,
  ]
  ```


### Get agent permissions
  `GET /api/v3/globalSettings/agents/{agentId}/permissions`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`agentId` | integer | yes  |  The id of the agent |

  #### Response

  The response is a list of [Permission](#permission) Objects


  #### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/agents/68/permissions
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json[
{
  "id": 201,
  "name": "Accept Chats",
  "description": "Accept Chats",
  "category": "Live Chat",
},
...,
]
```

### Get agent effective permissions

  `GET /api/v3/globalSettings/agents/{agentId}/permissions:effective`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`agentId` | integer | yes  |  The id of the agent |

  #### Response

  The response is a list of [Permission](#permission) Objects


  #### Example
  Using curl
  ```
  curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/agents/68/permissions:effective
  ```
  Response
  ```json
  HTTP/1.1 200 OK
  Content-Type:  application/json[
  {
    "id": 201,
    "name": "Accept Chats",
    "description": "Accept Chats",
    "category": "Live Chat",
  },
  ...,
  ]
  ```

### update role permissions

 `PUT /api/v3/globalSettings/roles/{roleId}/permissions`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`roleId` | Guid | yes  |  The id of the role |

Request body

  The request body contains data with the  [Permission](#permission-object) Id list

  example:
```json
[
  201,
  205,
  ...,
]
```

#### Response
the response is:
role [Permission](#permission-object) Object list

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
  201,
  205,
  ...,
]' -X PUT https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d68927777/permissions
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d68927777/permissions
[{
      "id": 201,
      "name": "Accept Chats",
      "description": "Accept Chats",
      "category": "Live Chat",
    },
    ...,
]
```

### update agent permissions
`PUT /api/v3/globalSettings/agents/{agentId}/permissions`

####  Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`agentId` | integer | yes  |  The id of the agent |

Request body

  The request body contains data with the  [Permission](#permission-object) Id list

  example:
```json
[
  201,
  205,
  ...,
]
```

#### Response
The response is:
   agent [Permission](#permission-object) Object list

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
  201,
  205,
  ...,
]' -X PUT https://domain.comm100.com/api/v3/globalSettings/agents/68/permissions
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/agents/68/permissions
[{
      "id": 201,
      "name": "Accept Chats",
      "description": "Accept Chats",
      "category": "Live Chat",
    },
    ...,
]
```



# Shift

- `GET /api/v3/globalSettings/shifts` - [Get all shifts in site](#get-all-shifts-in-site)
- `GET /api/v3/globalSettings/departments/{departmentId}/shifts` - [Get all shifts by department id](#get-all-shifts-by-department-id)
- `GET /api/v3/globalSettings/agents/{agentId}/shifts` - [Get all shifts by agent id](#get-all-shifts-by-agent-id)
- `GET /api/v3/globalSettings/shifts/{id}` - [Get a shift by id](#get-a-shift-by-id)
- `POST /api/v3/globalSettings/shifts` - [create a new shift](#create-a-new-shift)
- `PUT /api/v3/globalSettings/shifts/{id}` - [update a shift](#update-a-shift)
- `DELETE /api/v3/globalSettings/shifts/{id}` - [delete a shift](#delete-a-shift)

## Related Object Json Format

### Shift Object

  Shift Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | no | | Id of the current item.  |
  | `name` | string  | | no | yes | | Name of the shift. |
  | `timeZone` | string  | | no | no | | Time zone of shift. value include all [Time Zone Option](#time-zone-options) Ids. |
  | `holidays` | [Holiday](#holiday-object)[]  | | no | no | | |
  |`agentIds` | int[] | | yes | no | NULL | |
  |`departmentIds` | Guid[] | | yes | no | NULL | |
  | `agents` | [Agent](#Agent-Object)[] | yes | N/A | N/A | | |
  | `departments` | [Department](#Department-Object)[] | yes | N/A | N/A | | |
  | `workingHours` | [Working Hours](#Working-Hours-Object)[]  | | no | no | | |

### Holiday Object

  Holiday Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `name` | string  | no | yes | | The name of holiday. |
  | `date` | DateTime  | no | yes | | The date of the holiday. |


### Working Hours Object

  Working Hours Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `dayOfWeek` | string  | no | yes | | Including `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday` and `Sunday`. |
  | `startTime` | time  | no | yes | | |
  | `endTime` | time  | no | yes | | |
  | `awayStatusId` | Guid | no | no | | |

## Shift Endpoints

### Get all Shifts in site

  `GET /api/v3/globalSettings/shifts`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `department`, `agent` |

#### Response

the response is: list of [Shift](#shift-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/shifts?include=department
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
        "name": "Shifts",
        "timeZone": "(GMT) Coordinated Universal Time",
        "holidays": [{
          "name": "summary",
          "date": "2019-11-11"
        },
        ...
        ],
        "agentIds": [68],
        "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
        "departments": [{// include department
          "id": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
          "name": "departments",
          "siteId": "FEF12049-BF08-2CD4-C405-A5FC8AE75D0F",
          "description": "departments",
          "isAvailableInChat": false,
          "isAvailableInTicketingAndMessaging": false,
          "offlineMessageMailTo": "The email address(es)",
          "offlineMessageEmailAddresses": "test@comm100.com",
          "agentId": 68
        },
        ...
        ],
        "workingHours": [{
          "dayOfWeek": "sunday",
          "startTime": "12:00",
          "endTime": "14:00",
          "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
        },
        ...
        ]
    },
    ...
]
```

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

the response is: [Shift](#shift-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/shifts/3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED?include=department
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
  "name": "Shifts",
  "timeZone": "(GMT) Coordinated Universal Time",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "departments": [{// include department
    "id": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
    "name": "departments",
    "siteId": "FEF12049-BF08-2CD4-C405-A5FC8AE75D0F",
    "description": "departments",
    "isAvailableInChat": false,
    "isAvailableInTicketingAndMessaging": false,
    "offlineMessageMailTo": "The email address(es)",
    "offlineMessageEmailAddresses": "test@comm100.com",
    "agentId": 68
  },
  ...
  ],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
}
```

### Get all Shifts by department id

  `GET /api/v3/globalSettings/departments/{departmentId}/shifts`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `departmentId` | Guid | yes  |  The id of the department |

#### Response

the response is: [Shift](#shift-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/departments/1DC43077-E36F-F9EA-C7BA-C29620102F7E/shifts
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
        "name": "Shifts",
        "timeZone": "(GMT) Coordinated Universal Time",
        "holidays": [{
          "name": "summary",
          "date": "2019-11-11"
        },
        ...
        ],
        "agentIds": [68],
        "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
        "workingHours": [{
          "dayOfWeek": "sunday",
          "startTime": "12:00",
          "endTime": "14:00",
          "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
        },
        ...
        ]
    },
    ...
]
```

### Get all Shifts by agent id

  `GET /api/v3/globalSettings/agents/{agentId}/shifts`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `agentId` | integer | yes  |  the unique Id of the agent |

#### Response

the response is: [Shift](#shift-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/agents/68/shifts
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
        "name": "Shifts",
        "timeZone": "(GMT) Coordinated Universal Time",
        "holidays": [{
          "name": "summary",
          "date": "2019-11-11"
        },
        ...
        ],
        "agentIds": [68],
        "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
        "workingHours": [{
          "dayOfWeek": "sunday",
          "startTime": "12:00",
          "endTime": "14:00",
          "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
        },
        ...
        ]
    },
    ...
]
```

### Create a new Shift

  `POST /api/v3/globalSettings/shifts`

#### Parameters

Request Body

  The request body contains data with the [Shift](#shift-object) structure

example:
```Json
{
  "name": "Shifts1111",
  "timeZone": "UTC",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
}
```

#### Response

the response is: [Shift](#shift-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "Shifts1111",
  "timeZone": "UTC",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/shifts
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/shifts/3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED

{
  "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
  "name": "Shifts",
  "timeZone": "(GMT) Coordinated Universal Time",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
}
```

### Update a Shift

  `PUT /api/v3/globalSettings/shifts/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the shift |

Request Body

  The request body contains data with the [Shift](#shift-object) structure

example:
```Json
{
  "name": "Shifts2222",
  "timeZone": "UTC",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
}
```

#### Response

the response is: [Shift](#shift-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "Shifts2222",
  "timeZone": "UTC",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/shifts/3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
  "name": "Shifts2222",
  "timeZone": "(GMT) Coordinated Universal Time",
  "holidays": [{
    "name": "summary",
    "date": "2019-11-11"
  },
  ...
  ],
  "agentIds": [68],
  "departmentIds": ["1DC43077-E36F-F9EA-C7BA-C29620102F7E"],
  "workingHours": [{
    "dayOfWeek": "sunday",
    "startTime": "12:00",
    "endTime": "14:00",
    "awayStatusId": "BAACB779-2E41-27C5-B23D-1C8F2058862D"
    },
    ...
  ]
}
```

### Delete a Shift

  `DELETE /api/v3/globalSettings/shifts/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes  |  the unique Id of the shift |

#### Response

HTTP/1.1 204 No Content

#### Example

Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/shifts/3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED
```

Response
```Json
  HTTP/1.1 204 No Content
```

# Contact
 + `GET /api/v3/globalSettings/contacts` - [Get a list of contacts in site](#get-all-contacts)
 + `GET /api/v3/globalSettings/contacts/{id}` - [Get a contact by id](#get-an-contact)
 + `POST /api/v3/globalSettings/contacts` - [Create a new contact](#create-a-new-contact)
 + `PUT /api/v3/globalSettings/contacts/{id}` - [Update a contact](#update-a-contact)
 + `DELETE /api/v3/globalSettings/contacts/{id}` - [Delete a contact](#delete-a-contact)

## Contact Related Object Json Format

### Contact Object

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | integer  | | N/A | N/A |  |  |
  |`name` | string  | | no | yes | | Contact Name can be edited by Agents. Default value is read from the first Identity. Only when a Contact sends a message in a specific channel that has Name and Avatar, like Facebook Account, display Name and Avatar from that Identity in Agent Console. In other situations, display Contact Name and Avatar.|
  |`description` | string | | no | no | |  |
  |`firstName` | string | | no | no | |  |
  |`lastName` | string | | no | no | |  |
  |`alias` | string | | no | no | |  |
  |`title` | string | | no | no | |  |
  |`company` | string  | | no | no | |  |
  |`fax` | string  | | no | no | |  |
  |`phone` | string  | | no | no | | |
  |`mailingAddress` | string  | | no | no | |  |
  |`city` | string | | no | no | |  |
  |`stateOrProvince` | string  | | no | no | |  |
  |`countryOrRegion` | string  | | no | no | |  |
  |`postalOrZipCode` | string  | | no | no | |  |
  |`timeZone` | string | | no | no | |  Time zone of contact. value include all [Time Zone Option](#time-zone-options) Ids.|
  |`createdTime` | DateTime | | N/A | N/A | | When the contact is created.|
  |`lastUpdatedTime` | DateTime | | N/A | N/A | |  |
  |`contactIdentities` | [ContactIdentity](#Contact-Identity)[] | yes | no | no | | Contact Identity. |

### Contact List Response Object

  Agent List Object for agent list Response, include count and page information.

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`count` | integer  | N/A | yes | no | | The total count of the query  |
  |`nextPage` | string  | N/A | yes | no | | The next page url of the query  |
  |`previousPage` | string  | N/A | yes | no | | The previous page url of the query  |
  |`contacts`|   [Contact](#contact-object)[]| N/A | yes| no | | A list of contacts. |



## Contact Endpoints


### Get all contacts
  `GET /api/v3/globalSettings/contacts`

#### Parameters
   Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`name` | string | no  |  | Contact name. |
  |`company`|string|no|  | Contact company. |
  |`contactIdentityName` | string | no  |  | Contact identity name. |
  |`contactIdentityValue` | string | no  |  | Contact identity value. |
  |`contactIdentityType` | string | no  |  | Contact identity type. |
  |`keywords` | string | no  |  | Search scope includes: name, company, identity value, alias. |
  |`include` | string | no  |  | Available value: `contactIdentity` |
  |`pageIndex`|integer|no| 1 | The page index of the query. |
  |`pageSize`|integer|no| 10 | The page size of the query. |



  #### Response
  The response is a [Contact List Response](#contact-list-response-object) Object


#### Example
  Using curl
  ```
  curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contacts?name=Vincent
  ```
  Response
  ```json
  HTTP/1.1 200 OK
  Content-Type:  application/json
  {
    "count": 1234,
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/contacts?name=Vincent&pageIndex=2",
    "previousPage": null,
    "contacts": [{
      "id": 7,
      "name": "Vincent",
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe",
      "alias": "",
      "title": "CEO",
      "company": "BMW",
      ...
    },
    ...
    ]
}
  ```


### Get an contact
  `GET /api/v3/globalSettings/contacts/{id}`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the contact |
  | `include` | string | no  |  | Available value: `contactIdentity` |


#### Response
  The response is an [Contact](#contact-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contacts/7
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": 7,
  "name": "Vincent",
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe",
  "alias": "",
  "title": "CEO",
  "company": "BMW",
  ...
}
```

### Create a new contact

  `POST /api/v3/globalSettings/contacts`

####  Parameters

Request body

  The request body contains data with the [Contact](#contact-object) structure

example:
```json
{
      "name": "Vincent",
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe",
      "alias": "",
      "title": "CEO",
      "company": "BMW",
      ...
    }
```

#### Response

The response is:
  [Contact](#contact-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "name": "Vincent",
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe",
      "alias": "",
      "title": "CEO",
      "company": "BMW",
      ...
    }' -X POST https://domain.comm100.com/api/v3/globalSettings/contacts
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contacts/7
{
  "id": 7,
  "name": "Vincent",
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe",
  "alias": "",
  "title": "CEO",
  "company": "BMW",
  ...
}
```

### Update an contact
  `PUT /api/v3/globalSettings/contacts/{id}`

####  Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the contact |

Request body

  The request body contains data with the [Contact](#contact-object) structure

  example:
```json
{
  "name": "Vincent",
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe",
  "alias": "",
  "title": "CEO",
  "company": "BMW",
  ...
}
```

#### Response
The response is:
  [Contact](#contact-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "Vincent",
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe",
  "alias": "",
  "title": "CEO",
  "company": "BMW",
  ...
}' -X PUT https://domain.comm100.com/api/v3/globalSettings/contacts
```
Response
```json
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contacts/7
{
    "id": 7,
    "email": "Tom@gmail.com",
    "displayName":"Tom",
    "firstName":"Tom",
    "lastName":"Green",
    "title":"CEO",
    ...
}
```


### Delete an contact
  `DELETE /api/v3/globalSettings/contacts/{id}`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  | The contact id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/contacts/7
```

Response
```json
HTTP/1.1 204 No Content
```

# Contact Identity
 + `GET /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [Get a list of contact identities in a contact](#get-all-contact-identity)
 + `GET /api/v3/globalSettings/contactIdentities/{id}` - [Get an contact identity by id](#get-an-contact-identity)
 + `POST /api/v3/globalSettings/contacts/contactIdentities` - [create a new contact identity](#create-a-new-contact-identity)
 + `PUT /api/v3/globalSettings/contactIdentities/{id}` - [update an contact identity](#update-an-contact-identity)
 + `DELETE /api/v3/globalSettings/contactIdentities/{id}` - [delete an contact identity](#delete-an-contact-identity)

 ## Contact Identity Related Object Json Format

### Contact Identity Object

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | integer| | N/A | N/A | |  |
  |`contactId` | integer| | no | no | | Mandatory when post by contact identity api. |
  |`name` | string | | no | no | | The name used in a certain type, like the name of a user in Facebook. Not every type has name, for example, SMS Number doesn’t have one.|
  |`type` | string| | no | yes | | the options of the value are:  visitor, emailAddress, SMSNumber, facebookAccount, twitterAccount, weChatAccount, SSOUserID, externalID, whatsApp. In phase 1, one type only has one identity. We need remove the limitation in phase 2.|
  |`value` | string  | | no | yes | | The value of the identity.|
  |`avatarURL` | string | | no | no | | The avatar used in a certain type, like the avatar of a user in Facebook. Not every type has avatar, for example, SMS Number doesn’t have one.|
  |`infoURL` | string  | | no | no | | Contact information from the channels. Such as the number of Twitter followers, tweets of the twitter identity. The info is displayed in an iframe in agent console. Available for Twitter, Facebook, SMS, WeChat.|
  |`screenName` | string | | no | no | | Twitter only. Like @Comm100Corp. |
  |`originalContactPageURL` | string | | no | no | | The contact profile URL on Facebook or Twitter.|

## Contact Identity  Endpoints

### get all contact identity

  `GET /api/v3/globalSettings/contacts/{contactId}/contactIdentities`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`contactId` | integer | yes  |  The id of the contact of contact Identities belong|


#### Response

  The response is a list of [Contact Identity](#contact-identity-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contacts/7/contactIdentities
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json[
{
  "id": 25,
  "contactId": 7,
  "name": "Vincent",
  "type": "Visitor",
  "value": "",
  "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
  "infoURL": "",
  "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
},
...,
]
```



### get an contact identity
  `GET /api/v3/globalSettings/contactIdentities/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the contact Identitie |

#### Response

  The response is an [Contact Identity](#contact-identity-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contactIdentities/25
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
  "id": 25,
  "contactId": 7,
  "name": "Vincent",
  "type": "Visitor",
  "value": "",
  "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
  "infoURL": "",
  "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
}
```


### create a new contact identity
  `POST /api/v3/globalSettings/contacts/contactIdentities`

####  Parameters

Request body

  The request body contains data with the [Contact Identity](#contact-identity-object) structure

  example:
```json
 {
    "contactId": 7,
    "name": "Vincent",
    "type": "Visitor",
    "value": "",
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "infoURL": "",
    "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
  }
```

#### Response

The response is:
  [Contact Identity](#contact-identity-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d ' {
    "contactId": 7,
    "name": "Vincent",
    "type": "Visitor",
    "value": "",
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "infoURL": "",
    "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/contacts/contactIdentities
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contactIdentities/25
{
    "id": 25,
    "contactId": 7,
    "name": "Vincent",
    "type": "Visitor",
    "value": "",
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "infoURL": "",
    "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
  }
```

### Update an contact identity

  `PUT /api/v3/globalSettings/contactIdentities/{id}`

####  Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  The id of the contact Identitie |

Request body

  The request body contains data with the [Contact Identity](#contact-identity-object) structure

  example:
```json
 {
    "contactId": 7,
    "name": "Vincent",
    "type": "Visitor",
    "value": "",
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "infoURL": "",
    "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
  }
```

#### Response

The response is:
  [Contact Identity](#contact-identity-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
    "contactId": 7,
    "name": "Vincent",
    "type": "Visitor",
    "value": "",
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "infoURL": "",
    "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/contactIdentities/25
```
Response
```json
HTTP/1.1 200 OK
Content-Type: application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contactIdentities/25
 {
    "id": 25,
    "contactId": 7,
    "name": "Vincent",
    "type": "Visitor",
    "value": "",
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "infoURL": "",
    "extraAttributes" : "{
        \"screenName\": \"@Comm100Corp\",
        \"originalContactPageURL\": \"\",
    }",
  }
```

### delete an contact identity
  `DELETE /api/v3/globalSettings/contactIdentities/{id}`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | integer | yes  |  the contact identity id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/contactIdentities/25
```
Response
```json
HTTP/1.1 204 No Content
```

# Visitor

  You need `Manage Settings` permission to manage visitor.

- `GET /api/v3/globalSettings/visitors` - [Get all visitors in site](#get-all-visitors-in-site)
- `GET /api/v3/globalSettings/visitors/{id}` - [Get a visitor by id](#get-a-visitor-by-id)

## Related Object Json Format

### Visitor Object

  Visitor Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | N/A | N/A | | Id of the current item.  |
  | `name` | string  | N/A | N/A | | Name of the visitor. |
  | `email` | string  | N/A | N/A | | Email of the visitor. |
  | `numberOfVisits` | integer  | N/A | N/A | | The total number of web pages the visitor viewed on your website. |
  | `numberOfChats` | integer  | N/A | N/A | | The total times of chats a visitor has made on your website from the first time to present. |
  | `firstVisitTime` | datetime  | N/A | N/A | | The time the visitor first visited a web page pasted with Comm100 Live Chat code. |

## Visitor Endpoints

### Get all visitors in site

  `GET /api/v3/globalSettings/visitors`

#### Parameters

Query string

| Name  | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `requestedTime` | datetime | no  | today |  The time range of query time, defaults to today, format as `yyyy-MM-ddTHH:mm:ss`. |
| `pageIndex` | integer | no  | 1 | The page index of query. |
| `pageSize` | integer | no  | 50 | Page size.  |
| `keywords` | string | no  |  | Filter by keywords in visitor name, email address. |

#### Response

The response body contains data with the follow structure:

| Name | Type | Required | Default | Description |
| - | - | :-: | :-: | - |
| `totalCount` | integer | N/A | N/A | Total count of the list. |
| `previousPage` | string | N/A | N/A | Url of the previous page. |
| `nextPage` | string | N/A | N/A | Url of the next page. |
| `visitors` | [Visitor](#visitor-Object)[] | N/A | N/A |  |

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

{
    "totalCount": 28,
    "previousPage": "",
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/visitors?pageIndex=2",
    "visitors": [{
        "id": "7273e957-02cb-4c03-a84c-44283fcfd47d",
        "name": "test",
        "email": "",
        "numberOfVisits": 4,
        "numberOfChats": 1,
        "firstVisitTime": "2019-06-12T07:41:40.486Z"
    },
    ...
    ]
}
```

### Get a visitor by id

  `GET /api/v3/globalSettings/visitors/{id}`

#### Parameters

Path Parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  | `id` | Guid | yes |  The id of the visitor |

#### Response

the response is: [Visitor](#visitor-object) Object

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

## Public Canned Message Endpoints

### Get all Public Canned Message Categories in site

  `GET /api/v3/globalSettings/publicCannedMessageCategories`

#### Parameters

    No parameters

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
    "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
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
  | `id` | Guid | yes  |  The id of the public canned message category |

#### Response

the response is: [Public Canned Message Category](#public-Canned-Message-Category-object) Object

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
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

### Create a new Public Canned Message Category

  `POST /api/v3/globalSettings/publicCannedMessageCategories`

#### Parameters

Request Body

  The request body contains data with the [Public Canned Message Category](#public-Canned-Message-Category-object) structure

example:
```Json
{
  "name": "testtest",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

#### Response

the response is: [Public Canned Message Category](#public-Canned-Message-Category-object) Object

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
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/publicCannedMessageCategories/7D3E7435-F956-29FE-C089-57241AFBB297

{
  "id": "7D3E7435-F956-29FE-C089-57241AFBB297",
  "name": "testtest",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
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

  The request body contains data with the [Public Canned Message Category](#public-Canned-Message-Category-object) structure

example:
```Json
{
  "name": "testtest22222",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

#### Response

the response is: [Public Canned Message Category](#public-Canned-Message-Category-object) Object

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
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
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
```json
HTTP/1.1 204 No Content
```

# Public Canned Message

  You need `Manage Pulbic Canned Messages` permission to manage canned message.

- `GET /api/v3/globalSettings/publicCannedMessages` - [Get all public canned messages in site](#get-all-Public-Canned-Messages-in-site)
- `GET /api/v3/globalSettings/publicCannedMessages/{id}` - [Get a public canned message by id](#get-a-Public-Canned-Message-by-id)
- `POST /api/v3/globalSettings/publicCannedMessages` - [create a new public canned message](#create-a-new-Public-Canned-Message)
- `POST /api/v3/globalSettings/publicCannedMessages/{id}/similarQuestions`  - [create a new public similar questions](#create-a-new-public-similar-questions)
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
  | `IfSetHtmlMessageForEmail` | boolean  | | no | no | false | |
  | `htmlMessage` | string  | | no | no | | |
  | `categoryId` | Guid | | no | yes | | |
  | `category` | [Public Canned Message Category](#public-Canned-Message-Category-object)  | yes | N/A | N/A | |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `publicCannedMessageCategory` is included. |
  | `shortcuts` | string  | | no | no | | Whether the custom away status is system or not. |
  | `similarQuestions` | string[]  | | no | no | | Available when Agent Assist is enabled. |

## Public Canned Message Endpoints

### Get all Public Canned Messages in site

  `GET /api/v3/globalSettings/publicCannedMessages`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `publicCannedMessageCategory` |

#### Response

the response is: list of [Public Canned Message](#public-Canned-Message-object) Object

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
        "IfSetHtmlMessageForEmail": false,
        "htmlMessage": "",
        "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
        "category":    { // include public canned message category
          "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
          "name": "puddddtresult",
         "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
        },
        "shortcuts": "",
        "similarQuestions": ["are you ok?"]
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

the response is: [Public Canned Message](#public-Canned-Message-object) Object

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
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "category":    { // include public canned message category
    "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
    "name": "puddddtresult",
    "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
  },
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

### Create a new Public Canned Message

  `POST /api/v3/globalSettings/publicCannedMessages`

#### Parameters

Request Body

  The request body contains data with the [Public Canned Message](#public-Canned-Message-object) structure

example:
```Json
{
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

#### Response

the response is: [Public Canned Message](#public-Canned-Message-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages/19B21FEE-B0C5-2A61-0D34-26FB057D15EE

{
  "id": "19B21FEE-B0C5-2A61-0D34-26FB057D15EE",
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

### Create a new public similar questions

  `POST /api/v3/globalSettings/publicCannedMessages/{id}/similarQuestions`

#### Parameters

Request Body

  The request body contains data with the string array.

example:
```Json
 ["not ok?"]
```

#### Response

the response is: [Public Canned Message](#public-Canned-Message-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  ["not ok?"]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages/19B21FEE-B0C5-2A61-0D34-26FB057D15EE/similarQuestions
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/publicCannedMessages/19B21FEE-B0C5-2A61-0D34-26FB057D15EE/similarQuestions

{
  "id": "19B21FEE-B0C5-2A61-0D34-26FB057D15EE",
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?","not ok?"]
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

  The request body contains data with the [Public Canned Message](#public-Canned-Message-object) structure

example:
```Json
{
  "name": "test11111",
  "message": "test11111",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

#### Response

the response is: [Public Canned Message](#public-Canned-Message-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "test11111",
  "message": "test11111",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
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
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
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

## Private Canned Message Category Endpoints

### Get all Private Canned Message Categories in site

  `GET /api/v3/globalSettings/privateCannedMessageCategories`

#### Parameters

    No parameters

#### Response

the response is: list of [Private Canned Message Category](#private-Canned-Message-Category-object) Object

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
        "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
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

the response is: [Private Canned Message Category](#private-Canned-Message-Category-object) Object

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
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
}
```

### Create a new Private Canned Message Category

  `POST /api/v3/globalSettings/privateCannedMessageCategories`

#### Parameters

Request Body

  The request body contains data with the [Private Canned Message Category](#private-Canned-Message-Category-object) structure

example:
```Json
{
  "name": "testtest111111",
  "parentId": "D5673FC9-9B1A-7030-C7C5-0B4C7A641EFC"
}
```

#### Response

the response is: [Private Canned Message Category](#private-Canned-Message-Category-object) Object

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
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/privateCannedMessageCategories/FFD377AA-81FA-EC53-1E57-DD73C0B36F6C
{
  "id": "FFD377AA-81FA-EC53-1E57-DD73C0B36F6C",
  "name": "testtest111111",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
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

  The request body contains data with the [Private Canned Message Category](#private-Canned-Message-Category-object) structure

example:
```Json
{
  "name": "testtest22222",
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
}
```

#### Response

the response is: [Private Canned Message Category](#private-Canned-Message-Category-object) Object

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
  "parentId": "841193BB-8A51-E4F3-EB17-6B4C222D744F"
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
- `POST /api/v3/globalSettings/publicCannedMessages/{id}/similarQuestions`  - [create a new private similar questions](#create-a-new-private-similar-questions)
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
  | `IfSetHtmlMessageForEmail` | bool | | no | no | false | |
  | `htmlMessage` | string  | | no | no | | |
  | `categoryId` | Guid | | no | no | | |
  | `category` | [Private Canned Message Category](#private-Canned-Message-Category-object)  | yes | no | no | |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `privateCannedMessageCategory` is included. |
  | `shortcuts` | string  | | no | no | | Whether the custom away status is system or not. |
  | `similarQuestions` | string[]  | | no | no | | Available when Agent Assist is enabled. |

## Private Canned Message Endpoints

### Get all Private Canned Messages in site

  `GET /api/v3/globalSettings/privateCannedMessages`

#### Parameters

Query string

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  | `include` | string | no  |  | Available value: `privateCannedMessageCategory` |

#### Response

the response is: list of [Private Canned Message](#private-Canned-Message-object) Object

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
        "IfSetHtmlMessageForEmail": false,
        "htmlMessage": "",
        "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
        "category":    { // include private canned message category
          "id": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
          "name": "justfortest",
         "parentId": "A73FA2EB-4CE3-B195-94C6-567A24F7BDDC"
        },
        "shortcuts": "",
        "similarQuestions": ["are you ok?"]
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

the response is: [Private Canned Message](#private-Canned-Message-object) Object

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
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "category":    { // include private canned message category
    "id": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
    "name": "puddddtresult",
    "parentId": "A73FA2EB-4CE3-B195-94C6-567A24F7BDDC"
  },
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

### Create a new Private Canned Message

  `POST /api/v3/globalSettings/privateCannedMessages`

#### Parameters

Request Body

  The request body contains data with the [Private Canned Message](#private-Canned-Message-object) structure

example:
```Json
{
  "name": "privateCannedMessageCategorytest1111",
  "message": "privateCannedMessageCategorytest1111",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

#### Response

the response is: [Private Canned Message](#private-Canned-Message-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "privateCannedMessageCategorytest1111",
  "message": "privateCannedMessageCategorytest1111",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages/822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F

{
  "id": "822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F",
  "name": "privateCannedMessageCategorytest1111",
  "message": "privateCannedMessageCategorytest1111",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

### Create a new private similar questions

  `POST /api/v3/globalSettings/privateCannedMessages/{id}/similarQuestions`

#### Parameters

Request Body

  The request body contains data with the string array.

example:
```Json
 ["not ok?"]
```

#### Response

the response is: [Public Canned Message](#public-Canned-Message-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  ["not ok?"]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages/822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F/similarQuestions
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/privateCannedMessages/822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F/similarQuestions

{
  "id": "822B7B6A-05E9-5DA2-A1B0-1D0FB034AA0F",
  "name": "publicCannedMessageCategorytest",
  "message": "publicCannedMessageCategorytest",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "5A563046-374D-3C4E-4D4A-2CA3812A42C8",
  "shortcuts": "",
  "similarQuestions": ["are you ok?","not ok?"]
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

  The request body contains data with the [Private Canned Message](#private-Canned-Message-object) structure

example:
```Json
{
  "name": "privateCannedMessageCategorytest2222",
  "message": "privateCannedMessageCategorytest2222",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
}
```

#### Response

the response is: [Private Canned Message](#private-Canned-Message-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "privateCannedMessageCategorytest2222",
  "message": "privateCannedMessageCategorytest2222",
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
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
  "IfSetHtmlMessageForEmail": false,
  "htmlMessage": "",
  "categoryId": "579BCAE9-F43A-CD32-CAF8-BD56786F1447",
  "shortcuts": "",
  "similarQuestions": ["are you ok?"]
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

  | Name | Type | Read-only | Mandatory| Default | Description |
  | - | - | :-: | :-: | :-: | - |
  |`id` | Guid | yes | no | | Id of the current item.  |
  | `name` | string  | no | yes | | Name of the agent away status. |
  | `isSystem` | boolean  | yes | no | false | Whether the agent away status is system or not. |
  | `order` | integer  | yes | no | | The order of the agent away status. |

## Agent Away Status Endpoints

### Get all Agent Away Statuses of a site

  `GET /api/v3/globalSettings/agentAwayStatuses`

#### Parameters

    No parameters

#### Response

the response is: list of [Agent Away Status](#agent-Away-Status-object) Object

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

the response is: [Agent Away Status](#agent-Away-Status-object) Object

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

  The request body contains data with the [Agent Away Status](#agent-Away-Status-object) structure

example:
```Json
{
  "name": "agentAwayStatuses11",
  "isSystem": false,
  "order": 1
}
```

#### Response

the response is: [Agent Away Status](#agent-Away-Status-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "agentAwayStatuses11"
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses
```

Response
``` json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/agentAwayStatuses/D4F6BA7F-9BB6-C509-8BB9-0705B3E500F2

{
  "id": "D4F6BA7F-9BB6-C509-8BB9-0705B3E500F2",
  "name": "agentAwayStatuses11",
  "isSystem": false,
  "order": 5
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

  The request body contains data with the [Agent Away Status](#agent-Away-Status-object) structure

example:
```Json
{
  "name": "agentAwayStatuses23",
}
```

#### Response

the response is: [Agent Away Status](#agent-Away-Status-object) Object

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
  "name": "agentAwayStatuses23",
  "isSystem": false,
  "order": 5
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

You need `Manage Security` permission to manage whitelisted login ip restrictions.

   When Login IP Whitelist is enabled, site administrator can add IP range for this site and only agents within the IP range can log in successfully.

  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges` - [Get a list of whitelisted login IP ranges in site](#get-all-whitelisted-login-ip-ranges)
  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [Get a whitelisted login IP range by id](#get-a-whitelisted-login-ip-ranges)
  + `POST /api/v3/globalSettings/whitelistedLoginIPRanges` - [create a new whitelisted login IP range](#create-a-new-whitelisted-login-ip-range)
  + `PUT /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [update a whitelisted login IP range](#update-a-whitelisted-login-ip-range)
  + `DELETE /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [delete a whitelisted login IP range](#delete-a-whitelisted-login-ip-range)

## Whitelisted Login IP Range Related Object Json Format

### Whitelisted Login IP Range Object

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | Guid | | N/A | N/A | | |
  |`ipFrom` | string | | no | yes | | Where an IP range starts.|
  |`ipTo` | string | | no | yes | | Where an IP range ends.|
  |`createdTime` | DateTime | | N/A | N/A |  |  |

## Whitelisted Login IP Range Endpoints

### Get all Whitelisted Login IP Ranges

  `GET /api/v3/globalSettings/whitelistedLoginIPRanges`

  #### Parameters
    No parameters

  #### Response

  The response is a list of [Whitelisted Login IP Range](#whitelisted-login-ip-range-object) Objects

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json[
{
  "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
  "ipFrom": "201.195.21.5",
  "ipTo": "201.195.21.8",
  "createdTime": "2020-01-01",
},
...,
]
```

### Get a Whitelisted Login IP Ranges

  `GET /api/v3/globalSettings/whitelistedLoginIPRanges/{id}`

#### Parameters
Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The id of the whitelisted Login IP Ranges |

#### Response

The response is a [Whitelisted Login IP Range](#whitelisted-login-ip-range-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
  {
  "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
  "ipFrom": "201.195.21.5",
  "ipTo": "201.195.21.8",
  "createdTime": "2020-01-01",
  }
```

### Create a new whitelisted Login IP Range

  `POST /api/v3/globalSettings/whitelistedLoginIPRanges`

####  Parameters

Request body
  The request body contains data with the [Whitelisted Login IP Range](#whitelisted-login-ip-range-object) structure

  example:
```json
 {
    "ipFrom": "201.195.21.5",
    "ipTo": "201.195.21.8",
  }
```

#### Response

The response is:
  [Whitelisted Login IP Range](#whitelisted-login-ip-range-object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "ipFrom": "201.195.21.5",
      "ipTo": "201.195.21.8",
    }' -X POST https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
 {
    "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "ipFrom": "201.195.21.5",
    "ipTo": "201.195.21.8",
    "createdTime": "2020-01-01",
  }
```


### Update a whitelisted Login IP Range
  `PUT /api/v3/globalSettings/whitelistedLoginIPRanges/{id}`

####  Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  The id of the whitelisted Login IP Range |

Request body

  The request body contains data with the [Whitelisted Login IP Range](#whitelisted-login-ip-range-object) structure

  example:
```json
 {
    "ipFrom": "201.195.21.5",
    "ipTo": "201.195.21.8",
  }
```

#### Response

The response is:
  [Whitelisted Login IP Range](#whitelisted-login-ip-range-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "ipFrom": "201.195.21.5",
      "ipTo": "201.195.21.8",
    }' -X PUT https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
  HTTP/1.1 200 OK
  Content-Type: https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
 {
    "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "ipFrom": "201.195.21.5",
    "ipTo": "201.195.21.8",
    "createdTime": "2020-01-01",
  }
```

### Delete a whitelisted Login IP Range

  `DELETE /api/v3/globalSettings/whitelistedLoginIPRanges/{id}`

#### Parameters

Path parameters

  | Name  | Type | Required  | Description |
  | - | - | - | - |
  |`id` | Guid | yes  |  the whitelisted Login IP Range id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Agent SSO

  You need `Manage Settings` permission to setting sso for a site.

- `GET /api/v3/globalSettings/agentSSO` - [Get Agent SSO](#get-agent-sso)
- `PUT /api/v3/globalSettings/agentSSO` - [update Agent SSO](#update-agent-sso)

## Related Object Json Format

### Agent SSO Object

  Agent SSO Object is represented as simple flat JSON objects with the following keys:

  | Name | Type | Include | Read-only| Mandatory| Default | Description |
  | - | - | - | :-: | :-: | :-: | - |
  | `isEnabled` | bool  | | no | yes|| |
  | `protocolType` | string |  | no | yes | | including `SAML` and `JWT`. |
  | `samlSSOURL` | string |  | no |yes | |mandatory when Type is `SAML`. |
  | `samlLogoutURL` | string |  | no | no | | only available when Type is `SAML`. |
  | `samlCertificate` | string |  | no | yes | | SAML certificate, mandatory when Type is `SAML`.|
  | `jwtLoginURL` | string |  | no | yes | | mandatory when Type is `JWT`. |
  | `jwtLogoutURL` | string |  | no | no | | only available when Type is `JWT`.  |
  | `jwtSecret` | string |  | no | no | | mandatory when Type is `JWT`.  |

## Agent SSO Endpoints

### Get Agent SSO

  `GET /api/v3/globalSettings/agentSSO`

#### Parameters

    No parameters

#### Response

the response is: [Agent SSO](#agent-SSO-object) Object

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
  "protocolType": "SAML",
  "samlSSOURL": "https://domain.comm100.com/SAML/SSOLogin",
  "samlLogoutURL": "https://domain.comm100.com/SAML/SSOLogout",
  "samlCertificate": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----",
  "jwtLoginURL": "",
  "jwtLogoutURL": "",
  "jwtSecret": ""
}
```

### Update Agent SSO

  `PUT /api/v3/globalSettings/agentSSO`

#### Parameters

Request Body

  The request body contains data with the [Agent SSO](#agent-SSO-object) structure

 example:
```Json
  {
    "isEnabled": true,
    "protocolType": "JWT",
    "jwtLoginURL": "",
    "jwtLogoutURL": "",
    "jwtSecret": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----"
  }
```

#### Response

the response is: [Agent SSO](#agent-SSO-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "isEnabled": true,
    "protocolType": "JWT",
    "jwtLoginURL": "",
    "jwtLogoutURL": "",
    "jwtSecret": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----"
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/agentSSO
```
Response
```Json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "isEnabled": true,
  "protocolType": "JWT",
  "samlSSOURL": "",
  "samlLogoutURL": "",
  "samlCertificate": "",
  "jwtLoginURL": "https://domain.comm100.com/JWT/SSOLogin",
  "jwtLogoutURL": "https://domain.comm100.com/JWT/SSOLogin",
  "jwtSecret": "9F4709DB-C391-4896-94BA-3A17BE12D9E2jji-----"
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
  | `isEnabled` | bool  | | no | N/A | false | |
  | `loginURL` | string  | | no | N/A | | |
  | `logoutURL` | string  | | no | N/A | | |
  | `changePasswordURL` | string  | | no | N/A | | |
  | `certificate` | string  | | no | N/A | | Base64 data of certificate file. |
  | `certificateFileName` | string  | | no | N/A | | |
  | `fieldMappings` | [Field Mapping](#field-Mapping-object)[]  | | no | N/A | | |
  | `perCampaign` | [Visitor SSO Campaign](#visitor-SSO-Campaign-object)[]  |  | no | N/A | | |

### Field Mapping Object

Field Mapping is represented as simple flat JSON objects with the following keys:

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `attribute` | string | | no | yes | | SSO attribute name. |
  | `comm100Field` | string | | no | yes | | the Comm100 field name |

### Visitor SSO Campaign Object

Visitor SSO Campaign is represented as simple flat JSON objects with the following keys:

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `campaignId` | Guid |  | no | yes | | Id of the campaign. |
  | `campaign` | [Campaign](#campaign-object)  | yes | N/A | N/A | | Available only when campaign is included  |
  | `signInOption` | string |  | no | no | `noSignIn` | Type of the sign in, including `noSignIn`, `signInOptional` and `signInRequired`. |
  | `isPrechatFromSkipped` | bool |  | no | no | true | Whether the pre-chat form is skipped when visitors sign in. |

## Visitor SSO Endpoints

### Get Visitor SSO

  `GET /api/v3/globalSettings/visitorSSO`

#### Parameters

Query string

  | Name  | Type | Required | Default | Description |
  | - | - | :-: | :-: | - |
  | `include` | string | no  | |  Available value: `campaign` |

#### Response

the response is: [Visitor SSO](#visitor-SSO-object) Object

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
    "certificate": "amdoamdoaGdmcnRk",
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

  The request body contains data with the [Visitor SSO](#visitor-SSO-object) structure

example:
```Json
  {
    "isEnabled": true,
    "loginURL": "http://www.xzcs11ffffffff1a",
    "logoutURL": "http://www.xzcs11ffffffff1a",
    "changePasswordURL": "http://www.xzcs11ffffffff1a",
    "certificate": "amdoamdoaGdmcnRk",
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

the response is: [Visitor SSO](#visitor-SSO-object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "isEnabled": true,
    "loginURL": "http://www.xzcs11ffffffff1a",
    "logoutURL": "http://www.xzcs11ffffffff1a",
    "changePasswordURL": "http://www.xzcs11ffffffff1a",
    "certificate": "amdoamdoaGdmcnRk",
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
    "certificate": "amdoamdoaGdmcnRk",
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
  You need `View Audit Log` permission to view audit logs.

  + `GET /api/v3/globalSettings/auditLogs` - [Get audit logs list](#get-audit-logs-list)

## Audit Log Object Json Format

### Audit Log Object

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | integer | | N/A | N/A | |  |
  |`category` | string| | N/A | N/A | | The value options include: liveChat, ticketingAndMessaging, bot, globalSettings, knowledgeBase |
  |`createdTime` | DateTime | | N/A | N/A |  |  |
  |`actionType` | string | | N/A  | N/A  | | [action types for different applications](#action-types-for-different-applications) |
  |`actionSummary` | string| | N/A  | N/A  | |  |
  |`actionDetails` | string| | N/A  | N/A  | |  |
  |`createdBy` | integer | | N/A  | N/A  | | the id of oprator agent |
  |`agent` | [Agent](#agent) | yes | N/A  | N/A  | | the oprator agent |

### Audit Log List Response Object

  Agent List Object for agent list Response, include count and page information.

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | :-: | - |
  |`count` | integer  | N/A | yes | no | | The total count of the query  |
  |`nextPage` | string  | N/A | yes | no | | The next page url of the query  |
  |`previousPage` | string  | N/A | yes | no | | The previous page url of the query  |
  |`auditLogs`| [AuditLog](#audit-log-object)[]| N/A | yes| 0 | | a list of Audit Log. |

### Action types for different applications

  | Live Chat | Ticketing And Messaging | Knowledge Base | Bot|	Global |
  | - | - | - | - | - |
  | audioAndVideoChatManagement | autoAllocationManagement | categoryManagement | agentBotLearningManagement | accountProfileManagement |
  | autoAcceptSetting | blockSenderManagement | articleManagement | agentBotSettingManagement | agentManagement |
  | autoInvitationManagement | channelIntegrationManagement | tagManagement | agentBotSynonymManagement | agentRoleManagement |
  | autoTranslationManagement | conversationManagement | imageManagement | botSettings | applicationsManagement |
  | banManagement | fieldsAndMappingsManagement | designManagement | botsManagement | billingInfoManagement |
  | campaignsManagement | routingRulesManagement | customPageManagement | entitiesManagement | cannedMessageManagement |
  | chatsAuto-AllocationManagement | slaPoliciesManagement | knowledgeBaseManagement | intentsManagement | customAwayStatusManagement |
  | chatSettingsManagement | triggerManagement | | quickRepliesManagement | customerAccountsManagement |
  | cobrowsingManagement | workingTimeAndHolidaysManagement | | smartTriggersManagement | departmentManagement |
  | conversionManagement | | | visitorQuestioninLearningDelete | integrationAndAPIManagement |
  | customVariableManage | | | | licenseManagement |
  | dashboardCustomMetricManagement | | | | manageAccountStatusorState |
  | routingRulesManagement | | | | manuallyChargeandActiveAccount |
  | secureFormManagement | | | | restrictedWordsManagement |
  | segmentationManagement | | | | securityManagement |
  | shiftsManagement | | | | siteProfileManagement |
  | transcriptDelete | | | |   |
  | visitorSSOManagement | | | |   |

## Audit Log Endpoints

### Get audit logs list

  `GET /api/v3/globalSettings/auditLogs`

  #### Parameters

   Query stringno

  | Name  | Type | Required  | Default | Description |
  | - | - | - | - | - |
  |`dateFrom`|DateTime|no||The date from which agent did the action, format as yyyy-MM-ddTHH:mm:ss. |
  |`dateTo`|DateTime|no||The date when an agent ended the action, format as yyyy-MM-ddTHH:mm:ss. |
  |`category`|string|no||The category which the action belongs to |
  |`actionType`|string|no||The action type. |
  |`agentId`|integer |no||id of the agent who did the action. |
  |`keywords`|string|no||The key words associated with the action. |
  |`pageIndex`|integer|no| 1 | The page index of the query. |
  |`pageSize`|integer|no| 10 |The page size of the query. |
  |`include`|string|no||Available value: `agent` |


#### Response

  The response is a list of [Audit Log List Response](#audit-log-list-response-object) Objects

  #### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/auditLogs
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "count": 1234,
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/auditLogs?pageIndex=2",
    "previousPage": null,
    "auditLogs": [
      {
        "id": 201,
        "name": "add Agent",
        "category": "My Account Global Settings",
        "createdTime": "2020-02-02",
        "createdBy": 68,
        "actionType": "Add Agent",
        "actionSummary": "Add Agent",
        "actionDetails": "Add Agent for Live Chat",
      },
      ...,
      ]
}
```




# Time Zone Options


  |   Id    |   Display name   |
  |   -   |   -   |
  |  datelineStandardTime  |   (UTC-12:00) International Date Line West   |
  |  utc-11  |   (UTC-11:00) Coordinated Universal Time-11   |
  |  aleutianStandardTime  |   (UTC-10:00) Aleutian Islands   |
  |  hawaiianStandardTime  |   (UTC-10:00) Hawaii   |
  |  marquesasStandardTime  |   (UTC-09:30) Marquesas Islands   |
  |  alaskanStandardTime  |   (UTC-09:00) Alaska   |
  |  utc-09  |   (UTC-09:00) Coordinated Universal Time-09   |
  |  pacificStandardTime(Mexico)  |   (UTC-08:00) Baja California   |
  |  utc-08  |   (UTC-08:00) Coordinated Universal Time-08   |
  |  pacificStandardTime  |   (UTC-08:00) Pacific Time (US & Canada)   |
  |  usMountainStandardTime  |   (UTC-07:00) Arizona   |
  |  mountainStandardTime(Mexico)  |   (UTC-07:00) Chihuahua, La Paz, Mazatlan   |
  |  mountainStandardTime  |   (UTC-07:00) Mountain Time (US & Canada)   |
  |  centralAmericaStandardTime  |   (UTC-06:00) Central America   |
  |  centralStandardTime  |   (UTC-06:00) Central Time (US & Canada)   |
  |  easterIslandStandardTime  |   (UTC-06:00) Easter Island   |
  |  centralStandardTime(Mexico)  |   (UTC-06:00) Guadalajara, Mexico City, Monterrey   |
  |  canadaCentralStandardTime  |   (UTC-06:00) Saskatchewan   |
  |  saPacificStandardTime  |   (UTC-05:00) Bogota, Lima, Quito, Rio Branco   |
  |  easternStandardTime(Mexico)  |   (UTC-05:00) Chetumal   |
  |  easternStandardTime  |   (UTC-05:00) Eastern Time (US & Canada)   |
  |  haitiStandardTime  |   (UTC-05:00) Haiti   |
  |  cubaStandardTime  |   (UTC-05:00) Havana   |
  |  usEasternStandardTime  |   (UTC-05:00) Indiana (East)   |
  |  turksAndCaicosStandardTime  |   (UTC-05:00) Turks and Caicos   |
  |  paraguayStandardTime  |   (UTC-04:00) Asuncion   |
  |  atlanticStandardTime  |   (UTC-04:00) Atlantic Time (Canada)   |
  |  venezuelaStandardTime  |   (UTC-04:00) Caracas   |
  |  centralBrazilianStandardTime  |   (UTC-04:00) Cuiaba   |
  |  saWesternStandardTime  |   (UTC-04:00) Georgetown, La Paz, Manaus, San Juan   |
  |  pacificSAStandardTime  |   (UTC-04:00) Santiago   |
  |  newfoundlandStandardTime  |   (UTC-03:30) Newfoundland   |
  |  tocantinsStandardTime  |   (UTC-03:00) Araguaina   |
  |  e.SouthAmericaStandardTime  |   (UTC-03:00) Brasilia   |
  |  saEasternStandardTime  |   (UTC-03:00) Cayenne, Fortaleza   |
  |  argentinaStandardTime  |   (UTC-03:00) City of Buenos Aires   |
  |  greenlandStandardTime  |   (UTC-03:00) Greenland   |
  |  montevideoStandardTime  |   (UTC-03:00) Montevideo   |
  |  magallanesStandardTime  |   (UTC-03:00) Punta Arenas   |
  |  saintPierreStandardTime  |   (UTC-03:00) Saint Pierre and Miquelon   |
  |  bahiaStandardTime  |   (UTC-03:00) Salvador   |
  |  utc-02  |   (UTC-02:00) Coordinated Universal Time-02   |
  |  mid-AtlanticStandardTime  |   (UTC-02:00) Mid-Atlantic - Old   |
  |  azoresStandardTime  |   (UTC-01:00) Azores   |
  |  capeVerdeStandardTime  |   (UTC-01:00) Cabo Verde Is.   |
  |  utc  |   (UTC) Coordinated Universal Time   |
  |  gmtStandardTime  |   (UTC+00:00) Dublin, Edinburgh, Lisbon, London   |
  |  greenwichStandardTime  |   (UTC+00:00) Monrovia, Reykjavik   |
  |  saoTomeStandardTime  |   (UTC+00:00) Sao Tome   |
  |  moroccoStandardTime  |   (UTC+01:00) Casablanca   |
  |  w.EuropeStandardTime  |   (UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna   |
  |  centralEuropeStandardTime  |   (UTC+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague   |
  |  romanceStandardTime  |   (UTC+01:00) Brussels, Copenhagen, Madrid, Paris   |
  |  centralEuropeanStandardTime  |   (UTC+01:00) Sarajevo, Skopje, Warsaw, Zagreb   |
  |  w.CentralAfricaStandardTime  |   (UTC+01:00) West Central Africa   |
  |  jordanStandardTime  |   (UTC+02:00) Amman   |
  |  gtbStandardTime  |   (UTC+02:00) Athens, Bucharest   |
  |  middleEastStandardTime  |   (UTC+02:00) Beirut   |
  |  egyptStandardTime  |   (UTC+02:00) Cairo   |
  |  e.EuropeStandardTime  |   (UTC+02:00) Chisinau   |
  |  syriaStandardTime  |   (UTC+02:00) Damascus   |
  |  westBankStandardTime  |   (UTC+02:00) Gaza, Hebron   |
  |  southAfricaStandardTime  |   (UTC+02:00) Harare, Pretoria   |
  |  fleStandardTime  |   (UTC+02:00) Helsinki, Kyiv, Riga, Sofia, Tallinn, Vilnius   |
  |  israelStandardTime  |   (UTC+02:00) Jerusalem   |
  |  kaliningradStandardTime  |   (UTC+02:00) Kaliningrad   |
  |  sudanStandardTime  |   (UTC+02:00) Khartoum   |
  |  libyaStandardTime  |   (UTC+02:00) Tripoli   |
  |  namibiaStandardTime  |   (UTC+02:00) Windhoek   |
  |  arabicStandardTime  |   (UTC+03:00) Baghdad   |
  |  turkeyStandardTime  |   (UTC+03:00) Istanbul   |
  |  arabStandardTime  |   (UTC+03:00) Kuwait, Riyadh   |
  |  belarusStandardTime  |   (UTC+03:00) Minsk   |
  |  russianStandardTime  |   (UTC+03:00) Moscow, St. Petersburg   |
  |  e.AfricaStandardTime  |   (UTC+03:00) Nairobi   |
  |  iranStandardTime  |   (UTC+03:30) Tehran   |
  |  arabianStandardTime  |   (UTC+04:00) Abu Dhabi, Muscat   |
  |  astrakhanStandardTime  |   (UTC+04:00) Astrakhan, Ulyanovsk   |
  |  azerbaijanStandardTime  |   (UTC+04:00) Baku   |
  |  russiaTimeZone3  |   (UTC+04:00) Izhevsk, Samara   |
  |  mauritiusStandardTime  |   (UTC+04:00) Port Louis   |
  |  saratovStandardTime  |   (UTC+04:00) Saratov   |
  |  georgianStandardTime  |   (UTC+04:00) Tbilisi   |
  |  volgogradStandardTime  |   (UTC+04:00) Volgograd   |
  |  caucasusStandardTime  |   (UTC+04:00) Yerevan   |
  |  afghanistanStandardTime  |   (UTC+04:30) Kabul   |
  |  westAsiaStandardTime  |   (UTC+05:00) Ashgabat, Tashkent   |
  |  ekaterinburgStandardTime  |   (UTC+05:00) Ekaterinburg   |
  |  pakistanStandardTime  |   (UTC+05:00) Islamabad, Karachi   |
  |  qyzylordaStandardTime  |   (UTC+05:00) Qyzylorda   |
  |  indiaStandardTime  |   (UTC+05:30) Chennai, Kolkata, Mumbai, New Delhi   |
  |  sriLankaStandardTime  |   (UTC+05:30) Sri Jayawardenepura   |
  |  nepalStandardTime  |   (UTC+05:45) Kathmandu   |
  |  centralAsiaStandardTime  |   (UTC+06:00) Astana   |
  |  bangladeshStandardTime  |   (UTC+06:00) Dhaka   |
  |  omskStandardTime  |   (UTC+06:00) Omsk   |
  |  myanmarStandardTime  |   (UTC+06:30) Yangon (Rangoon)   |
  |  seAsiaStandardTime  |   (UTC+07:00) Bangkok, Hanoi, Jakarta   |
  |  altaiStandardTime  |   (UTC+07:00) Barnaul, Gorno-Altaysk   |
  |  w.MongoliaStandardTime  |   (UTC+07:00) Hovd   |
  |  northAsiaStandardTime  |   (UTC+07:00) Krasnoyarsk   |
  |  n.CentralAsiaStandardTime  |   (UTC+07:00) Novosibirsk   |
  |  tomskStandardTime  |   (UTC+07:00) Tomsk   |
  |  chinaStandardTime  |   (UTC+08:00) Beijing, Chongqing, Hong Kong, Urumqi   |
  |  northAsiaEastStandardTime  |   (UTC+08:00) Irkutsk   |
  |  singaporeStandardTime  |   (UTC+08:00) Kuala Lumpur, Singapore   |
  |  w.AustraliaStandardTime  |   (UTC+08:00) Perth   |
  |  taipeiStandardTime  |   (UTC+08:00) Taipei   |
  |  ulaanbaatarStandardTime  |   (UTC+08:00) Ulaanbaatar   |
  |  ausCentralW.StandardTime  |   (UTC+08:45) Eucla   |
  |  transbaikalStandardTime  |   (UTC+09:00) Chita   |
  |  tokyoStandardTime  |   (UTC+09:00) Osaka, Sapporo, Tokyo   |
  |  northKoreaStandardTime  |   (UTC+09:00) Pyongyang   |
  |  koreaStandardTime  |   (UTC+09:00) Seoul   |
  |  yakutskStandardTime  |   (UTC+09:00) Yakutsk   |
  |  cen.AustraliaStandardTime  |   (UTC+09:30) Adelaide   |
  |  aUSCentralStandardTime  |   (UTC+09:30) Darwin   |
  |  e.AustraliaStandardTime  |   (UTC+10:00) Brisbane   |
  |  aUSEasternStandardTime  |   (UTC+10:00) Canberra, Melbourne, Sydney   |
  |  westPacificStandardTime  |   (UTC+10:00) Guam, Port Moresby   |
  |  tasmaniaStandardTime  |   (UTC+10:00) Hobart   |
  |  vladivostokStandardTime  |   (UTC+10:00) Vladivostok   |
  |  lordHoweStandardTime  |   (UTC+10:30) Lord Howe Island   |
  |  bougainvilleStandardTime  |   (UTC+11:00) Bougainville Island   |
  |  russiaTimeZone10  |   (UTC+11:00) Chokurdakh   |
  |  magadanStandardTime  |   (UTC+11:00) Magadan   |
  |  norfolkStandardTime  |   (UTC+11:00) Norfolk Island   |
  |  sakhalinStandardTime  |   (UTC+11:00) Sakhalin   |
  |  centralPacificStandardTime  |   (UTC+11:00) Solomon Is., New Caledonia   |
  |  russiaTimeZone11  |   (UTC+12:00) Anadyr, Petropavlovsk-Kamchatsky   |
  |  newZealandStandardTime  |   (UTC+12:00) Auckland, Wellington   |
  |  utc+12  |   (UTC+12:00) Coordinated Universal Time+12   |
  |  fijiStandardTime  |   (UTC+12:00) Fiji   |
  |  kamchatkaStandardTime  |   (UTC+12:00) Petropavlovsk-Kamchatsky - Old   |
  |  chathamIslandsStandardTime  |   (UTC+12:45) Chatham Islands   |
  |  utc+13  |   (UTC+13:00) Coordinated Universal Time+13   |
  |  tongaStandardTime  |   (UTC+13:00) Nuku'alofa   |
  |  samoaStandardTime  |   (UTC+13:00) Samoa   |
  |  lineIslandsStandardTime  |   (UTC+14:00) Kiritimati Island   |


