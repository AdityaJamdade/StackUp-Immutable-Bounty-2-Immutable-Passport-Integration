# Immutable Bounty #2: Immutable Passport Integration

### Bounty Link
- [Immutable Bounty #2: Immutable Passport Integration](https://app.stackup.dev/bounty/immutable-bounty-2-immutable-passport-integration)

## Immutable Passport Guide
### Introduction
- Immutable Passport is a non-custodial wallet and authentication solution.
- Streamlines user onboarding through passwordless sign-on and automated wallet creation.
- Offers battle-tested security, frictionless gameplay, persistent identity across Web3 games, and a consistent configuration across all applications.
- Built on the Immutable X platform, a Layer 2 scaling solution for Ethereum.
- Immutable X offers instant transactions, zero gas fees, and carbon-neutral minting.

### Why use Immutable Passport?
- For Users:
  - Convenient and secure way to sign in to Web3 applications.
  - No need to manage multiple passwords.
  - Provides users with a persistent identity across Web3 games.
- For Developers:
  - Easy integration into existing applications.
  - Features like passwordless sign-on and automated wallet creation improve user experience.

### How to set up Immutable Passport
- Users need to create a wallet.
- Sign up for Immutable Passport using their email address.
- Log in to Immutable Passport-enabled applications using their email address and password.

### How to integrate Immutable Passport into your application
- Create a developer account on Immutable X.
- Generate a client ID and client secret.
- Register your application on the Immutable Developer Hub.
- Start using the Immutable Passport SDK to integrate Immutable Passport into your application.
- SDK provides methods for user login, identity verification, and transaction initiation.

### Logging in a user with Immutable Passport
- Use the `login()` method from the Immutable Passport SDK.
- Prompt the user to sign in with their Immutable Passport account.
- Receive a token for identity verification and transaction initiation.

Example code:
```javascript
// Get the login URL
const loginURL = await ImmutablePassport.login();

// Redirect the user to the login URL
window.location.href = loginURL;

// Once the user has logged in, you will receive a token
const token = await ImmutablePassport.getToken();
```

### Conclusion
Immutable Passport is a powerful and easy-to-use solution for integrating authentication and wallet functionality into your Web3 application. By following the steps in this guide, you can get started with Immutable Passport quickly and easily.
