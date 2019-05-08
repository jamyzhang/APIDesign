# General

| Object | Path |
| - | - |
| [Credential]($Credential) | `/oauth/token` |
| [Site]($Site) | `partner/sites` |

## Credential

### Access token Json Format

  Access token is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | access_token | string | yes | no | string of the token
  | expires_in | string | yes | no | time of expiry

 `GET https://hosted.comm100.com/oauth/token`

- Parameters:
  - `grant_type` - `password`, Specify the way to get the token as password
  - `email` - partner email
  - `password` - partner password

- Response:

    Access token Json Format

#### Example

  Sample request:

```bash
 curl -X POST -d "email=lizz@comm100.com&grant_type=password&password=111111" https://hosted.comm100.com/partner/oauth/token
```

  Sample response:

```json
{
    "access_token": "uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSwYcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnngtbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ",
    "token_type": "bearer",
    "expires_in": 43199,
    "refresh_token": "6960bae5cc2840f1bf9ee47d13180ab892aa2b1f3a564a0aa7df0bbd0ecb4ae6"
}
```

Developers can make API calls through the `access_token` obtained above, in the following format:

  `Authorization": "bearer {access_token}"`

## Sites

- `GET /api/v2/partner/sites/{site_id}` - Get information about one of the current Partner sites  
- `GET /api/v2/partner/sites` - Get site information for all customers of the current Partner
- `POST /api/v2/partner/sites` - Open an account, create a new site
- `PUT /api/v2/partner/sites/{site_id}` - Update site information for one of the Partner's customers
- `PUT /api/v2/partner/sites/{site_id}/paying` - Convert the trial period account into an official account

### Get a Site

  `Get /api/v2/partner/sites/{site_id}`

- Parameters

  - `site_id` - `required` Site ID
  
- Return
  
  Returns the Site object of the specified site number

```json
      {
        "id": 100001,     // Site number
        "company": "comm100", // Company name
        "website": "https://www.comm100.com", // Company website address
        "agents": 20, // Number of seats
        "country": "China", // Country
        "timezone": "GMT+08:00",  // Site default time zone
        "contact": {  // Contact information of the site, generally the information of the registrant
          "firstName": "allon", // Contact's first name
          "lastName": "lu",     // Contact's last name
          "email": "allon.lu@comm100.com",  // Contact's email address
          "phone": "+08618888888888",       // Contact's phone number
        },
        "activated": true, // Whether the site is activated
        "disabled": false, // Is the site disabled
        "status" : "trial", // Trial indicates that the site is in the trial period, if it is paid, it is paying
      }
```

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSwYcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnngtbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" https://hosted.comm100.com/partnerwebapi/api/v2/partner/sites/6000000
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
    "createTime": "2018-08-08T02:24:19.887"
}
```

### Get Sites

  `GET /api/v2/partner/sites?keywords=comm100`

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
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSwYcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnngtbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" https://hosted.comm100.com/partnerwebapi/api/v2/partner/sites
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
            "createTime": "2018-08-08T02:24:19.887"
        },
        ...
    ]
}
```

### Create Site

  `POST /api/v2/partner/sites`

- Parameters `JSON`

  - `email` - `required` User email of the registered site, also email for the registration site contact
  - `password` - `required` Register user password for the site
  - `firstName` - `required` The first name of the user who registered the site, also the first name of the registered site contact
  - `lastName` - `required` The last name of the user who registered the site, also the last name of the registered site contact
  - `phone` - `optional` The user phone of the registered site, also the phone number of the registered site contact
  - `company` - `optional` Registered site's company
  - `website` - `optional` Register site's website
  - `country` - `optional` Register site's country
  - `timezone` - `optional` Registered site's default time zone

- Return

  Return the created Site object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSwYcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnngtbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" -H "content-type:application/json" -X POST -d "{"password": "123456", "agents": 6, "contact": {"firstName": "test", "lastName": "comm100", "email": "test1@comm100.com", "phone": "123456"}, "company": "comm100", "website": "www.comm100.com", "fax": """disabled": false, "createTime": "2018-08-08T02:24:19.887"}" https://hosted.comm100.com/partnerwebapi/api/v2/partner/sites
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
    "createTime": "2018-08-16T05:48:24.157"
}
```

### Update a Site

  `PUT /api/v2/partner/sites/{site_id}`

- Parameters

  - `site_id` - `required` Site id

  - `JSON Data`

    - `activated` - `optional` true/false, whether the site has been activated
    - `disabled` - `optional` true/false, whether the site has been disabled
    - `company` - `optional` Site's company
    - `website` - `optional` Site's website
    - `country` - `optional` Site's country
    - `timezone` - `optional` Site's default time zone
    - `contact.firstName` - `optional` site contact's first name
    - `contact.lastName` - `optional` Site contact's last name
    - `contact.email` - `optional` Site contact's email
    - `contact.phone` - `optional` Site contact's phone number

- Return

  Return the modified Site object

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSwYcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnngtbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" -H "content-type:application/json" -X POST -d "{"password": "123456", "agents": 6, "contact": {"firstName": "test", "lastName": "comm100", "email": "test2@comm100.com", "phone": "123456"}, "company": "comm100", "website": "www.comm100.com", "fax": """disabled": false, "createTime": "2018-08-08T02:24:19.887"}" https://hosted.comm100.com/partnerwebapi/api/v2/partner/sites
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
    "createTime": "2018-08-16T05:48:24.157"
}
```

### Pay a site

  `PUT /api/v2/partner/sites/{site_id}/paying`

- Parameters

  - `site_id` - `required` Site id
  
- Return
  
  Status: 200 OK

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer uUR94EXGGmOazl2-ZTjmdS_LXowa5ed0uD3f4KXkwt-uuU1H-srQbJpFxdVo1rywxm65GSwYcmgNpXh7gVZX-DKcqaeUElPN9r5sj0gqsTb62qu5uOKmM-O0DI7GkiPGKcODzIO9dp0u-aY-rIjaU2iG5VctY4mTo_UVEQnngtbQeqLvYPQbT_gun6dWv8irWK098ceHuc_gMpHTUzkJdzdJmRnxQTYTeVjgeazvaLQ" -X PUT -d "site_id=6000012" https://hosted.comm100.com/partnerwebapi/api/v2/partner/sites/6000012/paying
```

  Sample response:

```json
Status: 200 OK
```
