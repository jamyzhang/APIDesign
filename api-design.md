
# 概述

1. API的设计文档使用markdown文件来维护
2. 所有的API统一放到 Teams >> Research and Development >> General >> API 下面, 每一个api一份文档, 如livechat可能有如下几个api
  - livechat visitor api
  - livechat agent console api
  - livechat restful api
  - livechat webhook api
  - livechat partner api
3. API 需要有版本号管理, API 文档中应该描述变更历史, 采用表格描述清楚

  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v1 | Live Chat Restful API | 2018-5-5 | Allon |
  | 1.1 | v1 | 添加了Report API | 2018-06-06 | Roy |
  | 2.0 | v2 | 使用Webapi重新设计的Live Chat Restful API | 2018-9-9 | Kim |
  | 2.0.1 | v2 | 修改了chat返回的结构 | 2018-09-20 | Surey |

  - Change Version 是 API文档的变更历史
  - API Version是公开出来的api调用的版本号, 会体现在api地址等各个地方

# WEB API 文档评审规范

## 描述该API下面的所有资源以及接口地址

针对一个API服务需要描述这个服务下面的所有资源以及对应的接口路径, 如LiveChatAPI有如下资源及对应的path:

| Object | Path |
| - | - |
| [Campaign](#campaign) | `/livechat/campaigns` |
| [Canned Message](#canned-message) | `/livechat/cannedMessages` |
| [Agent](#agent) | `livechat/agents` | 
| [Chat](#chat) | `livechat/chats` |

---

+ 说明:
  - Object列中的内容需要添加链接到下面对应的位置
  - Path一般为该资源的复数形式, 对应资源的所有接口都应该在这个path下面


## 定义具体资源的JSON结构

针对一个资源, 首先定义资源的属性, 针对该资源的增删改查都是基于这个资源的属性来控制参数和返回, 资源属性的标准格式如下: 


  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no | id of this agent |
  | `name` | string | no | yes | name of this agent |
  | `status` | string | no | no | type of this agent, maybe `online`, `away` or `offline` |
  | `departments` | integer[]  | no | no | department ids of this agent belong |
  | `permissions` | [permissions](#permissions) | no | no | permission of this group |
  | `preference.isEnableAutoTranslation` | string | no | no | whether enable auto translation for this agent |
  | `preference.autoTranslationLanguage` | string | no | no | the language of this agent uses auto translation |

---

  + 列表属性说明:
    - `Name` - 表示字段的名字, 如果名字中有`.`结构, 则表示这是一个子结构(只有当该子结构仅在这里使用时可以使用这种形式描述)
    - `Type` - 表示该字段的类型, 可以为常规的数据类型也可以为另外一个结构(如果是另一个结构应该加上链接), 如果类型后面有`[]`表示该字段是一个数组
    - `Read-only` - 表示该字段是否只读, 如果只读则表示用户无法通过新增/编辑指定该字段的值
    - `Mandatory` - 表示该字段是否必须, 如果必须则表示用户在新增时必须提供该字段的值
    - `Description` - 表示该字段的说明, 描述可能的值, 如果是枚举类型则需要列出所有可能的值, 如果有默认值还需要描述默认值


  如上述表格中定义的Agent的JSON结果如下
  ```json
  {
    "id": 1,
    "name": "allon",  
    "status": "online",
    "departments": [
      1,
      2
    ],
    "permissions": {
      "acceptChat": true,
      "monitorChat": true
    },
    "preference": {
      "isEnableAutoTranslation": true,
      "autoTranslationLanguage": "en",
    }
  }
  ```

## 确定具体资源的所有接口方法


按照资源区分, 针对每个资源的所有操作需要列出, 确定Http Method, 以及资源的url, 如针对Campaign可以有如下接口:

  + Endpoint
    - `GET api/v2/livechat/campaigns` - 获取Campaign列表
    - `GET api/v2/livechat/campaigns/{id}` - 获取单个Campaign的信息
    - `POST api/v2/livechat/campaigns` - 创建一个新的Campaign
    - `PUT api/v2/livechat/campaigns` - 修改一个Campaign
    - `DELETE api/v2/livechat/campaigns/{id}` - 删除一个Campaign

### HTTP Method的使用规则

#### HEAD
  
  在实际使用中, 会使用到唯一性检查, 采用HEAD操作来获取, 返回404就表示不存在, 否则就是存在的, 如果存在可以返回200, 顺便带上这个资源的endpoint

  - 如判断名字为`LiveChat`的Department是否存在
  
    `HEAD api/v2/livechat/departments/names/LiveChat`

#### GET
1. 获取批量的数据, 采用GET方法获取, 参数通过queryString传递
  
  - 如获取5月份的聊天数据: `GET api/v2/livechat/chats?timeFrom=2018-05-01&timeEnd=2018-05-31`

2. 获取单个资源, 采用GET方式获取, 一般使用id定位资源
  
  - 如获取id为1的聊天数据: `GET api/v2/livechat/chats/1`

3. 获取资源下面的子资源, 采用GET方式, 使用id及子资源的名称来定位资源

  - 如获取id为1的campaign下面的prechat信息: `GET api/v2/livechat/campaigns/1/prechat`

  - 如获取id为1的category下面的canned messages: `GET api/v2/livechat/categories/1/cannedMessages`

    注: 针对这种存在层次关系的可以同时提供两种API, 一种为下面采用query的方式, 一种为上面描述的层级关系

      `GET api/v2/livechat/cannedMessages?categoryId=1`

#### POST 
1. 创建新的资源, 采用POST方式新增资源, 参数通过JSON格式传递, 结构中描述的Mandatory为yes的属性必须有值, Read-Only的属性则不需要传
  
  - 如新增一个Campaign: `POST api/v2/livechat/campaigns`

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


#### PUT

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

  `PUST api/v2/account/agents/allon.lu@comm100.com`

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

#### DELETE

  当需要删除一个资源时, 使用DELETE方法

  如删除id为1的Campaign:
  `DELETE api/v2/livechat/campaigns/1`

#### PATCH
  
  当需要部分更新一个资源时, 使用PATCH方法, 参数为需要更新的对象中的部分属性组成的JSON格式
  
  如只需要更新id为1的Campaign的语言为中文: 
  `PUT api/v2/livechat/campaigns/{id}`
  ```json
  {
    "language": "zh",
  }
  ```

## 详细描述请求的输入输出，身份权限

  针对所有的接口都需要详细描述输入输出, 一般情况下输入输出都为上面定义的资源的JSON结构, 而针对其他情况则要另外说明具体的输入输出的参数, 以下内容也可以用列表的形式来说明, 如按照查询条件获取聊天, 结果分页返回:

  `GET api/v2/livechat/chats` 

  + Allowed For:
    - Agents with Permission `View Chats`
    - Admins
  
  + Request Parameters:
    - `dateFrom` - `optional`, defaults to today, (format: `yyyy-MM-dd`), the beginning of the query date
    - `dateTo` -  `optional`, default to today. (format: `yyyy-MM-dd`), the end of query date
    - `timeZone` - `optional`, default to UTC. (format: `±hh:mm` [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)), timezone of the query time
    - `pageSize` - `optional`, default to 10, page size of the paging
    - `pageIndex` - `optional`, default to 0, page index of the paging

  + Response:
    - `previousPage` - `string`, url of previous page, `null` indicates that currently on the first page
    - `nextPage` - `string`, url of next page, `null` indicates that currently on last last page
    - `total` - `number`, number of records
    - `chats` - `chat[]`, [chat](#chat) record of current page

---

  + 说明
    - Allowed For: 每一个操作需要说明权限, 即拥有什么样的角色/权限才能执行这个操作

    - Request Parameters, GET请求的参数都是通过QueryString传递, 这些参数需要包含以下内容
      - 参数的类型
      - 是否必须
      - 非必须的话默认值是什么
      - 可接受值的格式或范围, 如果是枚举则要列出所有的枚举类型
    
    - Response: 如果是简单的一个对象则只要描述是什么对象即可, 如果是特定的复杂结构则可以在这里单独描述, 同样需要说明每个属性的含义和类型
