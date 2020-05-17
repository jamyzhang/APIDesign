# General

| Object | Path |
| - | - |
| [Credential](#Credential) | `/partner/oauth/token` |
| [Sites](#Sites) | `/api/v3/partner/sites` |

<div>

## Credential

<div>

### Model

#### Access token JSON Format

  Access token is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | access_token | string | yes | no | string of the token
  | expires_in | string | yes | no | time of expiry

</div>
<div>

### Endpoint

#### Get oauth token

 `GET https://partner7.comm100.io/partner/oauth/token`

- Parameters:
  - `grant_type` - `password`, Specify the way to get the token as password
  - `email` - partner email
  - `password` - partner password

- Response:

    Access token Json Format

#### Example

  Sample request:

```bash
 curl -X POST  
     -d "email=lizz@comm100.com&grant_type=password&password=111111"   
     https://partner7.comm100.io/partner/oauth/token
```

  Sample response:

```json
{
    "access_token": "uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSw  
    YcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnng  
    tbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ",
    "token_type": "bearer",
    "expires_in": 43199,
    "refresh_token": "6960bae5cc2840f1bf9ee47d13180ab892aa2b1f3a564a0aa7df0bbd0ecb4ae6"
}
```

Developers can make API calls through the `access_token` obtained above, in the following format:

  `Authorization": "bearer {access_token}"`

</div>
</div>
<div>

## Sites

- `GET /api/v3/partner/sites/{site_id}` - Get information about one of the current Partner sites  
- `GET /api/v3/partner/sites` - Get site information for all customers of the current Partner
- `PUT /api/v3/partner/sites/{site_id}` - Update site information for one of the Partner's customers
- `PUT /api/v3/partner/sites/{site_id}/paying` - Convert the trial period account into an official account

<div>

### Endpoint

#### Get a Site

  `Get /api/v3/partner/sites/{site_id}`

- Parameters

  - `site_id` - `required` Site ID
  
- Return
  
  Returns the Site object of the specified site number

```json
      {
        "id": 100001,     // Site number
        "agents": 20, // Number of seats
        "contact": {  // Contact information of the site, generally the information of the registrant
          "firstName": "allon", // Contact's first name
          "lastName": "lu",     // Contact's last name
          "email": "allon.lu@comm100.com",  // Contact's email address
          "phone": "+08618888888888",       // Contact's phone number
        },
        "company": "comm100", // Company name
        "website": "https://www.comm100.com", // Company website address
        "fax": "", // Company fax
        "mailingAddress": "",  // email address
        "city": "",  // city
        "stateOrProvince": "",  // state or Province
        "postalOrZipCode": "",  // postal or zip code
        "country": "China", // Country
        "timezone": "GMT+08:00",  // Site default time zone
        "companySize": "101-180",  // company size
        "activated": true, // Whether the site is activated
        "disabled": false, // Is the site disabled
        "createTime": "2018-08-08T02:24:19.887", //Site create time
        "planList": [ //plan list array
          {
            "id": 1, // plan id
            "name": "planname", // plan name
            "products": 0 //plan products, no use right now
          },
        ]
      }
```

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSw  
    YcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnng  
    tbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ"
     https://partner7.comm100.io/api/v3/partner/sites/6000000
```

  Sample response:

```json
{
    "id": 6000000,
    "agents": 6,
    "contact": {
        "firstName": "test",
        "lastName": "comm100",
        "email": "test@comm100.com",
        "phone": "123456"
    },
    "company": "comm100",
    "website": "www.comm100.com",
    "fax": "",
    "mailingAddress": "",
    "city": "",
    "stateOrProvince": "",
    "postalOrZipCode": "",
    "country": "China",
    "timeZone": "71",
    "companySize": "101-180",
    "activated": true,
    "disabled": false,
    "createTime": "2018-08-08T02:24:19.887",
    "planList": [
      {
        "id": 1,
        "name": "planname",
        "products": 1
      },
      ...
    ]
}
```

#### Get Sites

  `GET /api/v3/partner/sites?keywords=comm100`

- Parameters

  - `keywords` - `optional` Get site's company/website, site contact's firstname/lastname/email, agent's name/email
  - `pageIndex` - `optional` Index page number to be returned

- Return

  Returns a list of up to 100 Site objects and paging information

```json
      {
        "total": 888, // The number of all sites that match the current query
        "previousPage" : "",  // Query the address of the previous page
        "nextPage": "", // Query the address of the Next page
        "sites" : [],   // Site list
      }
```

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSw  
    YcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnng  
    tbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ"
     https://partner7.comm100.io/api/v3/partner/sites
```

  Sample response:

```json
{
    "total": 8,
    "previousPage": "",
    "nextPage": "",
    "sites": [
        {
            "id": 6000000,
            "agents": 6,
            "contact": {
                "firstName": "test",
                "lastName": "comm100",
                "email": "test@comm100.com",
                "phone": "123456"
            },
            "company": "comm100",
            "website": "www.comm100.com",
            "fax": "",
            "mailingAddress": "",
            "city": "",
            "stateOrProvince": "",
            "postalOrZipCode": "",
            "country": "China",
            "timeZone": "71",
            "companySize": "101-180",
            "activated": true,
            "disabled": false,
            "createTime": "2018-08-08T02:24:19.887",
            "planList": [
              {
                "id": 1,
                "name": "planname",
                "products": 1
              },
              ...
            ]
        },
        ...
    ]
}
```

<!--
#### Create Site

  `POST /api/v3/partner/sites`

- Parameters `JSON`

  - `password` - `required` Register user password for the site
  - `contact.firstName` - `required` The first name of the user who registered the site, also the first name of the registered site contact
  - `contact.lastName` - `required` The last name of the user who registered the site, also the last name of the registered site contact
  - `contact.phone` - `optional` The user phone of the registered site, also the phone number of the registered site contact
  - `contact.email` - `required` User email of the registered site, also email for the registration site contact
  - `company` - `optional` Registered site's company
  - `website` - `optional` Register site's website
  - `fax` - `optional` Register site's fax
  - `mailingAddress` - `optional` Register site's mailing address
  - `city` - `optional` Register site's city
  - `stateOrProvince` - `optional` Register site's state or province
  - `postalOrZipCode` - `optional` Register site's postal or zip code
  - `companySize` - `optional` Register site's company size
  - `country` - `optional` Register site's country
  - `timezone` - `required` Registered site's default time zone
  - `planList` - `required` Array of registered site's plan

- Return

  Return the created Site object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSw  
    YcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnng  
    tbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" -H "content-type:application/json"  
     -d "{"password": "123456", "contact": {"firstName": "test", "lastName": "comm100",  
     "email": "test1@comm100.com", "phone": "123456"}, "company": "comm100", "website": "www.comm100.com",  
     "fax": "", "disabled": false, "planList": [{ "id": 1, "name": "planname", "products": 1 }]}"
     -X POST https://partner7.comm100.io/api/v3/partner/sites
