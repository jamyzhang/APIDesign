# Introduction
Welcome to Comm100 RESTful API help guide. Our APIs enable you to integrate your applications with Comm100 Live Chat and realize the benefit of seamless data sharing. With Comm100 APIs, you can create innovative projects, achieve great practices and raise your customer satisfaction.

## The Basics
Comm100 RESTful API must use **https** access. All API requests on the Hosted platform start with https://hosted.comm100.com/api/v1/. All requests on the Enterprise platform start with https://ent.comm100.com/api/v1/.

Please note that the current API version is **1.0**. You need to use 1 as the version number in the url. Our latest API version is [2.0](https://www.comm100.com/doc/api/introduction.htm), with 2 as the version number in the url.

## Authorization
For each method call, you must use your **email** and **API_KEY**.

Authentication to the API is done via [HTTP Basic Auth](https://en.wikipedia.org/wiki/Basic_access_authentication). Provide your **email** as the basic auth username and **API_KEY** as the password. You must authenticate for all API requests.

## Data Format
Comm100 RESTful API returns data in [JSON](https://en.wikipedia.org/wiki/JSON) format.

## Error Handling
Errors are returned using standard HTTP error code syntax. Generally, codes in the `2xx` range indicate success; codes in the `4xx` range indicate an error (bad or missing parameters, not authenticated, etc.); codes in the `5xx` range indicate an error with Comm100 Live Chat servers. 

- `400` - Bad Request. The request cannot be fulfilled due to bad syntax. You need to make sure that passed arguments are matching format in method's documentation.
- `401` - Unauthorized. The username or API key you provide is invalid. Please make sure that you authenticate with correct username or API key.
- `403` - Forbidden. Your permission to access the requested resource has been denied or the number of your API requests has exceeded the limit of the day.
- `404` - Not Found. The requested resource could not be found but may be available at a later time.
- `500` - Internal Server Error. The request was incorrect. You need to make sure that the passed arguments match the formats in method's documentation.

An error including `code` and `message` is returned in JSON format when an API request fails. For example: 
```javascript
{ code: 400000, message: "Parameter 'timeFrom' is required." }
```
## Frequency Limiting
Each account has a daily limit on the number of API requests that can be made. The limit is reset every day at 0:00 UTC time.