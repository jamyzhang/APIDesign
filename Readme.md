<center><h1> RESTful API Guidelines</h1></center>

# Table of contents
1. [Abstract](#abstract)
1. [URL Patterns](#URL-Patterns)
1. [Methods](#Methods)
    - [GET](#get)
    - [PUT](#put)
    - [DELETE](#delete)
    - [POST](#post)
    - [HEAD](#head)
    - [PATCH](#patch)
1. [Operations](#Operations)
    - [Sorting](#sorting)
    - [Pagination](#pagination)
    - [Including](#including)
1. [Errors & Faults](#Errors-&-Faults)

# Abstract
This Guidelines is base on [Microsoft REST API Guidelines](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md), you may be to read it first. Developers should follow this guidelines to design consistent RESTful APIs.

At first , some criterion are palaced here.
- Resources, parameters and JSON property names SHOULD be camelCased.
- The name of the resources, unabbreviated, pluralized.
- Objects, entities and properties SHOULD be named with nouns. 
- The content type SHOULD be application/json.
- Datetime string format based upon the [ISO8601](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15)
- The API design documentation must be written in the markdown file format and uploaded to [Github Repository](https://github.com/jamyzhang/APIDesign) to take advantage of Github's powerful version control and collaboration capabilities to increase our efficiency.

#  URL Patterns
The independent resource api url pattern.
```http
https://{serviceRoot}/api/{version}/{module}/{resource}
 ```
 The sub-resource api url pattern.
 ```http
https://{serviceRoot}/api/{version}/{module}/{parentResource}/{parentResourceId}/{resource}
 ```
 The parent resource usually corresponds to the concept of the domain in the domain driver design.  In the case where  an object is operated by the id, for example, retrieved by id,updated by Id and deleted  by Id etc, it's not needed for  ParentResource and ParentResourceId are present in the URL.


For example:
  - Get the conversation by an id of 10000.
  ```http
GET http://alpha.common100.com/api/v3/messaging/conversations/10000
  ```
  - Get the conversation created in May 2017.
  ```http
GET http://alpha.common100.com/api/v3/messaging/conversations?beginDate=2017-05-01&endDate=2017-05-31
  ```
   - Get the messages of a conversation with an id is 10000.
  ```http
GET http://alpha.common100.com/api/v3/messaging/conversations/10000/messages
  ```
  - Get the message by  id of 1000.
  ```http
GET http://alpha.common100.com/api/v3/messaging/messages/1000
  ```
  If an object has multiple methods to expose, but the API verb are the same. We use the colon with the method name to append to the url to distinguish.

  For example:

EndPoint|Description
---|---
`POST` api/v3/messaging/conversations | Create a new conversation
`POST` api/v3/messaging/conversations/{id}`:read`  | Mark a conversation as read
`POST` api/v3/messaging/conversations/{id}`:unread`  | Mark a conversation as unread 


# Methods
Operations MUST use the proper HTTP methods whenever possible, and operation idempotency MUST be respected. HTTP methods are frequently referred to as the HTTP verbs. The terms are synonymous in this context, however the HTTP specification uses the term method.

Below is a list of methods that our services SHOULD support. Not all resources will support all methods, but all resources using the methods below MUST conform to their usage.

Method  | Description| Is Idempotent
------- | --------------------------------- | -------------
GET     |  Return the current value of an object  | True
PUT     | Replace an object, or create a named object, when applicable         | True
DELETE  | Delete an object       | True
POST    | Create a new object based on the data provided, or submit a command   | False
HEAD    | Return metadata of an object for a GET response. Resources that support the GET method MAY support the HEAD method well | True
PATCH   | Apply a partial update to an object                         
## GET
Gets the value of an object by id.
```http
GET http://alpha.common100.com/api/v3/contacts/{id}
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

{
  ...
}
```
Gets a list of values for an object.
```http
GET http://alpha.common100.com/api/v3/contacts
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json
{
  "value":[....]
}
```
## PUT
If used to create a named object , it MAY return `201` status code and the newly created resource can be referenced by the URI(s) returned in Location header field of the response.If used to replace an object, it MAY return  `204` status code with no response body content.Also it's CAN return `200` status code with the response body content.

Create a named object by specifying the id.
```http
PUT http://alpha.common100.com/api/v3/contacts/10000
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 201 Created
Location:http://alpha.common100.com/api/v3/contacts/10000
```
```http
PUT http://alpha.common100.com/api/v3/contacts/10000
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 200 OK
Content-Type: application/json
{
  ....
}
```
Replace/Update an object:
```http
PUT http://alpha.common100.com/api/v3/contacts/10001
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 204 No Content
Location:http://alpha.common100.com/api/v3/contacts/10001
```
```http
PUT http://alpha.common100.com/api/v3/contacts/10001
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 200 OK
Content-Type: application/json
{
  ....
}
```
## DELETE
If successful, return the `204` status code.

Delete an object by Id.
```http
DELETE http://alpha.common100.com/api/v3/contacts/10000
Date: Wed, 24 Aug 2018 18:41:30 GMT

HTTP/1.1 204 No Content
```
## POST
If used to create an object , it SHOULD return `201` status code and the newly created resource can be referenced by the URI(s) returned in Location header field of the response, or  `200` status code with response body content.  

Create an object.
```http
POST http://alpha.common100.com/api/v3/contacts
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 201 Created
Location:http://alpha.common100.com/api/v3/contacts/10003
```
```http
POST http://alpha.common100.com/api/v3/contacts
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 200 OK
Content-Type: application/json
{
  ....
}
```
Send a command.
```http
POST http://alpha.common100.com/api/v3/contacts/10001:merge
Date: Wed, 24 Aug 2018 18:41:30 GMT
Accept: application/json
{
  ...
}
HTTP/1.1 200 OK
Content-Type: application/json
{
  ....
}
```
## HEAD
Checking a contact has registered by email address, the API endpoint is :
```http
HEAD http://alpha.common100.com/api/v3/contacts/emails/xxx@gmail.com
Date: Wed, 24 Aug 2018 18:41:30 GMT

HTTP/1.1 204 No Content
Location:http://alpha.common100.com/api/v3/contacts/123144
```
Checking a contact has registered by phone number, the API endpoint is :
```http
HEAD http://alpha.common100.com/api/v3/contacts/phones/134-1999-1111
Date: Wed, 24 Aug 2018 18:41:30 GMT

HTTP/1.1 404 Not Found
```
If the resource exists, it should return `204` status code and the "Location Header" SHOULD be assigned to GET url of the resource, otherwise it should return `404` status code.
## PATCH
PATCH is not supported now, but I recommend  implementing it.

Services that allow callers to specify key values on create SHOULD support UPSERT semantics, and those that do MUST support creating resources using PATCH. Because PUT is defined as a complete replacement of the content, it is dangerous for clients to use PUT to modify data. Clients that do not understand (and hence ignore) properties on a resource are not likely to provide them on a PUT when trying to update a resource, hence such properties could be inadvertently removed. Services MAY optionally support PUT to update existing resources, but if they do they MUST use replacement semantics (that is, after the PUT, the resource's properties MUST match what was provided in the request, including deleting any server properties that were not provided).

Under UPSERT semantics, a PATCH call to a nonexistent resource is handled by the server as a "create," and a PATCH call to an existing resource is handled as an "update." To ensure that an update request is not treated as a create or vice-versa, the client MAY specify precondition HTTP headers in the request. The service MUST NOT treat a PATCH request as an insert if it contains an If-Match header and MUST NOT treat a PATCH request as an update if it contains an If-None-Match header with a value of "*".

If a service does not support UPSERT, then a PATCH call against a resource that does not exist MUST result in an HTTP "409 Conflict" error.


#  Operations
There are 3 operations have been defined, **Sorting** and **Pagination** operations MAY be performed against a given collection, **Including** MAY be performed on a given object.The query  parameters of operations should named with the prefix '$' to distinguish them from the normal parameter.

## Sorting
The potentially filtered list is sorted according to the sort criteria.

The property is determined by the value of the `$orderBy` query parameter.The value of the `$orderBy` parameter contains a comma-separated list of expressions used to sort the items.A special case of such an expression is a property path terminating on a primitive property.

The expression MAY include the suffix "asc" for ascending or "desc" for descending, separated from the property name by one or more spaces.If "asc" or "desc" is not specified, the service MUST order by the specified property in ascending order.

For example:
```http
GET http://alpha.common100.com/api/v3/liveChat/contacts?$orderBy=name
```
```http
GET http://alpha.common100.com/api/v3/liveChat/contacts?$orderBy=name desc
```
```http
GET http://alpha.common100.com/api/v3/liveChat/contacts?$orderBy=name,email
```

## Pagination
RESTful APIs that return collections MAY return partial sets.
Consumers of these services MUST expect partial result sets and correctly page through to retrieve an entire set.

Sorting  parameters MUST be consistent across pages, because both  server-side paging is fully compatible with  sorting.

Query Parameters:

Parameter| Optional|Description
---------|------|-------
`$pageSize` | true| The default value is 10.
`$skip`|true| The default value is 0.
`$count`|true| If there is, the returning value SHOULD contains the totalCount.

For example:
```http
GET http://alpha.common100.com/api/v3/liveChat/contacts?$pageSize=10&$skip=10 HTTP/1.1
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

{
  "value": [...]
}
```
```http
GET http://alpha.common100.com/api/v3/liveChat/contacts?$pageSize=10&$skip=10&$count HTTP/1.1
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

{
  "totalCount":1000,
  "value": [...]
}
```
## Including
What describes which properties of object should be included when the service responds to the client. These properties are the sub-resources of an object which is also a resource. 

The property is determined by the value of the `$include` query parameter.The value of the `$include` parameter contains a comma-separated list of expressions used to  retrieve multiple sub-resources.

For example:
```http
GET http://alpha.common100.com/api/v3/messaging/conversations/{id}?$include=assignedAgent,createdBy,messages HTTP/1.1
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

 {
            "id": 1,
            "assignedAgentId": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
            "assignedAgent": {  //included the assignedAgent
                "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
                ...
            },
            "relatedType": "contact",
            "relatedId":"f9928d68-92e6-4487-a2e8-8234fc9d1f43",
            "createdById": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
            "createdByType": "agent",
            "createdBy": {  //included the createdBy.
                "id": "f9928d68-92e6-4487-a2e8-8234fc9d1f48",
                ...
            },
            "messages":[    //included the messages.
                {
                    "id": "f9928d68-92e6-4487-a2e8-8234fc9d1fe8", 
                    ...
                },
                {
                        "id": "f9928d68-92e6-4487-a2e8-8234fc9d1d48", 
                    ...
                }
            ]
            ...
        } 
```
# Errors & Faults
`Errors`, or more specifically Service Errors, are defined as a client passing invalid data to the service and the service correctly rejecting that data. Examples include invalid credentials, incorrect parameters, unknown version IDs, or similar. These are generally ["4xx" HTTP error codes](https://tools.ietf.org/html/rfc7231#section-6.5) and are the result of a client passing incorrect or invalid data.

`Errors` do not contribute to overall API availability.

`Faults`, or more specifically Service Faults, are defined as the service failing to correctly return in response to a valid client request. These are generally ["5xx" HTTP error codes](https://tools.ietf.org/html/rfc7231#section-6.6).

`Faults` do contribute to the overall API availability.

Calls that fail due to rate limiting or quota failures MUST NOT count as faults. Calls that fail as the result of a service fast-failing requests (often for its own protection) do count as faults.

##### ErrorResponse : Object

Property | Type | Required | Description
-------- | ---- | -------- | -----------
`error` | Error | ✔ | The error object.

##### Error : Object

Property | Type | Required | Description
-------- | ---- | -------- | -----------
`code` | String (enumerated) | ✔ | One of a server-defined set of error codes. It is a language-independent string and SHOULD be human-readable.
`message` | String | ✔ | A human-readable representation of the error. It is intended as an aid to developers and is not suitable for exposure to end users.
`target` | String |  | The target of the error.
`details` | Error[] |  | An array of details about specific errors that led to this reported error.
`innererror` | InnerError |  | An object containing more specific information than the current object about the error.

##### InnerError : Object

Property | Type | Required | Description
-------- | ---- | -------- | -----------
`code` | String |  | A more specific error code than was provided by the containing error.
`innererror` | InnerError |  | An object containing more specific information than the current object about the error.

##### Examples

Example of "innererror":

```json
{
  "error": {
    "code": "BadArgument",
    "message": "Previous passwords may not be reused",
    "target": "password",
    "innererror": {
      "code": "PasswordError",
      "innererror": {
        "code": "PasswordDoesNotMeetPolicy",
        "minLength": "6",
        "maxLength": "64",
        "characterTypes": ["lowerCase","upperCase","number","symbol"],
        "minDistinctCharacterTypes": "2",
        "innererror": {
          "code": "PasswordReuseNotAllowed"
        }
      }
    }
  }
}
```
Example of "details":

```json
{
  "error": {
    "code": "BadArgument",
    "message": "Multiple errors in ContactInfo data",
    "target": "ContactInfo",
    "details": [
      {
        "code": "NullValue",
        "target": "PhoneNumber",
        "message": "Phone number must not be null"
      },
      {
        "code": "NullValue",
        "target": "LastName",
        "message": "Last name must not be null"
      },
      {
        "code": "MalformedValue",
        "target": "Address",
        "message": "Address is not valid"
      }
    ]
  }
}
```
