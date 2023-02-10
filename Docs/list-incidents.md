# List Incidents 
List incidents endpoint allows you to retrieve list of the incidents in your tenant or any of your managed customer tenants.

This document covers the following topics:
- [List Incidents Request](#list-incident-requests)
- [Parameters](#authentication)
- [Response](#authentication)
- [Demo Request and Response](#authentication)

> List incidents endpoint is authenticated and an API key is required to access the resources. 
> Check out the [Authentication section in the ContraForce API Overview](https://github.com/ContraForce/contraforce-api/tree/main/Docs#authentication-for-the-contraforce-partner-api) to learn more.

## List Incidents Request
To list all the incidents in your tenant or any of your managed customer's tenant
 
![](https://img.shields.io/badge/HTTP-GET-green)

``` HTTP
 GET https://portal.contraforce.com/api/beta/partners/incidents?tenantId=[TARGET_TENANT_ID]
```
Not all the incidents are being retrieved at once, when you send the request only top 50 incidents will be retrieved with a token that you can send in the parameters to retrieve the next chunk and so on. 

## Parameters 
The list incidents *GET* accepts set of parameters for filtering, pagination, and or limiting the number of objects retrieved. 
The following table shows all the parameters accepted by the endpoint with its default values: 
|Parameter | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| tenantId | The tenant id of the your organization or any of your managed customer tenants | ?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73 | None | GUID | Yes
| take | Limits the number of incident objects retrieved at a time.  | ../incidents?take=10 | 50 | int (1, 2, ..1000) | No
| query | Search query to filter the incidents by various properties (number, title, description) | .../incidents?query=access fro | None | (string) text | No
| startDate | Define the oldest date of the incidents | /incidents?startDate=2023-02-1 | 24 Hours back | yyyy-MM-ddTHH:mm:ss.fffZ (2023-02-03T16:34:46.5737663Z) | No
| endDate| Define the newest (maximum) date of the incidents | /incidents?endDate=2023-02-10 | Current date/time | yyyy-MM-ddTHH:mm:ss.fffZ (2023-02-10T16:34:46.5737663Z) | No
| token | Define the token of the next page (the value retrieve in the response when the maximum limits of incidents reached, so you pass the token from the response to retrieve the next chunk of data for the same filter applied) | ../incidents?token=FDDdfa43yy4ejlkas5r43... | None | (string) text | No

Following shows sample requests with a combination of the mentioned parameters above: 
### Retrieve latest 10 incidents in the last week 
``` HTTP
GET /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73&take=10&startDate=2023-02-03
```
As of the date Feb 10th, 2023, the start date provided is 7 days back. 
### Retrieve all the incidents of January 2023 
``` HTTP
GET /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73&take=10&startDate=2023-01-01&endDate=2023-01-31
```
If the number of incidents are more than 50 then a ***nextPageToken*** will be retrieved in the response and you can use it to retrieve the next page as shown 
``` HTTP
GET /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73&take=10&startDate=2023-01-01&endDate=2023-01-31&token=AAAAABBBBCCCC...
```
## Response 



![](https://img.shields.io/badge/Response-200-green)

In case the request processed successfully, the response of the list incidents request represents an object that contains the following in a JSON format:
| Property | Description | Sample Value |
|--|--|--|--|
| Value | Array of incident object | | 
| message | The status of the request or the error message in case of request failure | Incidents have been retrieved successfully! |
| nextPageToken | (Nullable) only has a value if more data is available for the same request, so you can use the value provided to send another request with a ***token*** parameter to retrieve the rest | AAAAABBBCCCEDFASDF.....|
| isSuccess | It has the value of true | true

![](https://img.shields.io/badge/Response-400-red)

In case of something is not correct you will receive an object similar to the one above but without the ***value*** and in this case you can look at the ***message*** property to know more about the error.   
| Property | Description | Sample Value |
|--|--|--|--|
| message | Description of the error and what went wrong | Next page token is invalid |
| isSuccess | false | false

![](https://img.shields.io/badge/Response-401-red)

In case of unauthenticated request, you will receive the status response **401**

![](https://img.shields.io/badge/Response-404-red)
When providing an invalid ***tenantId*** you will receive the status response **404**

### Sample response 
``` JSON
{

	"value": {

	"nextPageLink": null,

	"previousPageLink": null,

	"incidents": [

	{

	"id": "2b460d82-ffd3-2a6e-a513-ded250099e33",

	"name": null,

	"title": "File with Extension 'exe' Downloaded from SharePoint - Office 365",

	"description": "",

	"number": 915,

	"type": null,

	"lastModificationTime": "2023-02-09T10:38:47.0111424Z",

	"creationTime": "2023-02-09T10:38:47.0111424Z",

	"lastActivityTime": "2023-02-09T09:31:22Z",

	"severity": 4,

	"classification": null,

	"comment": null,

	"classificationReason": null,

	"classificationComment": null,

	"tactics": null,

	"ruleIds": null,

	"alertProductNames": null,

	"user": {

	"id": null,

	"displayName": null,

	"email": null

	},

	"isAssigned": true,

	"productId": null,

	"status": 2,

	"alertsCount": 1

	},

	{

	"id": "cc976c97-2ae0-b8d1-2752-f8c2c20d3c77",

	"name": null,

	"title": "New Executable Uploaded to SharePoint or OneDrive - Office 365",

	"description": "The user ",

	"number": 914,

	"type": null,

	"lastModificationTime": "2023-02-09T09:36:01.884117Z",

	"creationTime": "2023-02-09T09:36:01.884117Z",

	"lastActivityTime": "2023-02-09T09:28:13Z",

	"severity": 2,

	"classification": null,

	"comment": null,

	"classificationReason": null,

	"classificationComment": null,

	"tactics": null,

	"ruleIds": null,

	"alertProductNames": null,

	"user": {

	"id": null,

	"displayName": null,

	"email": null

	},

	"isAssigned": true,

	"productId": null,

	"status": 2,

	"alertsCount": 1

	},
	...

		}

	]

	},

	"message": "50 have been retrieved successfully",

	"isSuccess": true

}
```

## ContraForce Partner API Endpoints
Following links provide a detailed documentation about each available endpoint in the current beta version of the ContraForce Partner API
- List Incidents 
- Get Incident by Id
- List Incident Entities
- List Incident Evidence