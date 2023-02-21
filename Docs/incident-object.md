# Overview 
Incidents are the core object in the world of cybersecurity, and all the exposed endpoints in the ContraForce API are related to retrieving incidents or the data associated with an incident (entities, evidence, etc.).

The documentation below covers the definition of the ***Incident*** object and each of the included properties:

# Incident object sample 

``` JSON
{
    "id": "33360934-ffd3-2a6e-a513-ded250099e33",
    "title": "File with Extension 'exe' Downloaded from SharePoint - Office 365",
    "description": "test@example.com downloaded TFTP-Server-Installer (1).exe from https://test.com/sharepoint/demo-file.ext\r\n is recommended to use application control to prevent or block potentially malicious applications from running, limit file and directory permissions, use mitigation tools that detect and mitigate common features used in exploitation, and ensureusers are able to spot phishing emails.\n\nFor more information on this particular technique, please visit the following MITRE article to learn more: https://attack.mitre.org/techniques/T1080/",
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
}
```

The following table explains each property and the value it represents. 

| Property | Type | Description | Sample Value | Is Nullable | 
|--|--|--|--|--|
| id | (string) - GUID | ID of the incident | 33360934-ffd3-2a6e-a513-ded250099e33 | No |
| title | (string) - text | Title of the incident | New authentication attempt for the user sample@user.com from a new geo-location | No |
| description | (string) - text | Further details about the incident and explination | User with the email sample@user.com has tried to authenticate from a new location muliple times ... | Yes |
| number | (int) - number | Reference number of the incident | 351 | No |
| type | (string) - text | The source of the incident | Microsoft.SecurityInsights/Incidents | Yes |
| lastModificationTime | date/time (UTC) | Date/Time of the last update happened to the incident | 2023-02-09T10:38:47.0111424Z | No | 
| creationTime | date/time (UTC) | The creation date/time of the incident | 2023-02-09T10:38:47.0111424Z |  No | 
| lastActivityTime | date/time (UTC) | Date/Time of the last activitity in the incident | 2023-02-09T10:38:47.0111424Z |  Yes | 
| severity | (int) - number - enum | The severity of the incident and it has the following values (Informational = 1, Low = 2, Medium = 3, High = 4) | 4 |  No | 
| classification | (int) - number - enum | The classification of the incident and it has the following values (BenignPositive = 1, FalsePositive = 2, TruePositive = 3, Undetermined = 4) | 1 |  Yes | 
| classificationReason | (string) - text | The reason of classification provided when closing the incident | Filled by the user when closing the incident | Yes |
| classificationComment | (string) - text | Comments about the classification | Filled by the user when closing the incident | Yes |
| tactics | (array of string) | Set of the tactics targeted by the incident based on the MITRE framework | [ "Initial Access", "Execution" ] | Yes |
| ruleIds | (array of string) | Id of the rules that triggered the incident in the Azure Sentinel of the customer | [ "/subscriptions/454dff-4455-41eb-4545454-85e97cacec70/resourceGroups/contraforce-rg/providers/Microsoft.OperationalInsights/workspaces/cf-loganalytics-ws/providers/Microsoft.SecurityInsights/alertRules/666851279-5f95-4f5b-8ffb-7ec11cb158e4" ] | Yes |
| alertProductNames | (array of string) | Names of the products that caused the alerts | [ "Azure Sentinel", "Microsoft Defender for Endponit" ] | Yes |
| user | JSON Object | Object about the user assigned to the incident | { "id": "345434534-43534-54325435-43523", "displayName: "John Smith", "email": "johnsmith@test.com" } **Please Note** that the properties of the object will be null when the incident is not assigned  | No |
| isAssigned | Boolean true/false | Indicator if the incident is assigned for a user or not | True  | Yes |
| productId | (string) - GUID | Id of the product that this incident is related to | 534543545-234234-45435-23423  | Yes |
| status | (int) - number - Enum | Status of the incident and it has the following values (Active = 1, New = 2, Closed = 3) | 534543545-234234-45435-23423  | Yes |
| alertsCount | (int) - number | Number of alerts | 3  | Yes |

**For futher explination and question please feel free to reach out to the ContraForce Enginnering team.**