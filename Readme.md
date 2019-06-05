<center><h1>API文档规范</h1></center>

# 规范说明
- 在文档开始，建立一个Resource List表，罗列此文档所有可操作的资源。
- 每个资源的说明包含Models和Endpoints两部分。
- Endpoints部分一开始罗列此资源的所有操作。
- 书写格式就按下面的样例套用。说明文字是可选项。

# 命名规范
- 资源以复数命名
- 资源不进行多层嵌套
    - 比如原来的`/api/v3/conversations/{id}/messages`来获取Message资源，这里进行了资源嵌套。建议采用`/api/v3/messages?conversationsId={id}`来获取。
-	API统一使用JS推荐的驼峰来命名，包括所有的文档中的url, 对象名称，对象属性
-	实体/属性的命名统一用名词
-	时间格式统一使用iso 8601标准, https://en.wikipedia.org/wiki/ISO_8601
-	唯一性检查的方法, 采用HEAD Method, 检查具体唯一性的资源
    -	HEAD intents/names/{name}
    -	HEAD agents/emails/{email}


# 格式样例

## Resource List

  | Resource | URL |Description
  | - | - | -
  | [User](#User) | `/api/v3/users` |获取用户资源
  | [Task](#Task) | `/api/v3/tasks` |获取任务资源
## User
### Models
#### UserModel
    定义用户资源格式。说明文字是可选项。
Name|Type |Description
---|---|---
id| int|`Read-only`<br>主键标识Id
name | string|`Optional`<br>名称

### Endpoints
Endpoint |Description
---|---
[*GET* `/api/v3/users/{id}`](#get-a-user)| 根据UserId获取单个用户信息
[*GET* `/api/v3/users`](#query-all-users)| 根据指定条件，获取所有满足条件用户
[*POST* `/api/v3/users`](#create-a-user)| 新建用户

#### Get a user

    根据UserId获取单个用户信息
- *GET* `/api/v3/users/{id}`
- **Path Paramters**
    - id: *int* `Required`
        - 主键
- **Request Body**
- **Response Body**
    - [UserModel](#UserModel)

#### Query all users

    根据指定条件，获取所有满足条件用户
-  *GET* `/api/v3/users`
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
# HTTP Method的使用规则

## HEAD
  
  在实际使用中, 会使用到唯一性检查, 采用HEAD操作来获取, 返回404就表示不存在, 否则就是存在的, 如果存在可以返回200, 顺便带上这个资源的endpoint

  - 如判断名字为`LiveChat`的Department是否存在
  
    `HEAD api/v2/livechat/departments/name/LiveChat`

## GET
1. 获取批量的数据, 采用GET方法获取, 参数通过queryString传递
  
    - 如获取5月份的聊天数据: `GET api/v2/livechat/chats?timeFrom=2018-05-01&timeEnd=2018-05-31`

2. 获取单个资源, 采用GET方式获取, 一般使用id定位资源
  
    - 如获取id为1的聊天数据: `GET api/v2/livechat/chats/1`

## POST 
1. 创建新的资源, 采用POST方式新增资源, 参数通过JSON格式传递, 结构中描述的Mandatory为yes的属性必须有值, Read-Only的属性则不需要传
  
    -  如新增一个Campaign: `POST api/v2/livechat/campaigns`

      ```json
      {
        "name": "support",
        "language": "en",
      }
      ```

2. 其他类型的action操作, 某些操作需要在服务器执行较复杂的操作, 这个时候允许使用action作为资源的一个操作

    - 如 merge ticket (将id为2的ticket merge到id为1的ticket): `POST api/v2/ticket/tickets/1/merge`

      ```json
      {
        "id": 2,
      }
      ```


## PUT

1. 当需要完整更新一个资源时, 使用PUT方法, 参数为需要更新的JSON格式对象.
  
  如更新id为1的camapgin:
  `PUT api/v2/livechat/campaigns/1`
  ```json
  {
    "id": 1,
    "name": "for website",
    "language": "en",
  }
  ```

2. 当新增一个已经确定uri的资源时, 可以是使用PUT方法, 参数为需要更新的JSON格式对象

  如以email地址定义资源的agent, 可以直接用put操作, 如果已经存在就修改, 如果不存在就添加

  `PUT api/v2/account/agents`

  ```json
  {
    "email": "allon.lu@comm100.com",
    // ...
  }
  ```

3. 当需要对多个资源进行批量操作时, 可以使用PUT方法进行

  如对多个ticket进行批量操作: `PUT api/v2/tickets`

  ```json
  {
    "ids": [1,2],
    "ticket": {
      "priority": "urgent",
      "assignee": {
        "agent": 2,
      }
    }
  }
  ```

## DELETE

  当需要删除一个资源时, 使用DELETE方法

  如删除id为1的Campaign:
  `DELETE api/v2/livechat/campaigns/1`

## PATCH
  
  当需要部分更新一个资源时, 使用PATCH方法, 参数为需要更新的对象中的部分属性组成的JSON格式
  
  如只需要更新id为1的Campaign的语言为中文: 
  `PUT api/v2/livechat/campaigns/{id}`
  ```json
  {
    "language": "zh",
  }
  ```
# 错误管理
- 在请求未正常执行时，Server会根据真实情况返回对应的http status code，在此基础上会从http response中返回Comm100定义的的error code和error message 
- 错误规范

| Http Status Code | 返回结果 |
| --- | --- |
200 - OK    |一切正常，且Response里面返回正确的结果
400 - Bad Request |参数传入不正确或者不合法。Response里面包含Comm100的error code和error string
401 - Unauthorized|无授权，用户验证不通过
403 - Forbidden|调用超出限制, Agent本身没有权限。Response里面包含Comm100的error code和error string
404 - Not Found|请求资源不存在。Response里面包含Comm100的error code和error string
500 - Internal Error|服务器内部错误。Response里面包含Comm100的error code和error string。这个错误包含比较广泛，上述错误外，其他的错误都会在500中返回。

- Error Response, 以json格式返回具体的错误信息
```json
    {
        "code": 403003,
        "message": "You have no permission to perform this operation."
    }
```
- 错误编码规范
    - 错误编码采用Comm100 Framework中对各个产品能够使用的错误码范围中使用，保留400000 – 600000为api中特定使用的错误编码


Error code|Http status code|Message
---|---|---
400000|400|Parameter '{param}' is required.
400001|400|Parameter '{param}' should be in time format of 'YYYY-MM-DDThh:mm:ssZ'.
400002|400|Parameter '{param}' should be in timezone format of '+-hh:mm'.
400003|400|Parameter '{param}' should be a number.
400004|400|Parameter '{param}' should be 'true' or 'false'.
400005|400|Parameter '{param}' should be an email.
400006|400|Unsupported '{param}' type.
400008|400|The time period should be within {duration} months.
400009|400|Parameter '{param}' is outside the number range, between {from} and {to}.
400010|400|Parameter '{param}' length exceeded the limit of {length}.
400011|400|You can only search for the records of the last {duration} months.
403000|403|Access denied.
403001|403|Your accout has been closed.
403002|403|Your accout is not available.
403003|403|You do not have '{permission}' permission.
403004|403|You have license(s) expired, or your current agent count has exceeded the total valid licenses. Please add new licenses to avoid any service interruption.
403005|403|There are no licenses in your account. Please contact your account manager to purchase new licenses.
404000|404|{url} not found.
404001|404|{object} with ID {id} does not exists.
409000|409|{object} with name {name} already exists.
500000|500|You have reached the daily API calling limit: {times}. If you want to increase your API calling times, please contact us at: {email}.

- error code范围
1.	公共400000 – 600000 (不包括600000，下同)
2.	Livechat 1000000-1100000
3.	KB 1100000-1200000
4.	Social 1200000-1300000
5.	Ticket 1300000-1400000
