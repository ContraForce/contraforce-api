# Overview
ContraForce API provides you access to the ContraForce data using various exposed API endpoints. 
The incidents API allows you to achieve the following: 
  - [List Incidents Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incidents.md)
  - [Get Incident Details Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/get-incident-details.md)
  - [List Incident Entities Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incident-entities.md)
  - [List Incident Evidence Request](https://github.com/ContraForce/contraforce-api/blob/main/Docs/list-incident-evidence.md)

To learn more about the ContraForce **Incident Object** please refer to  [ContraForce Incident Object](https://github.com/ContraForce/contraforce-api/blob/main/Docs/incident-object.md)

> ContraForce Partners API is currently in beta, in case of errors or unexpected behaviors, feel free to submit a new issue [here](https://github.com/ContraForce/contraforce-api/issues/new) 
> The final version is currently planned to be released for Q2 in 2022

This document covers the following topics
- [Overview](#overview)
	- [Multi-tenancy in ContraForce](#multi-tenancy-in-contraforce)
	- [Authentication for the ContraForce Partner API](#authentication-for-the-contraforce-partner-api)
	- [Testing the ContraForce Partner API](#testing-the-contraforce-partner-api)
	- [ContraForce Partner API Endpoints](#contraforce-partner-api-endpoints)

## Multi-tenancy in ContraForce
Through the ContraForce Partner program, partners can onboard and manage their own customers to ContraForce. By using the ContraForce Partners API, you can retrieve the data from ContraForce for your own organization or your customer organizations. 

![ContraForce Multi-Tenancy Diagram](https://raw.githubusercontent.com/ContraForce/contraforce-api/main/Images/Multi-Tenancy%20Flow%20for%20Partners.drawio.svg)

Based on the previous flow, if you are a ContraForce partner, you should be able to access all your data and your direct customers data using the ContraForce Partner API.
That's why any request you send to the ContraForce Partner API, the **Tenant Id** is a mandatory parameter. 

## Authentication for the ContraForce Partner API
The current version of the exposed endpoints of the ContraForce Partner API is secured using an ***API Key***, you can request an API key when you are a ContraForce partner and you would like to have an API access, the ContraForce team you will send an API key during the onboarding process. 
The key must be sent in the header of each HTTP request you are making to the ContraForce Partner API as shown below for a C# example: 
``` C#
using (var client = new HttpClient())
{
	// Set your API key in the header of the HTTP request
	client.DefaultRequestHeaders.Add("x-api-key", "YOUR_API_KEY");
	
	// Submit the request and the rest of the logic
	...
}
```
If you are test the API calls using **Postman**, you can set the API key as shown below: 

![Set API key for the authorization of the HTTP Header](https://github.com/ContraForce/contraforce-api/blob/main/Images/Postman%20screenshot%20for%20authentication.png?raw=true)


## Testing the ContraForce Partner API
After you obtain your API key, you can send a test request to make sure that everything is right for you:

![](https://img.shields.io/badge/HTTP-GET-green)
```
https://portal.contraforce.com/api/beta/partners
```
Once you submit the request successfully you should get a JSON response with a welcome message.
``` JSON
{
	"message": "Welcome to ContraForce API"
}
```

## ContraForce Partner API Endpoints
Following links provide a detailed documentation about each available endpoint in the current beta version of the ContraForce Partner API

