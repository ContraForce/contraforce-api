# List Incident Entities
The ***List Incident Entities*** endpoint allows you retrieve a list of all the associated entities involved with a specified incident.

This document covers the following topics:
- [List Incident Entities](#list-incident-entities)
  - [List Incident Entities Request](#list-incident-entities-request)
  - [Parameters](#parameters)
  - [Response](#response)
    - [Sample Response](#sample-response)
    - [Entity Object](#entity-object)
  - [Demo Request and Response](#demo-request-and-response)


> The List Incident Entities is authenticated and an API key is required to access the resources. 
> Check out the [Authentication section in the ContraForce API Overview](https://github.com/ContraForce/contraforce-api/tree/main/Docs#authentication-for-the-contraforce-partner-api) to learn more.

## List Incident Entities Request
To list all of the entities involved with a specific incident in your tenant or any of your managed customer's tenants:
 
![](https://img.shields.io/badge/HTTP-GET-green)

``` HTTP
 GET 
 https://portal.contraforce.com/api/beta/partners/incidents/[INCIDNET_ID]/entities?tenantId=[TARGET_TENANT_ID]
```


## Parameters 
The List Incident evidence *GET* accepts two parameters only, the ID of the incident and the Target Tenant ID: 

|Parameter | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| tenantId | The Tenant ID of your organization or any of your managed customer tenants | ?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73 | None | GUID | Yes |
| id | ID of the targeted incident  | ../incidents/10324234-324234-2323432/details | 5345345-5fsgf23-435faj-324gjkd | a1d9fe42-913e-4204-af1b-31b9a76b4d73 | Yes |

The following shows a sample request:

``` HTTP
GET /incidents/bf187080-88c6-4e5f-950b-5fdd12864727/entities?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73
```

## Response 

![](https://img.shields.io/badge/Response-200-green)

When the request is processed successfully, the response of the List Incident Entities request represents an object that contains the following in a JSON format:

| Property | Description | Sample Value |
|--|--|--|
| value | Object represents an array of entity objects | [Entity Object](#entity-object) | 
| message | The status of the request or the error message in case of request failure | Incidents have been retrieved successfully! |
| isSuccess | It has the value of true | true |

![](https://img.shields.io/badge/Response-400-red)

In case something is not correct you will receive an object similar to the one above but without the ***value*** and in this case you can look at the ***message*** property to know more about the error.   

| Property | Description | Sample Value |
|--|--|--|
| message | Description of the error and what went wrong | Next page token is invalid |
| isSuccess | false | false |

![](https://img.shields.io/badge/Response-401-red)

In case of unauthenticated request, you will receive the status response **401**

![](https://img.shields.io/badge/Response-404-red)

When providing an invalid ***tenantId*** or ***incidentId*** you will receive the status response **404**

### Sample response 

To know more details about the Incident object please referee to [Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md)

``` JSON
{
    "value": [
        {
            "id": "3333a85d-cc9a-ed2d-6b55-2fc5882cacda",
            "displayName": null,
            "fileName": null,
            "type": "Microsoft.SecurityInsights/Entities",
            "friendlyName": "OneDrive",
            "hostName": null,
            "kind": "CloudApplication",
            "accountEntityId": null,
            "commandLine": null,
            "userUpn": null,
            "deviceId": null
        },
        {
            "id": "6582dre6f-bbd5-867b-ff7d-b77ba88d2f6f",
            "displayName": null,
            "fileName": null,
            "type": "Microsoft.SecurityInsights/Entities",
            "friendlyName": "TFTP-Server-Installer (1).exe",
            "hostName": null,
            "kind": "File",
            "accountEntityId": null,
            "commandLine": null,
            "userUpn": null,
            "deviceId": null
        },
        {
            "id": "99248bwy-0667-35a5-6164-59ee47711a95",
            "displayName": null,
            "fileName": null,
            "type": "Microsoft.SecurityInsights/Entities",
            "friendlyName": "https://test-sharepoint-url.com/Documents/Microsoft Teams Chat Files/TFTP-Server-Installer (1).exe",
            "hostName": null,
            "kind": "Url",
            "accountEntityId": null,
            "commandLine": null,
            "userUpn": null,
            "deviceId": null
        }
    ],
    "message": "Incident entities have been retrieved successfully",
    "isSuccess": true
}
```

### Entity Object
Each entity in the retrieved array of entities represents a JSON object that wraps all the metadata about an entity. 

> Entity has a kind property and based on that kind property some properties will be null and other will be filled for example, the property ***UserUpn*** will be populated only if the entity kind is ***Account***

In ContraFoce, entity kind supports the following values: 
- Account
- Host
- IP
- Malware
- File
- Process
- FileHash
- AzureResource
- RegisterKey
- ReigsterValue
- SecurityGroup
- URL
- IoTDevice
- MailBox
- MailCluster
- MailMessage
- SubmissionMail
- SentitelEntities

The ***id*** and ***friendlyName*** are not nullable properties and will always have values for each entity type

## Demo Request and Response 
The ContraForce API allows you to test the call quickly using demo endpoints. 
In the development environment you can use demo enpoints so that the parameters passed won't be vaildated and you will be retrieving a valid response with sample data even if there is no data for that time. This will allow testing at any time to make the development experience faster and smoother. 

> The demo request also requires an API Key, but any parameters passed will be ignored in the result, as you will always get the same result. 

``` HTTP
GET /api/beta/partners/demo/incidents/[RANOM_ID]/entities?
```

