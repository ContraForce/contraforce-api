# List Incidents 
List incidents endpoint allows you to retrieve list of the incidents in your tenant or any of your managed customer tenants.

This document covers the following topics:
- [List Incidents](#list-incidents)
  - [List Incidents Request](#list-incidents-request)
  - [Parameters](#parameters)
    - [Retrieve latest 10 incidents in the last week](#retrieve-latest-10-incidents-in-the-last-week)
    - [Retrieve all the incidents of January 2023](#retrieve-all-the-incidents-of-january-2023)
  - [Response](#response)
    - [Incidents List Object](#incidents-list-object)
    - [Sample response](#sample-response)
  - [Demo Request and Response](#demo-request-and-response)


> List incidents endpoint is authenticated and an API key is required to access the resources. 
> Check out the [Authentication section in the ContraForce API Overview](https://github.com/ContraForce/contraforce-api/tree/main/Docs#authentication-for-the-contraforce-partner-api) to learn more.

## List Incidents Request
To list all the incidents in your tenant or any of your managed customer's tenant
 
![](https://img.shields.io/badge/HTTP-GET-green)

``` HTTP
 GET 
 https://portal.contraforce.com/api/beta/partners/incidents?tenantId=[TARGET_TENANT_ID]
```
Not all the incidents are being retrieved at once, when you send the request only top 50 incidents will be retrieved with a token that you can send in the parameters to retrieve the next chunk and so on. 

## Parameters 
The list incidents *GET* accepts set of parameters for filtering, pagination, and or limiting the number of objects retrieved. 
The following table shows all the parameters accepted by the endpoint with its default values: 

|Parameter | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| tenantId | The tenant id of the your organization or any of your managed customer tenants | ?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73 | None | GUID | Yes |
| take | Limits the number of incident objects retrieved at a time.  | ../incidents?take=10 | 50 | int (1, 2, ..1000) | No |
| query | Search query to filter the incidents by various properties (number, title, description) | .../incidents?query=access fro | None | (string) text | No |
| startDate | Define the oldest date of the incidents | /incidents?startDate=2023-02-1 | 24 Hours back | yyyy-MM-ddTHH:mm:ss.fffZ (2023-02-03T16:34:46.5737663Z) | No |
| endDate| Define the newest (maximum) date of the incidents | /incidents?endDate=2023-02-10 | Current date/time | yyyy-MM-ddTHH:mm:ss.fffZ (2023-02-10T16:34:46.5737663Z) | No |
| token | Define the token of the next page (the value retrieve in the response when the maximum limits of incidents reached, so you pass the token from the response to retrieve the next chunk of data for the same filter applied) | ../incidents?token=FDDdfa43yy4ejlkas5r43... | None | (string) text | No |


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
|--|--|--|
| value | Object represents a page contains list of incidents and a next page token if it's there | [Incidents List Object](#incidents-list-object) | 
| message | The status of the request or the error message in case of request failure | Incidents have been retrieved successfully! |
AAAAABBBCCCEDFASDF.....|
| isSuccess | It has the value of true | true |

![](https://img.shields.io/badge/Response-400-red)

In case of something is not correct you will receive an object similar to the one above but without the ***value*** and in this case you can look at the ***message*** property to know more about the error.   

| Property | Description | Sample Value |
|--|--|--|
| message | Description of the error and what went wrong | Next page token is invalid |
| isSuccess | false | false |

![](https://img.shields.io/badge/Response-401-red)

In case of unauthenticated request, you will receive the status response **401**

![](https://img.shields.io/badge/Response-404-red)

When providing an invalid ***tenantId*** you will receive the status response **404**

### Incidents List Object 

The ***value*** property of the full response contains an object represents a page of incidents, it contains the following: 

| Property | Description | Sample Value |
|--|--|--|
| nextPageLink | Token that represents the next set of incidents to be retrieved (It can be send with the ***token*** parameter in another request) | FJOEOBrklwmc8cjowpxzlwqcoeaabkpelxn43DA... |
| incidents | The array of the incidents retrieved | [ [Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md) ]

Following is a sample
``` JSON 
{
        "nextPageLink": "FJOEOBrklwmc8cjowpxzlwqcoeaabkpelxn43DA...",
        "incidents": [
            {
                "id": "2b460d82-ffd3-2a6e-a513-ded250099e33",
                "name": null,
                "title": "File with Extension 'exe' Downloaded from SharePoint - Office 365",
                "description": "The user 'test@example.com' uploaded an executable file with either of the extensions  'exe', 'inf', 'gzip', 'cmd', 'bat' to ....",
                "number": 111,
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
            }
            ... More Incidents here 
        ]
    }
```

### Sample response 

To know more details about the Incident object please referee to [Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md)

``` JSON
{
	"value": {
        "nextPageLink": "FJOEOBrklwmc8cjowpxzlwqcoeaabkpelxn43DA...",
        "incidents": [
            {
                "id": "2b460d82-ffd3-2a6e-a513-fggffgd4343543",
                "name": null,
                "title": "File with Extension 'exe' Downloaded from SharePoint - Office 365",
                "description": "The user 'test@example.com' uploaded an executable file with either of the extensions  'exe', 'inf', 'gzip', 'cmd', 'bat' to ....",
                "number": 111,
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
                "id": "2b460d82-ffd3-2a6e-a513-fggffgd4343543",
                "name": null,
                "title": "File with Extension 'exe' Downloaded from SharePoint - Office 365",
                "description": "The user 'test@example.com' uploaded an executable file with either of the extensions  'exe', 'inf', 'gzip', 'cmd', 'bat' to ....",
                "number": 111,
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
            }
        ]
    }
	"message": "2 Incidents have been retrieved successfully",
	"isSuccess": true
}
```

## Demo Request and Response 
ContraForce Parnter API allows you to test the call quickly using a demo endpoints. 
In the development environment you can use the demo enpoints so the parameters passed won't be vaildated and you will be retrieving a valid response with sample data everytime even if there was no data for the time period or the passed query, that makes your development experience faster and smoother. 

> The demo request also requires an API Key, but any parameters passed will be ignored in the result, as you will always get the same result. 

``` HTTP
GET /api/beta/partners/demo/incidents?
```

