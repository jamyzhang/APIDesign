# Site Status
Site status refers to the status of your chat button. There are two types of status for your site: online and offline.

### Path
```bash
GET https://hosted.comm100.com/api/v1/livechat/site_status
```

### Response
| Name | Description
| --- | ---
| `status`| the status of the site, `online`, `offline`

### Example
Sample request:
```bash
curl "https://hosted.comm100.com/api/v1/livechat/site_status" \
    -X GET –u tester@comm100.com:ef43f9362aac4f60ad428cb4d072f2c8
```

Sample response:
```json
{
    "status": "online"
}
```
