# Introduction

Welcome to Comm100 RESTful API help guide. Our APIs makes it possible for you to integrate your applications with Comm100 Live Chat so as to achieve seamless data sharing. It is our goal to help business to automate and enhance their customer support with innovative projects you can create using Comm100 API.

Please note that this documentation refers to the latest API version: 2.0. Please use 2 as the version number in the url. If you are looking for the previous version, check out the [API 1.0 documentation](https://www.comm100.com/doc/api/v1/introduction.htm#/).

<div>

## The Basics

Comm100 RESTful API must use **https** protocol. The api request starts with is depends on the control panel's URL. For example, if the control panel URL starts with ent.comm100.com, all requests should start with https://ent.comm100.com/api/v2, etc.

</div>
<div>

## Authentication

Comm100 provides 2 authentication methods.

- [API_key Authentication](#API_key-Authentication)
- [OAuth Authentication](#OAuth-Authentication)

</div>
<div>

## API_key Authentication

For each method call, you must use your email and API_KEY.Authentication to the API is done via HTTP Basic Auth. Provide your email as the basic auth username and API_KEY as the password. You must authenticate for all API requests. Even though we still support this type of authentication, we recommend using oauth authentication.

</div>
<div>

## OAuth Authentication

  You can use OAuth2 to authenticate all your API requests to Comm100. OAuth provides a more secure way for your application to access your account data without requiring that sensitive information like email and password to be sent with the requests. There are different OAuth flows for different types of API.

- [Account, Livechat & Report API OAuth Authentication](#account-and-livechat-api-oauth-authentication)
- [Partner API OAuth Authentication](#partner-api-oauth-authentication)

<div>

### Account, Livechat & Report API OAuth Authentication

  Comm100 supports several OAuth flows. The authorization code grant flow, uses an authorization code after getting user confirmation to exchange for an access token that acts on behalf of that user. The other two options are server-side grant types that don't require interacting with end users.

- [Authorization code grant flow](#authorization-code-grant-flow)
- [Implicit grant flow](#implicit-grant-flow)
- [Password grant type](#password-grant-type)
- [Client credentials type](#client-credentials-type)

#### Authorization Code Grant Flow

  To implement the authorization code grant flow, you need to get an authorization code first. Afterwards, you can use it to exchange for an access token and use the access token to call api.

##### Get an authorization code

  Params:

- client_id - the id of oauth client.
- siteId - the id of request site.
- redirect_uri - the redirect uri of oauth client.
- response_type - specify `code` as the value.

```bash
    curl "https://hosted.comm100.com/oauth/authorize?client_id={oauth_client_id}& 
    siteId={request_siteId}&redirect_uri={oauth_client_redirectUri}&response_type=code"
```

##### Example Response

```bash
  {oauth_client_redirectUri}?code=591c35a40c8145e0b08dfa2b6e3294f17afc56729eb943eeac290c70+ef49b6e
```

#### Exchange for an access token

  Params:
- grant_type - specify `authorization_code` as the value.
- code - the authorization code.
- redirect_uri - the redirect uri of oauth client.
- client_id - the id of oauth client.
- client_secret - the secret of oauth client.

```bash
    curl https://hosted.comm100.com/oauth/token 
      -H "Content-Type:application/x-www-form-urlencoded" 
      -d 'grant_type=authorization_code&code={authorization_code}& 
      redirect_uri={oauth_client_redirectUri}&client_id={oauth_client_id}& 
      client_secret={oauth_client_secret}'
      -X POST
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

#### Implicit Grant Flow

  The implicit grant flow is similar to the authorization code grant flow except there's no need to apply for the authorization code. You can request an access token directly if you set the value of the `response_type` parameter to `token` instead of `code`.

##### Get an access token

  Params:

- client_id - the id of oauth client.
- siteId - the id of request site.
- redirect_uri - the redirect uri of oauth client.
- response_type - specify `token` as the value.

```bash
    curl "https://hosted.comm100.com/oauth/authorize?client_id={oauth_client_id} 
    &siteId={request_siteId}&redirect_uri={oauth_client_redirectUri}&response_type=token"
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

#### Password Grant Type

  You can only use password grant type to exchange an agent's email and password for an access token directly while calling the account, livechat or report API. This grant type is highly secured by Comm100.

##### Using curl

  Params:

- email - the email of the agent account.
- password - the password of the agent account.
- grant_type - specify `password` as the value.

```bash
    curl https://hosted.comm100.com/oauth/token -H "Content-Type:application/x-www-form-urlencoded"  
     -d 'grant_type=password&email={comm100_agent_email}&password={comm100_agent_password}'  
     -X POST
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

#### Client Credentials Type

  The client credentials grant flow is used to access API endpoints designed specifically for the third party applications rather than for users.

##### Using curl

  Params:
  
- grant_type - specify `client_credentials` as the value.
- redirect_uri - the redirect uri of oauth client.
- client_id - the id of oauth client.
- client_secret - the secret of oauth client.
- siteId - the id of request site.

```bash
    curl https://hosted.comm100.com/oauth/token 
      -H "Content-Type:application/x-www-form-urlencoded" 
      -d 'grant_type=client_credentials&code={authorization_code} 
      &redirect_uri={oauth_client_redirectUri}&client_id={oauth_client_id} 
      &client_secret={oauth_client_secret}&siteId={request_siteId}'
      -X POST
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

</div>
<div>

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
     -X POST
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

- `400` - Bad Request. The request cannot be fulfilled due to bad syntax. You need to make sure that passed arguments are matching format in method's documentation.
- `401` - Unauthorized. The username or API key you provide is invalid. Please make sure that you authenticate with correct username or API key.
- `403` - Forbidden. Your permission to access the requested resource has been denied or the number of your API requests has exceeded the limit of the day.
- `404` - Not Found. The requested resource could not be found but may be available at a later time.
- `500` - Internal Server Error. The request was incorrect. You need to make sure that the passed arguments match the formats in method's documentation.

An error including `code` and `message` is returned in JSON format when an API request fails. For example:

```bash
{ code: 400000, message: "Parameter 'timeFrom' is required." }
```

</div>
&#32;