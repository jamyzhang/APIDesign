# Introduction

Welcome to the Comm100 RESTful API help guide. Our APIs make it possible for you to integrate your applications with Comm100 Live Chat to achieve seamless data sharing. It is our goal to help the business to automate and enhance their customer support with innovative projects you can create using Comm100 API.

Please note that this documentation refers to the latest API version: 2.0. Please use 2 as the version number in the url. If you are looking for the previous version, check out the [API 1.0 documentation](https://www.comm100.com/doc/api/v1/introduction.htm#/).

**Important Notice: We will stop support for the following old domains in API calls permanently at 12:00 AM Pacific time on Mar. 20th, 2020. To avoid any service disruption, please make sure that your applications have been updated to use the new domains.**

| Old domain | New domain |
| - | - |
|`eu.comm100.com` | `euportal.comm100.com`  |
|`ent.comm100.com` | `ent1portal.comm100.com`  |
|`ent7.comm100.com` | `ent7portal.comm100.com`  |
|`app.comm100.chat` | `appportal.comm100.chat`  |
|`enterprise.comm100.com` | `enterpriseportal.comm100.com`  |

<div>

## The Basics

Comm100 RESTful API must use **https** protocol. What the API requests should start with depends on your platform domain, which can be accessed from both your Control Panel and web version Agent Console after successful login. For example:

- If the domain of your Control Panel is hosted3.comm100.com, all API requests should start with https://hosted3.comm100.com/api/v2/.
- If the domain of your Control Panel is euportal.comm100.com, all API requests should start with https://euportal.comm100.com/api/v2/.
- If the domain of your Control Panel is Appportal.comm100.chat, all API requests should start with https://Appportal.comm100.chat/api/v2/.
- If the domain of your Control Panel is ent7portal.comm100.com, all API requests should start with https://ent7portal.comm100.com/api/v2/.
- If the domain of your Control Panel is enterpriseportal.comm100.com, all API requests should start with https://enterpriseportal.comm100.com/api/v2/.
- If the domain of your Control Panel is ent1portal.comm100.com, all API requests should start with https://ent1portal.comm100.com/api/v2/.
- If the domain of your Control Panel is hosted.comm100.com, all API requests should start with https://hosted.comm100.com/api/v2/.

</div>
<div>

## Authentication

Comm100 provides 2 authentication methods.

- [API_key Authentication](#API_key-Authentication)
- [JWT Authentication](#JWT-Authentication)

</div>
<div>

## API_key Authentication

For each method call, you must use your email and API_KEY.Authentication to the API is done via HTTP Basic Auth. Provide your email as the basic auth username and API_KEY as the password. You must authenticate for API requests. Even though we still support this type of authentication, we recommend using JWT authentication.

</div>
<div>

## JWT Authentication

  You can use JWT to authenticate all your API requests to Comm100.

- [Global, Livechat & Report API JWT Authentication](#global-and-livechat-api-JWT-authentication)

<div>

### Global, Livechat & Report API JWT Authentication

  You can only use jwt authenticate to exchange an agent's email、password and siteId for an jwt token directly while calling the global, livechat or report API. This grant type is highly secured by Comm100.

##### Using curl

  Params:

- loginType - specify `password` as the value.
- userName - the email of the agent account.
- password - the password of the agent account.
- siteId - the site which the agent belongs to.

```bash
    curl https://x.comm100.com/adminwebservice/api/jwttoken/generate -H "Content-Type:application/x-www-form-urlencoded"  
     -d 'loginType=password&userName={comm100_agent_email}&password={comm100_agent_password}&siteId={siteId}'  
     -x POST
```

##### Example Response

```bash
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
  ......
  "token": "vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q",
  ......
  }
```

</div>
</div>
<div>

## Data Format

Comm100 RESTful API returns data in [JSON](https://en.wikipedia.org/wiki/JSON) format.

</div>
<div>

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

</div>
&#32;