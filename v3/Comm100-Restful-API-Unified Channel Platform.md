# Unified Channel Platform

## Resource List

  | Resource | URL |Description
  | - | - | -
|[Integration Account](#integration-account)|`/api/v3/channelapp/integrationAccounts`|Integration Account管理
|[Message](#message)|`/api/v3/channelapp/messages`|	Message管理
|[PublicKey](#publicKey)|`	/api/v3/channelapp/publickeys`|获取公钥

## Integration Account
### Models
#### IntegrationAccountModel
    定义集成账号格式
Name|Type |Description
---|---|---
id| guid|`Read-only`<br>主键标识Id
accountName | string|`Optional`<br>此账号在界面展示的名字，可识别的名字
accountOriginalId|string|`Required`<br>此Account在Original Channel的ID。
isEnabled|bool|`Optional`<br>是否可用

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/channelapp/integrationAccounts/{id}`](#get-a-integrationAccount)| 根据id获取集成账号明细
[*GET* `/api/v3/channelapp/integrationAccounts`](#query-all-integrationAccounts)| 根据指定条件，获取所有满足条件集成账号
[*POST* `/api/v3/channelapp/integrationAccounts`](#create-a-integrationAccount)| 新建集成账号
[*PUT* `/api/v3/channelapp/integrationAccounts/{id}`](#update-a-integrationAccount)| 修改集成账号
[*DELETE* `/api/v3/channelapp/integrationAccounts/{id}`](#delete-a-integrationAccount)| 删除集成账号

#### Get a IntegrationAccount
- *GET* `/api/v3/channelapp/integrationAccounts/{id}`
- **Path Paramters**
    - id: *int* `Required` 主键
- **Request Body**
- **Response Body**
    - [IntegrationAccountModel](#IntegrationAccountModel)

#### Query all IntegrationAccounts
-  *GET* `/api/v3/channelapp/integrationAccounts`
- **Path Paramters**
    - name: *string* `Optional`
        - 根据名字模糊匹配
- **Request Body**
- **Response Body**
    - [UserModel](#UserModel)[ ]
        - List of User 
#### Create a user 

    新建用户
- *POST* `/api/v3/users`
- **Path Paramters**
- **Request Body**
    - [UserModel](#userModel)
- **Response Body**
    - [UserModel](#UserModel)
