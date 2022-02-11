# Partner API Specification v1.0.0

API Specification

History

| Version # | Date | Author            | Reviewed By               | Affected Sections & Summary of Change |
| --------- | ---- | ----------------- | ------------------------- | ------------------------------------- |
| v1        |      | Nitesh and Sujith | Sujith, Abhishek and Arul | Added partner subscription APIs       |

**Overview 4**

Audience 4

Getting Started 4

Environment Details 4

**API Conventions 5**

REST URI 5

Authentication 5

HTTP Operations 5

Common Request Parameters 6

Response Format 6

Common Responses 6

**Subscription Service 7**

Create Subscription 7

Request: 7

Response: 8

Examples: 9

Update Subscription 11

Request: 11

Response: 12

Examples: 12

Delete Subscription API 15

Request: 15

Response: 15

Examples: 16

Get Subscription API 18

Request 18

Response 18

Examples: 19

**Appendix 21**

Device Identifier 21

Subscription Status 21

### Overview <a href="#_ie19zzn5halk" id="_ie19zzn5halk"></a>

Viewlift Platform supports creating seamless digital experiences for your brand to reach every device and manage it all with one centralized platform. Viewlift Partners can access some of the APIs for user onboarding, deboarding, managing subscriptions, profile and entitlements exclusively via Partner Integration APIs.

#### Audience <a href="#_v9xiqvaxc2lv" id="_v9xiqvaxc2lv"></a>

This document is intended for software developers, architects and technologists planning or creating applications using the Viewlift Platform.

#### Getting Started <a href="#_30nei3apn1sz" id="_30nei3apn1sz"></a>

Before getting started you need the following.

Partner APIs are only accessible from a list of Allowed IP addresses. You need to send the IP address range (CIDR) to [Viewlift Support](mailto:techsupport@viewlift.com) in order to successfully communicate with the platform APIs.

The Viewlift Support team will provide you with a partner API key once the IP address has been added to the allowed list.

If you need certificate based authentication please reach out to support for the documentation on steps to be followed.

#### Environment Details <a href="#_kzpldl96hpjs" id="_kzpldl96hpjs"></a>

Apart from the production environment we provide a staging environment for testing and certification purposes.

| Environment | Domain                           |
| ----------- | -------------------------------- |
| Prod        | prod-api-partner.viewlift.com    |
| Staging     | staging-api-partner.viewlift.com |

### API Conventions <a href="#_i7dd0x175fi0" id="_i7dd0x175fi0"></a>

Viewlift Partner API provides Restful resource oriented application programming interface that developers can use to work with different platform services. Developers can use the preferred programming language to access the APIs using HTTP requests.

### REST URI <a href="#_vwkziukdh38j" id="_vwkziukdh38j"></a>

