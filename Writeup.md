### Git cloning a repository of the simple application
- Prequisites are you should have git and nodejs installed, if you don't have the setup don't worry, visit these websites for [NodeJs](https://nodejs.org/en), for [Git](https://github.com/git-guides/install-git)
- Clone the boilerplate code for ZkEvm using this command
``` javascript
git clone https://github.com/immutable/zkevm-boilerplate.git
```

### Registering the application on Immutable Developer Hub
- Register your application as an OAuth 2.0 client in the [Immutable Developer Hub](https://hub.immutable.com/?_gl=1*i3bh2g*_ga*ODgyMzk2NzY5LjE2OTc3ODIwOTI.*_ga_4JBHZ7F06X*MTY5Nzk3MjYwNi4zLjEuMTY5Nzk3NDIxOS4wLjAuMA..*_ga_7XM4Y7T8YC*MTY5Nzk3MjYwNy41LjEuMTY5Nzk3NTI1MC4wLjAuMA..) by following the "Add Client" button in the Passport page.

- An OAuth client needs to be registered for every type of application you own, so if you are a game publisher that requires the Passport login in a mobile app and a website, you need to create two clients.

- Here are a few things to note when adding a client in the Developer Hub
There are a few crucial details that must be provided when adding a client:

- **Application Type** - The type of your application. At the moment only the Web Application option is available. A Native option for mobile or desktop applications is coming soon.
- **Client name**	- The name you wish to use to identify your application.
- **Logout URLs** -	The URL that your users will be redirected to upon logging out of your application.
- **Callback URLs** -	The URL that your users will be redirected to once the authentication is complete. This is also where your application process the authentication response.
- **Web Origins URLs** - The URLs that are allowed to request authorisation. This field is available when you select the Native application type.


### Installing and initialising the Passport client

**Prerequisites**
- Install Node.js (Node v18+).
   
**Install the immutable sdk by running following command**
  
```javascript
npm install -D @imtbl/sdk
```

**Initialization**
- Example Passport instance:
```javascript
const passportInstance = new passport.Passport({
  baseConfig: new config.ImmutableConfiguration({
    environment: config.Environment.PRODUCTION,
  }),
  clientId: '<YOUR_CLIENT_ID>',
  redirectUri: 'https://example.com',
  logoutRedirectUri: 'https://example.com/logout',
  audience: 'platform_api',
  scope: 'openid offline_access email transact',
});
```
Here,
- **baseConfig**: baseConfig is the shared configuration for Immutable modules, defining the environment and other global settings.
- **clientId**: clientId is the unique identifier for your registered application in the Immutable Developer Hub.
**redirectUri**: redirectUri is the URL where users are redirected after successful authentication, matching a Callback URL in your client settings.
- **logoutRedirectUri**: logoutRedirectUri is the URL for user redirection after logging out, matching a Logout URL in your client settings.
- **audience**: audience is a string specifying the intended audience for the issued token, e.g., 'platform_api' for Immutable protocol APIs.
- **scope**: scope defines the access privileges requested, including custom scopes like 'transact' and standard OpenID Connect (OIDC) scopes such as 'openid', 'offline_access', and 'email'.


### Logging in a user with Passport
### Displaying on the app the id token, access token obtained from authenticating with Passport after login, and the user's nickname
### Logging out a user
### Initiate a transaction from Passport, such as sending a placeholder string and obtaining the transaction hash

This is just a basic guide to using Immutable Passport. For more information, please refer to the Immutable Passport documentation: https://docs.immutable.com/docs/x/passport
