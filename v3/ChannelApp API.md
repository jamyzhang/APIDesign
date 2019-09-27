# Unified Channel Platform

## Resource List
  | Resource | URL |Description
  | - | - | -
|[ChannelAccounts](#channel-accounts)|`/api/v3/channelApp/channelAccounts`| Management of Channel Account
|[Messages](#messages)|`/api/v3/channelApp/messages`|
|[PublicKeys](#publicKey)|`	/api/v3/channelApp/publicKeys`|
|[ContactIdentityTypes](#contact-Identity-Types)	|`/api/v3/channelApp/contactIdentityTypes`|
|[Apps](#apps)|`/api/v3/channelApp/apps`|
|[IpAddresses](#Ip-Addresses)|`/api/v3/channelApp/apps/{appId}/ipAddresses`|
|[Versions](#Versions)|`/api/v3/channelApp/apps/{appId}/versions`|
|[Channels](#Channels) 	|`/api/v3/channelApp/apps/{appId}/versions/{versionId}/channels`|

## Channel Accounts
### Models
#### ChannelAccount
    The fields of a Channel Account.
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
appId| guid|`Required`<br>
siteId| int|`Required`<br>
accountName | string|`Optional`<br>The unique name of a channels account.
accountOriginalId|string|`Required`<br>the user account id of an  original channel.
isEnabled|bool|`Optional`<br>

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/channelAccounts/{id}`](#get-a-channel-Account)| Retrieve a channel account by the id.
[*GET* `/api/v3/channelApp/channelAccounts`](#get-a-list-of-channel-Account)| Retrieve a list of channel account.
[*POST* `/api/v3/channelApp/channelAccounts`](#create-a-channel-Account)| create a channel account.
[*PUT* `/api/v3/channelApp/channelAccounts/{id}`](#update-a-channel-Account)| update the channel account.
[*DELETE* `/api/v3/channelApp/channelAccounts/{id}`](#delete-a-channelAccount)| Delete the channel account.

#### Get a Channel Account
- *GET* `/api/v3/channelApp/channelAccounts/{id}`
- **URL Parameters**
    - id: *guid* `Required` the primary key of a channel account.
- **Request Body**
- **Response Body**
    - [ChannelAccount](#ChannelAccount)

#### Get a list of channel Account
- *GET* `/api/v3/channelApp/channelAccounts`
- **URL Parameters**
    - appId: *guid* `Optional`
    - siteId: *int* `Optional` 
- **Request Body**
- **Response Body**
    - [ChannelAccount](#ChannelAccount)[ ]
#### Create a Channel Account
-  *POST* `/api/v3/channelApp/channelAccounts`
- **URL Parameters**
- **Request Body**
    - accountOriginalId：*string* `Required`
    - accountName：*string* `Required`
    - isEnable:*bool* `Optional`
- **Response Body**
    - [ChannelAccount](#IntegrtionAccountModel)

#### Update a Channel Account
-  *PUT* `/api/v3/channelApp/channelAccounts/{id}`
- **URL Parameters**
   - id: *guid* `Required` the primary key of a channel account.
- **Request Body**
    - accountOriginalId：*string* `Required`
    - accountName：*string* `Required`
    - isEnable:*bool* `Optional`
- **Response Body**
    - [ChannelAccount](#ChannelAccount)

#### Delete a Channel Account
-  *Delete* `/api/v3/channelApp/channelAccounts/{id}`
- **URL Parameters**
   - id: *guid* `Required` the primary key of a channel account.
- **Request Body**
- **Response Body**
## Messages
### Models
#### Channel App Contact Identity
Name|Type |Description
---|---|---
account| string|`Required`<br>The user account id of a visitor in original channel.
name | string|`Optional`<br>
avatarUrl|string|`Optional`<br>
originalContactInfoUrl|string|`Optional`<br>
#### Channel App Message
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
originalParentId | string|`Optional`<br>The parent message id of the message
originalConversationId|string|`Optional`<br>
channelId|guid|`Required`<br>
originalMessageId|string|`Optional`<br>
originalUrl|string|`Optional`<br>
cc|string|`Optional`<br>
subject|string|`Optional`<br>
contents|[Message Content](#message-content)[]|`Required`
createTime|time|`Required`



#### Message Content
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
type  | string|`Required`<br>Text/HtmlText/File/Video/Audio/Picture/Location
text| string| If the type is Text, this field is required.
htmlText|string|If the type is HtmlText, this field is required.
name|string|If the type is File, this field is required.
title|string|If the type is Video, Audio or Picture, this field is required.
mime|string|If the type is File, Video, Audio or Picture, this field is required.
previewUrl|string|If the type is  Video, this field is required.
url|string|If the type is File, Video, Audio or Picture, this field is required.
latitude|double|If the type is Location, this field is required.
longitude|double|If the type is Location, this field is required.
desc|string| The description of a loaction.

### Endpoints

Endpoint |Description
---|---
[*POST* `/api/v3/channelApp/messages`](#create-a-messsage)| Create a message.
[*DELETE* `/api/v3/channelApp/messages/{id}`](#delete-a-message)| Delete a message.
[*PUT* `/api/v3/channelApp/messages/{id}:updateResult`](#delete-a-message)| Update message processing result
#### Create a message
-  *POST* `/api/v3/channelApp/messages`
- **URL Parameters**
- **Request Body**
    - ChannelAccountId：*Guid*  `Required` The primary key of the integrated account that  receives messages.
    - ChannelAppContactIdentity：[Channel App Contact Identity](#channel-app-contact-identity)
    - IsReceive: *Bool* `Optional` If ture,it means that the message is sent to a channel account by a contact , or vice versa.
    - Message：[Channel App Message](#channel-app-message)
- **Response Body**
    - MessageId: *Guid* `Read-only`
- **Error Response Body**
    - http status code: 500
    - body
        - Code: *int*  `Required` 1200001/12000002
            1. 1200001 indicates that the message processing failed.
            2. 1200002 indicates that its parent message does not exist and needs to be transmitted by the 3rd App.
        - Message:

#### Delete a message
- *DELETE* `/api/v3/channelApp/messages/{id}`
- **URL Parameters**
   - id: *guid* `Required` the primary key of a message.
- **Request Body**
- **Response Body**

#### Update message processing result
- *PUT* `/api/v3/channelApp/messages/{id}:updateResult`
- **URL Parameters**
   - id: *guid* `Required` the primary key of a message.
- **Request Body**
    - IsSuccessful: *bool* `Required`
    - ErrorMessage：*string* `Optional`
    - Urls: `Optional` the list of new urls for files. 
        - Id: *guid* `Required`  the guid of a file.
        - Url: *string* `Required` the new url of a file.
     - OriginalMessageId: *string* `Optional`   
     - OrignalMessageUrl: *string* `Optional`
- **Response Body**
## PublicKeys
#### Retrieve public key
- *GET* `/api/v3/channelApp/publicKeys?appid={appId}`
- **URL Parameters**
   - appId: *guid* `Required` 
- **Request Body**
- **Response Body**
    - key: *string* the public key of an app.

## Channels
### Channel
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
appId|guid|
name|string|
contactIdentityTypeId|guid|
messageDisplayType|int|
outgoingMessageMaxLength|int|
outgoingMessageCapability|string|
ifSupportDiffAccountReply|bool|
ifAllowActiveCreation|bool|
ifDisplaySubject|bool|
ifDisplayContact|bool|
ifDisplayCc |bool|
ifDisplayToolbarOfEditor |bool|
ifDisplayAttachment |bool|
ifDisplayChannelAccount |bool|
ifEnableFullScreenReplay |bool|
IfHasNote |bool|
IfEnableSaveAsDraft |bool|
IfAllowAtFeature |bool|
### Endpoints

Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/versions/{versionId}/channels`](#Get-a-list-of-channels)| Get a list of channels.
[*GET* `/api/v3/channelApp/versions/{versionId}/channels/{id}`](#Get-the-channel)| Get the channel.
[*POST* `/api/v3/channelApp/versions/{versionId}/channels`](#create-a-channel)| Create a channel.
[*PUT* `/api/v3/channelApp/versions/{versionId}/channels/{id}`](#update-the-channel)| Update the channel.
[*DELETE* `/api/v3/channelApp/versions/{versionId}/channels/{id}`](#delete-the-channel)| Delete the channel.


### Get a list of channels 
    if the appId Parameter is not has a value,  all channels which have installed to  the siteId are returned.
- *GET* `/api/v3/channelApp/versions/{versionId}/channels`
- **URL Parameters**
   - appId: *guid*  
   - versionId: *guid*
- **Request Body**
- **Response Body**
    - [Channel](#channel)[ ]

### Get the channel
- `/api/v3/channelApp/apps/{appId}/channels/{id}`
- **URL Parameters**
    - id: *guid* 
- **Request Body**
- **Response Body**
    - [Channel](#channel)

### Create a channel
- *POST* `/api/v3/channelApp/versions/{versionId}/channels`
- **URL Parameters**
- **Request Body**
    - [Channel](#channel)
- **Response Body**
    - [Channel](#channel)
### Update the channel
- *PUT* `/api/v3/channelApp/versions/{versionId}/channels/{id}`
- **URL Parameters**
    - id: *guid* 
- **Request Body**
    - [Channel](#channel)
- **Response Body**
    - [Channel](#channel)
### Delete the channel
- *DELETE* `/api/v3/channelApp/versions/{versionId}/channels/{id}`
- **URL Parameters**
    - id: *guid* 
- **Request Body**
- **Response Body**
## Contact Identity Types
### Contact Identity Type
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
name|string|
iconUrl|string|
### Endpoints

Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/contactIdentityTypes`]()|
[*GET* `/api/v3/channelApp/contactIdentityTypes/{id}`]()| Get the contact identity type.<br>*Standard Design*
[*POST* `/api/v3/channelApp/contactIdentityTypes`]()|Create a contact identity type.<br>*Standard Design*
[*PUT* `/api/v3/channelApp/contactIdentityTypes/{id}`]()|Update the contact identity type.<br>*Standard Design*
[*DELETE* `/api/v3/channelApp/contactIdentityTypes/{id}`]()|Delete the contact identity type.<br>*Standard Design*
### Get the list of Contact Identity Type 
- *GET* `/api/v3/channelApp/contactIdentityType`
- **URL Parameters**
- **Request Body**
- **Response Body**
    - [Contact Identity Type](#Contact-identity-type)[ ]

## Apps
### App
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
secretKey|string|`Read-only`
isSystem|bool|`Required`
isVirtual|bool|`Required`
status|smallint|`Required`
authorName|string|
authorEmail|string|
publishVersionId|guid|
lastesVersionId|guid|
siteId|string|`Required`


### Endpoints

Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/apps`](#Get-a-list-of-apps)| Get a list of apps.
[*GET* `/api/v3/channelApp/apps/{id}`](#Get-the-app)| Get the app.
[*POST* `/api/v3/channelApp/apps`](#create-an-app)| Create an app.
[*PUT* `/api/v3/channelApp/apps/{id}`](#update-the-app)| Update the app.
[*DELETE* `/api/v3/channelApp/apps/{id}`](#delete-the-app)| Delete the app.

#### Get a list of apps
- *GET* `/api/v3/channelApp/apps`
- **URL Parameters**
- **Request Body**
- **Response Body**
    - [App](#app)[ ]

#### Get the app
- *GET* `/api/v3/channelApp/apps/{id}`
- **URL Parameters**
   - id: *guid* `Required`  
- **Request Body**
- **Response Body**
    - [App](#app)
#### Create an app
- *POST* `/api/v3/channelApp/apps`   
- **Request Body**
    - [App](#app)
- **Response Body**
    - [App](#app)
#### Update the app
- *PUT* `/api/v3/channelApp/apps/{id}`
- **URL Parameters**
   - id: *guid* `Required`  
- **Request Body**
    - [App](#app)
- **Response Body**
    - [App](#app)
#### Delete the app
- *DELETE* `/api/v3/channelApp/apps/{id}`
- **URL Parameters**
   - id: *guid* `Required`  
- **Request Body**
- **Response Body**
## Ip Addresses
### Ip Address
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
Ip|string|`Required`
### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/apps/{appId}/ipAddresses`]()| Get the Ip whitelist which have created in the app.<br>*Standard Design*
[*GET* `/api/v3/channelApp/apps/{appId}/ipAddresses/{id}`]()| Get the ip address.<br>*Standard Design*
[*POST* `/api/v3/channelApp/apps/{appId}/ipAddresses`]()| Create an  ip address to the whitelist.<br>*Standard Design*
[*PUT* `/api/v3/channelApp/apps/{appId}/ipAddresses/{id}`]()| Update the  ip address <br>*Standard Design*
[*DELETE* `/api/v3/channelApp/apps/{appId}/ipAddresses/{id}`]()| Delete the  ip address <br>*Standard Design*
## Versions
### Version
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
number|string|the number of version
name|string|
channelAccountName|string|`Required`
description|string|
largeIconUrl|string
smallIconUrl|string
installationUrl|string
oauthRedirectUrl|string
settingUrl|string
messageWebhookUrl|string|
channelIds| guid[ ]
status|smallint|`Required`
### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/apps/{appId}/versions`]()| Get a list of version which have created in the app.<br>*Standard Design*
[*GET* `/api/v3/channelApp/apps/{appId}/versions/{id}`]()| Get the version.<br>*Standard Design*
[*POST* `/api/v3/channelApp/apps/{appId}/versions`]()| Create a version.<br>*Standard Design*
[*PUT* `/api/v3/channelApp/apps/{appId}/versions/{id}`]()| Update the version <br>*Standard Design*
[*DELETE* `/api/v3/channelApp/apps/{appId}/versions/{id}`]()| Delete the version <br>*Standard Design*
