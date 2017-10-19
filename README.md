---
services: active-directory
platforms: nodejs
author: craigshoemaker
---

# Securing a Node.js REST-based Application with Azure Active Directory

This sample demonstrates how to secure a [Restify](http://restify.com/) API endpoint with [Passport](http://passportjs.org/) using the [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad) module to handle communication with Azure Active Directory (AAD). 

This is the sample code for the article, [Secure Node.js Web API with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devquickstarts-webapi-nodejs).

## Setup
Before you can connect to Azure Active Directory, you need the following information:

| Name  | Description | Variable Name in Config File |
| ------------- | ------------- | ------------- |
| Tenant Name  | [Tenant name](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) you want to use for authentication | `tenantName`  |
| Client ID  | Client ID is the OAuth term used for the AAD _Application ID_. |  `clientID`  |

Once you have cloned the repository open `config.js` you must add your values for tenant name and client ID in the following code:

```JavaScript
const tenantName    = //<YOUR_TENANT_NAME>;
const clientID      = //<YOUR_CLIENT_ID>;
const serverPort    = 3000;
```

For help on how to determin the values for these variables, read about the [Project Setup](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devquickstarts-webapi-nodejs#create-the-sample-project) in the accompanying article.

## Run the sample
Once configuration is complete, then install the dependencies and start the project.

```Shell
npm install
npm start
```

## Test an unsecured end point

To test a route that does not require authentication, enter the following command in a bash shell:

```Shell
curl -isS -X GET http://127.0.0.1:3000/
```
If you have configured your server correctly, the response should look similar to:

```Shell
HTTP/1.1 200 OK
Server: Azure Active Directroy with Node.js Demo
Content-Type: application/json
Content-Length: 49
Date: Tue, 10 Oct 2017 18:35:13 GMT
Connection: keep-alive

Try: curl -isS -X GET http://127.0.0.1:3000/api
```

## Test a secured end point
To test a secured route, enter the folling into a bash shell:

```Shell
curl -isS -X GET http://127.0.0.1:3000/api
```
If you have configured the server correctly, then the server should respond with a status of `Unauthorized`.

```Shell
HTTP/1.1 401 Unauthorized
Server: Azure Active Directroy with Node.js Demo
WWW-Authenticate: token is not found
Date: Tue, 10 Oct 2017 16:22:03 GMT
Connection: keep-alive
Content-Length: 12

Unauthorized
```