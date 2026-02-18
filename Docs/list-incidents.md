# List Incidents 
The List Incidents endpoint allows you to retrieve a list of the incidents in your tenant or from any of your managed customer tenants.

This document covers the following topics:
- [List Incidents](#list-incidents)
  - [List Incidents Request](#list-incidents-request)
  - [Parameters](#parameters)
  - [Request Body](#request-body)
    - [Retrieve the Latest Incidents](#retrieve-the-latest-incidents)
    - [Retrieve the most recent 10 incidents from the last 7 days](#retrieve-the-most-recent-10-incidents-from-the-last-7-days)
    - [Retrieve all incidents for a month](#retrieve-all-incidents-for-a-month)
  - [Response](#response)
    - [Incidents List Object](#incidents-list-object)
    - [Sample response](#sample-response)
  - [Demo Request and Response](#demo-request-and-response)


> The List Incidents Endpoint is authenticated with an API key which is required to access resources. 
> Review the [Authentication section in the ContraForce API Overview](https://github.com/ContraForce/contraforce-api/tree/main/Docs#authentication-for-the-contraforce-partner-api) to learn more.

## List Incidents Request
To list all the incidents in your tenant or any of your managed customers tenants:
 
![](https://img.shields.io/badge/HTTP-POST-blue)

``` HTTP
 POST 
 https://portal.contraforce.com/api/beta/partners/incidents?tenantId=[TARGET_TENANT_ID]
```
Not all the incidents are retrieved with a single request. When you send the request only the top 50 incidents will be retrieved. A token can then be re-generated and used to ingest the next 50 incidents after the initial request.

## Parameters 
The List Incidents *POST* accepts a set of parameters for filtering, pagination, and/or limiting the number of objects retrieved. 
The following table shows all the parameters accepted by the endpoint with its default values: 

|Parameter | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| tenantId | The Tenant ID of the your organization or any of your managed customer tenants | ?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73 | None | GUID | Yes |

## Request Body
The request has to be in JSON format and could contain none or any of the following properties to filter the returned incidents. 

| Property | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| take | Limits the number of incident objects retrieved at a time  | "take": 10 | 50 | int (1, 2, ..1000) | No |
| query | Search query to filter the incidents by various properties (number, title, description) | "query": "access fro" | None | (string) text | No |
| startDate | Define the oldest (minimum) date of the incidents | "startDate"="2023-02-1" | 24 Hours back | yyyy-MM-ddTHH:mm:ss.fffZ (2023-02-03T16:34:46.5737663Z) | No |
| endDate| Define the newest (maximum) date of the incidents | "endDate"="2023-02-10" | Current date/time | yyyy-MM-ddTHH:mm:ss.fffZ (2023-02-10T16:34:46.5737663Z) | No |
| pageToken | Define the token of the next page (the value retrieved in the response when the maximum limit of returned incidents is reached, so you pass the token from the response to retrieve the next chunk of data for the same filter applied) | "pageToken"="FDDdfa43yy4ejlkas5r43..." | None | (string) text | No |
status | Filter the incidents by their status | "status": "new" | None | Values "new", "active", "closed" | No |
severity | Filter the incidents by their severity | "severity": "medium" | None | Values "informational", "low", "medium", "high" | No |

The following shows sample requests with a combination of the mentioned parameters above: 
### Retrieve the Latest Incidents
``` HTTP
POST /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73
```
And the body can be empty so no filters applied, you will get the latest 50 incidents as they are sorted in the Azure Sentinel

### Retrieve the most recent 10 incidents from the last 7 days 
``` HTTP
POST /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73
```
And the body is the following JSON: 
``` JSON
{
    "take": 10,
    "startDate": "2023-02-03"
}
```

### Retrieve all incidents for a month
``` HTTP
POST /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73
```
And the body is the following JSON 
``` JSON
{
    "startDate": "2023-01-01",
    "endDate": "2023-01-31"
}
```

The example is for January.

If the number of incidents retreived is more than 50 then a ***nextPageToken*** will be retrieved in the response and you can use it to retrieve the next 50 incidents as shown below:  
``` HTTP
POST /incidents?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73&take=10&startDate=2023-01-01&endDate=2023-01-31&token=AAAAABBBBCCCC...
```
And the body is the following JSON: 
``` JSON
{
    "pageToken": "RGJLK546T54DFSGDJLG5T54.........",
    "startDate": "2023-01-01",
    "endDate": "2023-01-31"
}
```
## Response 



![](https://img.shields.io/badge/Response-200-green)

In case the request processed successfully, the response of the list incidents request represents an object that contains the following in a JSON format:

| Property | Description | Sample Value |
|--|--|--|
| value | Object represents a page contains list of incidents and a next page token if needed | [Incidents List Object](#incidents-list-object) | 
| message | The status of the request or the error message in case of request failure | Incidents have been retrieved successfully! |
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
                "alertProductNames": [],
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

To see more details about the Incident object please referee to [Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md).

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
                "alertProductNames": [],
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
                "alertProductNames": [],
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
The ContraForce API allows you to test the call quickly using demo endpoints. 
In the development environment you can use demo enpoints so that the parameters passed won't be vaildated and you will be retrieving a valid response with sample data even if there is no data for that time. This will allow testing at any time to make the development experience faster and smoother.

> The demo request also requires an API Key, but any parameters passed will be ignored in the result, as you will always get the same result. 

``` HTTP
POST /api/beta/partners/demo/incidents?
```

