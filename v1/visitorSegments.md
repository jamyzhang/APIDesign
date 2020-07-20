# Visitor Segments
Gets a full list of your [visitor segments](https://www.comm100.com/blog/visitor-segmentation.html) with some basic data. Only agents with **"Manage Settings"** permission have access to this resource.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/visitorSegments
```

### Response
Returns a list of visitor segments. Each item contains:

| Property | Description
| --- | ---
| `id` | the id of the visitor segment
| `name` | the name of the visitor segment
| `color` | the color of the block shown in Agent Console when the visitor falls into the segment based on pre-defined rules 
| `isEnable`| whether the visitor segment is enabled or not 

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/visitorSegments" \
    -X GET -u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
[
    {
        "id": 1,
        "name": "Chatted before",
        "color": "#329fd9",
        "isEnable": true,
    },
    {
        "id": 2,
        "name": "Visit Times more than 5",
        "color": "#329fd9",
        "isEnable": true,
    }
]
```
