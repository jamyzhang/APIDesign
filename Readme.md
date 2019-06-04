<center><h1>API设计格式样例</h1></center>

# 格式样例

## Resource List

  | Resource | URL |Description
  | - | - | -
  | [User](#User) | `/api/v3/users` |获取用户资源
  | [Task](#Task) | `/api/v3/tasks` |获取任务资源
## User
### Models
#### UserModel
    定义用户资源格式
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
# 命名规范
