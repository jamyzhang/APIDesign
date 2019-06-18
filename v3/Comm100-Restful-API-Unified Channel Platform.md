# Unified Channel Platform

## Resource List

  | Resource | URL |Description
  | - | - | -
|[Integration Account](#integration-account)|`/api/v3/channelapp/integrationAccounts`| Management of Integration Account
|[Message](#message)|`/api/v3/channelapp/messages`|	
|[PublicKey](#publicKey)|`	/api/v3/channelapp/publickeys`|
|[App](#app)|`/v3/channelApp/apps`|
|[PrivateKey](#PrivateKey)	|`/v3/channelApp/PrivateKeys`|
|[Channel](#Channel) 	|`/v3/channelApp/channels`|
|[ContactIdentityType](#contactIdentityType)	|`/v3/channelApp/contactIdentityTypes`|


## Integration Account
### Models
#### IntegrationAccountModel
    The fields of a Integration Account.
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
accountName | string|`Optional`<br>The unique name of a integration account.
accountOriginalId|string|`Required`<br>the user account id of a  orginal channel .
isEnabled|bool|`Optional`<br>

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelapp/integrationAccounts/{id}`](#get-a-integration-Account)| Retrieve a integration account by the id.
[*POST* `/api/v3/channelapp/integrationAccounts`](#create-a-integration-Account)| create a integration account.
[*PUT* `/api/v3/channelapp/integrationAccounts/{id}`](#update-a-integration-Account)| update the integration account.
[*DELETE* `/api/v3/channelapp/integrationAccounts/{id}`](#delete-a-integrationAccount)| Delete the integration account.

#### Get a Integration Account
- *GET* `/api/v3/channelapp/integrationAccounts/{id}`
- **Path Paramters**
    - id: *int* `Required` the primary key of a integaration account.
- **Request Body**
- **Response Body**
    - [IntegrationAccountModel](#IntegrationAccountModel)

#### Create a Integration Account
-  *POST* `/api/v3/channelapp/integrationAccounts`
- **Path Paramters**
- **Request Body**
    - accountOriginalID：*string* `Required`
    - accountName：*string* `Required`
    - isEnable:*bool* `Optional`
- **Response Body**
    - [IntegrationAccountModel](#IntegrationAccountModel)

#### Update a Integration Account
-  *PUT* `/api/v3/channelapp/integrationAccounts/{id}`
- **Path Paramters**
   - id: *int* `Required` the primary key of a integaration account.
- **Request Body**
    - accountOriginalID：*string* `Required`
    - accountName：*string* `Required`
    - isEnable:*bool* `Optional`
- **Response Body**
    - [IntegrationAccountModel](#IntegrationAccountModel)

#### Delete a Integration Account
-  *Delete* `/api/v3/channelapp/integrationAccounts/{id}`
- **Path Paramters**
   - id: *int* `Required` the primary key of a integaration account.
- **Request Body**
- **Response Body**
## Message
### Models
#### Channel App Message
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
originalParnetId | string|`Optional`<br>The parent message id of the message
originalConversationId|string|`Optional`<br>
channelId|guid|`Required`<br>
originalMessageId|string|`Optional`<br>
orignalUrl|string|`Optional`<br>
cc|string|`Optional`<br>
subject|string|`Optional`<br>
contents|[Message Content](#message-content)[]|`Required`
createTime|time|`Required`



#### Message Content
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
type  | string|`Required`<br>Text/HtmlText/File/Video/Audio/Picture/Location
text|string|`Optional`<br> 
htmlText|string|`Optional`<br> 
name|string|`Optional`<br> 
title|string|`Optional`<br> 
url|string|`Optional`<br> 
latitude|double|`Optional`<br> 
longitude|double|`Optional`<br> 
desc|string|`Optional`<br> 

### Endpoints