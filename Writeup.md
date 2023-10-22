### Git cloning a repository of the simple application
- Prequisites are you should have git and nodejs installed, if you don't have the setup don't worry, visit these websites for [NodeJs](https://nodejs.org/en), for [Git](https://github.com/git-guides/install-git)
- Clone the boilerplate code for ZkEvm using this command
``` javascript
git clone https://github.com/immutable/zkevm-boilerplate.git
```
After cloning, you are good to go, since you have basic setup for the ZkEvm of Immutable Passport.

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
### Logging in a user with Passport
### Displaying on the app the id token, access token obtained from authenticating with Passport after login, and the user's nickname
### Logging out a user
### Initiate a transaction from Passport, such as sending a placeholder string and obtaining the transaction hash

This is just a basic guide to using Immutable Passport. For more information, please refer to the Immutable Passport documentation: https://docs.immutable.com/docs/x/passport
