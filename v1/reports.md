# Reports
Comm100 Live Chat Report API allows you to pull the raw reporting data from Comm100 Live Chat into your own systems, so you can create custom and on-demand reports in Excel or your business intelligence platform.

## Reports in Business & Enterprise Editions
Below is a quick glance at what reports are available in the Business and Enterprise edition of Comm100 Live Chat. If a report is not available, status code `403` will return when you call the corresponding API.

| Report | Enterprise | Business 
| --- | --- | --- 
| Chat Volume | Yes | Yes 
| Visits (Metrics of this report are derived from Chat Volume Report) | Yes | Yes 
| Availability | Yes | Yes 
| Agent Status | Yes | Yes 
| Agent Performance | Metrics in this reports are available either in Workload or Efficiency report. | Yes 
| Rating | Yes | Yes
| Post Chat Survey | Yes | Yes
| Pre-Chat Survey | Yes | Yes
| Wrap-up | Yes | Yes
| Offline Message | Yes | Yes
| Canned Message | Yes | Yes
| Real Time – Right Now | Yes | Yes
| Real Time – Today | Yes | Yes
| Real Time – Agents | Yes | Yes
| Chat Source | Yes | No
| Queue | Yes | No
| Wait Time | Yes | No
| Chat Transfer | Yes | No
| Workload | Yes | No
| Efficiency | Yes | No
| Conversions | Yes | No
| Manual Invitation | Yes | No
| Auto Invitation | Yes | No
| Real Time – Queue | Yes | No
| Real Time – Custom Metrics | Yes | No