```

  Sample response:

```json
{
    "id": 6000012,
    "agents": 1,
    "contact": {
        "firstName": "test",
        "lastName": "comm100",
        "email": "test1@comm100.com",
        "phone": "123456"
    },
    "company": "comm100",
    "website": "www.comm100.com",
    "fax": "",
    "mailingAddress": "",
    "city": "",
    "stateOrProvince": "",
    "postalOrZipCode": "",
    "country": "China",
    "timeZone": "71",
    "companySize": "101-180",
    "activated": true,
    "disabled": false,
    "createTime": "2018-08-16T05:48:24.157",
    "planList": [
      {
        "id": 1,
        "name": "planname",
        "products": 1
      },
      ...
    ]
}
```
-->

#### Update a Site

  `PUT /api/v3/partner/sites/{site_id}`

- Parameters

  - `site_id` - `required` Site id

  - `JSON Data`

    - `activated` - `optional` true/false, whether the site has been activated
    - `disabled` - `optional` true/false, whether the site has been disabled
    - `company` - `optional` Site's company
    - `website` - `optional` Site's website
    - `fax` - `optional` Register site's fax
    - `mailingAddress` - `optional` Register site's mailing address
    - `city` - `optional` Register site's city
    - `stateOrProvince` - `optional` Register site's state or province
    - `postalOrZipCode` - `optional` Register site's postal or zip code
    - `companySize` - `optional` Register site's company size
    - `country` - `optional` Site's country
    - `timezone` - `optional` Site's default time zone
    - `contact.firstName` - `optional` site contact's first name
    - `contact.lastName` - `optional` Site contact's last name
    - `contact.email` - `optional` Site contact's email
    - `contact.phone` - `optional` Site contact's phone number
    - `planList` - `optional` Array of registered site's plan

- Return

  Return the modified Site object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSw  
    YcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnng  
    tbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" -H "content-type:application/json"  
     -d "{"contact": {"firstName": "test", "lastName": "comm100",  
      "phone": "123456"}, "company": "comm100", "website": "www.comm100.com",
      "fax": "", "disabled": false, "planList": [{ "id": 1,"name": "planname", "products": 1 }]}"
     -X PUT https://partner7.comm100.io/api/v3/partner/sites/6000012
```

  Sample response:

```json
{
    "id": 6000012,
    "agents": 1,
    "contact": {
        "firstName": "test",
        "lastName": "comm100",
        "email": "test2@comm100.com",
        "phone": "123456"
    },
    "company": "comm100",
    "website": "www.comm100.com",
    "fax": "",
    "mailingAddress": "",
    "city": "",
    "stateOrProvince": "",
    "postalOrZipCode": "",
    "country": "China",
    "timeZone": "71",
    "companySize": "101-180",
    "activated": true,
    "disabled": false,
    "createTime": "2018-08-16T05:48:24.157",
    "planList": [
      {
        "id": 1,
        "name": "planname",
        "products": 1
      }
    ]
}
```

#### Pay a site

  `PUT /api/v3/partner/sites/{site_id}/paying`

- Parameters

  - `site_id` - `required` Site id
  
- Return
  
  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSw  
    YcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnng  
    tbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ"  
     -X PUT -d "site_id=6000012"   
     https://partner7.comm100.io/api/v3/partner/sites/6000012/paying
```

  Sample response:

```json
Status: 200 OK
```

</div>
</div>
&#32;