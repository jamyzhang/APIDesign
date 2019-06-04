<center><h1>API设计格式样例</h1></center>

# 格式样例

## Resource List

  | Resource | URL |Desc
  | - | - | -
  | [User](#User) | `/api/v3/users` |获取资源
## Objects
### User
    定义用户资源格式
Name|DataType |Desc
---|---|---
id| int|`Read-only`<br>主键标识Id
name | string|`Optional`<br>名称

## Endpoints
### User
> Get a user

    根据UserId获取单个用户信息
- *GET* `/api/v3/users/{id}`
- **Path Paramters**
    - id: *int* `Required`
        - 主键
- **Request Body**
- **Response Body**
    - [User](#User)

>Query all users

    根据指定条件，获取所有满足条件用户
-  *GET* `/api/v3/users`
- **Path Paramters**
    - name: *string* `Optional`
        - 根据名字模糊匹配
- **Request Body**
- **Response Body**
    - [User](#User)[ ]
        - List of User 
>Create a user 

    新建用户
- *POST* `/api/v3/users`
- **Path Paramters**
- **Request Body**
    - [User](#user)
- **Response Body**
    - [User](#User)