## Available Paths
  | Methods | Name | Path
  | --- | --- | ---
  | GET | [Chat volume](#chat-volume) | /api/v1/livechat/reports/chatVolume
  | GET | [Visits](#visits) | /api/v1/livechat/reports/visits
  | GET | [Chat Source](#chat-source) | /api/v1/livechat/reports/chatSource<br />/api/v1/livechat/reports/chatSourceRequestPage
  | GET | [Queue](#queue) | /api/v1/livechat/reports/queue
  | GET | [Wait Time](#wait-time) | /api/v1/livechat/reports/waitTime
  | GET | [Chat Transfer](#chat-transfer) | /api/v1/livechat/reports/chatTransfer
  | GET | [Availability](#availability) | /api/v1/livechat/reports/availability
  | GET | [Agent Status](#agent-status) | /api/v1/livechat/reports/agentStatus
  | GET | [Agent Performance](#agent-performance) | /api/v1/livechat/reports/agentPerformance
  | GET | [Workload](#workload) | /api/v1/livechat/reports/workload
  | GET | [Efficiency](#efficiency) | /api/v1/livechat/reports/efficiency
  | GET | [Rating](#rating) | /api/v1/livechat/reports/rating
  | GET | [Post Chat Survey](#post-chat-survey) | /api/v1/livechat/reports/postChatSurvey
  | GET | [Pre-Chat Survey](#pre-chat-survey) | /api/v1/livechat/reports/prechatSurvey
  | GET | [Wrap-up](#wrap-up) | /api/v1/livechat/reports/wrapup/survey<br />/api/v1/livechat/reports/wrapup/completion
  | GET | [Conversions](#conversions) | /api/v1/livechat/reports/conversions
  | GET | [Manual Invitation](#manual-invitation) | /api/v1/livechat/reports/manualInvitation
  | GET | [Auto Invitation](#auto-invitation) | /api/v1/livechat/reports/autoInvitation
  | GET | [Offline Message](#offline-message) | /api/v1/livechat/reports/offlineMessage
  | GET | [Canned Message](#canned-message) | /api/v1/livechat/reports/cannedMessage
  | GET | [Real Time](#real-time) | /api/v1/livechat/reports/realtime/rightNow<br />/api/v1/livechat/reports/realtime/today<br />/api/v1/livechat/reports/realtime/today/customMetrics<br />/api/v1/livechat/reports/realtime/agents<br />/api/v1/livechat/reports/realtime/queue

## Data Format
- Comm100 Report API returns data in [JSON](https://en.wikipedia.org/wiki/JSON) format.
- Data items are returned at different levels of granularity according to the parameters within a specific time period. The detailed properties of each item are listed in every API instruction.
- Time Property in responses:
  - available when `group = hour/day/week/month/24*7Distribution/halfHourDistribution`
  - when `group = day/hour/week/month`, `time` contains `from` and `to`, in format `yyyy-MM-ddTHH:mm:ss`
  - when `group = halfHourDistribution`, `time` contains `from` and `to`, in format `hh:mm`
  - when `group = 24*7Distribution`, `time` contains `from` and `to`, in format `ddd. hh:mm` (`ddd` is abbreviation of the day of the week)
- When `group` is `agent`, `department` or `campaign`, each item in the response will contain `agentId`, `departmentId` or `campaignId` accordingly.
- Only agents with **"View Reports"** permission have access to the report API resources.

## Chat Volume
Shows the chat requests occurring on the website, as well as how many chat requests connected to agents.

### Path
    GET https://hosted.comm100.com/api/v1/livechat/reports/chatVolume

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `campaign`, `department`, `visitorSegment`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`, `departmentId`, `visitorSegmentId`
| `group` | required, `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `campaign`, `department`, `visitorSegment` 

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `chatRequests` | the total number of chat requests initiated on the website
| `chats` | the total number of chat sessions which occurred
| `missedChats` | the total number of chat requests missed by agents
| `refusedChats` | the number of chat requests rejected by agents
| `campaignId` | available when `group = campaign`
| `departmentId` | available when `group = department`
| `visitorSegmentId` | available when `group = visitorSegment`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgChats` | the average number of chat sessions which occurred
| `avgMissedChats` | the average number of chat requests missed by agents
| `avgRefusedChats` | the average number of chat requests rejected by agents
| `avgChatRequests` | the average number of chat requests initiated on the website

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \ 
    "https://hosted.comm100.com/api/v1/livechat/reports/chatVolume? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "chatRequests": 36.0,
        "chats": 30.0,
        "missedChats": 2.0,
        "refusedChats": 4.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "chatRequests": 43.0,
        "chats": 39.0,
        "missedChats": 1.0,
        "refusedChats": 3.0,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
    {
        "chatRequests": 42.0,
        "chats": 37.0,
        "missedChats": 3.0,
        "refusedChats": 2.0,
        "time": {
            "from": "2017-12-31T00:00:00",
            "to": "2018-01-01T00:00:00"
        }            
    }
]
```

## Visits
Shows the visits occurring on the website.

### Path
    GET https://hosted.comm100.com/api/v1/livechat/reports/visits

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `campaign`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `campaign`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `visits` | the number of visits
| `campaignId` | available when `group = campaign`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgVisits` | the average number of visits


### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \ 
    "https://hosted.comm100.com/api/v1/livechat/reports/visits? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00& \
    group=halfHourDistribution"
```

Sample response:
```json
[
    {
        "visits": 231,
        "time": {
            "from": "00:00",
            "to": "00:30"
        }
    },
    {
        "visits": 156,
        "time": {
            "from": "00:30",
            "to": "01:00"
        }
    },
    {
        "visits": 231,
        "time": {
            "from": "01:00",
            "to": "01:30"
        }
    },
    ...        
    {
        "visits": 156,
        "time": {
            "from": "23:30",
            "to": "24:00"
        }
    },
]
```

## Chat Source
Shows the number of chats requested by visitors, initiated by agents manually, and triggered by predefined auto invitation rules respectively.

### Path
    GET https://hosted.comm100.com/api/v1/livechat/reports/chatSource

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `department`
| `filterValue` | work together with `filterName` to filter data, namely `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `department`

### Response
| Property | Description
| --- | --
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `chats` | the number of chat sessions which occurred
| `chatsInitialtedByVisitors` | the total number of answered chats initiated by visitors
| `chatsFromManualInvitations` | the total number of chats initiated by agents' manual invitations and accepted by visitors
| `chatsFromAutoInvitations` | the total number of chats initiated by rule-based auto invitations and accepted by visitors
| `departmentId` | available when `group = department`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgChats` | the average number of answered chats initiated by visitors
| `avgChatsInitialtedByVisitors` | the average number of answered chats initiated by visitors
| `avgChatsFromManualInvitations` | the average number of chats initiated by agents' manual invitations and accepted by visitors
| `avgChatsFromAutoInvitations` | the average number of chats initiated by rule-based auto invitations and accepted by visitors

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/chatSource? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00& \
    group=24*7Distribution"
```

Sample response:
```json
[
    {
        "avgChats": 2.6,
        "avgChatsInitialtedByVisitors": 2.6,
        "avgChatsFromManualInvitations": 0.0,
        "avgChatsFromAutoInvitations": 0.0,
        "time": {
            "from": "Sun. 00:00",
            "to": "Sun. 01:00"
        }
    },
    {
        "avgChats": 3.5,
        "avgChatsInitialtedByVisitors": 2.34,
        "avgChatsFromManualInvitations": 1.16,
        "avgChatsFromAutoInvitations": 0.0,
        "time": {
            "from": "Sun. 01:00",
            "to": "Sun. 02:00"
        }
    },
    ...
    {
        "avgChats": 3.8,
        "avgChatsInitialtedByVisitors": 2.66,
        "avgChatsFromManualInvitations": 1.08,
        "avgChatsFromAutoInvitations": 0.16,
        "time": {
            "from": "Sun. 22:00",
            "to": "Sun. 23:00"
        }
    },
    {
        "avgChats": 3.8,
        "avgChatsInitialtedByVisitors": 1.23,
        "avgChatsFromManualInvitations": 1.57,
        "avgChatsFromAutoInvitations": 1.0,
        "time": {
            "from": "Sat. 23:00",
            "to": "Sat. 24:00"
        }
    }
]
```

## Chat Source Request Page
Shows the distribution of chats among your webpages.

### Path
    GET https://hosted.comm100.com/api/v1/livechat/reports/chatSource/requestPage

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | `yyyy-MM-ddTHH:mm:ss`, required, the beginning of query time
| `timeTo` | `yyyy-MM-ddTHH:mm:ss`, required, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time

### Response
| Property | Description
| --- | ---
| `requestPage` | the URL of a page where a chat request was initiated
| `chats` | the number of chat sessions which occurred on a specific page

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/chatSource/requestPage? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00"
```

Sample response:
```json
[
    {
        "chats": 53,
        "requestPage": "https://www.comm100.com/livechat/pricing.aspx" 
    },
    {
        "chats": 18,
        "requestPage": "https://www.comm100.com/livechat/enterprise.aspx"
    },
    ...
]
```

## Queue
Shows the details of the queue length and visitors' actions in the queue within a specific time range.
Chats can be routed to one agent, or multiple agents in a department. When agents or departments are handling their maximum number of chats, any new chats will enter a queue. The queue report shows all queue data in this scenario.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/queue
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `department`
| `filterValue` | work together with `filterName` to filter data, namely `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `department`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `queuedChatRequests` | the number of chat requests that waited in the queue before they were connected to agents, abandoned or switched to offline message
| `chatsFromQueue` | the number of chat requests which waited in the queue but later got connected to agents
| `switchedToMessages` | the number of chat requests which were switched to offline messages by visitors
| `abandonedChats` | the number of chat requests abandoned by visitors closing the chat window while waiting
| `refusedChats` | the number of chat requests rejected by agents within a defined time range
| `maxQueueSize` | the largest number of chat requests in one queue over a given time range
| `departmentId` | available when `group = department`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgQueuedChatRequests` | the average number of chat requests that waited in the queue before they were connected to agents, abandoned or switched to offline message
| `avgChatsFromQueue` | the average number of chat requests which waited in the queue but later got connected to agents
| `avgSwitchedToMessages` | the average number of chat requests which were switched to offline messages by visitors
| `avgAbandonedChats` | the average number of chat requests abandoned by visitors closing the chat window while waiting
| `avgRefusedChats` | the average number of chat requests rejected by agents within a defined time range
| `avgMmaxQueueSize` | the average largest number of chat requests in one queue over a given time range

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/queue? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "queuedChatRequests": 53,
        "chatsFromQueue": 25,
        "switchedToMessages": 3,
        "abandonedChats": 2,
        "refusedChats": 0,
        "maxQueueSize": 5,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        } 
    },
    {
        "queuedChatRequests": 46,
        "chatsFromQueue": 20,
        "switchedToMessages": 0,
        "abandonedChats": 0,
        "refusedChats": 0,
        "maxQueueSize": 5,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
]
```

## Wait Time
Shows more in-depth information on wait time in the queue.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/waitTime
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `department`
| `filterValue` | work together with `filterName` to filter data, namely `departmentId`
| `group` | required, `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `department`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `avgWaitTime` | the average time visitors waited in the queue before they were answered by agents, abandoned the queue, or switched to leaving a message
| `avgWaitTimeOfMissedChats` | the average time visitors waited in the queue before they abandoned the queue or switched to leaving a message
| `maxWaitTime` | the longest time length visitors waited in the queue before they were answered by agents, abandoned the queue, or switched to leaving a message
| `maxWaitTimeOfMissedChats` | the longest time length visitors waited in the queue before they abandoned the queue or switched to leaving a message
| `departmentId` | available when `group = department`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgWaitTime` | the average time visitors waited in the queue before they were answered by agents, abandoned the queue, or switched to leaving a message
| `avgWaitTimeOfMissedChats` | the average time visitors waited in the queue before they abandoned the queue or switched to leaving a message
| `avgMaxWaitTime` | the average longest time length visitors waited in the queue before they were answered by agents, abandoned the queue, or switched to leaving a message
| `avgMaxWaitTimeOfMissedChats` | the average longest time length visitors waited in the queue before they abandoned the queue or switched to leaving a message

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/waitTime? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "avgWaitTime": 0,
        "avgWaitTimeOfMissedChats": 0,
        "maxWaitTime": 0.0,
        "maxWaitTimeOfMissedChats": 0.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "avgWaitTime": 0,
        "avgWaitTimeOfMissedChats": 0,
        "maxWaitTime": 0.0,
        "maxWaitTimeOfMissedChats": 0.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    ...
]
```


## Chat Transfer
Shows how many chats were being transferred to another agent or department within a specific period of time.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/chatTransfer
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `department`
| `filterValue` | work together with `filterName` to filter data, namely `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `department`

### Response
When `group = depratment`, each data item in response list will contain the following properties:

| Property | Description
| --- | ---
| `departmentId` | the id of the department
| `departmentTransferredInChats` | the number of chat sessions transferred to the department
| `departmentTransferredOutChats` | the number of chat sessions transferred out from the department
| `chats` | total number of chats


Otherwise, the structure of each data item is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `chats` | the number of chat sessions which occurred
| `totalTransferredChats` | the number of chat sessions during which chat transfers between agents or departments took place
| `departmentTransferredChats` | the number of chat sessions during which chat transfers between departments took place


### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/chatTransfer? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=departmemt"
```

Sample response:
```json
[
    {
        "departmentTransferredInChats": 4.0,
        "departmentTransferredOutChats": 2.0,
        "chats": 10.0,
        "departmentId": 1
    },
    {
        "departmentTransferredInChats": 3.0,
        "departmentTransferredOutChats": 4.0,
        "chats": 8.0,
        "departmentId": 2
    }
]
```

## Availability
Shows data regarding the online time of your live chat team or a specific department within a specific time period.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/availability
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`, `department`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `agent`, `department`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`
| `online` | the length of time that an agent/a department/the live chat team is online and accessible
| `departmentId` | available when `group = department`
| `agentId` | available when `group = agent`
| `statusDistribution` | available when `group = agent` or `filterName = agent`, a list of the online status distrubution, including the sum of online time and away time

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/availability? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=agent"
```

Sample response:
```json
[
    {
        "online": 2678400.0,
        "agentId": 1,
        "statusDistribution": [
            {
                "status": "Logged-in",
                "time": 2678400.0
            },
            {
                "status": "Online",
                "time": 2678400.0
            },
            {
                "status": "Total Away",
                "time": 0.0
            }
        ]
    },
    {
        "online": 2678400.0,
        "agentId": 2,
        "statusDistribution": [
            {
                "status": "Logged-in",
                "time": 2678400.0
            },
            {
                "status": "Online",
                "time": 1296000.0
            },
            {
                "status": "Total Away",
                "time": 1382400.0
            }
        ]
    },
    ...
]
```

## Agent Status
Shows details on agent status change log within a defined time range.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/agentStatus
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`, `department`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `agentId` | the id of the agent
| `changeLogs` | a list of every agent status change log, each item has two properties, `time` is the moment when the agent status change happens, `status` is the status to which the agent changes

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/agentStatus? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00"
```

Sample response:
```json
[
    {
        "agentId": 1,
        "changeLogs": [
            {
                "time": "2017-12-01T00:00:00",
                "name": "Online"
            },
            {
                "time": "2017-12-01T18:00:00",
                "name": "Offline"
            },
            ...
            {
                "time": "2017-12-31T18:00:00",
                "name": "Offline"
            }
        ]
    },
    {
        "agentId": 2,
        "changeLogs": [
            {
                "time": "2017-12-01T00:00:00",
                "name": "Offline"
            }
        ]
    }
]
```

## Agent Performance
Shows overall performance of agents.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/agentPerformance
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`, `department`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `agent`, `department`

### Response
| Property | Description
| --- | --
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`
| `avgChatTime` | the average time it took an agent to finish a chat
| `avgWaitTime` | the average time visitors waited before they were answered by agents, abandoned the queue, or switched to leaving a message
| `totalChatTime` | the sum of the length of all chats, viewable by agent, department, or the live chat team as a whole
| `lastMessageSentByAgent` | the number of chats where the last chat message is sent by Agent
| `agentId` | available when `group = agent`
| `departmentId` | available when `group = deparment`


### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/agentPerformance? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "avgChatTime": 736.0,
        "avgWaitTime": 1383.0,
        "totalChatTime": 18332.0,
        "lastMessageSentByAgent": 6.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "avgChatTime": 684,
        "avgWaitTime": 1080.0,
        "totalChatTime": 16530.0,
        "lastMessageSentByAgent": 3.0,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
    {
        "avgChatTime": 562.0,
        "avgWaitTime": 935.0,
        "totalChatTime": 14635.0,
        "lastMessageSentByAgent": 4.0,
        "time": {
            "from": "2017-12-31T00:00:00",
            "to": "2018-01-01T00:00:00"
        }
    }
]
```

## Workload
Shows utilization through comparing time on chats with idle time.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/workload
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`, `department`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `department`, `agent`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `linearChatTime` | the length of time when agents were involved in chatting during their logged-in time
| `idleTime` | the length of time when there was no chat occurring
| `agentUtilization` | the percentage of time agents were involved in chats during their logged-in time
| `avgConcurrentChats` | the average number of chats agents handled at the same time
| `totalChatTime` | the sum of the length of all chats
| `chats` | the number of chat sessions which occurred
| `agentId` | available when `group = agent`
| `departmentId` | available when `group = department`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgLinearChatTime` | the average time when agents were involved in chatting during their logged-in time
| `avgIdleTime` | the average time when there was no chat occurring
| `avgAgentUtilization` | the average percentage of time agents were involved in chats during their logged-in time
| `avgConcurrentChats` | the average number of chats agents handled at the same time
| `avgTotalChatTime` | the average sum of the length of all chats
| `avgChats` | the average number of chat sessions which occurred

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/workload? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "linearChatTime": 76.0,
        "idleTime": 8632.0,
        "agentUtilization": 0.16,
        "avgConcurrentChats": 0.17,
        "totalChatTime": 14392.0,
        "chats": 4.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "linearChatTime": 1287.0,
        "idleTime": 85113.0,
        "agentUtilization": 0.24,
        "avgConcurrentChats": 0.24,
        "totalChatTime": 20710,
        "chats": 2.0,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
]
```

## Efficiency
Shows the average response time, wait time and chat time of each agent, department, and the whole live chat team.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/efficiency
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`, `department`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `department`, `agent`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `avgAgentResponseTime` | the average amount of time an agent took to respond to a message from visitors
| `avgWaitTime` | the average time visitors waited before they were answered by agents, abandoned the queue, or switched to leaving a message
| `avgChatTime` | the average time it took an agent to finish a chat
| `avgAgentsChatMessages` | the average number of messages sent by agents during a chat session
| `avgVisitorsChatMessages` | the average number of messages sent by visitors during a chat session
| `avgCannedMessages` | the average number of canned messages sent by agents during a chat session
| `lastMessageSentByAgent` | the total number of chats where the last chat message is sent by Agent
| `agentId` | available when `group = agent`
| `departmentId` | available when `group = department`

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/efficiency? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "avgAgentResponseTime": 977.0,
        "avgWaitTime": 16.0,
        "avgChatTime": 4078.0,
        "avgAgentsChatMessages": 18.0,
        "avgVisitorsChatMessages": 12.0,
        "avgCannedMessages": 2.0,
        "lastMessageSentByAgent": 3.0, 
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "avgAgentResponseTime": 458.0,
        "avgWaitTime": 22.0,
        "avgChatTime": 4680.0,
        "avgAgentsChatMessages": 22.0,
        "avgVisitorsChatMessages": 16.0,
        "avgCannedMessages": 1.0,
        "lastMessageSentByAgent": 2.0,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
    {
        "avgAgentResponseTime": 685.0,
        "avgWaitTime": 13.8,
        "avgChatTime": 3672.0,
        "avgAgentsChatMessages": 17.0,
        "avgVisitorsChatMessages": 13.5,
        "avgCannedMessages": 2.0,
        "lastMessageSentByAgent": 3.0, 
        "time": {
            "from": "2017-12-31T00:00:00",
            "to": "2018-01-01T00:00:00"
        }
    }
]
```

## Rating
Shows details of visitors' rating on the chat performance of an agent, a department, and the live chat team as a whole within a defined time range.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/rating
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`, `department` 
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `agent`, `department`

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `score5` | the number of chats under score 5
| `score4` | the number of chats under score 4
| `score3` | the number of chats under score 3
| `score2` | the number of chats under score 2
| `score1` | the number of chats under score 1
| `agentId` | available when `group = agent`
| `departmentId` | available when `group = department`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgScore5` | the average number of chats under score 5
| `avgScore4` | the average number of chats under score 4
| `avgScore3` | the average number of chats under score 3
| `avgScore2` | the average number of chats under score 2
| `avgScore1` | the average number of chats under score 1

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/rating? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=agent"
```

Sample response:
```json
[
    {
        "score5": 15.0,
        "score4": 6.0,
        "score3": 4.0,
        "score2": 2.0,
        "score1": 0.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "score5": 14.0,
        "score4": 8.0,
        "score3": 7.0,
        "score2": 3.0,
        "score1": 1.0,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
    {
        "score5": 17.0,
        "score4": 8.0,
        "score3": 6.0,
        "score2": 3.0,
        "score1": 1.0,
        "time": {
            "from": "2017-12-31T00:00:00",
            "to": "2018-01-01T00:00:00"
        }
    }
]
```

## Post Chat Survey
Shows the statistics on survey questions which allow visitors to select one or more options from a list of defined answers.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/postChatSurvey
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `campaign`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`

### Response
| Property | Description
| --- | ---
| `campaignId` | the id of the campaign
| `fields` | a list of fields for a post-chat survey 

Each item in `field` has the following properties:

| Property | Description
| --- | ---
| `fieldId` | the id of the field
| `fieldName` | the name of the field
| `options` | a list of options of each field, `name` is the display text of each option, `count` is the total times an option has been selected for a post-chat survey

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/postChatSurvey? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00"
```

Sample response:
```json
[
    {
        "campaignId": 1,
        "fields": [
            {
                "fieldId": 1,
                "fieldName": "This is a check box.",
                "options": [
                    {
                        "name": "false",
                        "count": 3
                    },
                    {
                        "name": "true",
                        "count": 5
                    }
                ]
            },
            {
                "fieldId": 2,
                "fieldName": "This is a check box.",
                "options": [
                    {
                        "name": "false",
                        "count": 3
                    },
                    {
                        "name": "true",
                        "count": 5
                    }
                ]
            }
        ]
    },
    {
        "campaignId": 2,
        "fields": [
            {
                "fieldId": 3,
                "fieldName": "This is a radio box.",
                "options": [
                    {
                        "name": "Option I.",
                        "count": 6
                    },
                    {
                        "name": "Option II.",
                        "count": 5
                    }
                ]
            }
        ]
    }
]
```

## Pre-Chat Survey
Shows the statistics on survey questions which allow visitors to select one or more options from a list of defined answers.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/prechatSurvey
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time 
| `filterName` | optional, `campaign`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`

### Response
| Property | Description
| --- | --
| `campaignId` | the id of the campaign
| `fields` | a list of fields containing detailed 

Each item in `field` has the following properties:

| Property | Description
| --- | ---
| `fieldId` | the id of the field
| `fieldName` | the name of the field
| `options` | a list of options of each field, `name` is the display text of each option, `count` is the total times an option has been selected for a pre-chat survey question

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/prechatSurvey? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00& \
    filterName=campaign&filterValue=1"
```
    
Sample response:
```json
[
    {
        "campaignId": 1,
        "fields": [
            {
                "fieldId": 1,
                "fieldName": "This is a check box.",
                "options": [
                    {
                        "name": "true",
                        "count": 16
                    },
                    {
                        "name": "false",
                        "count": 3
                    }
                ]
            },
            {
                "fieldId": 2,
                "fieldName": "This is a drop down list.",
                "options": [
                    {
                        "name": "Option A.",
                        "count": 7
                    },
                    {
                        "name": "Option B.",
                        "count": 3
                    },
                    {
                        "name": "Option C.",
                        "count": 6
                    }
                ]
            }
        ]
    }
]
```

## Wrap-up
Shows details of the categorization of your chats via the wrap-up survey.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/wrapup/survey
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time 
| `filterName` | optional, `campaign`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`

### Response
| Property | Description
| --- | ---
| `campaignId` | the id of the campaign
| `fields` | a list of fields containing detailed 


Each item in `field` has the following properties:


| Property | Description
| --- | ---
| `fieldId` | the id of the field
| `fieldName` | the name of the field
| `options` | a list of options of each field, `name` is the display text of each option, `count` is the total times an option has been selected for a wrap-up survey


For the **category** field of wrap-up, if the advanced mode is turned on, the structure will be different:


| Property | Description
| --- | ---
| `fieldId` | the id of the field
| `fieldName` | the name of the field
| `groups` | a list of option groups of **category** field, `name` is the display text of the group name and `options` contains the sub options


### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/wrapup/survey? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00"
```

Sample response:
```json
[
    {
        "campaignId": 1,
        "fields": [
            {
                "fieldId": 105,
                "fieldName": "Category",
                "groups": [
                    {
                        "name": "Product",
                        "options": [
                            {
                                "name": "Live Chat",
                                "count": 4,
                            },
                            {
                                "name": "Ticket",
                                "count": 2,
                            }
                        ]
                    }
                ]
            },
            {
                "fieldId": 106,
                "fieldName": "This is a drop down list.",
                "options": [
                    {
                        "name": "A.",
                        "count": 7
                    },
                    {
                        "name": "B.",
                        "count": 3
                    }
                ]
            }
        ]
    }
]
```

## Wrap-up Completion
Shows the proportion of chats where agents' wrap-up comments are completed.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/wrapup/completion
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time 
| `filterName` | optional, `agent`, `department`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`, `departmentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `agent`, `department`

### Response
| Property | Description
| --- | --- |
| `time` | `{from: ..., to: ...}`, each time period |
| `wrapups` | the number of the chats that had wrap-up comments
| `chats` | the number of chat sessions established between agents and visitors
| `agentId` | available when `group = agent`
| `departmentId` | available when `group = department`

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/wrapup/completion? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "wrapups": 25.0,
        "chats": 28.0,
        "time": {
            "from": "2017-12-01T00:00:00",
            "to": "2017-12-02T00:00:00"
        }
    },
    {
        "wrapups": 28.0,
        "chats": 33.0,
        "time": {
            "from": "2017-12-02T00:00:00",
            "to": "2017-12-03T00:00:00"
        }
    },
    ...
    {
        "wrapups": 18.0,
        "chats": 30.0,
        "time": {
            "from": "2017-12-31T00:00:00",
            "to": "2018-01-01T00:00:00"
        }
    }
]
```

## Conversions
Shows all achieved conversions, total conversion value, and your live chat conversion rate. Knowing how your live chat contributes to conversions helps you better understand your live chat ROI, and make more informed decisions about your chat performance. [Learn more about Conversions](https://www.comm100.com/livechat/features/conversions.aspx)

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/conversions
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `department`, `agent`, `conversion`
| `filterValue` | work together with `filterName` to filter data, namely `departmentId`, `agentId`, `conversion`
| `group` | required,  `hour`, `day`, `week`, `month`, `department`, `agent`, `conversionAction`

### Response
| Parameter | Description
| --- | ---
| `conversions` | the number of achieved conversions
| `chats` | the number of chat sessions which have occurred
| `chattedVisitors` | the number of chatted visitors – who chatted on your website
| `convertedVisitors` | the number of converted visitors – who took the conversion actions you've defined
| `convertedChattedVisitors` | the number of converted chatted visitors – who chatted on your website, and in the meanwhile, took the conversion actions you've defined
| `value` | the total value of all achieved conversions

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/conversions? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=day"
```

Sample response:
```json
[
    {
        "conversions": 6.0,
        "chats": 2.0,
        "chattedVisitors": 1,
        "convertedVisitors": 0,
        "convertedChattedVisitors": 0,
        "value": 0.0
    },
    {
        "conversions": 3.0,
        "chats": 3.0,
        "chattedVisitors": 2,
        "convertedVisitors": 1,
        "convertedChattedVisitors": 0,
        "value": 50.0
    },
    ...
    {
        "conversions": 5.0,
        "chats": 2.0,
        "chattedVisitors": 1,
        "convertedVisitors": 1,
        "convertedChattedVisitors": 1,
        "value": 150.0
    }
]
```

## Manual Invitation
Shows the number of invitations sent by agents manually within a specific period of time.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/manualInvitation
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `agent`
| `filterValue` | work together with `filterName` to filter data, namely `agentId`
| `group` | required,  `hour`, `day`, `week`, `month`, `agent` 

### Response
| Property | Description
| --- | --- |
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`
| `sent` | the number of invitations manually sent by agents
| `accepted` | the number of manual invitations accepted by visitors
| `agentId` | available when `group = agent`

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/manualInvitation? \
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=agent"
```

Sample response:
```json
[
    {
        "sent": 6.0,
        "accepted": 2.0,
        "agentId": 1
    },
    {
        "sent": 5.0,
        "accepted": 2.0,
        "agentId": 2
    },
    ...
    {
        "sent": 6.0,
        "accepted": 3.0,
        "agentId": 6
    }
]
```

## Auto Invitation
Shows the number of invitations triggered by predefined rules as well as the number of invitations accepted within a specific period of time.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/autoInvitation
```

### Parameters
| Parameter | Description 
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `campaign`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`
| `group` | required,  `hour`, `day`, `week`, `month`, `campaign`, `autoInvitation` 

### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`
| `sent` | the number of auto invitations sent to visitors
| `accepted` | the number of auto invitations accepted by visitors
| `campaignId` | available when `group = campaign` or `group = autoInvitation`
| `autoInvitationId` | available when `group = autoInvitation`

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/autoInvitation? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=autoInvitation"
```

Sample response:
```json
[
    {
        "sent": 13.0,
        "accepted": 9.0,
        "autoInvitationId": 1,
        "campaignId": 1
    },
    {
        "sent": 5.0,
        "accepted": 2.0,
        "autoInvitationId": 2,
        "campaignId": 1
    },
    ...
    {
        "sent": 6.0,
        "accepted": 0.0,
        "autoInvitationId": 5,
        "campaignId": 1
    }
]
```

## Offline Message
Shows the number of messages received from the queue and from the offline message button.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/offlineMessage
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time 
| `filterName` | optional, `department`, `campaign`, `visitorSegment`
| `filterValue` | work together with `filterName` to filter data, namely `campaignId`
| `group` | required,  `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`, `department`, `campaign`, `visitorSegment`


### Response
| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period, available when `group` is `hour`, `day`, `week`, `month`, `24*7Distribution`, `halfHourDistribution`
| `messages` | the number of offline messages left by visitors
| `fromOfflineButton` | the number of offline messages left by visitors when agents are offline
| `fromChatQueue` | the number of offline messages left by visitors when they are waiting in queue
| `departmentId` | available when `group = department`
| `campaignId` | available when `group = campaign`
| `visitorSegmentId` | available when `group = visitorSegment`


If parameter `group` is `24*7Distribution` or `halfHourDistribution`, the data item in the response list is as follows:


| Property | Description
| --- | ---
| `time` | `{from: ..., to: ...}`, each time period
| `avgMessages` | the average number of offline messages left by visitors
| `avgFromOfflineButton` | the average number of offline messages left by visitors when agents are offline
| `avgFromChatQueue` | the average number of offline messages left by visitors when they are waiting in queue

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/offlineMessage? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00&group=campaign"
```

Sample response:
```json
[
    {
        "messages": 6.0,
        "fromOfflineButton": 4.0,
        "fromChatQueue": 2.0,
        "campaignId": 1
    },
    {
        "messages": 1.0,
        "fromOfflineButton": 0.0,
        "fromChatQueue": 1.0,
        "campaignId": 2
    },
    ...,
    {
        "messages": 0.0,
        "fromOfflineButton": 0.0,
        "fromChatQueue": 0.0,
        "campaignId": 6
    }
]
```

## Canned Message
Shows how many times and by how many agents each canned message was used within a defined time range.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/cannedMessage
```

### Parameters
| Parameter | Description
| --- | ---
| `timeFrom` | required, `yyyy-MM-ddTHH:mm:ss`, the beginning of query time
| `timeTo` | required, `yyyy-MM-ddTHH:mm:ss`, the end of query time (not included)
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time 
| `filterName` | optional, `category`
| `filterValue` | work together with `filterName` to filter data, namely `categoryId`

### Response
| Property | Description
| --- | ---
| `id` | the id of the canned message
| `usedTimes` | the times a canned message was used within a defined time range
| `agentsUsedIt` | the number of agents a canned message was used by within a defined time range

### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/cannedMessage? \ 
    timeFrom=2017-12-01T00:00:00&timeTo=2018-01-01T00:00:00&timezone=+08:00"
```

Sample response:
```json
[
    {
        "id": 1,
        "usedTimes": 32,
        "agentsUsedIt": 5
    },
    {
        "id": 2,
        "usedTimes": 16,
        "agentsUsedIt": 3
    },
    ...,
    {
        "id": 5,
        "usedTimes": 25,
        "agentsUsedIt": 5
    }
]
```

## Real Time
Gives an at-a-glance view of the chats and visits on a Website, performance of Agents and the visitors and wait time in the Queue.

### Real Time – Right Now
Shows the current number of chats, visits, available agents, queue length, etc.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/realtime/rightnow
```

#### Response
| Property | Description
| --- | ---
| `agentsInChat` | the number of agents who are chatting with customers
| `ongoingChats` | the number of chats currently occurring
| `visitorsOnSite` | the number of visitors currently on the website
| `loggedInAgents` | the number of agents who are logged in
| `currentQueueLength` | the number of visitors waiting in the queue, available when auto-allocation is enabled
| `chatUtilization` | the percentage of total ongoing chats (of all online agents) to the sum of maximum concurrent chats of all online agents, available when auto-allocation is enabled
| `ongoingChatsWithAgents` | available when the Chatbot add-on feature is purchased, the total number of chats currently occurring between visitors and agents
| `ongoingChatsWithChatbot` | available when the Chatbot add-on feature is purchased, the total number of chats currently occurring between visitors and Chatbot

#### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \ 
    "https://hosted.comm100.com/api/v1/livechat/reports/rightnow"
```

Sample response:
```json
{
    "agentsInChat": 2,
    "ongoingChats": 2,
    "visitorsOnSite": 16,
    "loggedInAgents": 3,
    "currentQueueLength": 0,
    "chatUtilization": 0.22,
    "ongoingChatsWithAgents": 6,
    "ongoingChatsWithChatbot": 0
}
```

### Real Time – Today
Shows the data of the current day so far.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/realtime/today
```

#### Parameters
| Property | Description
| --- | ---
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time |

#### Response
| Name | Detail | Description
| --- | --- | ---
| `chatOverview` | `chatRequests`, `chats`, `chatAcceptanceRate`, `abandonedChats`, `switchToMessages`, `missedChats` | an overview of how many chats have been requested, answered, missed, abandoned or switched to offline messages
| `serviceEfficiency` | `avgWaitTime`, `avgChatTime`, `avgResponseTime`, `acceptedInvitations`, `departmentTransferChats`, `totalTransferChats` | an overview of the chat efficiency in the day so far, available in Enterprise edition
| `agentPerformance` | `uniqueChatRate`, `agentUtilization`, `avgScore` | an overview of the average chat performance of agents, available in Enterprise edition
| `chatbot` | `chatbotOnlyChats`, `chatsFromChatbotToAgent`, `answers`, `highConfidenceAnswers` | an overview of your chatbot performance, available when Chatbot is on

### Real Time – Custom Metric
Shows custom live chat performance metrics defined by custom expressions. It's available in Enterprise edition.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/realtime/today/customMetrics
```

#### Parameters
| Property | Description
| --- | ---
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time |

#### Response
The reponse contains a list of data contains:

| Property | Description
| --- | ---
| `id` | the id of the custom metric (you can use `id` to index the detailed configuration of the custom metric, such as `name`, `expression` and so on, through [Custom Metric Settings API])
| `value` | the result of the custom metric


#### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/realtime/today/customMetrics? \
    timezone=+08:00"
```

Sample response:
```json
[
    {
        "id": 1,
        "value": 0.23
    },
    {
        "id": 2,
        "value": 0.88
    },
    ...
]
```

### Real Time – Agents
Shows an overview of each agent's workload in real time and today. It's available in Enterprise edition.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/realtime/agents
```

#### Parameters
| Property | Description
| --- | ---
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time
| `filterName` | optional, `department`
| `filterValue` | work together with `filterName` to filter data, namely `departmentId`

#### Response
The reponse contains a list of agents' data, every item contains:

| Property | Description
| --- | --- |
| `agentId` | the id of the agent
| `currentStatus` | current status of the agent
| `ongoingChats` | the number of chats currently taking place for the agent
| `todayChats` | the number of chats the agent has handled throughout the day
| `todayLinearChatTime` | the total length of time the agent has been involved in at least one chat
| `statusDistribution` | status changes of the agent throughout the day, every item contains `status`(the status name), `time`(the duration of each status)

#### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/realtime/agents? \
    timezone=+08:00&filterName=department&filterValue=1"
```

Sample response:
```json
[
    {
        "agentId": 1,
        "currentStatus": "Online",
        "ongoingChats": 1,
        "todayChats": 3.0,
        "todayLinearChatTime": 356.0,
        "statusDistribution": [
            {
                "status": "Online",
                "time": 7200.0
            },
            {
                "status": "Away",
                "time": 0.0
            },
            {
                "status": "Offline",
                "time": 28800.0
            }
        ]
    },
    {
        "agentId": 2,
        "currentStatus": "Onlin",
        "ongoingChats": 0,
        "todayChats": 2.0,
        "todayLinearChatTime": 285.0,
        "statusDistribution": [
            {
                "status": "Online",
                "time": 7200.0
            },
            {
                "status": "Away",
                "time": 0.0
            },
            {
                "status": "Offline",
                "time": 28800.0
            }
        ]
    },
    ...
]
```

### Real Time – Queue
Shows current queue length and visitors' wait time. Where different routing rules are set up resulting in multiple queues, statistics for each can be viewed.

#### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/reports/realtime/queue
```

#### Parameters
| Property | Description
| --- | ---
| `timezone` | `±hh:mm`, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time 

#### Response
The reponse contains a list of queue related metrics:

| Property | Description
| --- | ---
| `routeTo` | to whom a chat request is routed to, containing `type`, `id`.<br />When `type = 0`, it routes to **Site**, i.e. all agents; when `type = 1`, it routes to **Department**;<br />When `type = 2`, it routes to **Agent**.<br />The id is the specific department or agent.
| `ongoingChats` | the number of ongoing chats
| `avgWaitTimeInLast30Mins` | the average length of time visitors waited in the queue during the last 30 minutes
| `avgWaitTimeInLast60Mins` | the average length of time visitors waited in the queue during the last hour
| `abandonedChatsInLast30Mins` | the number of chat requests abandoned by visitors closing the chat window while they were waiting in the queue during the last 30 minutes
| `switchedToMessagesInLast30Mins` | the number of chat requests that were switched to offline messages by visitors during the last 30 minutes
| `queue` | the list of visitors waiting in the queue, each item contains `visitorId`, `waitTime`(how long the visitor has waited in the queue)

#### Example
Sample request:
```bash
curl -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8 -X GET \
    "https://hosted.comm100.com/api/v1/livechat/reports/realtime/queue?timezone=+08:00"
```

Sample response:
```json
[
    {
        "routeTo": {
            "type": 0
        },
        "ongoingChats": 5,
        "avgWaitTimeInLast30Mins": 12.0,
        "avgWaitTimeInLast60Mins": 15.0,
        "abandonedChatsInLast30Mins": 0.0,
        "switchedToMessagesInLast30Mins": 0.0,
        "queue": [
            {
                "visitorId": 230,
                "waitTime": 50.0
            }
        ]
    },
    {
        "routeTo": {
            "type": 1,
            "id": 1
        },
        "ongoingChats": 3,
        "avgWaitTimeInLast30Mins": 15.0,
        "avgWaitTimeInLast60Mins": 13.0,
        "abandonedChatsInLast30Mins": 0.0,
        "switchedToMessagesInLast30Mins": 0.0,
        "queue": [
            {
                "visitorId": 231,
                "waitTime": 20.0
            }
        ]
    },
    {
        "routeTo": {
            "type": 1,
            "id": 2
        },
        "ongoingChats": 2,
        "avgWaitTimeInLast30Mins": 12.0,
        "avgWaitTimeInLast60Mins": 14.0,
        "abandonedChatsInLast30Mins": 0.0,
        "switchedToMessagesInLast30Mins": 0.0,
        "queue": [
            {
                "visitorId": 232,
                "waitTime": 14.0
            },
            {
                "visitorId": 233,
                "waitTime": 15.0
            }
        ]
    },
    ...
]
```
