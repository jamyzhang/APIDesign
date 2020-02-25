  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 2.0 | v3 | Global API | 2020-02-20 | Alen | 


# Summary
  - [Site](#Site)
  - [Agent](#Agent)
    - [Agent List Response Object](#Agent-List-Response-Object)
  - [Roles](#Roles)
  - [Department](#Department)
  - [Permission](#Permission)
  - [Contact](#Contact)
  - [Contact Identity](#Contact-Identity)
  - [Whitelisted Login IP Range](#Whitelisted-Login-IP-Range)
  - [Audit Log](#Audit-Log)
    - [Audit Log List Response Object](#Audit-Log-List-Response-Object)

     


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
  |`permissionIds` | string[] | | no | no | [all agents's permission ids ??] | Permissions assigned to this role.|
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


# OAuth Client
OAuth is an open protocol to allow secure API authorization in a simple and standard method from web, mobile and desktop applications. It is used to authorize client application to get access to Comm100 API. Partners also have their OAuth Client entity.
   + `GET /api/v3/globalSettings/OAuthClient` - [Get a list of OAuth Client in site](#get-all-OAuth-Client) 

## OAuth Client Related Object Json Format

### OAuth Client Object
  | Name | Type | Include | Read-only For Put | Mandatory For Post | Default | Description |    
  | - | - | :-: | :-: | :-: | :-: | - | 
  |`clientName` | string | | no | yes | | The name of client application.|
  |`clientID` | string | | yes | yes | | It is the unique identifier for each client application.|
  |`secret` | string | | no | yes | | The secret is like the password, it is used to verify the client application. Client secret is known only to the client application and authorization server.|
  |`scopes` | string | | no | yes | | The permissions which have been granted to the client application.|
  |`grantTypes` | string | | no | yes | | There are 4 grant types: authorization code, implicit, resource owner password credentials, client credentials. Each client application can have one or multiple grant types.|
  |`redirectUris` | string | | no | yes | | When the client application is successfully authorized, the authorization server will redirect it back to the application with an access token in the Redirect Uri.|
  |`accessTokenValidationHours` | Integer.| | no | yes | 0 | Define within how many hours the access token is valid.|
  |`refreshTokenValidationHours` | Integer.| | no | yes | 0 | Define within how many hours the refresh token is valid|
  |`isTrusted` | bool| | no | no | yes | If the client application is trusted, it can get a new token without client’s authorization. Otherwise, each time client application wants to get a new token, it is required to authorize again.|
  |`isActive` | bool| | no | no | true | If it is inactive, the client application cannot have access to Comm100 API even the access token or refresh token is still valid. For example, if the site is closed, system should update "Is Active" to false.|
  |`createdTime` | Date| | yes | no | | .|

## OAuth Client Endpoints

### Get all OAuth Client
  `GET /api/v3/globalSettings/OAuthClient`

  #### Parameters
  No parameters

  #### Response
    the response is a list of [OAuth Client](#OAuth-Client-Object) Objects

  #### Example
    Using curl
    ```
    curl -H "Content-Type: application/json" -X GET https://domain.comm100.com/api/v3/globalSettings/OAuthClient
    ```
    Response
    ```json
    HTTP/1.1 200 OK
    Content-Type:  application/json[
    {
      "clientName": "vincent", 
      "clientID": "42dwdaww-92e6-4487-a2e8-92e68d6892e6", 
      "secret": "", 
      "scopes": "", 
      "grantTypes": "authorization code", 
      ...,
    },
    ...,
    ]
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


