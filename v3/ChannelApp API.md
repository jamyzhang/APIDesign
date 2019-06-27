# Unified Channel Platform

## Resource List

  | Resource | URL |Description
  | - | - | -
|[ChannelAccounts](#channel-accounts)|`/api/v3/channelApp/channelAccounts`| Management of Channel Account
|[Messages](#messages)|`/api/v3/channelApp/messages`|	
|[PublicKeys](#publicKey)|`	/api/v3/channelApp/publicKeys`|
|[Apps](#apps)|`/api/v3/channelApp/apps`|
|[PrivateKeys](#PrivateKeys)	|`/api/v3/channelApp/privateKeys`|
|[Channels](#Channels) 	|`/api/v3/channelApp/channels`|
|[ContactIdentityTypes](#contact-Identity-Types)	|`/api/v3/channelApp/contactIdentityTypes`|


## Channel Accounts
### Models
#### ChannelAccount
    The fields of a Channel Account.
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
accountName | string|`Optional`<br>The unique name of a channels account.
accountOriginalId|string|`Required`<br>the user account id of an  original channel .
isEnabled|bool|`Optional`<br>

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/channelAccounts/{id}`](#get-a-channel-Account)| Retrieve a channel account by the id.
[*POST* `/api/v3/channelApp/channelAccounts`](#create-a-channel-Account)| create a channel account.
[*PUT* `/api/v3/channelApp/channelAccounts/{id}`](#update-a-channel-Account)| update the channel account.
[*DELETE* `/api/v3/channelApp/channelAccounts/{id}`](#delete-a-channelAccount)| Delete the channel account.

#### Get a Channel Account
- *GET* `/api/v3/channelApp/channelAccounts/{id}`
- **URL Parameters**
    - id: *int* `Required` the primary key of a channel account.
- **Request Body**
- **Response Body**
    - [ChannelAccount](#ChannelAccount)

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
   - id: *int* `Required` the primary key of a channel account.
- **Request Body**
    - accountOriginalId：*string* `Required`
    - accountName：*string* `Required`
    - isEnable:*bool* `Optional`
- **Response Body**
    - [ChannelAccount](#ChannelAccount)

#### Delete a Channel Account
-  *Delete* `/api/v3/channelApp/channelAccounts/{id}`
- **URL Parameters**
   - id: *int* `Required` the primary key of a channel account.
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

Endpoint |Description
---|---
[*POST* `/api/v3/channelApp/messages`](#create-a-messsage)| Create a message.
[*DELETE* `/api/v3/channelApp/messages/{id}`](#delete-a-message)| Delete a message.
[*PATCH* `/api/v3/channelApp/messages/{id}/updateResult`](#delete-a-message)| Update message processing result
#### Create a message
-  *POST* `/api/v3/channelApp/messages`
- **URL Parameters**
- **Request Body**
    - ChannelAccountId：*Guid*  `Required` The primary key of the integrated account that  receives messages.
    - ChannelAppContactIdentity：[Channel App Contact Identity](#channel-app-contact-identity)
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
- *PATCH* `/api/v3/channelApp/messages/{id}/updateResult`
- **URL Parameters**
   - id: *guid* `Required` the primary key of a message.
- **Request Body**
    - IsSuccessful: *bool* `Required`
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
   - appId: *int* `Required` 
- **Request Body**
- **Response Body**
    - key: *string* the public key of an app.

## Apps
#### App
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
name|string|
channelAccountName|string|
description|string|
largeIconUrl|string|
smallIconUrl|string|
authorEmail|string|
authorName|string|
supportWebsite|string|
versionNumber|string|
installationUrl|string|
oauthRedirectUrl|string|
settingUrl|string|
messageWebhookUrl|string|

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/apps`](#retrieve-apps)| Retrieve  apps.
[*GET* `/api/v3/channelApp/apps/installed`](#Get-installed-apps)|Get the list of apps that installed at a site.
[*GET* `/api/v3/channelApp/apps/allowInstallation`](#get-allow-installation-apps)|Get the list of apps that is allowed to install at a site.
#### Retrieve apps
- *GET* `/api/v3/channelApp/apps?isSystem={isSystem}`
- **URL Parameters**
   - isSystem: *bool* `Optional`  if isSysetem is true, the result must be System apps.
- **Request Body**
- **Response Body**
    - [App](#app)[ ]
#### Get installed apps
- *GET* `/api/v3/channelApp/apps/installed?siteId={siteId}`
- **URL Parameters**
   - siteId: *int* `Required`  
- **Request Body**
- **Response Body**
    - [App](#app)[ ]
 #### Get allow installation apps
- *GET* `/api/v3/channelApp/apps/allowInstallation?siteId={siteId}`
- **URL Parameters**
   - siteId: *int* `Required`  
- **Request Body**
- **Response Body**
    - [App](#app-model)[ ]

## PrivateKey
#### Get PrivateKey
- *GET* `/api/v3/channelApp/privateKeys?appId={appId}`
- **URL Parameters**
   - appId: *guid* `Required`  
- **Request Body**
- **Response Body**
    - key: *string*

## Channels
### Channel
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
name|string|
contactIdentityType|string|
messageDisplayType|int|
outgoingMessageMaxLength|int|
outgoingMessageCapability|string|
isSupportDiffAccountReply|bool|
isAllowActiveCreatation|bool|

### Get the list of channels in an app
- *GET* `/api/v3/channelApp/channels?appId={appId}`
- **URL Parameters**
   - appId: *guid* `Required`  
- **Request Body**
- **Response Body**
    - [Channel](#channel)[ ]

### Get the list of available channels at a site

- *GET* `/api/v3/channelApp/channels/bySite?siteId={siteId}`
- **URL Parameters**
   - siteId: *int* `Required`  
- **Request Body**
- **Response Body**
    - [Channel Model](#channel-model)[ ]

## Contact Identity Types
### Contact Identity Type
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
name|string|
iconUrl|string|
### Get the list of Contact Identity Type at a site
- *GET* `/api/v3/channelApp/contactIdentityType?siteId={siteId}`
- **URL Parameters**
   - siteId: *int* `Required`  
- **Request Body**
- **Response Body**
    - [Contact Identity Type](#Contact-identity-type)[ ]
