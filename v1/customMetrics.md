# Custom Metrics
Gets a full list of your custom metrics. Only agents with **"Manage Dashboard Custom Metrics"** permission have access to this resource. Custom Metrics is available in **Enterprise** edition.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/customMetrics
```

### Response
Returns the configurations of a list of custom metrics. Each item contains:

| Property | Description
| --- | ---
| `id` | the id of the custom metric
| `name` | the name of the custom metric
| `description` | the description of the custom metric
| `expression` | the expression of the custom metric, determine how the metric is calculated
| `isEnable` | whether the custom metric is enabled

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/customMetrics" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 1,
        "name": "Chats in Sales",
        "description": "Query the total number of chats which the department is \"Sales\"",
        "expression": "Compute(\"count({!Prechat.Department})\",\"{!Prechat.Department}='Sales'\")",
        "isEnable": true,
    },
    {
        "id": 2,
        "name": "Non-Junk Chat",
        "description": "Query the portion of chats where wrap-up field Category is not \"Junk\"",
        "expression": "Compute(\"count({!Wrapup.Priority})\",\"{!Wrapup.Priority}<>'Junk'\")/Compute(\"count({!Wrapup.Category})\",\"true\")",
        "isEnable": true,            
    }
]
```
