# Overview
The ContraForce API provides you access to ContraForce Portal data using various exposed API endpoints. 
The ContraForce API allows the use the following requests:
  - [List All Workspaces Incidents Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-all-workspaces-incidents.md) - Fetch incidents from all managed workspaces in one call
  - [List Incidents Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incidents.md)
  - [Get Incident Details Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/get-incident-details.md)
  - [List Incident Entities Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incident-entities.md)
  - [List Incident Evidence Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incident-evidence.md)

To learn more about the ContraForce **Incident Object** please refer to  [ContraForce Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md)

> The ContraForce API is currently in beta. If you encounter any errors or unexpected behavior you can submit an issue [here](https://github.com/ContraForce/contraforce-api/issues/new). 
> ContraForce plans to release the final version of the API in Q2 of 2023.

This ReadMe document covers the following topics:
- [Overview](#overview)
	- [Multi-tenancy in ContraForce](#multi-tenancy-in-contraforce)
	- [Authentication for the ContraForce API](#authentication-for-the-contraforce-partner-api)
	- [Testing the ContraForce API](#testing-the-contraforce-partner-api)
	- [ContraForce API Endpoints](#contraforce-partner-api-endpoints)

## Multi-Tenancy in ContraForce
Through the ContraForce Partner Program, partners can create ContraForce environments for their customers and then manage their incidents and connected data sources within the ContraForce web application. The ContraForce API allows users to retrieve portal data via API calls in addition to web application user interface.

![ContraForce Multi-Tenancy Diagram](https://github.com/ContraForce/contraforce-api/blob/main/Images/Multi-Tenancy%20Flow%20for%20Partners.drawio.svg?raw=true)

ContraForce environments are created per customer. Because of this, a **Tenant ID** is a mandatory parameter for any ContraForce API request. By sepcifying the Tenant ID in the request body, partners are enabled to access data for any of the customer ContraForce environments under their management.

## Authentication for the ContraForce API
In the current version of the ContraForce API, the exposed endpoints of the API are secured using an ***API Key***. An API key can be requested after Partner Onboarding has been completed. A member of the ContraForce Engineering team will provide you with an API key and assist you with the connection process.

The generated API key must be sent in the header of each HTTP request you are making to the ContraForce API as shown below for a C# example: 
``` C#
using (var client = new HttpClient())
{
	// Set your API key in the header of the HTTP request
	client.DefaultRequestHeaders.Add("x-api-key", "YOUR_API_KEY");
	
	// Submit the request and the rest of the logic
	...
}
```
If you are testing the API calls using **Postman**, you can set the API key as shown below: 

![Set API key for the authorization of the HTTP Header](https://github.com/ContraForce/contraforce-api/blob/main/Images/Postman%20screenshot%20for%20authentication.png?raw=true)


## Testing the ContraForce API
After you obtain an API key, you can send a test request to ensure that the ContraForce API is functioning as intended.

![](https://img.shields.io/badge/HTTP-GET-green)
```
https://portal.contraforce.com/api/beta/partners
```
After you submit the test request, a sucess response should appear as shown below.
``` JSON
{
	"message": "Welcome to the ContraForce API"
}
```

## ContraForce API Endpoints
The following links provide a detailed documentation about each available endpoint in the current beta version of the ContraForce API:
  - [List All Workspaces Incidents Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-all-workspaces-incidents.md) - Fetch incidents from all managed workspaces in one call
  - [List Incidents Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incidents.md)
  - [Get Incident Details Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/get-incident-details.md)
  - [List Incident Entities Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incident-entities.md)
  - [List Incident Evidence Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incident-evidence.md)

