# Contact

| Object | Path |
| - | - | 
|[Contact](#contact)| `/api/v3/contact/contacts`|
|[Contact Identity](#Contact-Identities)| `/api/v3/contact/contacts/{contactId}/identities`|


<div>

## Contacts

- You need `Manage Contacts` permission to manage contacts.
  - `GET /api/v3/contact/contacts` - Search contacts
  - `GET /api/v3/contact/contacts/{id}` - Get a contact by contact id
  - `PUT /api/v3/contact/contacts/{id}` - Update a contact
  - `POST /api/v3/contact/contacts` - Create a contact
  - `DELETE /api/v3/contact/contacts/{id}` - Remove a contact

<div>

### Model

#### Contact Json Format

 Contact is represented as simple flat JSON objects with the following keys:  

| Name | Type | Description |
| - | - | - |
| `id` | string | read-only, id of contact |
| `name` | string | required, the name of the contact |
| `alias` | string | optional, the alias name of the contact |
| `avatar` | string | optional, the avatar url of the contact |
| `identities` | [identity](#identity)[] | optional, identity array of the contact |
| `description` | string | optional, a small description of the contact |
| `company` | string | optional, the primary company name which this contact belongs to |
| `title` | string | optional, the title of the contact|
| `phoneNumber` | string | optional, telephone number of the contact|
| `faxNumber` | string | optional, fax number of the contact |
| `address` | string | optional, the address of the contact  |
| `city` | string | optional, the city of the contact  |
| `stateOrProvince` | string | optional, the state or province of the contact |
| `country` | string | optional, the country of the contact |
| `postalOrZipCode` | string | optional, the postal or zip code of the contact  |
| `createdTime` | datetime | optional, the time the contact was created |
| `tags` | [tag](#tag)[] | optional, tag array of the contact  |

 ### Identity
| Name | Type | Description | 
| - | - | - |
| `id` | string | read-only, the id of identity |
| `type` | string | required, `emailAddress`, `SSOUserId`, `externalId`, `smsNumber`, `facebookAccount`, `twitterAccount`, `weChatAccount` |
| `value` | string | required, the value of one identity, should be unique |
| `name` | string | required, the name of one identity |
| `avatar` | string | optional, the avatar of one identity |
| `identityInfoUrl` | string | optional, the original identity info url of one identity |

 - Note: We currently only allow one for each type.

</div>
<div>
 
 ### Endpoints

 #### Search contacts

- Max 50 contacts are responded for each request.
- `GET  /api/v3/contact/contacts`

- Query Parameters

      Optional:
    - `pageIndex`: integer, default 1
    - `keywords`: string, search scope includes: name/identity id/identity value/alias 

- Response

    - `contacts`: [Contact](#contact)[]
    - `total`: integer, total number of contacts.
    - `previousPage`: string, next page uri, the first page return null.
    - `nextPage`: string, the last page return null.
    - `currentPage`: string, current page uri.

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/contact/contacts?keywords=comm100
```

  Sample response:

```json
{
    "total": 1,
    "previousPage": "",
    "nextPage": "",
    "nextPage": "?keywords=comm100&pageindex=1",
    "contacts": [
        {
            "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
            "name": "tony",
            "alias": "test comm100",
            "avatar": "",
            "identities": [],
            "description": "test",
            "company": "comm100",
            "title": "",
            "phoneNumber": "",
            "faxNumber": "-1",
            "address": "",
            "city": "",
            "stateOrProvince": "",
            "country": "",
            "postalOrZipCode": "",
            "createdTime": "2019-05-08T10:21:44.403",
            "tags": []
        }
    ]
}
```

#### Get a contact by contact id

`GET  /api/v3/contact/contacts/{id}`

- Path Parameters

  - id: string, id of the contact

- Response

  [Contact](#contact)


#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

  Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "name": "tony",
    "alias": "test comm100",
    "avatar": "",
    "identities": [],
    "description": "test",
    "company": "comm100",
    "title": "",
    "phoneNumber": "",
    "faxNumber": "-1",
    "address": "",
    "city": "",
    "stateOrProvince": "",
    "country": "",
    "postalOrZipCode": "",
    "createdTime": "2019-05-08T10:21:44.403",
    "tags": []
}
```

 #### Create a contact

`POST  /api/v3/contact/contacts`

- Request Parameters 

   [Contact](#contact)

 - Response

   [Contact](#contact)


#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x POST -H "Content-Type: application/json"  
     -d "{"name": 'tony',"alias": 'test comm100',"identities": [{"id": 'ABCD053B-97DB-4E2F-9B7F-664CA3A14951', "type": 'emailAddress', "value": 'test@comm100.com'}]}"    
     https://hosted.comm100.com/api/v3/contact/contacts
```

Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "name": "tony",
    "alias": "test comm100",
    "avatar": "",
    "identities": [
      {
        "id": "ABCD053B-97DB-4E2F-9B7F-664CA3A14951",
        "type": "emailAddress",
        "value": "test@comm100.com",
        "name": "tony",
        "avatar": "",
        "identityInfoUrl": ""
      }
    ],
    "description": "test",
    "company": "comm100",
    "title": "",
    "phoneNumber": "",
    "faxNumber": "-1",
    "address": "",
    "city": "",
    "stateOrProvince": "",
    "country": "",
    "postalOrZipCode": "",
    "createdTime": "2019-05-08T10:21:44.403",
    "tags": []
}
```


 #### Update a contact

`PUT  /api/v3/contact/contacts/{id}`

- Path Parameters

    - id: string, id of the contact

- Request Parameters

  [Contact](#contact)

- Response

  [Contact](#contact)

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"name": 'jason',"alias": 'my alias'}"    
     https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "name": "jason",
    "alias": "my alias",
    "avatar": "",
    "identities": [
      {
        "id": "ABCD053B-97DB-4E2F-9B7F-664CA3A14951",
        "type": "emailAddress",
        "value": "test@comm100.com",
        "name": "tony",
        "avatar": "",
        "identityInfoUrl": ""
      }
    ],
    "description": "test",
    "company": "comm100",
    "title": "",
    "phoneNumber": "",
    "faxNumber": "-1",
    "address": "",
    "city": "",
    "stateOrProvince": "",
    "country": "",
    "postalOrZipCode": "",
    "createdTime": "2019-05-08T10:21:44.403",
    "tags": []
}
```

 #### Delete a contact

 `DELETE  /api/v3/contact/contacts/{id}`

- Path Parameters

    - id: string, id of the contact

- Response

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>


<div>

## Contact Identities

- You need `Manage Contacts` permission to manage contacts identities.
  - `GET  /api/v3/contact/contacts/{contactId}/identities` - Get identities of one contact
  - `GET  /api/v3/contact/contacts/{contactId}/identities/{id}` - Get a identity of one contact
  - `POST  /api/v3/contact/contacts/{contactId}/identities` - Add contact identity
  - `PUT  /api/v3/contact/contacts/{contactId}/identities/{id}` - Update contact identity
  - `DELETE  /api/v3/contact/contacts/{contactId}/identities/{id}` - Delete contact identity

<div>

### Model

 ### Identity Json Format
| Name | Type | Description | 
| - | - | - |
| `id` | string | read-only, the id of identity |
| `type` | string | required, `emailAddress`, `SSOUserId`, `externalId`, `smsNumber`, `facebookAccount`, `twitterAccount`, `weChatAccount` |
| `value` | string | required, the value of one identity, should be unique |
| `name` | string | required, the name of one identity |
| `avatar` | string | required, the avatar of one identity |
| `identityInfoUrl` | string | required, the original identity info url of one identity |

 - Note: We currently only allow one for each type.

</div>
<div>
 
 ### Endpoints

 #### Get contact identities

- `GET  /api/v3/contact/contacts/{contactId}/identities`

- Path Parameters

    - contactId: string, contact id

- Response

    - [Identity](#Identity-Json-Format)[]

#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/contact/contacts/{contactId}/identities
```

  Sample response:

```json
[
    {
        "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
        "type": "emailAddress",
        "value": "test@comm100.com",
        "name": "tony",
        "avatar": "",
        "identityInfoUrl": ""
    }
]
```

#### Get a contact identity

`GET  /api/v3/contact/contacts/{contactId}/identities/{id}`

- Path Parameters

  - contactId: string, id of the contact
  - id: string, id of the identity

- Response

  [Identity](#Identity-Json-Format)


#### Example

  Sample request:

```bash
curl -H "Authorization: Bearer yHShF0rEGY0BcO9TvsjxVRygYl_Ad7-eO3YZ4L1jIrRXUa-_IGHMGHqhRXXd  
        gjvJsYjLlo3i0h_nMmlAeD0eFrW18uFABigYk21hm4n95eEhaWqi6gIiPFddWkoVJTX_jkK_g5me9zwP_RJ  
        SunV7okaqciXPRozb2ita6MjS0b7Vrxcy1_ufHNzOjzaUH7AvOmqtL6zMCuBlPcLeDNG3S74Ui5F2npOyg-  
        j0MdIrtfq8gjqMqwywSJc8Kk8gtXGFzZKDK6qdHzT8TeojT9-M4A"   
     https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities/87EDE98E-9B70-42DC-90A8-1C0FF38775B0
```

  Sample response:

```json
{
    "id": "87EDE98E-9B70-42DC-90A8-1C0FF38775B0",
    "type": "emailAddress",
    "value": "test@comm100.com",
    "name": "tony",
    "avatar": "",
    "identityInfoUrl": ""
}
```

 #### Add a contact identity

`POST  /api/v3/contact/contacts/{contactId}/identities`

- Path Parameters

    - contactId: string, contact id

- Request Parameters

    [Identity](#identity)

- Response

    [Identity](#identity)


#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x POST -H "Content-Type: application/json"  
     -d "{"type": 'smsNumber', "value": '123456789'}"    
     https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities
```

Sample response:

```json
{
    "id": "18266526-49F7-4DB3-937A-CE9902E90BA3",
    "type": "smsNumber",
    "value": "123456789",
    "name": "tony",
    "avatar": "",
    "identityInfoUrl": ""
}
```

 #### Update a contact identity

`PUT  /api/v3/contact/contacts/{contactId}/identities/{id}`

- Path Parameters

    - contactId: string, contact id
    - id: string, contact identity id

- Request Parameters

    - value: string, the value of this identity.

- Response

    [Identity](#identity)


#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x PUT -H "Content-Type: application/json"  
     -d "{"value": '987654321'}"    
     https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities/18266526-49F7-4DB3-937A-CE9902E90BA3
```

Sample response:

```json
{
    "id": "18266526-49F7-4DB3-937A-CE9902E90BA3",
    "type": "smsNumber",
    "value": "987654321",
    "name": "tony",
    "avatar": "",
    "identityInfoUrl": ""  
}
```

 #### Delete a contact identity

 `DELETE  /api/v3/contact/contacts/{contactId}/identities/{id}`

- Path Parameters

    - contactId: string, contact id
    - id: string, contact identity id

- Response

    Status: 200 OK

#### Example

Sample request:

```shell
curl -H "Authorization: Bearer jRhriWa2_yX-z1Y5ABCytDz3CrSBbCK155hRCw85FHTaYzTG9S7ZLHrDzOk  
    -aM-jE_GaqwzEXNzbk_IJw2RgFcrqpSHiSnolFgij80g_tU6f1Tmr6LDCj-puxRgceKMCIlC1PibtzxY2A_BRb  
    fmGPgS0xO6BkGa_TFv2jRVzz-e50P6OaTA05BkaBuEqWVi7FEtqqg33_-kHrMFaiP3HmPumTyB6gqDzDopLn1x  
    UTdSzWolvAD0lL6WYLU_hszD_K-qhJa_xnMKpOnLLEm22kQ"  
     -x DELETE https://hosted.comm100.com/api/v3/contact/contacts/87EDE98E-9B70-42DC-90A8-1C0FF38775B0/identities/18266526-49F7-4DB3-937A-CE9902E90BA3
```

Sample response:

```json
Status: 200 OK
```

</div>
</div>

&#32;
