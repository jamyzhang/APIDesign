# Unified Channel Platform

## Resource List
  | Resource | URL |Description
  | - | - | -
|[ChannelAccounts](#channel-accounts)|`/api/v3/channelApp/channelAccounts`| Management of Channel Account
|[Messages](#messages)|`/api/v3/channelApp/messages`|	
|[PublicKeys](#publicKey)|`	/api/v3/channelApp/publicKeys`|
|[AppInfos](#appInfos)|`/api/v3/channelApp/appInfos`|
|[PrivateKeys](#PrivateKeys)	|`/api/v3/channelApp/privateKeys`|
|[Channels](#Channels) 	|`/api/v3/channelApp/channels`|
|[ContactIdentityTypes](#contact-Identity-Types)	|`/api/v3/channelApp/contactIdentityTypes`|
|[Apps](#apps)|`/api/v3/channelApp/apps`|
|[IpWhitelists](#IpWhitelists)|`/api/v3/channelApp/apps/{appId}/ipWhitelists`|
|[Versions](#Versions)|`/api/v3/channelApp/apps/{appId}/versions`|


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
[*PUT* `/api/v3/channelApp/messages/{id}/updateResult`](#delete-a-message)| Update message processing result
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
- *PUT* `/api/v3/channelApp/messages/{id}/updateResult`
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

## AppInofs
#### AppInfo
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
supportWebsit|string|
versionNumber|string|
installationUrl|string|
oauthRedirectUrl|string|
settingUrl|string|
messageWebhookUrl|string|

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/appInfos`](#retrieve-appInfos)| Retrieve  appInfos.
[*GET* `/api/v3/channelApp/appInfos/installed`](#Get-installed-appInfos)|Get the list of appInfos that installed at a site.
[*GET* `/api/v3/channelApp/appInfos/allowInstallation`](#get-allow-installation-appInfos)|Get the list of appInfos that is allowed to install at a site.
#### Retrieve appInfos
- *GET* `/api/v3/channelApp/appInfos?isSystem={isSystem}`
- **URL Parameters**
   - isSystem: *bool* `Optional`  if isSysetem is true, the result must be System appInfos.
- **Request Body**
- **Response Body**
    - [AppInfo](#appInfo)[ ]
#### Get installed appInfos
- *GET* `/api/v3/channelApp/appInfos/installed?siteId={siteId}`
- **URL Parameters**
   - siteId: *int* `Required`  
- **Request Body**
- **Response Body**
    - [AppInfo](#appInfo)[ ]
 #### Get allow installation appInfos
- *GET* `/api/v3/channelApp/appInfos/allowInstallation?siteId={siteId}`
- **URL Parameters**
   - siteId: *int* `Required`  
- **Request Body**
- **Response Body**
    - [AppInfo](#appInfo)[ ]




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
### Endpoints

Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/channels`](#Get-a-list-of-channels)| Get a list of channels.
[*GET* `/api/v3/channelApp/channels/{id}`](#Get-the-channel)| Get the channel.
[*POST* `/api/v3/channelApp/channels`](#create-a-channel)| Create a channel.
[*PUT* `/api/v3/channelApp/channels/{id}`](#update-the-channel)| Update the channel.
[*DELETE* `/api/v3/channelApp/channels/{id}`](#delete-the-channel)| Delete the channel.
### Get a list of channels 
    if the appId Parameter is not has a value,  all channels which have installed to  the siteId are returned.
- *GET* `/api/v3/channelApp/channels`
- **URL Parameters**
   - appId: *guid*  
   - versionId: *guid*
- **Request Body**
- **Response Body**
    - [Channel](#channel)[ ]

### Get the channel
- *GET* `/api/v3/channelApp/channels/{id}`
- **URL Parameters**
    - id: *guid* 
- **Request Body**
- **Response Body**
    - [Channel](#channel)

### Create a channel
- *POST* `/api/v3/channelApp/channels`
- **URL Parameters**
- **Request Body**
    - [Channel](#channel)
- **Response Body**
    - [Channel](#channel)
### Update the channel
- *PUT* `/api/v3/channelApp/channels/{id}`
- **URL Parameters**
    - id: *guid* 
- **Request Body**
    - [Channel](#channel)
- **Response Body**
    - [Channel](#channel)
### Delete the channel
- *DELETE* `/api/v3/channelApp/channels/{id}`
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
### Get the list of Contact Identity Type at a site
    Get the contact Identity Types of the site
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
status|smallint|`Required`
authorName|string|
authorEmail|string|
publishVersion|string|
lastesVersion|string|`Required`
siteId|string|`Required`
channelAccountName|string|`Required`


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
## IpWhitelists
### Ip Address
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
Ip|string|`Required`
### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/apps/{appId}/ipWhitelists`]()| Get the Ip whitelist which have created in the app.<br>*Standard Design*
[*GET* `/api/v3/channelApp/apps/{appId}/ipWhitelists/{id}`]()| Get the ip address.<br>*Standard Design*
[*POST* `/api/v3/channelApp/apps/{appId}/ipWhitelists`]()| Create an  ip address to the whitelist.<br>*Standard Design*
[*PUT* `/api/v3/channelApp/apps/{appId}/ipWhitelists/{id}`]()| Update the  ip address <br>*Standard Design*
[*DELETE* `/api/v3/channelApp/apps/{appId}/ipWhitelists/{id}`]()| Delete the  ip address <br>*Standard Design*
## Versions
### Version
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>Primary key
number|string|the number of version
name|string|
description|string|
largeIconUrl|string
smallIconUrl|string
installationUrl|string
oauthRedirectUrl|string
settingUrl|string
messageWebhookUrl|string
### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelApp/apps/{appId}/versions`]()| Get a list of version which have created in the app.<br>*Standard Design*
[*GET* `/api/v3/channelApp/apps/{appId}/versions/{id}`]()| Get the version.<br>*Standard Design*
[*POST* `/api/v3/channelApp/apps/{appId}/versions`]()| Create a version.<br>*Standard Design*
[*PUT* `/api/v3/channelApp/apps/{appId}/versions/{id}`]()| Update the version <br>*Standard Design*
[*DELETE* `/api/v3/channelApp/apps/{appId}/versions/{id}`]()| Delete the version <br>*Standard Design*
[*DELETE* `/api/v3/channelApp/apps/{appId}/versions/{id}/removeChannel`]()| Remove the channel from the version.
[*PATCH* `/api/v3/channelApp/apps/{appId}/versions/{id}/addChannel`]()| Add the channel to the version.
[*POST* `/api/v3/channelApp/apps/{appId}/versions/{id}/addChannel`]()| Create a  channel to the version.

#### Remove the channel from the version
- *DELETE* `/api/v3/channelApp/apps/{appId}/versions/{id}/removeChannel?channelId={channelId}`
- **URL Parameters**
    - appId: *guid* `Required`  
   - id: *guid* `Required`  
   - channelId: *guid* `Required`
- **Request Body**
- **Response Body**
####  Add the channel to the version
- *PATCH* `/api/v3/channelApp/apps/{appId}/versions/{id}/addChannel?channelId={channelId}`
- **URL Parameters**
    - appId:  *guid* `Required`  
   - id: *guid* `Required`  
   - channelId: *guid* `Required`
- **Request Body**
- **Response Body**
#### Create a  channel to the version.
- *POST* `/api/v3/channelApp/apps/{appId}/versions/{id}/addChannel`
- **URL Parameters**
    - appId:  *guid* `Required`  
   - id: *guid* `Required`   
- **Request Body**
    - [Channel](#channel)
- **Response Body**
    - [Channel](#channel)