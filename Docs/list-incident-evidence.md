# List Incident Evidence
The List Incident Evidence endpoint allows you retrieve a table of all the evidence assocaited with an incident. 

**Please Note**
> Not all incidents have an evidence table, so some requests will not retrieve data.

This document covers the following topics:
- [List Incident Evidence](#list-incident-evidence)
  - [List Incident Evidence Request](#list-incident-evidence-request)
  - [Parameters](#parameters)
  - [Response](#response)
    - [Sample response](#sample-response)
    - [Evidence Table Object](#evidence-table-object)
  - [Demo Request and Response](#demo-request-and-response)


> The List Incident Evidence endpoint is authenticated and an API key is required to access the resources. 
> Check out the [Authentication section in the ContraForce API Overview](https://github.com/ContraForce/contraforce-api/tree/main/Docs#authentication-for-the-contraforce-partner-api) to learn more.

## List Incident Evidence Request
To list all the entities involved with a specific incident in your tenant or any of your managed customer's tenants:
 
![](https://img.shields.io/badge/HTTP-GET-green)

``` HTTP
 GET 
 https://portal.contraforce.com/api/beta/partners/incidents/[INCIDNET_ID]/evidence?tenantId=[TARGET_TENANT_ID]
```


## Parameters 
The List Incident Evidence *GET* accepts two parameters only, the ID of the incident and the target Tenant ID: 

|Parameter | Description | Usage | Default Value | Format | Required|
|--|--|--|--|--|--|
| tenantId | The Tenant ID of your organization or any of your managed customer tenants | ?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73 | None | GUID | Yes |
| id | ID of the targeted incident  | ../incidents/10324234-324234-2323432/details | 5345345-5fsgf23-435faj-324gjkd | a1d9fe42-913e-4204-af1b-31b9a76b4d73 | Yes |

The following shows sample request:

``` HTTP
GET /incidents/bf187080-88c6-4e5f-950b-5fdd12864727/entities?tenantId=a1d9fe42-913e-4204-af1b-31b9a76b4d73
```

## Response 

![](https://img.shields.io/badge/Response-200-green)

When the request is processed successfully, the response of the list incident evidence request represents an object that contains the following in a JSON format:

| Property | Description | Sample Value |
|--|--|--|
| value | Object represents an a table in the JSON format | [Evidence Table Object](#evidence-table-object) | 
| message | The status of the request or the error message in case of request failure | Incident evidence has been retrieved successfully! |
| isSuccess | It has the value of true | true |

![](https://img.shields.io/badge/Response-400-red)

When something is not correct, you will receive an object similar to the one above but without the ***value*** and in this case you can look at the ***message*** property to know more about the error.   

| Property | Description | Sample Value |
|--|--|--|
| message | Description of the error and what went wrong | Invalid id |
| isSuccess | false | false |

![](https://img.shields.io/badge/Response-401-red)

In case of unauthenticated request, you will receive the status response **401**.

![](https://img.shields.io/badge/Response-404-red)

When providing an invalid ***tenantId*** or ***incidentId*** you will receive the status response **404**.

### Sample response 

``` JSON
{
    "value": {
        "columns": [
            "TenantId",
            "Application",
            "UserDomain",
            "Activity",
            "UserAgent",
            "RecordType",
            "TimeGenerated",
            "Operation",
            "OrganizationId",
            "OrganizationId_",
            "UserType",
            "UserKey",
            "OfficeWorkload",
            "ResultStatus",
            "ResultReasonType",
            "OfficeObjectId",
            "UserId",
            "UserId_",
            "ClientIP",
            "ClientIP_",
            "Scope",
            "Site_",
            "ItemType",
            "EventSource",
            "Source_Name",
            "MachineDomainInfo",
            "MachineId",
            "Site_Url",
            "Site_Url_",
            "SourceRelativeUrl",
            "SourceRelativeUrl_",
            "SourceFileName",
            "SourceFileName_",
            "SourceFileExtension",
            "DestinationRelativeUrl",
            "DestinationFileName",
            "DestinationFileExtension",
            "UserSharedWith",
            "SharingType",
            "CustomEvent",
            "Event_Data",
            "ModifiedObjectResolvedName",
            "Parameters",
            "ExternalAccess",
            "OriginatingServer",
            "OrganizationName",
            "Logon_Type",
            "InternalLogonType",
            "MailboxGuid",
            "MailboxOwnerUPN",
            "MailboxOwnerSid",
            "MailboxOwnerMasterAccountSid",
            "LogonUserSid",
            "LogonUserDisplayName",
            "ClientInfoString",
            "Client_IPAddress",
            "ClientMachineName",
            "ClientProcessName",
            "ClientVersion",
            "Folder",
            "CrossMailboxOperations",
            "DestMailboxId",
            "DestMailboxOwnerUPN",
            "DestMailboxOwnerSid",
            "DestMailboxOwnerMasterAccountSid",
            "DestFolder",
            "Folders",
            "AffectedItems",
            "Item",
            "ModifiedProperties",
            "SendAsUserSmtp",
            "SendAsUserMailboxGuid",
            "SendOnBehalfOfUserSmtp",
            "SendonBehalfOfUserMailboxGuid",
            "ExtendedProperties",
            "Client",
            "LoginStatus",
            "Actor",
            "ActorContextId",
            "ActorIpAddress",
            "InterSystemsId",
            "IntraSystemId",
            "SupportTicketId",
            "TargetContextId",
            "DataCenterSecurityEventType",
            "EffectiveOrganization",
            "ElevationTime",
            "ElevationApprover",
            "ElevationApprovedTime",
            "ElevationRequestId",
            "ElevationRole",
            "ElevationDuration",
            "GenericInfo",
            "SourceSystem",
            "OfficeId",
            "SourceRecordId",
            "AzureActiveDirectory_EventType",
            "AADTarget",
            "Start_Time",
            "OfficeTenantId",
            "OfficeTenantId_",
            "TargetUserOrGroupName",
            "TargetUserOrGroupType",
            "MessageId",
            "Members",
            "TeamName",
            "TeamGuid",
            "ChannelType",
            "ChannelName",
            "ChannelGuid",
            "ExtraProperties",
            "AddOnType",
            "AddonName",
            "TabType",
            "Name",
            "OldValue",
            "NewValue",
            "ItemName",
            "ChatThreadId",
            "ChatName",
            "CommunicationType",
            "AADGroupId",
            "AddOnGuid",
            "AppDistributionMode",
            "TargetUserId",
            "OperationScope",
            "AzureADAppId",
            "OperationProperties",
            "AppId",
            "ClientAppId",
            "ApplicationId",
            "SRPolicyId",
            "SRPolicyName",
            "SRRuleMatchDetails",
            "IsManagedDevice",
            "ActorContextId_",
            "Type",
            "_ResourceId"
        ],
        "rows": [
            [
                "333840c6-2bdb-4c16-9526-9596afd5260b",
                "",
                "",
                "",
                "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Teams/1.6.00.1381 Chrome/96.0.4664.174 Electron/16.2.8 Safari/537.36",
                "SharePointFileOperation",
                "2023-02-09T09:31:22Z",
                "FileDownloaded",
                "111128b2-32e9-4b8b-8fa0-0d12a58b148a",
                "111128b2-32e9-4b8b-8fa0-0d12a58b148a",
                "Regular",
                "i:0h.f|membership|2222@test.com",
                "OneDrive",
                "",
                "",
                "https://test-sharepoint.com/Documents/Microsoft Teams Chat Files/TFTP-Server-Installer (1).exe",
                "johnsmith@test.com",
                "johnsmith@test.com",
                "111.22.22.244",
                "111.22.22.244",
                "",
                "44408ded-5262-4b3f-9796-1cd90d33c0b7",
                "File",
                "SharePoint",
                "",
                "",
                "",
                "https://test-sharepoint.com/",
                "https://test-sharepoint.com/",
                "Documents/Microsoft Teams Chat Files",
                "Documents/Microsoft Teams Chat Files",
                "TFTP-Server-Installer (1).exe",
                "TFTP-Server-Installer (1).exe",
                "exe",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "2023-02-09T09:39:11.3765261Z",
                "",
                "",
                "",
                "",
                "",
                "",
                "OfficeActivityManager",
                "7eb787de-2526-40d9-d5ca-08db0a806845",
                "7eb787de-2526-40d9-d5ca-08db0a806845",
                "",
                "",
                "2023-02-09T09:39:11.3765261Z",
                "$RestApiTenantId$",
                "$RestApiTenantId$",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "",
                "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
                "",
                "",
                "",
                "False",
                "",
                "OfficeActivity",
                ""
            ]
        ]
    },
    "message": "Incident evidence has been retrieved successfully",
    "isSuccess": true
}
```

### Evidence Table Object
The Evidence Table object is a JSON object that represents a table and consists of a set of columns and rows.

**Please Note**
> Each incident has a different evidence and data structure, so the columns (names, types, and count) won't have a specific structure.
> You can render this table in your project so it is easier to view. 

The JSON object has the following properties:

| Property | Description | Sample Value | 
|--|--|--|
| columns | Array of string represents the name of all the columns in the table in the right order | ["firstName", "entityName", "url", "lastModificationDate"] |
| rows | Array of objects and each object represents an array of string that holds the value for each column | [ ["Test", "Account", "https://test.com", "2023-01-05"], ["Name 02", "Account", "https://test.com", "2023-01-05"] ]

The following visualization makes it easier to understand the properties as it shows a table alongside the JSON representation of it: 

![](https://github.com/ContraForce/contraforce-api/blob/main/Images/Incident%20Table%20of%20Evidence.svg)

``` JSON
{
    "columns": [
        "name",
        "entityType",
        "date",
        "url"
    ],
    "rows": [
        [
            "Sharepoint",
            "URL",
            "2023-02-15",
            "https://sample.com"
        ],
        [
            "Azure User",
            "Account",
            "2023-02-15",
            "https://sample.com"
        ]
    ]
}
```

## Demo Request and Response 
The ContraForce API allows you to test the call quickly using demo endpoints. 
In the development environment you can use demo enpoints so that the parameters passed won't be vaildated and you will be retrieving a valid response with sample data even if there is no data for that time. This will allow testing at any time to make the development experience faster and smoother. 

> The demo request also requires an API Key, but any parameters passed will be ignored in the result, so you will always get the same result. 

``` HTTP
GET /api/beta/partners/demo/incidents/[RANOM_ID]/evidence?
```