[https://{baseURI}/{version}/{service}/{resource}](https://baseuri/%7Bversion%7D/%7Bservice%7D/%7Bresource%7D)}

{baseURI} - The base URI will be different for each environment. Please look at section Environment Details

{service} - The name of the Viewlift Platform service. A set of resources are logically grouped under a specific service. Resources from the subscription service are exposed at this point.

{version} - The version of the API. We ensure that any changes to a specific version made are backward compatible. When there are non backward compatible changes to the APIs we will need you to move to higher versions to use those.

The versions should be specified in the format v1, v2, v3 etc.

Example:

[https://prod-api-partner.viewlift.com/v1/subscription](https://prod-api-partner.viewlift.com/subscription/v1)

[https://prod-api-partner.viewlift.com/v1/subscription/plans](https://prod-api-partner.viewlift.com/v1/subscription/plans)

### Authentication <a href="#_bxsetnquso9i" id="_bxsetnquso9i"></a>

1. We recommend our partners to provide us with a set of ip addresses in order to allow the given IPs access to our APIs.
2. In case of any queries or any suggestions, please contact techsupport@viewlift.

### HTTP Operations <a href="#_2uspncvzyioc" id="_2uspncvzyioc"></a>

The different operations on resources are mapped to corresponding HTTP operations. Each operation has specific functions and characteristics as explained below.

GET - All safe, idempotent cacheable requests to retrieve the data from the platform.

POST - Non-Idempotent request which will result in the creation of a new resource or updating an existing resource

PUT - Idempotent request which will result in the updating an existing resource

DELETE - Idempotent request to delete or inactivate an existing resource.

### Common Request Parameters <a href="#_cithkgsgbeam" id="_cithkgsgbeam"></a>

| **Param**    | **Type** | **Description**                 | **Required** |
| ------------ | -------- | ------------------------------- | ------------ |
| Accept       | Header   | application/json                | Y            |
| x-api-key    | Header   | Success - New Resource created. | Y            |
| Content-Type | Header   | application/json                | Y            |
| site         | Query    | Viewlift provided identifier    | Y            |
| partner      | Query    | Name of the partner             | Y            |

### Response Format <a href="#_hijjheft67cv" id="_hijjheft67cv"></a>

All responses will be JSON. The content type should be specified as application/json

### Common Responses <a href="#_i5zyywp3zyz8" id="_i5zyywp3zyz8"></a>

Response Status Codes:

| Code | Description                       |
| ---- | --------------------------------- |
| 200  | Success                           |
| 201  | Success - New Resource created.   |
| 400  | Failure - Invalid request         |
| 401  | Unauthorized                      |
| 403  | X-api-key is incorrect. Forbidden |
| 412  | Precondition check failed.        |
| 500  | Failure - Internal Server Error   |

### Subscription Service <a href="#_61apzs3pf9k4" id="_61apzs3pf9k4"></a>

### Create Subscription <a href="#_xo7ngtv6y6zx" id="_xo7ngtv6y6zx"></a>

URL: /subscription/{resource}

Http method: POST

#### Request: <a href="#_7gznt6dnt0bq" id="_7gznt6dnt0bq"></a>

Headers:

Provided in the common request Headers

Query Parameters:

Provided in the common request params.

Body:

| **Parameter**  | **Datatype** | **Description**                                                                                                                    | **Required**                                                    |
| -------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| phoneNumber    | String       | phone number of the user                                                                                                           | YES if One Time Password Login is enabled in Viewlift Platform. |
| email          | String       | Email of the user                                                                                                                  | Yes if phoneNumber is not provided                              |
| planCode       | String       | Plan code of the plan applied to the user                                                                                          | YES                                                             |
| startDate      | String       | Specify the Start date of the user subscription in UTC                                                                             | NO, default will be current date                                |
| endDate        | String       | Specify End date of the user subscription in UTC                                                                                   | NO, default will be plan duration added to current date         |
| device         | String       | Device using which user subscribed for our subscription on partner platform. This should be one of the values in Device Identifier | NO, default will be web\_browser                                |
| externalUserId | String       | Unique identifier used in the partner system to identify a user/account.                                                           | YES                                                             |
| password       | String       | The password for the user registration along with email.                                                                           | Only if the email/password login is the primary option.         |

#### Response: <a href="#_d2at3eodvths" id="_d2at3eodvths"></a>

Success:

| Parameter   | Datatype | Description                                                                        |
| ----------- | -------- | ---------------------------------------------------------------------------------- |
| phoneNumber | String   | phone number of the user                                                           |
| email       | String   | Email of the user                                                                  |
| planCode    | String   | Plan code of the plan applied to the user                                          |
| id          | String   | Unique identifier of a user at viewlift server                                     |
| requestId   | String   | Unique Identifier assigned to a partner’s request                                  |
| startDate   | String   | Start date of the user subscription                                                |
| endDate     | String   | End date of the user subscription                                                  |
| status      | String   | Subscription status of the user. The status will be one of the Subscription Status |

Error:

| Parameter | Datatype | Description              |
| --------- | -------- | ------------------------ |
| error     | String   | Description of the error |

#### Examples: <a href="#_f9pnhk9kpr6j" id="_f9pnhk9kpr6j"></a>

Request:

| <p>curl --location --request POST 'https://staging-api-partner.viewlift.com/subscription/subscribe?site=xyz&#x26;partner=ABC' \</p><p>--header 'x-api-key: JdfefBdsREfdsgkSBbok02k6RLRzI23wauoSfC3FP7u' \</p><p>--header 'Content-Type: application/json' \</p><p>--data-raw '{</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>"device": "android_phone",</p><p>"planCode": "configuredPlanCode",</p><p>"endDate": "2020-10-04T11:22:23.958Z",</p><p>"startDate": "2020-09-04T11:23:42.958Z",</p><p>"externalUserId": "123456722"</p><p>}'</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Success): Status Code 201

| <p>{</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>"planCode": "configuredPlanCode",</p><p>“id”: “1234-XXXXXXXXXX- 45678”,</p><p>“requestId”: “4531-XXXXXXXXXXX-342422”,</p><p>“startDate”: “2020-09-04T11:23:42.958Z”,</p><p>“endDate”: “2020-10-04T11:22:23.958Z”,</p><p>"status": "COMPLETED"</p><p>}</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Success): Status Code 200

| <p>{</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>"planCode": "configuredPlanCode",</p><p>"id": "1234-XXXXXXXXXX- 45678",</p><p>"requestId": "4531-XXXXXXXXXXX-342422",</p><p>"startDate": "2020-09-04T11:23:42.958Z",</p><p>"endDate": "2020-10-04T11:23:42.958Z",</p><p>"status": "COMPLETED"</p><p>}</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 400

| <p>{<br>"error”: “Invalid Request. Please try again.”</p><p>}</p> |
| ----------------------------------------------------------------- |

Response Body (Failure): Status Code 412

| <p>{<br>"error”: “Precondition check failed. Mandatory parameters are missing. Please try again.”</p><p>}</p> |
| ------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 500

| <p>{<br>"error”: “Something went wrong. Please contact viewlift technical support (<a href="mailto:techsupport@viewlift.com">techsupport@viewlift.com</a>) for resolution.”</p><p>}</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### &#x20;<a href="#_c4hi31ncvxo5" id="_c4hi31ncvxo5"></a>

### Update Subscription <a href="#_8bd6szs2qklm" id="_8bd6szs2qklm"></a>

URL: /subscription/{resource}

Http method: PUT

#### Request: <a href="#_8s4vmxb9ronn" id="_8s4vmxb9ronn"></a>

Headers:

Provided in the common request Headers

Query Parameters:

Provided in the common request params.

Body:

| **Parameter**  | **Datatype** | **Description**                                                          | **Required**                                                                                                                          |
| -------------- | ------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| phoneNumber    | String       | phone number of the user                                                 | YES if One Time Password Login is enabled in Viewlift Platform.                                                                       |
| email          | String       | Email of the user                                                        | <p>Yes if phoneNumber is not provided</p><p>If phoneNumber and email are provided, phoneNumber will be used to identify the user.</p> |
| planCode       | String       | Plan code of the plan applied to the user                                | YES                                                                                                                                   |
| startDate      | String       | Specify the Start date of the user subscription in UTC                   | NO, default will be set to current date                                                                                               |
| endDate        | String       | Specify End date of the user subscription in UTC                         | NO, default will be plan duration added to current date                                                                               |
| id             | String       | Unique identifier of a user at viewlift server                           | YES, if phoneNumber is not provided.                                                                                                  |
| externalUserId | String       | Unique identifier used in the partner system to identify a user/account. | YES                                                                                                                                   |

#### Response: <a href="#_c6250e1oy7ul" id="_c6250e1oy7ul"></a>

Success:

| Parameter   | Datatype | Description                                                                        |
| ----------- | -------- | ---------------------------------------------------------------------------------- |
| phoneNumber | String   | phone number of the user                                                           |
| email       | String   | Email of the user                                                                  |
| planCode    | String   | Plan code of the plan applied to the user                                          |
| id          | String   | Unique identifier of a user at viewlift server                                     |
| requestId   | String   | Unique Identifier assigned to a partner’s request                                  |
| startDate   | String   | Start date of the user subscription                                                |
| endDate     | String   | End date of the user subscription                                                  |
| status      | String   | Subscription status of the user. The status will be one of the Subscription Status |

Error:

| Parameter | Datatype | Description              |
| --------- | -------- | ------------------------ |
| error     | String   | Description of the error |

#### &#x20;<a href="#_j9nvn1yfeui" id="_j9nvn1yfeui"></a>

#### Examples: <a href="#_617ema3r28l5" id="_617ema3r28l5"></a>

Request:

| <p>curl --location --request PUT 'https://staging-api-partner.viewlift.com/subscription/subscribe?site=xyz&#x26;partner=ABC' \</p><p>--header 'x-api-key: JdfefBdsREfdsgkSBbok02k6RLRzI23wauoSfC3FP7u' \</p><p>--header 'Content-Type: application/json' \</p><p>--data-raw '{</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>"planCode": "configuredPlanCode",</p><p>"endDate": "2020-10-04T11:22:23.456Z",</p><p>"startDate": "2020-09-04T11:23:42.456Z",</p><p>"externalUserId": "123456722"</p><p>}'</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Success): Status Code 201

| <p>{</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>"planCode": "configuredPlanCode",</p><p>“id”: “1234-XXXXXXXXXX- 45678”,</p><p>“requestId”: “4531-XXXXXXXXXXX-342422”,</p><p>“startDate”: “2020-09-04T11:23:42.958Z”,</p><p>“endDate”: “2020-10-04T11:23:42.958Z”,</p><p>"status": "COMPLETED"</p><p>}</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Success): Status Code 200

| <p>{</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>"planCode": "configuredPlanCode",</p><p>"id": "1234-XXXXXXXXXX- 45678",</p><p>"requestId": "4531-XXXXXXXXXXX-342422",</p><p>"startDate": "2020-09-04T11:23:42.958Z",</p><p>"endDate": "2020-10-04T11:23:42.958Z",</p><p>"status": "COMPLETED"</p><p>}</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 400

| <p>{<br>"error”: “Invalid Request. Please try again.”</p><p>}</p> |
| ----------------------------------------------------------------- |

Response Body (Failure): Status Code 412

| <p>{<br>"error”: “Precondition check failed. Mandatory parameters are missing. Please try again.”</p><p>}</p> |
| ------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 500

| <p>{<br>"error”: “Something went wrong. Please contact viewlift technical support (<a href="mailto:techsupport@viewlift.com">techsupport@viewlift.com</a>) for resolution.”</p><p>}</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### &#x20;<a href="#_a973k3lei22d" id="_a973k3lei22d"></a>

### Delete Subscription API <a href="#_w0oxy5lmwo91" id="_w0oxy5lmwo91"></a>

URL: /subscription

Http method: DELETE

#### Request: <a href="#_f84hbxl262wv" id="_f84hbxl262wv"></a>

Headers:

Provided in the common request headers.

Query Parameters:

Please provide the following parameters in addition to what is specified in the common request params.

| Parameter      | Datatype | Description                                                                 | Whether mandatory                      |
| -------------- | -------- | --------------------------------------------------------------------------- | -------------------------------------- |
| id             | String   | Unique identifier of the user in viewlift platform                          | YES if externalUserId is not provided. |
| phoneNumber    | String   | Phone number of the user                                                    | YES, if id is not provided             |
| externalUserId | String   | The user id or account id used by the partner to identify the user account. | Yes if id is not provided.             |

Body: No request body

#### Response: <a href="#_4391ksble57c" id="_4391ksble57c"></a>

Success:

| Parameter      | Datatype | Description                                                                 |
| -------------- | -------- | --------------------------------------------------------------------------- |
| id             | String   | Unique identifier of a user at viewlift server                              |
| externalUserId | String   | The user id or account id used by the partner to identify the user account. |
| status         | String   | Current status of the subscription                                          |

Error:

| Parameter | Datatype | Description              |
| --------- | -------- | ------------------------ |
| error     | String   | Description of the error |

#### &#x20;<a href="#_xb5irnf02sry" id="_xb5irnf02sry"></a>

#### Examples: <a href="#_3mwaomulkfa6" id="_3mwaomulkfa6"></a>

Request

| <p>curl --location --request DELETE 'https://staging-api-partner.viewlift.com/subscription/subscribe?site=xyz&#x26;id=d5d276fc-f82b-4e21-b1e9-bdddef5e8e7e&#x26;partner=ABC \</p><p>--header 'x-api-key: JdfefBdsREfdsgkSBbok02k6RLRzI23wauoSfC3FP7u' \</p><p>--header 'Content-Type: application/json'</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Success): Status Code 200

| <p>{</p><p>"subscriptionId": "1234-XXXXXXXXXX- 45678",</p><p>"subscriptionStatus": "CANCELLED"</p><p>}</p> |
| ---------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 400

| <p>{<br>"error”: “Invalid Request. Please try again.”</p><p>}</p> |
| ----------------------------------------------------------------- |

Response Body (Failure): Status Code 412

| <p>{<br>"error”: “Precondition check failed. Mandatory parameters are missing. Please try again.”</p><p>}</p> |
| ------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 500

| <p>{<br>"error”: “Something went wrong. Please contact viewlift technical support (<a href="mailto:techsupport@viewlift.com">techsupport@viewlift.com</a>) for resolution.”</p><p>}</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### &#x20;<a href="#_nbdebr13jlpp" id="_nbdebr13jlpp"></a>

### &#x20;<a href="#_9r6s4uldl5wj" id="_9r6s4uldl5wj"></a>

### &#x20;<a href="#_pdpri1yl3942" id="_pdpri1yl3942"></a>

### &#x20;<a href="#_3zqwwa2caka8" id="_3zqwwa2caka8"></a>

### &#x20;<a href="#_v0erpy9pd58x" id="_v0erpy9pd58x"></a>

### Get Subscription API <a href="#_fv3aa68d4h1d" id="_fv3aa68d4h1d"></a>

URL: /subscription

Http method: GET

#### Request <a href="#_ffygj9ti5p70" id="_ffygj9ti5p70"></a>

Headers:

Provided in the common request headers.

Query Parameters:

Provided in the common request params.

| Parameter      | Datatype | Description                                                                 | Whether mandatory                     |
| -------------- | -------- | --------------------------------------------------------------------------- | ------------------------------------- |
| id             | String   | Unique identifier of a user at viewlift server                              | YES if externalUserId is not provided |
| phoneNumber    | String   | Phone number of the user                                                    | Yes if id is not provided             |
| externalUserId | String   | The user id or account id used by the partner to identify the user account. | Yes if id is not provided.            |

#### Response <a href="#_pfmi52q0ipqm" id="_pfmi52q0ipqm"></a>

Success:

| Parameter   | Datatype | Description                                                 |
| ----------- | -------- | ----------------------------------------------------------- |
| id          | String   | Unique identifier of a user at viewlift server              |
| phoneNumber | String   | Phone number of the user at viewlift server                 |
| planCode    | String   | Plan code of the plan subscribed by user in viewlift server |
| startDate   | String   | Start date of the user subscription                         |
| endDate     | String   | End date of the user subscription                           |
| email       | String   | Email of the user in viewlift server                        |
| status      | String   | Subscription status of the user at viewlift server          |

\
Error:

| Parameter | Datatype | Description              |
| --------- | -------- | ------------------------ |
| error     | String   | Description of the error |

#### &#x20;<a href="#_igw6k5b82x" id="_igw6k5b82x"></a>

#### Examples: <a href="#_j8u0l0gl0o7a" id="_j8u0l0gl0o7a"></a>

Request:

| <p>curl --location --request GET 'https://staging-api-partner.viewlift.com/subscription/user?site=xyz&#x26;id=e280c222-768b-4daf-9c23-9741365462c0&#x26;partner=ABC' \</p><p>--header 'x-api-key: JdfefBdsREfdsgkSBbok02k6RLRzI23wauoSfC3FP7u' \</p><p>--header 'Content-Type: application/json'</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Success): Status Code 200

| <p>{</p><p>“id”: “1234-XXXXXXXXXX- 45678”,</p><p>"phoneNumber": "+91XXXXXXXXXX",</p><p>“planCode”: “configuredPlanCode”,</p><p>"email”: “<a href="mailto:test1@xyz.com">test1@xyz.com</a>”,</p><p>“startDate”: “2020-10-26T14:12:10.476Z”,</p><p>“endDate”: “2020-11-26T14:12:10.476Z”,</p><p>"status": "CANCELLED"</p><p>}</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 400

| <p>{<br>"error”: “Invalid Request. Please try again.”</p><p>}</p> |
| ----------------------------------------------------------------- |

Response Body (Failure): Status Code 412

| <p>{<br>"error”: “Precondition check failed. Mandatory parameters are missing. Please try again.”</p><p>}</p> |
| ------------------------------------------------------------------------------------------------------------- |

Response Body (Failure): Status Code 500

| <p>{<br>"error”: “Something went wrong. Please try again later.”</p><p>}</p> |
| ---------------------------------------------------------------------------- |

### &#x20;<a href="#_8prn0zepqxji" id="_8prn0zepqxji"></a>

### &#x20;<a href="#_34xshv4i72q" id="_34xshv4i72q"></a>

### Appendix <a href="#_eb5ggehdmzib" id="_eb5ggehdmzib"></a>

### Device Identifier <a href="#_drryy3pg5rtn" id="_drryy3pg5rtn"></a>

| ios\_phone      |
| --------------- |
| web\_browser    |
| android\_phone  |
| jio\_stb        |
| android\_tablet |
| fire\_tv        |
| ios\_ipad       |
| ios\_apple\_tv  |
| roku\_box       |

### Subscription Status <a href="#_uv8qefso72lr" id="_uv8qefso72lr"></a>

| COMPLETED              |
| ---------------------- |
| SUSPENDED              |
| CANCELLED              |
| DEFERRED\_CANCELLATION |
