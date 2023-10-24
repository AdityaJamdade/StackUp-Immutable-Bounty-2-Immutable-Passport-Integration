# Table of Contents

1. Git cloning a repository of the simple application
2. Registering the application on Immutable Developer Hub
3. Installing and initialising the Passport client
4. Logging in a user with Passport
5. Displaying on the app the id token, access token obtained from authenticating with Passport after login, and the user's nickname
6. Logging out a user
7. Initiate a transaction from Passport, such as sending a placeholder string and obtaining the transaction hash


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
Now that we have initialised our passport, we need to create functionality for logging in, here for this guide we are using the Ethers.js library for loggin in but we can also do it using the Passport (EIP-1193) method. for more information [visit](https://docs.immutable.com/docs/zkEVM/products/passport/identity/login).

**1. Initialise the provider**
```javascript
import { ethers } from 'ethers';
const passportProvider = passport.connectEvm();
const provider = new ethers.providers.Web3Provider(passportProvider);

const signer = provider.getSigner();
const address = await signer.getAddress();
```

**2. Trigger the login process**

```javascript
import { ethers } from 'ethers';

const passportProvider = passport.connectEvm();
const provider = new ethers.providers.Web3Provider(passportProvider);
const accounts = await provider.send("eth_requestAccounts", []);
```

Once the requestAccounts RPC method has been called, the Passport module will begin the authentication process. If the user successfully authenticates, then the user will be redirected to the Redirect URI that was set in the OIDC Configuration.

**3. Configure the login callback**

At this point, the route that handles requests to the Redirect URI will need to call the loginCallback method on page load. Your specific implementation will vary based on your application's architecture, but a vanilla Javascript implementation may look as follows:
```javascript
window.addEventListener('load', function() {
  passport.loginCallback();
});
```

The loginCallback method will then process the response from the Immutable's auth domain, store the authenticated user in session storage and close the pop-up. Once the authentication flow is complete, the Promise returned from requestAccounts will also resolve with a single-item array containing the user's address.

### Displaying on the app the id token, access token obtained from authenticating with Passport after login, and the user's nickname
#### Prequisites
- The user must be logged into your application via Passport.

**- 1. Getting user information**
The getUserInfo function returns a promise that resolves the following information about the currently logged-in user:
```javascript
const userProfile = await passport.getUserInfo();
```
Here - 
- ```email``` - The email address of the logged-in user. This property will be undefined if the email scope has not been requested.
- ```sub``` -	The subject (unique identifier) of the logged-in user.
- ```nickname``` - The nickname of the logged-in user.

The getUserInfo function may throw the following error:

```NOT_LOGGED_IN_ERROR```,	No user is logged in at the time of the function call.	Verify that a user has logged in before attempting to call getUserInfo

### Logging out a user
**1. It is really simple to logout users using the logout method.**

Exaple:

```javascript
// 1. Initialise Passport and set the preferred logout mode
const passport = new Passport({
  logoutRedirectUri: 'http://localhost:3000',
  logoutMode: 'redirect', // defaults to 'redirect' if not set
  // ...
});

// 2. authenticate user
// ... refer to the "Enable user login" page for more information

// 3. Log the user out
await passport.logout();
```

**2. Logout Modes - Redirect Mode:**

- The above explanation provides details about the 'redirect' logout mode.
- In the 'redirect' mode:
- The user's application session is cleared by removing the JWT (JSON Web Token) from the browser's local storage.
- The user is then redirected to the Passport authentication domain, where the Passport session is cleared.
- Finally, the user is redirected back to the specified logoutRedirectUri.

### Initiate a transaction from Passport, such as sending a placeholder string and obtaining the transaction hash

This is just a basic guide to using Immutable Passport. For more information, please refer to the Immutable Passport documentation: https://docs.immutable.com/docs/x/passport
