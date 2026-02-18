# List All Workspaces Incidents

Fetches incidents from **all workspaces** managed by the authenticated partner in a single API call, across all configured incident sources (Sentinel, Defender XDR, SentinelOne, CrowdStrike, QRadar, Splunk).

Unlike the [List Incidents](list-incidents.md) endpoint which requires a `tenantId` for a single workspace, this endpoint automatically resolves all workspaces the partner manages and queries them in parallel.

## Request

![](https://img.shields.io/badge/HTTP-POST-orange)
```
https://portal.contraforce.com/api/beta/partners/incidents/all
```

### Headers

| Header | Value | Required |
|--------|-------|----------|
| `X-API-KEY` | Your API key | Yes |
| `Content-Type` | `application/json` | Yes |

### Request Body

All fields are optional. An empty body `{}` will use all defaults.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `startDate` | datetime (UTC) | 3 hours ago | Start of the incident query window |
| `endDate` | datetime (UTC) | Now | End of the incident query window |
| `severity` | string | All | Filter: `"informational"`, `"low"`, `"medium"`, `"high"` |
| `status` | string | All | Filter: `"new"`, `"active"`, `"closed"` |
| `take` | int (1-1000) | 50 | Max total incidents returned across all workspaces |
| `query` | string | None | Free-text search on title and description |
| `sources` | array of int | All configured | Filter by incident source (see table below) |
| `accountId` | string (GUID) | All | Filter by a specific customer workspace Account ID |

### Source Values

| Value | Source |
|-------|--------|
| `1` | Sentinel |
| `2` | Defender XDR |
| `3` | QRadar |
| `4` | Splunk |
| `5` | CrowdStrike |
| `6` | SentinelOne |

## Example Requests

### Minimal (all defaults)
```json
{}
```
Returns incidents from the last 3 hours, all sources, all severities, all statuses.

### With filters
```json
{
  "startDate": "2026-02-16T07:00:00Z",
  "endDate": "2026-02-16T10:00:00Z",
  "severity": "high",
  "sources": [1, 2],
  "take": 25
}
```
Returns high-severity incidents from Sentinel and Defender XDR only, within the specified time range.

### Only SentinelOne incidents
```json
{
  "sources": [6]
}
```

## Response

### Success (HTTP 200)

```json
{
  "value": {
    "incidents": [
      {
        "id": "abc123-def456",
        "title": "Suspicious login from unusual location",
        "description": "A sign-in was detected from...",
        "number": 1042,
        "severity": 4,
        "status": 2,
        "source": 1,
        "sourceDisplayName": "Sentinel",
        "workspaceName": "Contoso Corp",
        "workspaceId": "guid-of-workspace",
        "alertProductNames": ["Microsoft Defender for Endpoint"],
        "creationTime": "2026-02-16T09:30:00Z",
        "lastModificationTime": "2026-02-16T09:35:00Z",
        "lastActivityTime": "2026-02-16T09:32:00Z",
        "alertsCount": 3,
        "user": {
          "id": "user-guid",
          "displayName": "John Doe",
          "email": "john@contoso.com"
        },
        "isAssigned": true,
        "tactics": ["InitialAccess", "Persistence"],
        "classification": null,
        "classificationReason": null
      }
    ],
    "totalCount": 42
  },
  "message": "42 incidents retrieved from 5 workspaces",
  "isSuccess": true
}
```

### Key Fields

Each incident in the response includes:
- **`workspaceName`** and **`workspaceId`**: Identifies which customer workspace the incident belongs to
- **`source`** and **`sourceDisplayName`**: Which incident source produced this incident
- **`alertProductNames`**: The security products that generated the alerts (e.g., "Microsoft Defender for Endpoint", "SentinelOne")

### Error Responses

| HTTP Code | Scenario |
|-----------|----------|
| `400` | Invalid severity or status value |
| `401` | Missing or invalid API key |
| `404` | Partner account not found |

## Notes

- Incidents are sorted by `creationTime` in descending order (newest first)
- If a workspace fails to respond (e.g., connectivity issues), incidents from other workspaces are still returned
- The `take` parameter applies globally across all workspaces after results are aggregated and sorted. The total count in the response reflects the capped result
- The `alertProductNames` field helps distinguish pure Sentinel incidents from Defender-forwarded incidents. For non-Microsoft sources (SentinelOne, CrowdStrike, etc.), it contains the source name
