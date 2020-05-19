# Introduction

Welcome to the Comm100 RESTful API help guide. Our APIs make it possible for you to integrate your applications with Comm100 Live Chat to achieve seamless data sharing. It is our goal to help the business to automate and enhance their customer support with innovative projects you can create using Comm100 API.

Note: Comm100 currently has two versions of our customer engagement platform.

- If you started using Comm100 on/after April 26, 2020, or you have migrated to the new platform, this is the latest API version for the platform you are on.
- If you started using Comm100 before April 26, 2020, you can access API 1.0 [here](https://www.comm100.com/doc/api/v1/introduction.htm#/) or the latest API version 2.0 [here](https://www.comm100.com/doc/api/introduction.htm#/).

<div>

## The Basics

Comm100 RESTful API must use https protocol. What the API requests should start with depends on your platform domain, which can be accessed from both your Control Panel and web version Agent Console after successful login. For example:


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
- [OAuth Authentication](#OAuth-Authentication)

</div>
<div>

## API_key Authentication

For each method call, you must use your email and API_KEY.Authentication to the API is done via HTTP Basic Auth. Provide your email as the basic auth username and API_KEY as the password. You must authenticate for API requests. Even though we still support this type of authentication, we recommend using OAuth authentication.

</div>
<div>

## OAuth Authentication

  You can use OAuth2 to authenticate all your API requests to Comm100. OAuth provides a more secure way for your application to access your account data without requiring that sensitive information like email and password to be sent with the requests. There are different OAuth flows for different types of API.

- [Account, Livechat & Report API OAuth Authentication](#account-and-livechat-api-oauth-authentication)
- [Partner API OAuth Authentication](#partner-api-oauth-authentication)

<div>

### Account, Livechat & Report API OAuth Authentication

  You can only use password grant type to exchange an agent's email and password for an access token directly while calling the account, livechat or report API. This grant type is highly secured by Comm100.

##### Using curl

  Params:

- email - the email of the agent account.
- password - the password of the agent account.
- grant_type - specify `password` as the value.

```bash
    curl https://hosted.comm100.com/oauth/token -H "Content-Type:application/x-www-form-urlencoded"  
     -d 'grant_type=password&email={comm100_agent_email}&password={comm100_agent_password}'  
     -x POST
```

##### Example Response

```bash
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
  }
```

### Partner API OAuth Authentication

  You can only use password grant type to exchange a partner's email and password for an access token directly while calling the Partner API. This grant type is supported for the partner which is highly secured by Comm100, and it can operate on data which belongs to the partner.

#### Using curl

  Params:

- email - the email of the partner account.
- password - the password of the partner account.
- grant_type - specify `password` as the value.

```bash
    curl https://hosted.comm100.com/partner/oauth/token -H "Content-Type:application/x-www-form-urlencoded"  
     -d 'grant_type=password&email={comm100_parnter_email}&password={comm100_partner_password}'  
     -x POST
```

#### Example Response

```bash
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "access_token":"vQAQmLX8jvtsG71ItN2QAisqI_F7cDIE0yaX0FfS3RX6g-HR4gfHSVMaOukomYJiJX0Q"
    ,"token_type":"bearer"
    ,"expires_in":43199
    ,"refresh_token":"91a728cdd4c64fb7b128f74f4855c3daee44167ef60542a2b45c21e16373ed02"
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