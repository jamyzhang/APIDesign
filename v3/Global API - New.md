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
  + `GET /api/v3/globalSettings/site` - [Get profile of a single site](#Get-profile-of-a-single-site)
  + `PUT /api/v3/globalSettings/site` - [Update profile of a site](#Update-profile-of-a-site)


## Site Related Object Json Format

### Site Object
  Each Comm100 account is treated as a Site and has a unique Site ID.  

 | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
 | - | - | :-: | :-: | :-: | :-: | - | 
 |`id` | integer  | | yes | no | 0 |Site ID will not be upgraded to GUID.|
 |`dateTimeFormat` | enum| | no | no | 'MM-dd-yyyy HH:mm:ss'|Date & Time Format of site.|
 |`timeZone` | enum| | no | yes |  |Time zone of site.|
 |`company` | string | | no | yes | |Company name.|
 |`companySize` | enum| | no | no | 0 ??|1-20, 21-50, 51-100, 101-180, 181-310, 311-600, Above 600. The number of staff of the company.|
 |`website` | string  | | no | yes | |Company website. cpanel 客户端的 site profile 不一致??|
 |`registeredEmail` | string  | | no | yes | |Email used for site registration.|
 |`phone` | string | | no | no | |Company phone number.|
 |`fax` | string | | no | no | |Company fax number.|
 |`mailingAddress` | string | | no | no | |The mailing address of the company.|
 |`city` | string  | | no | no | |City where the company located.|
 |`stateOrProvince` | string  | | no | no | |State/Province where the company located.|
 |`countryOrRegion` | string | | no | no | |Country/Region where the company located.|
 |`postalOrZipCode` | string | | no | no | |Postal/Zip Code where the company located.|
 |`firstName` | string  | | no | yes | |First Name of site registrant.|
 |`lastName` | string  | | no | yes | |Last Name of site registrant.|
 |`agents` | [Agent](#Agent)[]| yes | yes | no | |.|
 |`roles` | [Role](#Role)[]| yes | yes | no | |.|
 |`contact` | [Contact](#Contact)[]| yes | yes | no | |.|
 |`visitor` | [Visitor](#Visitor)[]| yes | yes | no | |.|
 |`publicCannedMessage` | [PublicCannedMessage](#Public-Canned-Message)[]| yes | yes | no |  |.|
 |`publicCannedMessageCategory` | [PublicCannedMessageCategory](#Public-Canned-Message-Category)[]| yes | yes | no |  |.|
 |`PrivateCannedMessage` | [Private-Canned-Message](#Private-Canned-Message)[]| yes | yes | no | |.|
 |`privateCannedMessageCategory` | [PrivateCannedMessageCategory](#Private-Canned-Message-Category)[]| yes | yes | no | |.|
 |`shift` | [Shift](#Shift)[]| yes | yes | no | |.|
 |`auditLog` | [AuditLog](#Audit-Log)[]| yes | yes | no | |.|
 |`oAuthClient` | [OAuthClient](#OAuth-Client)[]| yes | yes | no | |.|


## Site Endpoints

### Get profile of a single site
  `GET /api/v3/globalSettings/site`

#### Parameters
Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`agent`,`role`,`contact`
  ,`visitor`,`publicCannedMessage`,`publicCannedMessageCategory`
  ,`PrivateCannedMessage`,`privateCannedMessageCategory`,`shift`,`auditLog`,`oAuthClient` |

#### Response
  the response is forfile of [Site](#Site-Object) Object, just include base informations.

#### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/site?include=role
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json
    {
        "id"："10000"，
        "dateTimeFormat"："yyyy-MM-dd hh:mm:ss"，
        "timeZone"："(GMT-09:00)Alaska"，
        "company"："BMW"，
        "companySize"："5000"，
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
        "roles"[{
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "CustomRole",
      ...,
    },
        ...,]
    }
    ```


### Update profile of a site
  `PUT /api/v3/globalSettings/site`

#### Parameters
No Parameters

Request body 
  The request body contains data with the [Site](#Site-Object) Structure

#### Response
  the response is the forfile of [Site](#Site-Object) Object, just include base informations.

#### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -d '{
        "dateTimeFormat"："yyyy-MM-dd hh:mm:ss"，
        "timeZone"："(GMT-09:00)Alaska"，
        "company"："BMW"，
        "companySize"："5000"，
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
    }' -X PUT https://domain.comm100.com//api/v3/globalSettings/site
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json
    {
        "id"："10000"，
        "dateTimeFormat"："yyyy-MM-dd hh:mm:ss"，
        "timeZone"："(GMT-09:00)Alaska"，
        "company"："BMW"，
        "companySize"："5000"，
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
    }
    ```


# Agent

  + `GET /api/v3/globalSettings/agents` - [Get a list of agents in site](#Get-a-list-of-agents-in-site)  include department, role
  + `GET /api/v3/globalSettings/agents/{id}` - [Get an agent by id](#Get-an-agent-by-id)  include department, role
  + `GET /api/v3/globalSettings/roles/{roleId}/agents` - [Get a list of agents by role id](#Get-a-list-of-agents-by-role-id)  include department, role
  + `GET /api/v3/globalSettings/departments/{departmentId}/agents` - [Get a list of agents by department id](#Get-a-list-of-agents-by-department-id)  include department, role
  + `GET /api/v3/globalSettings/agents/me` - [Get current agent](#Get-current-agent)  include department, role
  + `POST /api/v3/globalSettings/agents` - [Create a new agent](#Create-a-new-agent)
  + `POST /api/v3/globalSettings/agents/{id}:unlock` - [Unlock the agent](#unlock-the-agent)
  + `POST /api/v3/globalSettings/agents/{id}:changePassword` - [Admin set an agent's password](#Admin-set-an-agent's-password)
  + `POST /api/v3/globalSettings/agents/me:changePassword` - [Change own password](#Change-own-password)
  + `PUT /api/v3/globalSettings/agents/{id}` - [Update an agent](#Update-an-agent)
  + `PUT /api/v3/globalSettings/agents/me` - [Update current agent](#Update-current-agent)
  + `DELETE /api/v3/globalSettings/agents/{id}` - [Delete an agent](#Delete-an-agent)

## Agent Related Object Json Format

### Agent Object
  This is the entity details of the Agent. 怎么没有departments??

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`id` | Guid| | yes | no | | .|
  |`email` | string| | yes | yes | | Agent login email address, can not change ??|
  |`displayName` | string  | | no | yes | | Different Agents can have the same Display Name.|
  |`firstName` | string  | | no | yes | | The first name of the agent|
  |`lastName` | string  | | no | yes | | The last name of agent|
  |`isAdmin` | bool| | no | no | false | Whether the agent is an administrator or not.|
  |`isActive` | bool| | no | yes | | Whether the agent is active or not.|
  |`phone` | string | | no | no | | Mobile phone number of the agent.|
  |`title` | string  | | no | no | | The title of the agent.|
  |`bio` | string  | | no | no | | The bio info of the agent.|
  |`timeZone` | enum| | no | yes | | The selected time of agent. Remove the Automatically use the time zone of my machine option|
  |`datetimeFormat` | enum| | no | yes | | Date/time format selected by agent to display on the site.|
  |`avatar` | Image| | no | yes | |.|
  |`createdTime` | Date| | yes | no | current UTC date | The create time of the agent.|
  |`isLocked` | bool| | no | no | false | Account will be locked after several failed login attempts.|
  |`lockedTime` | Date| | yes | no | current UTC date | When the agent is locked.|
  |`APIKey` | string | | no | yes | | API key of the agent ??|
  |`lastLoginTime` | Date| | yes | no | current UTC date | The time of the last login to Comm100 account (Control Panel or Agent Console).|
  |`lastLoginIP` | string  | | yes | no | | The IP address where the agent logs in from.|
  |`forgetPasswordTag` | string | | yes | no |  | When the agent submits his email address on Forget Password Page, system will generate a new Forget Password GUID Tag and overwrite the previous value. System will check this GUID to see whether the verification link is the latest one and only the latest one can work.|
  |`forgetPasswordTagTime` | Date| | yes | no | current UTC date |.|
  |`iPVerificationTagTime` | Date| | yes | no | current UTC date |.|
  |`permissionIds` | string[]  |  | no | no | [] | Agent permission settings.|
  |`permission` | [Permission](#Permission)[]  |yes | yes | no | | Agent permission settings. ?? 这里是的列表对象是不是用处不大??|
  |`roleIds` | string[]  |  | no | no | [All Agets's Id] | The list of the roles which the agent belongs to.|
  |`roles` | [Roles](#Role)[]  |yes | yes | no | | The list of the roles which the agent belongs to.|
  |`shift` | [Shift](#Shift)[]  | yes | yes | no  | | The list of shifts which the agent belongs to.|


### Agent List Response Object
  Agent List Object for agent list Response, include count and page information.
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`total` | string  | N/A | yes | 1 | | . |
  |`previousPage` | string  | N/A | yes| 1 | | . |
  |`nextPage` | string  | N/A | yes| 1 | | . |
  |`agents`|   [Agent](#Agent-Object)[]| N/A | yes| 0 | | a list of agents. |


## Agent Endpoints

### Get a list of agents in site
  `GET/api/v3/globalSettings/agents`

#### Parameters
   Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`department`,`role`,`permission` |
  |`keywords` | string | no  |  | filter by keywords in agent display name, email address. |

#### Response
  the response is a [Agent List Response ](#Agent-List-Response-Object) Object

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
        "total" : "100",
        "previousPage": "https://domain.comm100.com/api/v3/globalSettings/agents?pageindex=1&pagesize=10",
        "nextPage": "https://domain.comm100.com/api/v3/globalSettings/agents?pageindex=3&pagesize=10",
        "agents": [{
            "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
|`id` | Guid | yes  |  the unique id of the agent |

Query string
| Name  | Type | Required  | Default | Description |     
| - | - | - | - | - |
|`include`|string|no||Availablevalue:`department`,`role` |

#### Response
the response is a [Agent](#Agent-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" 
-X GET https://domain.comm100.com/api/v3/globalSettings/agents/f9928d68-92e6-4487-a2e8-8234fc9d1f48?include=role,department
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
  |`roleId` | Guid | yes  |  the unique id of the role |

   Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`department`,`role` |

#### Response
the response is a [Agent List Response](#Agent-List-Response-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles/f9928d68-92e6-4487-a2e8-8234fc9d1f48/agents
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "total" : "100",
    "previousPage": "https://domain.comm100.com/api/v3/globalSettings/roles/f9928d68-92e6-4487-a2e8-8234fc9d1f48/agents?pageindex=1&pagesize=10",
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/roles/f9928d68-92e6-4487-a2e8-8234fc9d1f48/agents?pageindex=3&pagesize=10",
    "agents": [{
        "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
  |`departmentId` | Guid | yes  |  the unique id of the department |

   Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`department`,`role` |

#### Response
the response is a [Agent List Response](#Agent-List-Response-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/departments/f9928d68-92e6-4487-a2e8-8234fc9d1f48/agents
```
Response
```json
HTTP/1.1 200 OK
Content-Type:  application/json
{
    "total" : "100",
    "previousPage": "https://domain.comm100.com/api/v3/globalSettings/departments/f9928d68-92e6-4487-a2e8-8234fc9d1f48/agents?pageindex=1&pagesize=10",
    "nextPage": "https://domain.comm100.com/api/v3/globalSettings/departments/f9928d68-92e6-4487-a2e8-8234fc9d1f48/agents?pageindex=3&pagesize=10",
    "agents": [{
        "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
  |`include`|string|no||Availablevalue:`department`,`role` |

#### Response
the response is a [Agent](#Agent-Object) Object

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
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
Path parameters
   No Path Parameters

Request body 

  The request body contains data with the [Agent](#Agent-Object) Structure

example:
```json
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
the response is:
  [Agent](#Agent-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
Location: https://domain.comm100.com//api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
  `PUT /api/v3/globalSettings/agents/{id}:unlock`

####  Parameters
Path parameters
     Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the agent |

Request body 
   No Request body

#### Response
the response is: the result of the unlock;

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{} ' -X PUT https://domain.comm100.com/api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48:unlock
```
Response
```string
true 
```


### Admin set an agent's password
  `Put /api/v3/globalSettings/agents/{id}:changePassword`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the agent |

Request body 
   The request body contains the string new password.

#### Response
the response is: the result of the change password:true/false;

#### Example
Using curl
```
Using curl
```
curl -H "Content-Type: application/json" -d 'UdadncIGcing85sd ' -X Put https://domain.comm100.com/api/v3/globalSettings/agents/f9928d68-92e6-4487-a2e8-8234fc9d1f48:changePassword
```
Response
```string
true 
```

### Change own password
  `Put /api/v3/globalSettings/agents/me:changePassword`

####  Parameters

Request body 
   The request body contains the string new password.

#### Response
the response is: the result of the change password:true/false;

#### Example
Using curl
```
Using curl
```
curl -H "Content-Type: application/json" -d 'UdadncIGcing85sd ' -X Put https://domain.comm100.com/api/v3/globalSettings/agents/me:changePassword
```
Response
```string
true 
```


### Update an agent
  `PUT /api/v3/globalSettings/agents/{id}`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the agent |
Request body
  The request body contains data with the [Agent](#Agent-Object) Structure

  example:
```json
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
the response is:
  [Agent](#Agent-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
} ' -X PUT https://domain.comm100.com/api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com//api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
The request body contains data with the [Agent](#Agent-Object) Structure

  example:
```json
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
the response is: [Agent](#Agent-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com//api/v3/globalSettings/agents/me
{
    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
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
  |`id` | Guid | yes  |  the agent id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com//api/v3/globalSettings/agents/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```



# Roles
 This is role entity, formerly known as Groups.
  + `GET /api/v3/globalSettings/roles` - [Get a list of roles in site](#Get-a-list-of-roles-in-site) include agent, permission
  + `GET /api/v3/globalSettings/roles/{id}` - [Get a role by id](#Get-a-role-by-id) include agent, permission
  + `POST /api/v3/globalSettings/roles` - [Create a new role](#create-a-new-role)
  + `PUT /api/v3/globalSettings/roles/{id}` - [Update a role](#update-a-role)
  + `DELETE /api/v3/globalSettings/roles/{id}` - [Delete a role](#delete-a-role)

## Role Related Object Json Format

### Role Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`id` | Guid| | yes | no | | .|
  |`name` | string| | no | yes | | Name.|
  |`description` | string| | no | no | | Description of this role.|
  |`type` | Site Administrator, All Agents, Custom Role| | no | yes | |Site Administrator and All Agents are the system roles. They cannot be deleted.|
  |`memberIds` | string[] | | no | no | []| The selected agents for this role.|
  |`member` | [Agent](#Agent)[] | yes | yes | no | | The selected agents for this role.|
  |`permissionIds` | string[] | | no | no | [ role of all agents's permission ids ??] | Permissions assigned to this role.|
  |`permission` | [Permission](#Permission)[] | yes | yes | no | | Permissions assigned to this role.|

## Role Endpoints

### Get a list of roles in site
  `GET GET /api/v3/globalSettings/roles`

#### Parameters
  Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`Member`,`Permission` |

#### Response
    the response is a list of [Role](#Role) Object

#### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles?include=Permission
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json
    [{
      "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "CustomRole",
      "MemberIds":  [
        "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "...",
      ],
      "permissionIds" :
        [
         "201",
         "205",
         "...",
        ],,
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
  |`id` | Guid | yes  |  the unique id of the role |
  Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`Member`,`Permission` |

#### Response
   the response is a [Role](#Role) Object

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
      "type": "CustomRole",
      "memberIds":  [
        "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "...",
      ],
      "permissionIds" :
        [
         "201",
         "205",
         "...",
        ],
    }
    ```


### Create a new role

  `POST /api/v3/globalSettings/roles`

####  Parameters
Path parameters
   No Path Parameters

Request body 

  The request body contains data with the [Role](#Role-Object) Structure

  example:
```json
 {
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "CustomRole",
      "MemberIds":  [
        "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "...",
      ],
      "permissionIds" :
        [
         "201",
         "205",
         "...",
        ],
    }
```

#### Response
the response is:
   [Role](#Role-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "CustomRole",
      "MemberIds":  [
        "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
        "...",
      ],
      "permissionIds" :
        [
         "201",
         "205",
         "...",
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
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "CustomRole",
      "MemberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
      "permissionIds" :
        [
         "201",
         "205",
         "...",
        ],
    }
```


### Update a role
  `PUT /api/v3/globalSettings/role/{id}`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the role |
Request body
  The request body contains data with the  [Role](#Role-Object) Structure

  example:
```json
 {
      "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
      "name": "markting",
      "description": "yyyy-MM-dd hh:mm:ss",
      "type": "CustomRole",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
      "permissionIds" :
        [
         "201",
         "205",
         "...",
        ],
    }
```

#### Response
the response is:
  [Role](#Role-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "Name": "markting",
      "Description": "yyyy-MM-dd hh:mm:ss",
      "Type": "CustomRole",
      "MemberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
        "permissionIds" :
        [
         "201",
         "205",
         "...",
        ],
    },
    } ' -X PUT https://domain.comm100.com/api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com//api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48 
{
  "id": "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
  "name": "markting",
  "description": "yyyy-MM-dd hh:mm:ss",
  "type": "CustomRole",
  "member":  [
    "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "...",
  ],
  "permissionIds" :
    [
      "201",
      "205",
      "...",
    ],
}
```

### Delete a role
  `DELETE /api/v3/globalSettings/roles/{id}`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the role id |

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
  + `GET /api/v3/globalSettings/departments` - [Get a list of departments in site](#get-all-departments) include agent
  + `GET /api/v3/globalSettings/departments/{id}` - [Get a department by id](#get-a-department) include agent
  + `POST /api/v3/globalSettings/departments` - [Create a new department](#create-a-new-department)
  + `PUT /api/v3/globalSettings/departments/{id}` - [Update a department](#update-a-department)
  + `DELETE /api/v3/globalSettings/departments/{id}` - [Delete a department](#Delete-a-department)


## Department Related Object Json Format

### Department Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`id` | Guid| | yes | no | | .|
  |`name` | string | | no | yes | |.|
  |`site` | Site | | yes | no | |??.|
  |`description` | string | | no | no | |.|
  |`isAvailableInChat` | bool| | no | yes | | When it is false, the Department will not be displayed in the Pre-chat window Department drop down list, routing rules, chat transfer etc. Default: true.|
  |`isAvailableInTicketingAndMessaging` | bool| | no | yes | | When it is false, the department name will not be displayed in the ‘Assigned Department’ field. Default: true.|
  |`offlineMessageMailType` | All agents in the department, The email address(es)| | no | yes | All agents in the department | .|
  |`offlineMessageEmails` | string  | | no | no | | Specific email addresses that mail offline message to. Available and required when Offline Message Mail Type is ‘The email address(es)’.|
  |`memberIds` | string[] | | no | no | [] | The selected agents for this department.|
  |`member` | [Agent](#Agent)[]| yes | yes | no |  | . |
  |`shift` | [Shift](#Shift)[]| yes | yes | no |  | ??|

## Department Endpoints

### get all departments
  `GET /api/v3/globalSettings/departments`

#### Parameters
  Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`Member` |

#### Response
  the response is a list of [Department](#Department-Object) Object

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
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "member":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
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
  |`id` | Guid | yes  |  the unique id of the department |
Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`Member` |

  #### Response
  the response is a [Department](#Department-Object) Object

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
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
    }
    ```


### Create a new department
  `POST /api/v3/globalSettings/departments`

####  Parameters
Path parameters
   No Path Parameters

Request body 
  The request body contains data with the [Department](#Department-Object) Structure

  example:
```json
 {
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
    }
```

#### Response
the response is:
    [Department](#Department-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
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
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
    }
```



### update a department
  `PUT /api/v3/globalSettings/departments/{id}`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the department |
Request body
  The request body contains data with the  [Department](#Department-Object) Structure

  example:
```json
{
      "name": "markting",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
      ],
    }
```

#### Response
the response is:
   [Department](#Department-Object)  Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
  "Name": "markting",
  "Site": "10000",
  "Description": "markting departments",
  "IsAvailableInChat": "yes",
  "IsAvailableInTicketingAndMessaging": "yes",
  "OfflineMessageMailType": "All agents in the department",
  "OfflineMessageEmails": "",
  "memberIds":  [
    "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
    "...",
  ],
}' -X PUT https://domain.comm100.com/api/v3/globalSettings/departments/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com//api/v3/globalSettings/departments/bs22qa68-92e6-4487-a2e8-8234fc9d1f48
{
      "name": "markting",
      "site": "10000",
      "description": "markting departments",
      "isAvailableInChat": "yes",
      "isAvailableInTicketingAndMessaging": "yes",
      "offlineMessageMailType": "All agents in the department",
      "offlineMessageEmails": "",
      "memberIds":  [
        "4487fc9d-92e6-4487-a2e8-92e68d6892e6",
        "...",
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
  Permission is hard-coded.  这里跟后台是实际实现有出入，估计需要重新处理一下，添加一个获取所有权限数据的接口??
  + `GET /api/v3/globalSettings/roles/{roleId}/permission` - [Get role permission](#Get-role-permission)
  + `GET /api/v3/globalSettings/agents/{agentId}/permission` - [Get agent permission](#Get-agent-permission)
  + `GET /api/v3/globalSettings/agents/{agentId}/permission:effective` - [Get a list of agent's effective permissions](#Get-agent-effective-permission) ,including the permissions of the agent and the permissions of the roles which the agent belongs to.
  + `PUT /api/v3/globalSettings/roles/{roleId}/permission` - [Update role permission](#update-role-permission)
  + `PUT /api/v3/globalSettings/agents/{agentId}/permission` - [Update agent permission](#update-agent-permission)


## Permission Related Object Json Format

### Permission Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`id` | integer| | yes | no | 0| .|
  |`name` | string| | yes | no | |.|
  |`description` | string| | yes | no | |.|
  |`category` | Live Chat, Ticketing & Messaging, Bot, Knowledge Base, Global Setting| | yes | no | |.|

## Permission Endpoints

### Get role permission
  `GET /api/v3/globalSettings/roles/{roleId}/permission`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`roleId` | Guid | yes  |  the unique id of the role |

#### Response
    the response is a [Permission](#Permission) Object
  

#### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d68927777/permission
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json[
    {
      "id": "201",
      "name": "Accept Chats",
      "description": "Accept Chats",
      "category": "Live Chat",
    },
    ...,
    ]
    ```


### Get agent permission
  `GET /api/v3/globalSettings/agents/{agentId}/permission`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`agentId` | Guid | yes  |  the unique id of the agent |

  #### Response
  the response is a list of [Permission](#Permission) Objects
  

  #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/agents/4487fc9d-92e6-4487-a2e8-92e68d68927777/permission
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json[
    {
      "id": "201",
      "name": "Accept Chats",
      "description": "Accept Chats",
      "category": "Live Chat",
    },
    ...,
    ]
    ```

### Get agent effective permission
  `GET /api/v3/globalSettings/agents/{agentId}/permission:effective`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`agentId` | Guid | yes  |  the unique id of the agent |

  #### Response
  the response is a list of [Permission](#Permission) Objects
  

  #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/agents/4487fc9d-92e6-4487-a2e8-92e68d68927777/permission:effective
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json[
    {
      "id": "201",
      "name": "Accept Chats",
      "description": "Accept Chats",
      "category": "Live Chat",
    },
    ...,
    ]
    ```

### update role permission
 `PUT /api/v3/globalSettings/roles/{roleId}/permission`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`roleId` | Guid | yes  |  the unique id of the role |
Request body
  The request body contains data with the  [Permission](#Permission-Object) Id list

  example:
```json
[
  "201",
  "205",
  "...",
]
```

#### Response
the response is:
  role [Permission](#Permission-Object) Object list

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
  "201",
  "205",
  "...",
]' -X PUT https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d68927777/permission
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/roles/4487fc9d-92e6-4487-a2e8-92e68d68927777/permission
[{
      "id": "201",
      "name": "Accept Chats",
      "description": "Accept Chats",
      "category": "Live Chat",
    },
    ...,
]
```

### update agent permission
`PUT /api/v3/globalSettings/agents/{agentId}/permission`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`agentId` | Guid | yes  |  the unique id of the agent |
Request body
  The request body contains data with the  [Permission](#Permission-Object) Id list

  example:
```json
[
  "201",
  "205",
  "...",
]
```

#### Response
the response is:
   agent [Permission](#Permission-Object) Object list

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '[
  "201",
  "205",
  "...",
]' -X PUT https://domain.comm100.com/api/v3/globalSettings/agents/4487fc9d-92e6-4487-a2e8-92e68d68927777/permission
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com//api/v3/globalSettings/agents/bs22qa68-92e6-4487-a2e8-8234fc9d1f48?include=Permission
[{
      "id": "201",
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

  //Mandatory for post 这列完全不对啊
  Shift Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  |`id` | Guid | | yes | no | | Id of the current item.  |
  | `name` | string  | | no | no | | Name of the shift. |
  | `timeZone` | timezone  | | no | no | | Enum. Time Zone selected for this shift. //这个time zone 应该怎么填? |
  | `holidays` | [Holiday](#Holiday-Object)[]  | | no | no | | //这个字段我也说不清|
  |`agentId` | Guid | | yes | no | | |
  |`departmentId` | Guid | | yes | no | | |
  | `members` | [Agent](#Agent-Object)[] or [Department](#Department-Object)[] | yes | no | no | | |
  | `workingHours` | [Working Hours](#Working-Hours-Object)[]  | | no | no | |//这2个字段我也说不清 |

### Holiday Object

  Holiday Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `name` | string  | no | no |//创建的时候应该是必填的 | The name of holiday. |
  | `holiday` | date  | no | no | //创建的时候应该是必填的| The date of the holiday. |

### Working Hours Object

  Working Hours Object is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - | :-: | :-: | :-: | - |
  | `dayofWeek` | string  | no | no | | Including `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday` and `sunday`. |
  | `startTime` | datetime  | no | no | //这些字段创建的时候应该都是必填的| |
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
        "timeZone": "(GMT-10:00) Hawaii",
        "holidays": [{
          "name": "summary",
          "holiday": "2019-11-11"
        },
        ...
        ],
        "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2", //这里应该是数组,
        "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E", //这里应该是数组
        "members": [{// include department
          "id": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
          "name": "departments",
          "siteId": "FEF12049-BF08-2CD4-C405-A5FC8AE75D0F",
          "description": "departments",
          "isAvailableInChat": false,
          "isAvailableInTicketingAndMessaging": false,
          "offlineMessageMailType": "theEmailAddress",
          "offlineMessageEmails": "test@comm100.com",
          "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2"
        },
        ...
        ],
        "workingHours": [{
          "dayofWeek": "sunday",
          "startTime": "2019-06-12T07:41:40.486Z",
          "endTime": "2019-06-13T07:41:40.486Z",
          "awayStatus": {
            "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
            "name": "agentAwayStatuses",
            "isSystem": false,
            "order": 1
          }
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

the response is: [Shift](#Shift-Object) Object

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
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "members": [{// include department
    "id": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
    "name": "departments",
    "siteId": "FEF12049-BF08-2CD4-C405-A5FC8AE75D0F",
    "description": "departments",
    "isAvailableInChat": false,
    "isAvailableInTicketingAndMessaging": false,
    "offlineMessageMailType": "theEmailAddress",
    "offlineMessageEmails": "test@comm100.com",
    "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2"
  },
  ...
  ],
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
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
  | `departmentId` | Guid | yes  |  the unique Id of the department |

#### Response

the response is: [Shift](#Shift-Object) Object

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
        "timeZone": "(GMT-10:00) Hawaii",
        "holidays": [{
          "name": "summary",
          "holiday": "2019-11-11"
        },
        ...
        ],
        "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
        "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
        "workingHours": [{
          "dayofWeek": "sunday",
          "startTime": "2019-06-12T07:41:40.486Z",
          "endTime": "2019-06-13T07:41:40.486Z",
          "awayStatus": {
            "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
            "name": "agentAwayStatuses",
            "isSystem": false,
            "order": 1
          }
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
  | `agentId` | Guid | yes  |  the unique Id of the agent |

#### Response

the response is: [Shift](#Shift-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json"
-X GET https://domain.comm100.com/api/v3/globalSettings/agents/0CB71531-F8C4-92F6-E619-1989A92972F2/shifts
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

[
    {
        "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
        "name": "Shifts",
        "timeZone": "(GMT-10:00) Hawaii",
        "holidays": [{
          "name": "summary",
          "holiday": "2019-11-11"
        },
        ...
        ],
        "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
        "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
        "workingHours": [{
          "dayofWeek": "sunday",
          "startTime": "2019-06-12T07:41:40.486Z",
          "endTime": "2019-06-13T07:41:40.486Z",
          "awayStatus": {
            "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
            "name": "agentAwayStatuses",
            "isSystem": false,
            "order": 1
          }
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

  The request body contains data with the [Shift](#Shift-Object) structure

example:
```Json
{
  "name": "Shifts1111",
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
    },
    ...
  ]
}
```

#### Response

the response is: [Shift](#Shift-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "Shifts1111",
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
    },
    ...
  ]
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/shifts
```

Response
``` json
HTTP/1.1 200 OK
Content-Type:  application/json

{
  "id": "3964B5AE-6DAD-D774-BFCB-8C1F6B58ACED",
  "name": "Shifts",
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
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

  The request body contains data with the [Shift](#Shift-Object) structure

example:
```Json
{
  "name": "Shifts2222",
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
    },
    ...
  ]
}
```

#### Response

the response is: [Shift](#Shift-Object) Object

#### Example

Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "Shifts2222",
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
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
  "timeZone": "(GMT-10:00) Hawaii",
  "holidays": [{
    "name": "summary",
    "holiday": "2019-11-11"
  },
  ...
  ],
  "agentId": "0CB71531-F8C4-92F6-E619-1989A92972F2",
  "departmentId": "1DC43077-E36F-F9EA-C7BA-C29620102F7E",
  "workingHours": [{
    "dayofWeek": "sunday",
    "startTime": "2019-06-12T07:41:40.486Z",
    "endTime": "2019-06-13T07:41:40.486Z",
    "awayStatus": {
      "id": "BAACB779-2E41-27C5-B23D-1C8F2058862D",
      "name": "agentAwayStatuses",
      "isSystem": false,
      "order": 1
    }
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
 根据ssoId 查询 contact (查看 zendesk api)???
 + `GET /api/v3/globalSettings/contacts` - [Get a list of contacts in site](#get-all-contacts)  通过 query string 来实现复杂查询
  + `GET /api/v3/globalSettings/contacts/{id}` - [Get a contact by id](#get-an-contact)
  + `POST /api/v3/globalSettings/contacts` - [Create a new contact](#create-a-new-contact)
  + `PUT /api/v3/globalSettings/contacts/{id}` - [Update a contact](#update-a-contact)
  + `DELETE /api/v3/globalSettings/contacts/{id}` - [Delete a contact](#delete-a-contact)

  ## Contact Related Object Json Format

### Contact Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`id` | Guid| | yes | no | | .|
  |`name` | string  | | no | yes | | Contact Name can be edited by Agents. Default value is read from the first Identity. Only when a Contact sends a message in a specific channel that has Name and Avatar, like Facebook Account, display Name and Avatar from that Identity in Agent Console. In other situations, display Contact Name and Avatar.|
  |`description` | string | | no | no | |.|
  |`firstName` | string | | no | yes | |.|
  |`lastName` | string | | no | yes | |.|
  |`alias` | string | | no | no | |.|
  |`avatar` | Image| | no | yes | |.|
  |`title` | string | | no | no | |.|
  |`company` | string  | | no | no | |.|
  |`fax` | string  | | no | no | |.|
  |`phone` | string  | | no | no | | DB document is using ‘mobile’.|
  |`mailingAddress` | string  | | no | no | |.|
  |`city` | string | | no | no | |.|
  |`stateOrProvince` | string  | | no | no | |.|
  |`countryOrRegion` | string  | | no | no | |.|
  |`postalOrZipCode` | string  | | no | no | |.|
  |`timeZone` | enum | | no | yes | |.|
  |`createdTime` | Date | | yes | no | current date time | When the contact is created.|
  |`lastUpdatedTime` | Date| | yes | no |current date time |.|
  |`contactIdentity` | [Contact Identity](#Contact-Identity-Object)| yes | yes | no | |Contact Identity.|

## Contact Endpoints


### Get all contacts
  `GET /api/v3/globalSettings/contacts`

#### Parameters
 Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`ContactIdentity` |
   如何实现复杂查询?? 有哪些键值??

  #### Response
    the response is a list of [Contact](#Contact-Object) Objects
  

  #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contacts
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json[
    {
      "name": "Vincent", 
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe", 
      "alias": "", 
      "avatar": {
        "name": "bot.png",
        "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
      }, 
      "title": "CEO", 
      "company": "BMW", 
      ...
    },
    ...,
    ]
    ```


### Get an contact
  `GET /api/v3/globalSettings/contacts/{id}`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the agent |

 Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`ContactIdentity` |


#### Response
    the response is an [Contact](#Contact-Object) Object
  
 #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contacts/42dwdaww-92e6-4487-a2e8-92e68d6892e6
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json
    {
      "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
      "name": "Vincent", 
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe", 
      "alias": "", 
      "avatar": {
        "name": "bot.png",
        "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
      }, 
      "title": "CEO", 
      "company": "BMW", 
      ...
    }
    ```

### Create a new contact

  `POST /api/v3/globalSettings/contacts`

####  Parameters
Path parameters
   No Path Parameters

Request body 
  The request body contains data with the [Contact](#Contact-Object) Structure

example:
```json
{
      "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
      "name": "Vincent", 
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe", 
      "alias": "", 
      "avatar": {
        "name": "bot.png",
        "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
      }, 
      "title": "CEO", 
      "company": "BMW", 
      ...
    }
```

#### Response
the response is:
  [Contact](#Contact-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
      "name": "Vincent", 
      "description": "Accept Chats",
      "firstName": "Vincent",
      "lastName": "Crabbe", 
      "alias": "", 
      "avatar": {
        "name": "bot.png",
        "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
      }, 
      "title": "CEO", 
      "company": "BMW", 
      ...
    }' -X POST https://domain.comm100.com/api/v3/globalSettings/contacts
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contacts/42dwdaww-92e6-4487-a2e8-92e68d6892e6
{
  "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
  "name": "Vincent", 
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe", 
  "alias": "", 
  "avatar": {
    "name": "bot.png",
    "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
  }, 
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
  |`id` | Guid | yes  |  the unique id of the contact |
Request body 
  The request body contains data with the [Contact](#Contact-Object) Structure

  example:
```json
{
  "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
  "name": "Vincent", 
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe", 
  "alias": "", 
  "avatar": {
    "name": "bot.png",
    "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
  }, 
  "title": "CEO", 
  "company": "BMW", 
  ...
}
```

#### Response
the response is:
  [Contact](#Contact-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d '{
  "name": "Vincent", 
  "description": "Accept Chats",
  "firstName": "Vincent",
  "lastName": "Crabbe", 
  "alias": "", 
  "avatar": {
    "name": "bot.png",
    "url": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6"
  }, 
  "title": "CEO", 
  "company": "BMW", 
  ...
}' -X PUT https://domain.comm100.com/api/v3/globalSettings/contacts
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contacts/42dwdaww-92e6-4487-a2e8-92e68d6892e6
{
    "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
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
  |`id` | Guid | yes  |  the agent id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/contacts/4487fc9d-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 204 No Content
```

# Contact Identity
 + `GET /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [Get a list of contactIdentities in a contact](#get-all-Contact_Identity)
  + `GET /api/v3/globalSettings/contactIdentities/{id}` - [Get a contactIdentity by id](#get-a-contactIdentity)
  + `POST /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [create a new contactIdentity](#create-a-new-contactIdentity)
  + `PUT /api/v3/globalSettings/contactIdentities/{id}` - [update a contactIdentity](#update-a-contactIdentity)
  + `DELETE /api/v3/globalSettings/contactIdentities/{id}` - [delete a contactIdentity](#delete-a-contactIdentity)

 ## Contact Identity Related Object Json Format

### Contact Identity Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`id` | Guid| | yes | no | | .|
  |`name` | string | | no | no | | The name used in a certain type, like the name of a user in Facebook. Not every type has name, for example, SMS Number doesn’t have one.|
  |`type` | enum| | no | yes | | Visitor, Email Address, SMS Number, Facebook Account, Twitter Account, WeChat Account, SSO User ID, External ID, WhatsApp. In phase 1, one type only has one identity. We need remove the limitation in phase 2.|
  |`value` | string  | | no | yes | | The value of the identity.|
  |`avatarURL` | string | | no | no | | The avatar used in a certain type, like the avatar of a user in Facebook. Not every type has avatar, for example, SMS Number doesn’t have one.|
  |`infoURL` | string  | | no | no | | Contact information from the channels. Such as the number of Twitter followers, tweets of the twitter identity. The info is displayed in an iframe in agent console. Available for Twitter, Facebook, SMS, WeChat.|
  |`screenName` | string | | no | no | | Twitter only. Like @Comm100Corp.|
  |`originalContactPageURL` | string  | | no | no | | The contact profile URL on Facebook or Twitter.|

## Contact Identity  Endpoints

### get all Contact Identity
  `GET /api/v3/globalSettings/contacts/{contactId}/contactIdentities`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`contactId` | Guid | yes  |  the unique id of the contact of contact Identities belong|


  #### Response
    the response is a list of [Contact Identity](#Contact-Identity-Object) Objects
  
  #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contacts/42dwdaww-92e6-4487-a2e8-92e68d6892e6/contactIdentities
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json[
    {
      "name": "Vincent", 
      "type": "Visitor", 
      "value": "??", 
      "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
      "infoURL": "", 
      "screenName": "@Comm100Corp", 
      "originalContactPageURL": "", 
    },
    ...,
    ]
    ```



### get an contactIdentity
  `GET /api/v3/globalSettings/contactIdentities/{id}`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the contact Identitie |

  #### Response
    the response is an [Contact Identity](#Contact-Identity-Object) Object
  
  #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/contactIdentities/42dwdaww-92e6-4487-a2e8-92e68d6892e6
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json
    {
      "name": "Vincent", 
      "type": "Visitor", 
      "value": "??", 
      "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
      "infoURL": "", 
      "screenName": "@Comm100Corp", 
      "originalContactPageURL": "", 
    }
    ```


### create a new contactIdentity
  `POST /api/v3/globalSettings/contacts/{contactId}/contactIdentities`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`contactId` | Guid | yes  |  the unique id of the contact of contact Identities belong|

Request body 
  The request body contains data with the [Contact Identity](#Contact-Identity-Object) Structure

  example:
```json
 {
    "name": "Vincent", 
    "type": "Visitor", 
    "value": "??", 
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
    "infoURL": "", 
    "screenName": "@Comm100Corp", 
    "originalContactPageURL": "", 
  }
```

#### Response
the response is:
  [Contact Identity](#Contact-Identity-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
    "name": "Vincent", 
    "type": "Visitor", 
    "value": "??", 
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
    "infoURL": "", 
    "screenName": "@Comm100Corp", 
    "originalContactPageURL": "", 
  }' -X POST https://domain.comm100.com/api/v3/globalSettings/contacts
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contactIdentities/42dwdaww-92e6-4487-a2e8-92e68d6892e6
{
    "id": "42dwdaww-92e6-4487-a2e8-92e68d6892e6",
    "name": "Vincent", 
    "type": "Visitor", 
    "value": "??", 
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
    "infoURL": "", 
    "screenName": "@Comm100Corp", 
    "originalContactPageURL": "", 
  }
```

### Update an contactIdentity
  `PUT /api/v3/globalSettings/contactIdentities/{id}`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the contact Identitie |
Request body 
  The request body contains data with the [Contact Identity](#Contact-Identity-Object) Structure

  example:
```json
 {
    "name": "Vincent", 
    "type": "Visitor", 
    "value": "??", 
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
    "infoURL": "", 
    "screenName": "@Comm100Corp", 
    "originalContactPageURL": "", 
  }
```

#### Response
the response is:
  [Contact Identity](#Contact-Identity-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
    "name": "Vincent", 
    "type": "Visitor", 
    "value": "??", 
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
    "infoURL": "", 
    "screenName": "@Comm100Corp", 
    "originalContactPageURL": "", 
  }' -X PUT https://domain.comm100.com/api/v3/globalSettings/contactIdentities/42dwdaww-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/contactIdentities/42dwdaww-92e6-4487-a2e8-92e68d6892e6
 {
    "name": "Vincent", 
    "type": "Visitor", 
    "value": "??", 
    "avatarURL": "https://bot.comm100.com/api/v3/chatbot/images/42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
    "infoURL": "", 
    "screenName": "@Comm100Corp", 
    "originalContactPageURL": "", 
  }
```

### delete an contactIdentity
  `DELETE /api/v3/globalSettings/contactIdentities/{id}`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the contact identity id |

#### Response
HTTP/1.1 204 No Content

#### Example
Using curl
```
curl -X DELETE https://domain.comm100.com/api/v3/globalSettings/contactIdentities/4487fc9d-92e6-4487-a2e8-92e68d6892e6
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

  //N/A 的理解不对啊, Vistor 是不可以创建和修改的, 应该全部是N/A
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
  | `categoryId` | Guid | | no | no | //创建的时候可以不填categoryId吗？| |
  | `category` | [Public Canned Message Category](#Public-Canned-Message-Category-Object)  | yes | no | no |//这2个都是N/A吧 |  Category can be blank. Please note that this is different from Intent Category and Article Category. Available only when `publicCannedMessageCategory` is included. |
  | `createdBy` | Guid | | N/A | N/A | | Which agent create the current item. |
  | `shortcuts` | string  | | no | no | | Whether the custom away status is system or not. |
  | `similarQuestions` | [Similar Question](#Similar-Question-Object)[]  | | no | no | //这里昨天评审的时候记得说是用String[]| Available when Agent Assist is enabled. |

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
   When Login IP Whitelist is enabled, site administrator can add IP range for this site and only agents within the IP range can log in successfully.
   + `GET /api/v3/globalSettings/whitelistedLoginIPRanges` - [Get a list of whitelistedLoginIPRanges in site](#get-all-whitelisted-Login-IP-Ranges) 
  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [Get a whitelistedLoginIPRange by id](#get-a-whitelisted-Login-IP-Ranges) 
  + `POST /api/v3/globalSettings/whitelistedLoginIPRanges` - [create a new whitelistedLoginIPRange](#create-a-new-whitelisted-Login-IP-Range)
  + `PUT /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [update a whitelistedLoginIPRange](#update-a-whitelisted-Login-IP-Range)
  + `DELETE /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [delete a whitelistedLoginIPRange](#delete-a-whitelisted-Login-IP-Range)

 ## Whitelisted Login IP Range Related Object Json Format

### Whitelisted Login IP Range Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`iPFrom` | string | | no | yes | | Where an IP range starts.|
  |`iPTo` | string | | no | yes | | Where an IP range ends.|
  |`createdTime` | Date| | yes | no | current date time |.|

## Whitelisted Login IP Range Endpoints

### Get all whitelisted Login IP Ranges
  `GET /api/v3/globalSettings/whitelistedLoginIPRanges`

  #### Parameters
  No parameters

  #### Response
    the response is a list of [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range-Object) Objects

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
      "iPFrom": "201.195.21.5", 
      "iPTo": "201.195.21.8", 
      "createdTime": "2020-01-01", 
    },
    ...,
    ]
    ```

### Get a whitelisted Login IP Ranges
  `GET /api/v3/globalSettings/whitelistedLoginIPRanges/{id}`

#### Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the whitelisted Login IP Ranges |

#### Response
    the response is a [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range-Object) Object
  
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
      "iPFrom": "201.195.21.5", 
      "iPTo": "201.195.21.8", 
      "createdTime": "2020-01-01", 
    }
    ```



### Create a new whitelisted Login IP Range
  `POST /api/v3/globalSettings/whitelistedLoginIPRanges`

####  Parameters
No parameters

Request body 
  The request body contains data with the [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range-Object) Structure

  example:
```json
 {
    "iPFrom": "201.195.21.5", 
    "iPTo": "201.195.21.8", 
    "createdTime": "2020-01-01", 
  }
```

#### Response
the response is:
  [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "iPFrom": "201.195.21.5", 
      "iPTo": "201.195.21.8", 
      "createdTime": "2020-01-01", 
    }' -X POST https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
 {
    "iPFrom": "201.195.21.5", 
    "iPTo": "201.195.21.8", 
    "createdTime": "2020-01-01", 
  }
```


### Update a whitelisted Login IP Range
  `PUT /api/v3/globalSettings/whitelistedLoginIPRanges/{id}`

####  Parameters
Path parameters
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` | Guid | yes  |  the unique id of the whitelisted Login IP Range |
Request body 
  The request body contains data with the [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range-Object) Structure

  example:
```json
 {
    "iPFrom": "201.195.21.5", 
    "iPTo": "201.195.21.8", 
    "createdTime": "2020-01-01", 
  }
```

#### Response
the response is:
  [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range-Object) Object

#### Example
Using curl
```
curl -H "Content-Type: application/json" -d ' {
      "iPFrom": "201.195.21.5", 
      "iPTo": "201.195.21.8", 
      "createdTime": "2020-01-01", 
    }' -X PUT https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
```
Response
```json
HTTP/1.1 201 Created
Content-Type:  application/json
Location: https://domain.comm100.com/api/v3/globalSettings/whitelistedLoginIPRanges/42dwdaww-92e6-4487-a2e8-92e68d6892e6
 {
      "iPFrom": "201.195.21.5", 
      "iPTo": "201.195.21.8", 
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
HTTP/1.1 200 OK//创建成功好像是 Created
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
  | `attribute` | string | | no | yes | | SSO attribute name. |
  | `comm100Field` | string | | no | yes | | the Comm100 field name |

### Visitor SSO Campaign Object

Visitor SSO Campaign is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |
  | - | - |- | :-: | :-: | :-: | - |
  | `campaignId` | Guid |  | no | yes | | Id of the campaign. |
  | `campaign` | [Campaign](#Campaign-Object)  | yes | N/A | N/A | | Available only when campaign is included  |
  | `signInOption` | string |  | no | no | `noSignIn` | Type of the sign in, including `noSignIn`, `signInOptional` and `signInRequired`. |
  | `isPrechatFromSkipped` | boolean |  | no | no | true | Whether the pre-chat form is skipped when visitors sign in. |

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
+ `GET /api/v3/globalSettings/auditLogs` - [Get audit logs list](#Get-audit-logs-list) include agent

 ## Audit Log Object Json Format

### Audit Log Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - |
  |`id` | integer | | yes | no | | .| 
  |`category` | Live Chat, Ticketing & Messaging, Bot, My Account Global Settings, Knowledge Base| | yes | no | |.|
  |`createdTime` | Date| | yes | no | current date time |.|
  |`createdBy` | Agent| | yes | no | |.|
  |`actionType` | enum| | yes | no | |.|
  |`actionSummary` | string| | yes | no | |.|
  |`actionDetails` | string| | yes | no | |.|

### Audit Log List Response Object
  Agent List Object for agent list Response, include count and page information.
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`total` | string  | N/A | yes | 1 | | . |
  |`previousPage` | string  | N/A | yes| 1 | | . |
  |`nextPage` | string  | N/A | yes| 1 | | . |
  |`auditLogs`| [Audit Log](#Audit-Log-Object)[]| N/A | yes| 0 | | a list of Audit Log. |

## Audit Log Endpoints

### Get audit logs list
  `GET /api/v3/globalSettings/auditLogs`

  #### Parameters
   Query string
  | Name  | Type | Required  | Default | Description |     
  | - | - | - | - | - |
  |`include`|string|no||Availablevalue:`agent` |


  #### Response
    the response is a [Audit Log List Response](#Audit-Log-List-Response-Object) Object

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
        "total" : "100",
        "previousPage": "https://domain.comm100.com/api/v3/globalSettings/agents?pageindex=1&pagesize=10",
        "nextPage": "https://domain.comm100.com/api/v3/globalSettings/agents?pageindex=3&pagesize=10",
        "auditLogs": [
          {
            "name": "add Agent",
            "Category": "My Account Global Settings",
            "CreatedTime": "2020-02-02",
            "CreatedBy": {??},
            "ActionType": "Add Agent",
            "ActionSummary": "Add Agent",
            "ActionDetails": "Add Agent for Live Chat",
          },
          ...,
          ]
    }
    ```