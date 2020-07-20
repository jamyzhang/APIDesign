# Canned Message Categories
Use this to get a list of your Canned Messages and to modify them. Only agents with **"Manage Public Canned Messages"** permission have access to this resource.

### Available Paths
| Methods | Name | Path
| --- | --- | ---
| GET | [List all canned message categories](#list-all-canned-message-categories) | /api/v1/livechat/cannedMessageCategories
| GET | [Get a single canned message categories](#get-a-single-canned-message-categories) | /api/v1/livechat/cannedMessageCategories/{id}
| POST | [Add a new canned message category](#add-a-new-canned-message-category) | /api/v1/livechat/cannedMessageCategories
| PUT | [Update a canned message category](#update-a-canned-message-category) | /api/v1/livechat/cannedMessageCategories/{id}
| DELETE | [Delete a canned message category](#delete-a-canned-message-category) |/api/v1/livechat/cannedMessageCategory/{id}


In addition, there are two more APIs which helps you can get all canned message under a specific category, or add new canned message to a specific category.

| Methods | Name | Path
| --- | --- | ---
| GET | [Get Canned Messages of a Specific Category](#get-canned-messages-of-a-specific-category) | /api/v1/livechat/cannedMessageCategories/{id}/cannedMessages
| POST | [Add a Canned Message to a Specific Category](#add-a-canned-message-to-a-specific-category) | /api/v1/livechat/cannedMessageCategories/{id}/cannedMessages

## List All Canned Message Categories
This API allows you get a list of canned message categories available in your account. If your agents have **"Manage Public Canned Messages"** permission, they can access all public canned messages as well as their own private canned messages; otherwise, only their own private canned messages are accessible.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories
```

### Response
The response contains a list of canned message categories. Each canned message category has the following properties:

| Property | Description |
| --- | ---
| `id` | the id of the canned message category
| `name` | the name of the canned message category
| `parentId` | the id of the parent category
| `isPrivate` | whether the canned message category is private or not

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 1,
        "name": "Greeting",
        "parentId": 0,
        "isPrivate": false,
    },
    {
        "id": 2,
        "name": "Price",
        "parentId": 0,
        "isPrivate": false,
    },
    ...
]
```

## Get a Single Canned Message Category
Gets specific canned message category by id.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id` | the id of the canned message category, which can be obtained from the [list of all canned message categories](#list-all-canned-message-categories)

### Response
| Property | Description |
| --- | ---
| `id` | the id of the canned message category
| `name` | the name of the canned message category
| `parentId` | the id of the parent category
| `isPrivate` | whether the canned message category is private or not

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/1" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "id": 1,
    "name": "Greeting",
    "parentId": 0,
    "isPrivate": false,
}
```

## Add a New Canned Message Category
Creates a new canned message category.

### Path
```bash
POST https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories
```

### Parameters
| Property | Description
| --- | ---
| `name` | required, the name of the canned message category
| `parentId` | optional, the id of the parent category
| `isPrivate` | optional, whether the canned message category is private or not

### Response
Returns the details of the newly created canned message category.

| Property | Description
| --- | ---
| `id` | the id of the newly added canned message category
| `name` | the name of the newly added canned message category
| `parentId` | the id of the parent category
| `isPrivate` | whether the canned message category is private or not, defaults to `false`

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories" \
    -X POST -d "name=testCategory" \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 \
```

Sample response:
```json
{
    "id": 6,
    "name": "testCategory",
    "parentId": 0,
    "isPrivate": false
}
```

## Update a Canned Message Category
Updates a specified canned message category by setting the values of the parameters passed. Any properties not provided will be left unchanged.

### Parameters
| Property | Description
| --- | ---
| `id` | the id of the canned message category, which can be obtained from the [list of all canned message categories](#list-all-canned-message-categories)
| `name` | the name of the canned message category
| `parentId` | the id of the parent category
| `isPrivate` | whether the canned message category is private or not

### Response
Returns the details of the updated canned message category.

| Property | Description |
| --- | ---
| `id` | the id of the updated canned message category
| `name` | the name of the updated canned message category
| `parentId` | the id of the parent category
| `isPrivate` | whether the canned message category is private or not

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/1" \
    -X PUT "name=testCategory" \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "id": 1,
    "name": "testCategory",
    "parentId": 0,
    "isPrivate": false,
}
```

## Delete a Canned Message Category
Deletes a specific canned message category.

### Path
```bash
DELETE https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/{id}
```

### Parameters
| Property | Description
| --- | ---
| `id` | the id of the canned message category, which can be obtained from the [list of all canned message categories](#list-all-canned-message-categories)

### Response
Returns status `200` when the canned message is deleted successfully.

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategory/6" \
    -X DELETE -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:

    Status: 200 OK

## Get Canned Messages of a Specific Category
Gets all canned messages of a specific category.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/{id}/cannedMessages
```

### Parameters
| Property | Description |
| --- | ---
| `id` | the id of the canned message category, which can be obtained from the [list of all canned message categories](#list-all-canned-message-categories)

### Response
| Property | Description |
| --- | ---
| `id` | the id of the canned message
| `name` | the name of the canned message
| `message` | the content of the canned message
| `categoryId` | the id of the category to which the canned message belongs
| `isPrivate` | whether the canned message is private or not
| `shortcuts` | the shortcuts of the canned message, available when the Shortcuts feature is on

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/1/cannedMessages" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 1,
        "name": "Hello",
        "message": "Hello!",
        "categoryId": 1,
        "isPrivate": false,
        "shortcuts": "hello",
    },
    {
        "id": 2,
        "name": "Hello",
        "message": "Hello!",
        "categoryId": 1,
        "isPrivate": false,
        "shortcuts": "hello",
    },
]
```

## Add a Canned Message to a Specific Category
Creates a canned message beloging to a specific category.

### Path
```bash
POST https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/{id}/cannedMessages
```

### Parameters
| Property | Description
| --- | ---
| `name` | required, the name of the canned message
| `message` | required, the content of the canned message
| `shortcuts` | optional, the shortcuts of the canned message, only works when the Shortcuts feature is on

### Response
Returns the details of the newly created canned message.

| Property | Description |
| --- | ---
| `id` | the id of the newly added canned message
| `name` | the name of the newly added canned message
| `message` | the content of the newly added canned message
| `categoryId` | the id of the category to which the canned message belongs, determined by `id`
| `isPrivate` | whether the canned message is private or not, determined by the category
| `shortcuts` | the shortcuts of the canned message, available when the Shortcuts feature is on

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/cannedMessageCategories/1/cannedMessages" \
    -X POST -d "name=testCannedMessage&message=testCannedMessage" \
    -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "id": 1,
    "name": "testCannedMessage",
    "message": "testCannedMessage",
    "categoryId": 1,
    "isPrivate": false,
    "shortcuts": ""
}
```
