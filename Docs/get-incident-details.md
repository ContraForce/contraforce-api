# Get Incident Details 
Get incident details endpoint allows you to retrieve full details of the incident, as the list incidents endpoint will retrieve only the main keys in the incident object, this endpoint will retrieve the full details needed

This document covers the following topics:
- [Get Incident Details](#get-incident-details)
  - [Get Incident Details Request](#get-incident-details-request)
  - [Parameters](#parameters)
  - [Response](#response)
    - [Sample response](#sample-response)
  - [Demo Request and Response](#demo-request-and-response)


> Get incident details is authenticated and an API key is required to access the resources. 
> Check out the [Authentication section in the ContraForce API Overview](https://github.com/ContraForce/contraforce-api/tree/main/Docs#authentication-for-the-contraforce-partner-api) to learn more.

## Get Incident Details Request
To list all the incidents in your tenant or any of your managed customer's tenant
 
![](https://img.shields.io/badge/HTTP-GET-green)

``` HTTP
 GET 
 https://portal.contraforce.com/api/beta/partners/incidents/[INCIDNET_ID]/details?tenantId=[TARGET_TENANT_ID]
```


## Parameters 
The Get incident details *GET* accepts two parameters only, the Id of the incident and the target tenant id: 

|Parameter | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| tenantId | The tenant id of the your organization or any of your managed customer tenants | ?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73 | None | GUID | Yes |
| id | Id of the targeted incident  | ../incidents/10324234-324234-2323432/details | 5345345-5fsgf23-435faj-324gjkd | a1d9fe42-913e-4204-af1b-31b9a76b4d73 | Yes |

Following shows sample request

``` HTTP
GET /incidents/bf187080-88c6-4e5f-950b-5fdd12864727/details?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73
```

## Response 

![](https://img.shields.io/badge/Response-200-green)

In case the request processed successfully, the response of the list incidents request represents an object that contains the following in a JSON format:

| Property | Description | Sample Value |
|--|--|--|
| value | Object represents a a full detailed incident object | [Incidents List Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md) | 
| message | The status of the request or the error message in case of request failure | Incidents have been retrieved successfully! |
| isSuccess | It has the value of true | true |

![](https://img.shields.io/badge/Response-400-red)

In case of something is not correct you will receive an object similar to the one above but without the ***value*** and in this case you can look at the ***message*** property to know more about the error.   

| Property | Description | Sample Value |
|--|--|--|
| message | Description of the error and what went wrong |  |
| isSuccess | false | false |

![](https://img.shields.io/badge/Response-401-red)

In case of unauthenticated request, you will receive the status response **401**

![](https://img.shields.io/badge/Response-404-red)

When providing an invalid ***tenantId*** or ***incidentId*** you will receive the status response **404**

### Sample response 

To know more details about the Incident object please referee to [Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md)

``` JSON
{
    "value": {
        "id": "33360934-ffd3-2a6e-a513-ded250099e33",
        "title": "File with Extension 'exe' Downloaded from SharePoint - Office 365",
        "description": "test@example.com downloaded TFTP-Server-Installer (1).exe from https://test.com/sharepoint/demo-file.ext\r\n is recommended to use application control to prevent or block potentially malicious applications from running, limit file and directory permissions, use mitigation tools that detect and mitigate common features used in exploitation, and ensureusers   are able to spot phishing emails.\n\nFor more information on this particular technique, please visit the following MITRE article to learn more: https://attack.mitre.org/techniques/T1080/",
        "number": 001,
        "type": "Microsoft.SecurityInsights/Incidents",
        "lastModificationTime": "2023-02-09T10:38:47.0111424Z",
        "creationTime": "2023-02-09T10:38:47.0111424Z",
        "lastActivityTime": "2023-02-09T09:31:22Z",
        "severity": 4,
        "classification": null,
        "comment": null,
        "classificationReason": null,
        "classificationComment": null,
        "tactics": [
            "LateralMovement"
        ],
        "ruleIds": [
            "/subscriptions/454dff-4455-41eb-4545454-85e97cacec70/resourceGroups/contraforce-rg/providers/Microsoft.OperationalInsights/workspaces/cf-loganalytics-ws/providers/Microsoft.SecurityInsights/alertRules/666851279-5f95-4f5b-8ffb-7ec11cb158e4"
        ],
        "alertProductNames": [
            "Azure Sentinel"
        ],
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
    "message": "Incident has been retrieved successfully",
    "isSuccess": true
}
```

## Demo Request and Response 
ContraForce Parnter API allows you to test the call quickly using a demo endpoints. 
In the development environment you can use the demo enpoints so the parameters passed won't be vaildated and you will be retrieving a valid response with sample data everytime even if there was no data for the time period or the passed query, that makes your development experience faster and smoother. 

> The demo request also requires an API Key, but any parameters passed will be ignored in the result, as you will always get the same result. 

``` HTTP
GET /api/beta/partners/demo/incidents/[RANOM_ID]/details?
```

