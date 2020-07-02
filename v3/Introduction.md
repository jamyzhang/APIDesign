# Introduction

Welcome to the Comm100 RESTful API help guide. Our APIs make it possible for you to integrate your applications with Comm100 Live Chat to achieve seamless data sharing. It is our goal to help the business to automate and enhance their customer support with innovative projects you can create using Comm100 API.

Note: Comm100 currently has two versions of our customer engagement platform.  

- If you started using Comm100 on/after April 26, 2020, or you have migrated to the new platform, this is the latest API version for the platform you are on.  
- If you started using Comm100 before April 26, 2020, you can access API 1.0 [here](https://www.comm100.com/doc/api/v1/introduction.htm#/) or the latest API version 2.0 [here](https://www.comm100.com/doc/api/introduction.htm#/).

## The Basics

Comm100 RESTful API must use **https** protocol. What the API requests should start with depends on your platform domain, which can be accessed from both your Control Panel and web version Agent Console after successful login. For example:

- If the domain of your Control Panel is portal1.comm100.io, all API requests should start with https://api1.comm100.io/api/v3/.
- If the domain of your Control Panel is portal3.comm100.io, all API requests should start with https://api3.comm100.io/api/v3/.
- If the domain of your Control Panel is portal5.comm100.io, all API requests should start with https://api5.comm100.io/api/v3/.
- If the domain of your Control Panel is portal7.comm100.io, all API requests should start with https://api7.comm100.io/api/v3/.

## Authentication

Comm100 use JWT authentication method.

- [JWT Authentication](#JWT-Authentication)

## JWT Authentication
  You can only use jwt authenticate to exchange an agent's email, password and siteId for a jwt token directly while calling the global, livechat or report API. This grant type is highly secured by Comm100.

### How to get the jwt token?

### Using curl

  Params:

- LoginType - specify `password` as the value.
- Username - the email of the agent account.
- Password - the password of the agent account.
- SiteId - the site which the agent belongs to.

```bash
  curl https://x.comm100.com/adminwebservice/api/jwttoken/generate -H "Content-Type:application/json"  
  -d '{"LoginType":"Password","Username":{comm100_agent_email},"Password":{comm100_agent_password},"SiteId":{siteId}}'  
  -X POST
```

#### Example Response

```bash
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    ......
    "token": "eyJhbGciOiJodHRwOi8vd3d3LnczLm9yZy8yMDAxLzA0L3htbGRzaWctbW9yZSNyc2Etc2hhMjU2IiwidHlwIjoiSldUIn0.eyJqdGkiOiI1NjIzNDFjZS0zZDkyLTRlZDYtOGY3ZS0zYTQ0NTdlYjQ0OTEiLCJhZ2VudElkIjoiMSIsInNpdGVJZCI6IjEwMDAxMDAwIiwidGh1bWJwcmludCI6IjhBNjhBOThBQzg0MUI1QTc5OEQ5RkE1MTY1QUU0Nzk3NEVERkIyRjYiLCJzdWNjZXNzIjoiVHJ1ZSIsIm5iZiI6MTU4NzY5NTk4MSwiZXhwIjoxNTg3NzAzMTgxLCJpc3MiOiJwb3J0YWwxLmNvbW0xMDAuaW8ifQ.MKuNrAqkbX5HMPwGH9hT-LlZp__CrNJpavXN7UR2qwM2C5TKG1ooghriQruaEBNDFwV8d7mjuwUMcydII2ayngX5jneabirqlhEu0O3LxGitR7P8NyQMDRMEh2ssJmIIJiCKwz9Mr_IzbtNgBZ5yAJ59jQ3hZZErrs62tlhPcMDAxOvTd9wAePUsISb3_-MbUU_WM9cLIKmQi9XWAUw0U4Lvxqp2dopkTLFyynahQGKbKMP934MMwRlKDQko0GZzcjIokYMWfqhesW9iZnJHP-_JQYjbkd4YL1IGUrD2BygD_trcm6Tk2odcYQKPx8vFvR62lU2_pm8i66ECvN-sAA",
    ......
  }
```

##### Notes

The token has an expiration time, if the token has expired, please call the API again to obtain a new token.

### How to call the comm100 v3 api by the jwt token?
You can use the jwt token to call the comm100 v3 api as follow Example.

### Example

##### Using curl

```bash
    curl -H "Authorization: Bearer eyJhbGciOiJodHRwOi8vd3d3LnczLm9yZy8yMDAxLzA0L3htbGRzaWctbW9yZSNyc2Etc2hhMjU2IiwidHlwIjoiSldUIn0.eyJqdGkiOiI1NjIzNDFjZS0zZDkyLTRlZDYtOGY3ZS0zYTQ0NTdlYjQ0OTEiLCJhZ2VudElkIjoiMSIsInNpdGVJZCI6IjEwMDAxMDAwIiwidGh1bWJwcmludCI6IjhBNjhBOThBQzg0MUI1QTc5OEQ5RkE1MTY1QUU0Nzk3NEVERkIyRjYiLCJzdWNjZXNzIjoiVHJ1ZSIsIm5iZiI6MTU4NzY5NTk4MSwiZXhwIjoxNTg3NzAzMTgxLCJpc3MiOiJwb3J0YWwxLmNvbW0xMDAuaW8ifQ.MKuNrAqkbX5HMPwGH9hT-LlZp__CrNJpavXN7UR2qwM2C5TKG1ooghriQruaEBNDFwV8d7mjuwUMcydII2ayngX5jneabirqlhEu0O3LxGitR7P8NyQMDRMEh2ssJmIIJiCKwz9Mr_IzbtNgBZ5yAJ59jQ3hZZErrs62tlhPcMDAxOvTd9wAePUsISb3_-MbUU_WM9cLIKmQi9XWAUw0U4Lvxqp2dopkTLFyynahQGKbKMP934MMwRlKDQko0GZzcjIokYMWfqhesW9iZnJHP-_JQYjbkd4YL1IGUrD2BygD_trcm6Tk2odcYQKPx8vFvR62lU2_pm8i66ECvN-sAA" 
         -H "Content-Type: application/json"
      -d '{
            "name": "livechat15293908029",
            "color": "339FD9",
            "isEnable": false,
            "order": 1,
            "description": "",
            "conditionMetType": "all",
            "logicalExpression": "",
            "conditions": [
              {
                "field": "CurrentPageUrl",
                "operator": "include",
                "value": "live",
                "order": 1
              }
            ],
            "alertTo":{
                "agentIds":[4,5],
                "departmentIds":[]
            }
          }' 
      -X POST https://api1.comm100.io/api/v3/livechat/customerSegments
```

##### Example Response

```bash
  HTTP/1.1 201 Created
  Location: https://api1.comm100.io/api/v3/livechat/customerSegments/1487fc9d-92e6-4487-a2e8-92e68d6892e6
  Content-Type:  application/json
  {
    "name": "livechat15293908029",
    "color": "339FD9",
    "isEnable": false,
    "order": 1,
    "description": "",
    "conditionMetType": "all",
    "logicalExpression": "",
    "conditions": [
      {
        "field": "CurrentPageUrl",
        "operator": "include",
        "value": "live",
        "order": 1
      }
    ],
    "alertTo":{
        "agentIds":[4,5],
        "departmentIds":[]
    }
  }
```

## Data Format

Comm100 RESTful API returns data in [JSON](https://en.wikipedia.org/wiki/JSON) format.

## Error Handling

Errors are returned using standard HTTP error code syntax. Generally, codes in the `2xx` range indicate success; codes in the `4xx` range indicate an error (bad or missing parameters, not authenticated, etc.); codes in the `5xx` range indicate an error with Comm100 Live Chat servers.

- `400` - Bad Request. The request cannot be fulfilled due to bad syntax. You need to make sure that passed arguments are matching format in the method's documentation.
- `401` - Unauthorized. The username or API key you provide is invalid. Please make sure that you authenticate with the correct username or API key.
- `403` - Forbidden. Your permission to access the requested resource has been denied or the number of your API requests has exceeded the limit of the day.
- `404` - Not Found. The requested resource could not be found but may be available at a later time.
- `500` - Internal Server Error. The request was incorrect. You need to make sure that the passed arguments match the formats in the method's documentation.

An error including `code` and `message` is returned in JSON format when an API request fails. For example:

```bash
{ code: 400000, message: "Parameter 'timeFrom' is required." }
```
