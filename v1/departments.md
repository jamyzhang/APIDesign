# Departments

### Available Paths

| Method | Name | Path
| --- | --- | ---
| GET | [Get List of Departments](#get-list-of-departments) | /api/v1/livechat/departments
| GET | [Get a Single Department](#get-a-single-department) | /api/v1/livechat/departments/{id}
| POST | [Create a New Department](#create-a-new-department) | /api/v1/livechat/departments
| PUT | [Update a Department](#update-a-department) | /api/v1/livechat/departments/{id}
| DELETE | [Remove a Department](#remove-a-department) | /api/v1/livechat/departments/{id}

## Get List of Departments
Gets a list of departments.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/departments
```

### Response
| Property | Description
| --- | ---
| `id` | the id of the department
| `name` | the name of the department
| `description` | the description of the department
| `members` | the members of the department, an array of agent ids
| `status` | the status of the department, int `0` indicates online, `2` indicates offline

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/departments" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
[
    {
        "description": "comm100 live chat development",
        "id":1,
        "members":[
            1,
            2
        ],
        "name": "livechat",
        "status": 0
    },
    {
        "description": "comm100 live chat support",
        "id": 2,
        "members": [
            1,
            2
        ],
        "name": "support",
        "status": 0
    }
]
```

## Get a Single Department
Get a specific department by id.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/departments/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id`| the id of the department

### Response
| Property | Description
| --- | ---
| `id` | the id of the department
| `name` | the name of the department
| `description` | the description of the department
| `members` | the members of the department, an array of operator ids
| `status` | the status of the department, int `0` indicates online, `2` indicates offline

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/departments/1" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "description": "comm100 live chat development",
    "id": 1,
    "members": [
        1,
        2
    ],
    "name": "livechat",
    "status": 0
}
```

## Create a New Department
Creates a new department.

### Path
```bash
POST https://hosted.comm100.com/api/v1/livechat/departments
```

### Parameters
| Property | Description
| --- | ---
| `name` | required, the name of the department, it must be unique
| `description` | optional, the description of the department
| `members` | optional, the members of the department, operator ids, separated by comma

### Response
| Property | Description
| --- | ---
| `id` | the id of the department
| `name` | the name of the department
| `description` | the description of the department
| `members` | the members of the department, an array of operator ids
| `status` | the status of the department, int `0` indicates online, `2` indicates offline

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/departments" \
    -X POST -d "name=sales&member=1,2,11" \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 
```
Sample response:
```json
{
    "description": "",
    "id": 3,
    "members": [
        1,
        2,
        11
    ],
    "name": "sales",
    "status": 0
}
```

## Update a Department
Updates a specified department.

### Path
```bash
PUT https://hosted.comm100.com/api/v1/livechat/departments/{id}
```
### Parameters
| Property | Description
| --- | ---
| `name` | optional, the name of the department, it must be unique
| `description` | optional, the description of the department
| `members` | optional, the members of the department, operator ids, separated by comma

### Response
| Property | Description
| --- | ---
| `id` | the id of the department
| `name` | the name of the department
| `description` | the description of the department
| `members` | the members of the department, an array of operator ids
| `status` | the status of the department, int `0` indicates online, `2` indicates offline

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/departments/3" \
    -X PUT -d "description=comm100+live+chat+sales&member=2,11" \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```
Sample response:
```json
{
    "description": "comm100 live chat sales",
    "id": 1,
    "members": [
        2,
        11
    ],
    "name": "sales",
    "status": 0
}
```

## Remove a Department
Deletes a specific department.<br />
**Note**: Removing a department will permanently remove all the chat transcripts and offline messages that are related to this department.

### Path
```bash
DELETE https://hosted.comm100.com/api/v1/livechat/departments/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id`| the id of the department

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/departments/3" \
    -X DELETE -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "result": "Deparement '3' has been removed."
}
```